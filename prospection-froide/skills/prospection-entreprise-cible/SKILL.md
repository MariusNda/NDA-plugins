---
name: prospection-entreprise-cible
description: >-
  Recherche des entreprises cibles pour du look-alike commercial NDA, en
  croisant l'API ouverte Recherche d'entreprises (data.gouv.fr), l'annuaire
  French Tech 120/Next40, et la liste de référence des clients NDA dans
  Notion. Qualifie chaque cible sur sa maturité technologique (besoin réel
  de transformation Data/IA/Cyber), pas sur la seule ressemblance
  sectorielle. Déclencher quand un collaborateur demande de "trouver des
  entreprises cibles", "faire du look-alike", "chercher des prospects",
  "skill prospection entreprise cible".
---

# Recherche d'entreprises cibles (Skill 1)

**Entrée** : des critères de ciblage, ou le discours de campagne produit par la Skill 0.
**Sortie** : un Top 20 d'entreprises cibles vérifiées.

## Objectif

Produire, par look-alike des clients NDA, une liste d'entreprises à qui NDA peut apporter quelque chose et à qui cette utilité peut être démontrée.

## Principes de sélection

Le critère n'est pas la ressemblance sectorielle, mais le besoin réel : IAM/API, Data/IA, architecture, transformation.

La maturité technologique doit tomber dans la bonne fenêtre :

- trop en avance (digital-native, transition déjà menée seule) : l'aide de NDA serait inutile ;
- trop en retard (entreprise jeune ou petite, sans enjeu constitué) : l'entreprise n'est pas encore concernée ;
- entre les deux : éligible.

Exemple repère : Alan et MGEN relèvent du même secteur, l'assurance-santé, avec des besoins opposés.

Trois verticales sont déjà instruites et servent d'ancrage par défaut : **TSV**, **Assurance**, **Agroalimentaire**, avec pour références look-alike Nexecur, MGEN et Savencia. Le segment visé est ETI et PME.

La santé financière fait partie du filtre, pas seulement la taille : une entreprise doit avoir la capacité réelle d'investir dans du conseil. C'est à cela que servent `resultat_net_min` et `ca_min`.

**Règle de preuve.** Chaque entreprise retenue s'appuie sur des faits vérifiables, jamais sur une intuition sectorielle. Pour chacune, conserver l'URL de la source et la date de vérification. Ne jamais inventer un chiffre d'affaires, un effectif ou une activité : un élément introuvable se note « non vérifié » plutôt que d'être estimé.

Ne jamais proposer une entreprise déjà présente dans [Liste des clients NDA — Industrie & Segment](https://app.notion.com/p/nda-partners/Liste-des-clients-NDA-Industrie-Segment-3bf852cc7e1581d69b4af9ea8bc01793).

## Étape 1 — Sélectionner les filtres

Parcourir les sections de filtres une par une, dans l'ordre ci-dessous. Pour chaque section :

- **4 paramètres ou moins** : poser une question à choix via l'outil AskUserQuestion, en proposant chaque paramètre de la section plus une option « passer ».
- **Plus de 4 paramètres** : ne pas utiliser AskUserQuestion. Lister les paramètres en clair dans le chat et demander lesquels retenir.

L'utilisateur peut répondre « passer » sur n'importe quelle section. La recherche ne démarre qu'une fois toutes les sections parcourues, ou sur demande explicite de lancer.

**Le secteur ne peut pas rester vide.** Sans `activite_principale` ni `section_activite_principale`, l'API plafonne à 10 000 résultats qu'elle ne classe pas par pertinence : les vingt-cinq premiers sont alors un tirage. Un essai sur la seule catégorie « grande entreprise » a rendu sur la même page La Poste, EDF, la Ville de Paris, la Croix-Rouge, Lidl et un opérateur funéraire. Si ni la campagne ni l'utilisateur ne donnent de secteur, le demander avant de lancer.

**Exclure par défaut les entités non marchandes**, sauf campagne visant explicitement le secteur public : `est_administration`, `est_collectivite_territoriale` et `est_association` remontent sinon des collectivités et des associations au milieu des cibles.

**Valeurs par défaut issues de la méthode du prospecteur**, à proposer si la personne n'a pas de critère arrêté : un secteur ou une industrie précise, un plancher d'effectif de l'ordre de 200 à 300 salariés, et une taille suffisante pour porter un projet. Une entreprise trop petite ne fera pas de projet, quel que soit son fit.

Un critère utilisé sur le terrain n'est pas couvert par l'API : **l'effectif dans la fonction visée** — par exemple au moins vingt personnes dans la direction data. Une entreprise de 300 salariés dont 5 seulement relèvent du périmètre cible n'est pas une bonne cible. Ce filtre se vérifie à l'étape 3, via les offres d'emploi de l'entreprise et une requête moteur du type `site:linkedin.com/in "Entreprise" [fonction]` dont on lit les résultats sans jamais ouvrir de page LinkedIn — ouvrir une page engagerait le compte du collaborateur.

### 1. Secteur / activité — 2 paramètres → AskUserQuestion
- `activite_principale` (code NAF précis)
- `section_activite_principale` (grande catégorie d'activité, A à U)

### 2. Taille — 2 paramètres → AskUserQuestion
- `categorie_entreprise` (PME / ETI / GE)
- `tranche_effectif_salarie` (tranche d'effectif salarié)

**Deux pièges vérifiés par appel réel, à ne pas ignorer.**

`categorie_entreprise` ne mesure pas la taille de l'entité interrogée : la catégorie est portée par l'unité légale rattachée à son groupe. Une filiale de dix personnes appartenant à une ETI ressort en ETI. Un test sur l'agroalimentaire a remonté trois sociétés de moins de 3,5 M€ de chiffre d'affaires étiquetées ETI. Ce filtre ne remplace donc pas la vérification de taille de l'étape 3.

Le même mécanisme fait remonter **plusieurs entités d'un même groupe** : le test a rendu SILL et SILL DAIRY INTERNATIONAL, même activité, même département, même groupe. Deux lignes pour une seule entreprise réelle. Voir la règle de dédoublonnage à l'étape 3.

`tranche_effectif_salarie` renvoie un code INSEE, pas un nombre de salariés, et il décrit l'établissement siège :

| Code | Effectif | Code | Effectif |
|---|---|---|---|
| NN | Non renseigné | 22 | 100 à 199 |
| 11 | 10 à 19 | 32 | 250 à 499 |
| 12 | 20 à 49 | 41 | 500 à 999 |
| 21 | 50 à 99 | 42 | 1 000 à 1 999 |

### 3. Localisation — 6 paramètres → liste en clair
- `code_postal`
- `code_commune`
- `departement`
- `region`
- `epci`
- `code_collectivite_territoriale`

### 4. Finances — 4 paramètres → AskUserQuestion
- `ca_min`
- `ca_max`
- `resultat_net_min`
- `resultat_net_max`

**Ne pas filtrer sur ces valeurs par défaut.** Les millésimes publiés sont hétérogènes — un test réel a renvoyé des chiffres d'affaires datant de 2014 à 2025 selon les entreprises, et cinq sur vingt-cinq sans aucun chiffre. Un filtre financier exclut silencieusement toute société dont les comptes ne sont pas déposés ou sont anciens, y compris de bonnes cibles.

Récupérer plutôt le chiffre d'affaires **avec son millésime**, l'afficher dans le livrable, et trancher après coup.

### 5. Statut juridique / administratif — 7 paramètres → liste en clair
- `nature_juridique` (forme juridique)
- `etat_administratif` (active / cessée)
- `est_entrepreneur_individuel`
- `est_association`
- `est_administration`
- `est_collectivite_territoriale`
- `est_ess` (économie sociale et solidaire)

### 6. Labels / certifications — 14 paramètres → liste en clair
- `est_qualiopi`, `est_rge`, `est_bio`, `est_patrimoine_vivant`, `est_societe_mission`, `est_achats_responsables`, `egapro_renseignee`, `convention_collective_renseignee`, `est_siae`, `est_finess`, `est_uai`, `est_organisme_formation`, `est_alim_confiance`, `est_entrepreneur_spectacle`

### 7. Personnes / dirigeants — 5 paramètres → liste en clair
- `nom_personne`, `prenoms_personne`, `type_personne` (dirigeant ou élu), `date_naissance_personne_min`, `date_naissance_personne_max`

Précision à mentionner : ce champ ne couvre que les représentants légaux (gérant, président, DG, administrateurs), jamais les cadres opérationnels (CDO, managers, cadres supérieurs). Il sert à l'étape 2 du look-alike, pas à identifier les interlocuteurs opérationnels.

### 8. Recherche libre — 1 paramètre → AskUserQuestion
- `q` (texte libre : nom, adresse, SIREN/SIRET)

## Étape 2 — Constituer la longlist

1. **API Recherche d'entreprises.** Appeler `https://recherche-entreprises.api.gouv.fr/search` avec les seuls filtres retenus. Les résultats ne sont **pas classés par pertinence commerciale** : prendre les vingt-cinq premiers d'un ensemble large revient à tirer au hasard. C'est le filtrage qui fait la qualité, pas le rang. Récupérer 40 à 60 candidats, soit deux à trois fois la cible : une partie sera éliminée à l'étape suivante. Toujours inclure `date_creation`.

   Trois points opérationnels : l'API est **ouverte, sans authentification ni clé**, plafonnée à **7 appels par seconde** ; elle **ignore silencieusement tout paramètre inconnu**, donc une faute de frappe dans un filtre élargit la recherche sans lever d'erreur — relire les noms de paramètres avant d'interpréter un volume anormal ; les réponses portent désormais `activite_principale` (NAF rév. 2) **et** `activite_principale_naf25` (nomenclature 2025), à ne pas confondre au moment de filtrer.

2. **Annuaires sectoriels et registres de certification.** Quand une verticale rend trop peu de candidats via l'API, chercher l'organisme qui certifie ou réglemente le secteur et parcourir sa liste publique d'adhérents à jour : APSAD pour la sécurité privée et la télésurveillance, ordres et annuaires professionnels pour les experts-comptables, fédérations de branche ailleurs. C'est la technique d'élargissement la plus productive du terrain. Vérifier que la consultation de l'annuaire est autorisée et rester sur des pages publiques.

3. **Next40 / French Tech 120** ([frenchtech120.numeum.fr](https://frenchtech120.numeum.fr/), annuaire Numeum, promotion 2026, consultation libre sans compte). Complément seulement, jamais source par défaut : ce vivier est digital-native, à l'opposé du profil recherché. N'ajouter un candidat que si un signal positif précis le justifie.

## Étape 3 — Vérifier chaque candidat

- [ ] Exclure les ESN, SSII, cabinets de conseil et sociétés de services numériques. Vérifier l'activité réelle, pas le seul code NAF : ce sont des concurrents ou des partenaires de NDA, jamais des clients.
- [ ] Vérifier que la maturité tombe dans la fenêtre définie plus haut.
- [ ] Vérifier le secteur réel si le code API est ambigu. Un secteur inhabituel ne vaut pas exclusion : NDA a accompagné Savencia, groupe laitier, sur ses cas d'usage IA.
- [ ] Vérifier que la fonction visée existe en volume suffisant dans l'entreprise, pas seulement l'effectif total.
- [ ] Vérifier la capacité d'investissement : une entreprise en procédure collective ou en perte lourde sort.
- [ ] Vérifier la taille réelle de l'entité, sans se fier à `categorie_entreprise` : une filiale de groupe en hérite sans l'atteindre.

### Dédoublonner par groupe, avant de constituer le Top 20

L'API raisonne par unité légale, pas par groupe. Plusieurs filiales d'une même maison mère occupent donc plusieurs lignes de la longlist.

Repérer les doublons sur trois indices convergents : une racine de dénomination commune, la même activité principale, et le même département de siège. Confirmer en consultant les dirigeants ou la structure du groupe sur [data.inpi.fr](https://data.inpi.fr/) ou [Pappers](https://www.pappers.fr/).

Pour chaque groupe identifié, **ne garder qu'une entité** : celle qui porte réellement la fonction visée. La direction des systèmes d'information et la direction data siègent presque toujours dans la maison mère ou dans la principale entité opérationnelle, pas dans une filiale de distribution ou une société immobilière du groupe.

Mentionner les entités écartées sous le tableau, avec leur rattachement. Deux raisons : éviter qu'une prochaine campagne les repropose, et éviter que deux collaborateurs contactent le même groupe en croyant travailler deux cibles distinctes.

Repère qualité : si moins de 70 % de la longlist survit, élargir la longlist plutôt que compléter le Top 20 avec des candidats non vérifiés.

### Niveau de confiance

Qualifier chaque information retenue, plutôt que de tout présenter au même niveau :

| Niveau | Ce qu'il exige |
|---|---|
| Élevé | Deux sources indépendantes, ou une page officielle de l'entreprise |
| Moyen | Une source crédible, corroborée par un indice convergent |
| Faible | Information incomplète — signaler ce qui manque |

### Classement de chaque candidat

| Palier | Condition |
|---|---|
| **Chaud** | Fit confirmé, capacité d'investissement établie, fonction cible présente en volume |
| **Tiède** | Fit confirmé, mais un critère reste non vérifié |
| **Froid** | Fit lâche, ou un critère manque franchement |
| **Écarté** | Un critère d'exclusion est touché — ESN, client existant, entreprise en difficulté |

Une répartition saine tourne autour de 20 % de chaud et 30 % de tiède. Un Top 20 entièrement « chaud » signale une vérification trop indulgente.

## Étape 4 — Arrêter le Top 20

Cible par défaut : **20 entreprises distinctes, c'est-à-dire 20 groupes différents**. Deux filiales d'une même maison mère ne comptent que pour une.

Si le compte n'y est pas, distinguer deux causes avant de conclure :

- **Le vivier est trop étroit.** L'API a rendu peu de résultats, ou le dédoublonnage en a absorbé une bonne part. Élargir alors la recherche : codes d'activité voisins, catégorie de taille adjacente, secteur connexe, périmètre géographique plus large. Un test réel sur le transport en grande entreprise n'a rendu que 26 lignes, dont la moitié appartenant à deux groupes — élargir était la seule réponse correcte.
- **Le vivier est suffisant mais peu pertinent.** Là, livrer une liste plus courte et dire pourquoi. Le remplissage n'a pas de valeur.

Ne jamais compléter un Top 20 avec des entités du même groupe pour faire du nombre.

## Format de sortie

| Nom | Secteur | CA (millésime) | Date de création | Palier | Confiance | Source (URL) | Vérifié le | Pourquoi cette entreprise | Ressemble à |
|---|---|---|---|---|---|---|---|---|---|
| … | … | … | … | Chaud / Tiède / Froid | Élevée / Moyenne / Faible | (lien) | AAAA-MM-JJ | Une phrase de justification factuelle | Client NDA de référence |

La colonne « Pourquoi cette entreprise » porte l'essentiel : une justification rédigée, rattachée à un fait, vaut mieux qu'un score nu. Elle doit pouvoir être lue et contestée par un humain.

Préciser sous le tableau les filtres utilisés, les entités écartées pour cause de dédoublonnage avec leur groupe de rattachement, et les entreprises écartées avec leur motif — cela évite qu'une prochaine campagne les repropose.

## Limites

Cette skill automatise une étape que le prospecteur fait aujourd'hui à la main, et cet arbitrage n'est pas unanime : le praticien considère que l'entonnoir de constitution de listes reste manuel et que LinkedIn est la source la plus à jour, tandis que les essais de recherche assistée ont trouvé des cibles que l'outil précédent manquait. La skill retient la seconde option. Traiter sa sortie comme une longlist à valider par un humain, pas comme une liste arrêtée.

Deux critères ne sont pas couverts par l'API et se vérifient à la main : l'effectif dans la fonction visée, et la maturité technologique réelle.

## Enchaînement

Deux skills prennent le relais sur la même liste : `recherche-contacts-entreprise` (Skill 2, qui contacter) et `veille-signaux-affaires` (Skill 3, pourquoi et quand les contacter). Leurs sorties alimentent `ranking-entreprises-cibles` (Skill 3.5), qui fixe l'ordre de traitement avant l'activation par `suivi-relance-discours-prospection` (Skill 4).

Conserver la même liste d'entreprises d'une skill à l'autre plutôt que redemander le contexte.

Si la demande découle d'un discours de campagne déjà cadré (`discours-campagne-prospection`, Skill 0), reprendre ses critères de cible entreprise (groupe B) au lieu de les redemander.

## Sources

- API Recherche d'entreprises : https://recherche-entreprises.api.gouv.fr — [documentation](https://www.data.gouv.fr/dataservices/api-recherche-dentreprises). Maintenue par la DINUM avec l'INSEE et l'INPI. Ouverte, gratuite, Licence Ouverte 2.0, 7 appels/seconde.
- French Tech 120 / Next40 : https://frenchtech120.numeum.fr/ — annuaire Numeum, promotion 2026, libre d'accès.
- Registres légaux complémentaires, gratuits : [data.inpi.fr](https://data.inpi.fr/) (RNE, compte requis), [bodacc.fr](https://www.bodacc.fr/) (API sans clé), [annuaire-entreprises.data.gouv.fr](https://annuaire-entreprises.data.gouv.fr/) (vérification unitaire).
- Référence clients NDA : https://app.notion.com/p/nda-partners/Liste-des-clients-NDA-Industrie-Segment-3bf852cc7e1581d69b4af9ea8bc01793

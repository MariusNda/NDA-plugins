---
name: veille-signaux-affaires
description: >-
  Recherche des signaux d'affaires (trigger events : levée de fonds,
  recrutement, nomination, incident, appel d'offres…) sur des entreprises
  cibles déjà identifiées — presse économique, LinkedIn, recrutements,
  annonces légales, actualité cyber. Priorise chaque signal par fraîcheur
  et pertinence Data/IA/Cyber, avec un angle d'approche commercial par
  signal. Déclencher pour : « trouver des signaux », « veille sur une
  entreprise », « pourquoi/quand contacter telle entreprise », « triggers
  commerciaux », ou face à un Top 20 (ex. prospection-entreprise-cible) à
  prioriser. Marche pour une entreprise seule ou une liste. Différent de
  prospection-entreprise-cible (trouve de nouvelles entreprises) et
  recherche-contacts-entreprise (trouve qui contacter) : ici on part
  d'entreprises connues et on cherche pourquoi/quand les contacter. Les
  tiers produits ici alimentent ranking-entreprises-cibles (Skill 3.5),
  qui les recroise avec les contacts trouvés pour prioriser qui contacter
  en premier.
---

# Veille de signaux d'affaires (Skill 3)

**Entrée** : une ou plusieurs entreprises déjà identifiées.
**Sortie** : un tableau de signaux datés, sourcés et priorisés, avec un angle d'approche par signal.

## Objectif

Un signal d'affaires est un événement observable et daté — levée de fonds, recrutement, nomination, incident, appel d'offres — qui révèle un besoin concret, actuel ou imminent.

Cette skill répond à une question précise : pourquoi et quand contacter cette entreprise. Elle se distingue de la Skill 1, qui répond à « cette entreprise pourrait théoriquement avoir besoin de NDA ».

## Principes

**La fraîcheur prime.** Un signal se périme. Une levée de fonds ou une nomination de DSI se traite en jours ou en semaines. Un mouvement de fond — recrutements en hausse, migration cloud annoncée — se traite en semaines. Un signal isolé sans actualité récente n'a presque plus de valeur commerciale. Dater précisément chaque signal et le classer selon sa fraîcheur (Étape 4).

**Un signal est un prétexte d'entrée, pas une preuve de besoin.** Les entreprises communiquent le plus souvent après coup : le signal arrive donc en aval de la décision, rarement avant. Il ouvre une conversation — « j'ai vu que vous faisiez X, voici ce qu'on pourrait faire ensuite » — plus qu'il ne révèle un achat imminent. Formuler les angles d'approche dans ce registre, sans surjouer l'urgence.

**Le cumul fait le dossier.** Un signal isolé est un indice faible. Deux ou trois signaux convergents sur la même entreprise — nomination d'un DSI, recrutements Data en cours, levée de fonds récente — forment un dossier solide. Balayer plusieurs catégories par entreprise avant de conclure qu'il n'y a rien à signaler.

## Étape 0 — Clarifier la demande

Récupérer la liste d'entreprises. Elle arrive sous forme de tableau collé dans le chat (souvent la sortie de la Skill 1), de fichier, ou de simples noms cités.

Clarifier deux points avant de lancer la recherche.

1. **Fenêtre temporelle.** Via AskUserQuestion : 3 mois, 6 mois, 12 mois (par défaut), ou pas de limite. Un signal de plus d'un an n'est en général plus actionnable, sauf recherche volontairement large.
2. **Catégories à prioriser.** Les 8 catégories dépassent le seuil de 4 : les lister en clair dans le chat plutôt que via AskUserQuestion, puis demander lesquelles privilégier. L'utilisateur peut répondre « toutes » ou « passer ».

La recherche ne démarre qu'une fois ces deux points tranchés, ou sur demande explicite de lancer.

## Étape 1 — Vérifier les connecteurs disponibles

À faire à chaque exécution, pas une fois pour toutes.

Appeler `SearchMcpRegistry` avec des mots-clés comme « BODACC », « Pappers », « INPI », « BOAMP », « France Travail », « veille économique », « news monitoring ». Les connecteurs disponibles varient selon la session et l'organisation.

Si un connecteur pertinent est actif — base légale, presse spécialisée — l'utiliser en complément des recherches web. Sinon, le signaler dans le résultat final et procéder par WebSearch et WebFetch, avec le navigateur si le bridge Chrome est connecté.

Les API publiques listées dans `references/sources-verifiees.md` sont interrogeables directement, sans connecteur : BODACC et BOAMP n'exigent aucune clé, l'API Recherche d'entreprises aucune authentification.

## Étape 2 — Les 8 catégories de signaux

Pour chaque entreprise, balayer les huit catégories plutôt que s'arrêter au premier résultat. Les formulations de recherche associées figurent dans `references/typologie-signaux-requetes.md`.

1. **Financier / corporate** — levée de fonds, résultats en forte croissance, procédure collective, fusion-acquisition, changement d'actionnariat. Sources gratuites : **BODACC** (une augmentation de capital est un proxy daté d'une levée), INPI/RNE, BALO et Info-financière pour les sociétés cotées. Presse : Maddyness. Les Echos, La Tribune et Challenges sont sous paywall, à réserver à la lecture humaine.
2. **Dirigeants & organisation** — nomination d'un DG, DSI, CTO, CDO, RSSI, changement de comité de direction. Un dirigeant entrant réévalue souvent ses prestataires dans ses 90 premiers jours. Sources : communiqués de presse, page Direction du site, BODACC et INPI pour les mandataires sociaux, index du moteur pour repérer un changement de poste, sans ouvrir de page LinkedIn.
3. **Recrutement & croissance** — hausse des offres sur des postes Data/IA/Cyber/DSI, ouverture de bureaux ou de filiales, croissance d'effectif. Source gratuite et outillable : **l'API France Travail « Offres d'emploi v2 »**. Pages carrières de l'entreprise. Welcome to the Jungle par son sitemap. Indeed n'a plus d'API publique depuis 2023.
4. **Technologie & transformation** — migration cloud, projet IA annoncé, refonte de SI, adoption d'outils, partenariat technologique. Sources gratuites : LeMagIT, Le Monde Informatique, Journal du Net, tous avec flux RSS libre. **Ajouter la presse de la verticale traitée** : ces trois titres sont IT-centrés et parlent peu des ETI industrielles. Pour l'agroalimentaire, LSA Conso et L'Usine Nouvelle couvrent bien mieux ; chercher l'équivalent pour chaque secteur avant de conclure qu'il n'y a rien. L'Usine Digitale est en partie payante. Offres d'emploi mentionnant la stack, communiqués de partenaires tech.
5. **Cyber & conformité** — incident de sécurité, fuite de données, sanction ou mise en demeure CNIL, mise en conformité (NIS2, DORA, RGPD), certification ISO 27001 en cours. Sources : **CERT-FR** (avis et alertes ANSSI), **Cybermalveillance.gouv.fr**, page des sanctions CNIL, ZATAZ, LeMagIT.
6. **Commande publique** — appel d'offres ou marché public touchant à la Data, l'IA ou la Cyber. Pertinent surtout si l'entreprise émet elle-même des marchés. Sources : **API BOAMP**, PLACE (`marches-publics.gouv.fr`), les DECP consolidées pour les marchés attribués, TED pour l'échelon européen.
7. **Actualité stratégique générale** — nouveau produit, expansion géographique, partenariat commercial, changement de positionnement. Sources : rubrique presse du site de l'entreprise, flux RSS des médias cités ci-dessus. Google News n'a plus d'API et ses flux RSS sont interdits par son robots.txt : appoint manuel seulement.

8. **Signaux portés par l'interlocuteur** — publications et prises de parole récentes de la personne visée, changement de poste, ancienneté dans la fonction, sujets sur lesquels elle communique de façon répétée, cas d'usage publié sur le site de l'entreprise. Un directeur data qui publie régulièrement sur un sujet indique un intérêt actif, exploitable dans l'accroche. Sources : index du moteur sur les profils et publications (`site:linkedin.com/...`, sans ouvrir les pages), interventions en conférence, tribunes, rubrique « cas clients » du site.

Ne pas forcer une catégorie manifestement hors sujet, par exemple la commande publique pour une PME purement privée. Le préciser vaut mieux qu'inventer un signal.

## Étape 2 bis — Compiler le Trigger Playbook du segment

Une fois par campagne, pas par entreprise.

Avant de scanner les entreprises, synthétiser pour tout le segment un Trigger Playbook. Pour chaque catégorie retenue, expliciter pourquoi ce type de signal justifie un contact, et pas seulement qu'il existe.

| Catégorie | Logique métier | Fenêtre par défaut | Persona visée | Angle de message |
|---|---|---|---|---|
| Dirigeants & organisation | Un DSI entrant réévalue ses prestataires dans ses 90 premiers jours | Tier 1 | DSI/CTO entrant | Point de contexte avant qu'il fige ses choix |
| … | … | … | … | … |

Ce tableau sert de grille de lecture pour chaque entreprise scannée à l'Étape 3. La logique métier et l'angle sont fixés une fois ; il reste à vérifier si le signal concret existe et à le dater.

Si la campagne a été cadrée par `discours-campagne-prospection` (Skill 0), reprendre le momentum et la cible interlocuteur définis aux groupes A et C comme base du playbook.

## Étape 3 — Méthodologie de recherche

Pour chaque entreprise et chaque catégorie retenue :

- **Restreindre le champ, sinon la recherche rend du bruit.** Une requête généraliste du type `"Entreprise" 2026 IA OR recrutement data` remonte massivement des articles de fond sans rapport avec l'entreprise : un test réel a donné un seul résultat pertinent sur huit. La même recherche avec restriction `site:` en a donné huit sur huit. Toujours ajouter une restriction de site, ou un second ancrage propre à l'entreprise — une ville, un dirigeant, une marque.
- **Multiplier les requêtes.** Le nom de l'entreprise seul remonte rarement un signal précis. Combiner le nom exact, entre guillemets, avec des mots-clés de la catégorie visée. Des formulations prêtes à l'emploi figurent dans `references/typologie-signaux-requetes.md`.
- **Varier les angles** : flux RSS des médias spécialisés, recherche par site (`site:linkedin.com/company/...`, `site:welcometothejungle.com`), recherche par source spécialisée (nom du média et nom de l'entreprise).
- **Filtrer par date à chaque résultat.** Un article non daté ou vieux de plus d'un an sort du périmètre, sauf consigne contraire.
- **Privilégier la source primaire** — communiqué officiel, site de l'entreprise, presse spécialisée — plutôt qu'un blog ou un agrégateur qui reprend l'information sans la dater.
- **Ne jamais inventer un signal** à partir d'une déduction sectorielle du type « ce secteur est en transformation IA en ce moment ». Un signal se rattache à un événement concret, daté et sourcé. Si rien de concret n'apparaît, le dire.

## Étape 4 — Prioriser les signaux

Classer chaque signal dans l'un des trois niveaux. Les signaux les plus chauds se périment vite, les signaux de fond durent.

| Priorité | Fenêtre d'action | Exemples |
|---|---|---|
| **Tier 1 — agir sous 48 h** | Se périme très vite | Levée de fonds récente, nomination DSI/CDO/RSSI, appel d'offres ouvert, incident cyber ou sanction CNIL récente |
| **Tier 2 — agir sous 1 semaine** | Se périme en semaines | Hausse des recrutements Data/IA/Cyber, migration technologique annoncée, résultats en forte croissance, changement d'actionnariat |
| **Tier 3 — à surveiller** | Se périme en mois | Expansion géographique, actualité stratégique générale, certification en cours, mention de presse isolée |

**Cumul sectoriel.** Regarder aussi le cumul entre entreprises : quand un même type de signal apparaît chez plusieurs cibles du même secteur — une évolution réglementaire, une vague d'investissements, une tension commune — c'est le segment entier qui s'ouvre, pour quelques mois. Le signaler dans la synthèse : cela vaut souvent plus qu'un signal individuel spectaculaire, et alimente le Trigger Playbook de l'Étape 2 bis.

Appliquer l'effet de cumul par entreprise : une entreprise qui totalise deux signaux ou plus, même de tiers différents, remonte en tête de liste. Signaler explicitement la combinaison. C'est elle qui mérite le contact prioritaire, pas nécessairement le signal isolé le plus spectaculaire.

## Format de sortie

Ouvrir par une synthèse d'une ou deux phrases : les entreprises à contacter en priorité, c'est-à-dire celles qui cumulent plusieurs signaux ou portent un signal Tier 1.

Puis un tableau, une ligne par signal. Une entreprise à plusieurs signaux occupe plusieurs lignes.

| Entreprise | Signal détecté | Catégorie | Date | Source | Priorité | Angle d'approche NDA |
|---|---|---|---|---|---|---|
| … | … | … | … | (lien) | Tier 1/2/3 | … |

La colonne « Angle d'approche NDA » porte la valeur du tableau. Elle explique en une phrase pourquoi le signal justifie un contact et quel besoin il révèle. Exemple : « Nouveau DSI arrivé il y a 3 semaines → réévalue probablement les prestataires en place. »

Terminer par la liste des sources consultées et un rappel bref des limites.

## Limites

Rappeler dans la sortie, sans insister :

- la recherche s'appuie sur des sources publiques et sur les connecteurs disponibles : l'absence de signal trouvé ne signifie pas absence de signal réel, seulement absence de visibilité publique au moment de la recherche ;
- la fraîcheur et la complétude dépendent de la couverture presse de chaque entreprise — une PME peu médiatisée aura structurellement moins de signaux visibles qu'un grand groupe, sans que son potentiel soit moindre ;
- l'accès aux données d'intention propriétaires (visites de site, recherches d'outils) dépend des connecteurs actifs au moment de l'exécution.

## Enchaînement

Cette skill s'utilise après `prospection-entreprise-cible` (Skill 1), pour prioriser le Top 20, et avant ou en parallèle de `recherche-contacts-entreprise` (Skill 2). Conserver la même liste d'entreprises d'une skill à l'autre.

Les tiers produits à l'Étape 4 constituent l'une des deux entrées de `ranking-entreprises-cibles` (Skill 3.5), qui les recroise avec les contacts pour produire un classement par actionnabilité. Ce classement alimente ensuite `suivi-relance-discours-prospection` (Skill 4).

Si la Skill 2 a déjà tourné sur la même liste, proposer d'enchaîner sur la Skill 3.5 plutôt que s'arrêter au tableau de signaux.

## Références

- `references/sources-verifiees.md` — gratuité, API, accès sans compte et restrictions d'usage de chaque source, et sources payantes à ne pas présenter comme gratuites.
- `references/typologie-signaux-requetes.md` — requêtes prêtes à l'emploi pour les catégories d'entreprise, à adapter au nom de l'entreprise.

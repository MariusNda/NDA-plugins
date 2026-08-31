---
name: prospection-entreprise-cible
description: Recherche des entreprises cibles pour du look-alike commercial NDA, en croisant l'API ouverte Recherche d'entreprises (data.gouv.fr), l'annuaire French Tech 120/Next40, et la liste de référence des clients NDA dans Notion. Qualifie chaque cible sur sa maturité technologique (besoin réel de transformation Data/IA/Cyber), pas sur la seule ressemblance sectorielle. Déclencher quand un collaborateur demande de "trouver des entreprises cibles", "faire du look-alike", "chercher des prospects", "skill prospection entreprise cible".
---

# Prospection-Entreprise-cible

Objectif : à partir du look-alike des clients NDA, sortir un **Top 20 d'entreprises à qui NDA pourrait apporter quelque chose et à qui on pourrait montrer qu'elles ont besoin de nous**.

## Filtre par défaut

Critère : pas la ressemblance sectorielle, mais le besoin réel — IAM/API, Data/IA, architecture, transformation.

Ne jamais proposer une entreprise déjà présente dans [Liste des clients NDA — Industrie & Segment](https://app.notion.com/p/nda-partners/Liste-des-clients-NDA-Industrie-Segment-3bf852cc7e1581d69b4af9ea8bc01793).

La maturité technologique doit être dans la bonne fenêtre : trop en avance (digital-native, transition déjà faite seule) → notre aide serait inutile ; trop en retard (trop jeune/petite, pas encore de vrai enjeu) → pas encore concernée ; entre les deux → éligible.

Exemple repère : Alan vs MGEN — même secteur assurance-santé, besoin opposé.

## Règle d'interaction pour la sélection des filtres (à suivre strictement)

Parcourir les sections de filtres une par une, dans l'ordre ci-dessous. Pour chaque section :
- Si elle contient **4 paramètres ou moins** : poser une question à choix via l'outil AskUserQuestion, en proposant chaque paramètre de la section (+ une option pour passer la section).
- Si elle contient **plus de 4 paramètres** : NE PAS utiliser AskUserQuestion. Lister tous les paramètres de la section en clair dans le chat, et demander à l'utilisateur lesquels il veut utiliser.
- L'utilisateur peut répondre "passer" à n'importe quelle section pour l'ignorer et continuer.
- Ne jamais lancer la recherche avant d'avoir parcouru toutes les sections (ou que l'utilisateur ait dit de tout passer / de lancer maintenant).

## Sections et paramètres

### 1. Secteur / activité — 2 paramètres → AskUserQuestion
- `activite_principale` (code NAF précis)
- `section_activite_principale` (grande catégorie d'activité, A à U)

### 2. Taille — 2 paramètres → AskUserQuestion
- `categorie_entreprise` (PME / ETI / GE)
- `tranche_effectif_salarie` (tranche d'effectif salarié)

### 3. Localisation — 6 paramètres → liste en clair (pas d'AskUserQuestion)
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
- Rappel à mentionner : ce champ ne contient QUE les représentants légaux (gérant, président, DG, administrateurs), jamais les cadres opérationnels (CDO, managers, cadres sup) — utile pour l'étape 2 du look-alike, pas pour trouver les vrais interlocuteurs opérationnels.

### 8. Recherche libre — 1 paramètre → AskUserQuestion
- `q` (texte libre : nom, adresse, SIREN/SIRET)

## Process

1. **API Recherche d'entreprises** : appeler `https://recherche-entreprises.api.gouv.fr/search` avec uniquement les filtres choisis à l'étape précédente. Récupérer une longlist de 40-60 candidats (2-3x la cible), pas juste 20 — une partie sera éliminée à l'étape suivante. Toujours inclure `date_creation`.
2. **Next40/French Tech 120** ([https://frenchtech120.numeum.fr/](https://frenchtech120.numeum.fr/)) : à utiliser en complément seulement, jamais par défaut — ce vivier est digital-native, à l'opposé du profil recherché. N'en ajouter un candidat que si un signal positif spécifique le justifie.
3. **Vérifier chaque candidat** avant de le garder (voir checklist ci-dessous).
4. **Livrer le Top 20** (voir format ci-dessous).

## Sélection finale — Top 20

À partir de la longlist, ne retenir que les entreprises réellement pertinentes.
- Cible par défaut : 20 entreprises.
- Si moins de 20 sont vraiment pertinentes, livrer une liste plus courte plutôt que de compléter avec du remplissage.

## Checklist de vérification

- [ ] Exclure si ESN / SSII / cabinet de conseil / société de services numériques (vérifier l'activité réelle, pas juste le NAF) — ce sont des concurrents/partenaires NDA, jamais des clients
- [ ] Vérifier que la maturité tombe bien dans la fenêtre définie plus haut (ni trop en avance, ni trop en retard)
- [ ] Vérifier le secteur réel si le code API est ambigu (ne veut pas dire exclure un secteur inhabituel : NDA a déjà accompagné Savencia, groupe laitier, sur ses cas d'usage IA)

Repère qualité : si moins de 70% de la longlist survit, élargir la longlist plutôt que compléter le Top 20 avec des candidats non vérifiés.

## Livrable — Top 20

Tableau : `Nom | Secteur | Taille/Segment | Date de création | Source (API Data Gouv ou French Tech 120) | Ressemble à (client de référence)`

Préciser les filtres utilisés pour arriver à cette liste.

## Enchaînement avec les autres skills

Une fois le Top 20 livré, deux skills prennent le relais sur la même liste : **recherche-contacts-entreprise** (Skill 2, qui contacter) et **veille-signaux-affaires** (Skill 3, pourquoi/quand les contacter). Leurs deux sorties nourrissent ensuite **ranking-entreprises-cibles** (Skill 3.5), qui priorise qui traiter en premier avant l'activation par **suivi-relance-discours-prospection** (Skill 4). Garde la même liste d'entreprises d'une skill à l'autre plutôt que de redemander le contexte depuis zéro. Si la demande vient d'un discours de campagne déjà cadré (**discours-campagne-prospection**, Skill 0), reprends ses critères cible entreprise (Groupe B) au lieu de les redemander.

## Sources
- API Recherche d'entreprises : https://recherche-entreprises.api.gouv.fr (doc : https://www.data.gouv.fr/dataservices/api-recherche-dentreprises)
- French Tech 120 / Next40 : https://frenchtech120.numeum.fr/
- Référence clients NDA : https://app.notion.com/p/nda-partners/Liste-des-clients-NDA-Industrie-Segment-3bf852cc7e1581d69b4af9ea8bc01793

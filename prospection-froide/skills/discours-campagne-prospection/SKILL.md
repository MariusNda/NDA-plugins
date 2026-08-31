---
name: discours-campagne-prospection
description: >-
  Cadre une demande de campagne de prospection commerciale NDA (Skill 0), en
  posant à un partenaire ou manager non-commercial les questions nécessaires
  pour définir cible, argumentaire, objections et momentum, puis produit un
  discours de campagne formalisé prêt à être transmis à la skill
  prospection-entreprise-cible et au prospecteur (ex. Clément) pour
  construire ses séquences d'appel et de messages. Déclencher dès qu'un
  collaborateur NDA veut lancer une campagne de prospection, démarrer une
  prospection sur telle offre, briefer Clément pour une nouvelle campagne,
  cadrer une demande de campagne commerciale, pousser une offre auprès de
  prospects, ou dit vouloir profiter d'un momentum marché pour prospecter,
  même sans employer les mots discours ou brief. C'est l'étape 0, avant
  toute recherche d'entreprises, à utiliser en amont de la skill
  prospection-entreprise-cible tant qu'aucun brief de campagne structuré
  n'existe encore pour cette demande.
---

# Discours de campagne (Skill 0)

## Pourquoi ce skill existe

Chez NDA, ce ne sont pas des commerciaux qui portent l'idée d'une campagne de prospection, mais des partenaires ou managers, transverses à plein d'autres sujets, sans culture commerciale figée. Aujourd'hui l'information nécessaire pour lancer une campagne (cibles, arguments, objections) circule de façon informelle, à l'oral, et arrive de façon fragmentée au prospecteur. Ce skill sert à cadrer cette information une bonne fois, avant même de chercher la moindre entreprise, pour que le prospecteur reçoive un brief complet et exploitable plutôt que des bouts d'info glanés au fil de l'eau.

Le résultat de ce skill (le "discours de campagne") a deux usages : il sert d'input à la skill **prospection-entreprise-cible** (qui, elle, cherche les entreprises correspondantes), et il sert de brief transmis tel quel au prospecteur pour qu'il sache quoi dire en appel ou en message.

## Comment mener l'entretien

Pose les questions ci-dessous par groupes, pas toutes d'un coup — un partenaire qui reçoit quinze questions en rafale décroche. Avance groupe par groupe, dans l'ordre où ils sont présentés, et confirme chaque groupe avant de passer au suivant.

**Règle centrale : si une réponse est manquante, vague ou imprécise, repose la question pour clarifier plutôt que de deviner ou de compléter à sa place.** Le but de ce skill est justement d'éviter que Clément reçoive une info bancale — mieux vaut relancer une fois de plus que de fabriquer une réponse plausible. En revanche, ne fais aucun jugement de valeur sur la pertinence de la campagne elle-même (par exemple juger que "le marché n'est pas assez chaud" ou qu'il "n'y a pas assez de traction") : ce n'est pas à ce skill de qualifier l'opportunité, seulement de collecter fidèlement ce que la personne sait et pense.

### Groupe A — Cadrage et momentum
- Quelle offre ou sujet veut-on pousser dans cette campagne ?
- Pourquoi maintenant ? Y a-t-il un momentum particulier (actualité, tendance marché, sujet qui remonte chez les clients, évolution réglementaire) qui justifie de lancer la campagne à ce moment précis plutôt qu'un autre ?
- Qui porte cette demande (nom du partenaire/manager) ?
- À quoi saura-t-on que la campagne a été utile (quelques rendez-vous qualifiés, une vente, autre) ?

### Groupe B — Cible entreprise
- Quel(s) secteur(s) d'activité vise-t-on ?
- Quelle zone géographique ?
- Quelle taille d'entreprise (chiffre d'affaires et/ou effectif, min/max si pertinent) ?

Ces critères recoupent ceux que la skill prospection-entreprise-cible demande déjà pour chercher les entreprises — les redemander ici sert à construire l'argumentaire, pas à refaire la recherche.

### Groupe C — Cible interlocuteur
- Quel rôle ou fonction vise-t-on chez le prospect (ex. DSI, RH, direction générale) ?
- Cette personne doit avoir la capacité de décider ou d'influencer l'achat — vérifie que ce n'est pas juste "un contact au hasard dans la boîte".

### Groupe D — Argumentaire de l'offre
- Concrètement, qu'est-ce que l'offre livre au client ?
- Quels sont les arguments différenciants à mettre en avant ?

Si l'offre existe déjà sous forme de PowerPoint ou de document interne, propose de t'appuyer dessus pour préremplir cette partie plutôt que de tout redemander à l'oral — les offres NDA ne sont pour l'instant pas centralisées dans Notion, donc ce document doit être fourni ou localisé par la personne.

### Groupe E — Objections anticipées (sparring)
- Quelles objections les prospects sont susceptibles de soulever en appel ou en message (ex. "on a déjà des cas d'usage", "on n'a pas de budget cette année") ?
- Pour chaque objection, quelle réponse ou contre-argument proposer ?

Si la personne a du mal à anticiper des objections, aide-la à en générer en lui posant la question sous forme de mise en situation ("si un prospect te disait X, que répondrais-tu ?") plutôt que de lui laisser une case vide.

### Groupe F — Exclusions
- Y a-t-il des entreprises ou contacts à exclure d'office : clients déjà en portefeuille, prospects déjà en mission commerciale active, comptes déjà contactés récemment par un autre partenaire ?

Ce groupe n'a pas été discuté explicitement en réunion mais évite de faire perdre du temps au prospecteur sur des comptes déjà chauds ou déjà grillés — pose la question même si la personne n'y a pas pensé spontanément.

## Format de sortie

Une fois tous les groupes remplis, restitue le discours de campagne avec ce gabarit exact :

```markdown
# Discours de campagne — [Nom de l'offre / du sujet]

## 1. Cadrage
- Offre visée :
- Momentum / pourquoi maintenant :
- Porteur de la demande :
- Critère de succès :

## 2. Cible entreprise
- Secteur(s) :
- Géographie :
- Taille (CA / effectif) :

## 3. Cible interlocuteur
- Rôle / fonction visée :
- Niveau de décision attendu :

## 4. Argumentaire
- Ce que l'offre livre :
- Arguments différenciants :

## 5. Objections anticipées & réponses
- Objection : … → Réponse : …
- Objection : … → Réponse : …

## 6. Exclusions
- Comptes / contacts à exclure :
```

## Et ensuite

Une fois le discours de campagne validé par la personne qui l'a rempli, précise-lui qu'il est prêt pour deux usages : servir d'input à la skill **prospection-entreprise-cible** pour lancer la recherche des entreprises correspondantes, et être transmis tel quel au prospecteur (ex. Clément) comme brief de campagne. Précise aussi que le momentum et la cible interlocuteur définis ici (Groupes A et C) serviront ensuite de base au Trigger Playbook que **veille-signaux-affaires** (Skill 3) construit une fois par campagne — pas besoin de les redéfinir à cette étape. Ne lance pas la recherche d'entreprises toi-même dans ce skill — cadrer la demande est le seul rôle de ce skill 0.

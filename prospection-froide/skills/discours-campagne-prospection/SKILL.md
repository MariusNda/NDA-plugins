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

**Entrée** : une intention de campagne exprimée par un partenaire ou un manager.
**Sortie** : un discours de campagne formalisé, en six sections.

## Objectif

Chez NDA, les campagnes de prospection sont portées par des partenaires et des managers, pas par des commerciaux. L'information utile — cibles, arguments, objections — circule à l'oral et arrive fragmentée au prospecteur.

Cette skill collecte cette information une seule fois, avant toute recherche d'entreprises. Le discours obtenu a deux usages :

- il alimente la skill `prospection-entreprise-cible`, qui cherche les entreprises correspondantes ;
- il sert de brief transmis tel quel au prospecteur, qui sait alors quoi dire en appel ou en message.

## Principes

Deux règles encadrent l'entretien.

- **Relancer plutôt que deviner.** Une réponse manquante, vague ou imprécise se reformule en question. Compléter à la place de l'interlocuteur produit exactement l'information bancale que cette skill sert à éviter.
- **Recueillir la justification, ne pas trancher.** Le temps du prospecteur est une ressource rare : chaque porteur de campagne doit pouvoir dire pourquoi il la lance maintenant. La skill formalise cette justification et la rend lisible pour l'arbitrage. Elle ne rend pas elle-même le verdict — ni « le marché n'est pas assez chaud », ni « il n'y a pas assez de traction ». Elle collecte fidèlement ce que la personne sait et pense, et laisse décider.

- **Ne rien inventer.** Aucune réponse n'est complétée à la place de l'interlocuteur. Un argument, un chiffre ou une objection absent reste absent, et la case le signale.

## Statut de chaque affirmation

Un discours de campagne mélange des convictions et des faits, et cette différence se perd à l'oral. Marquer chaque argument, chaque objection et chaque critère d'un des trois statuts suivants :

| Statut | Ce qu'il signifie |
|---|---|
| **Hypothèse** | Personne ne l'a encore vérifié sur le terrain |
| **Validée** | Confirmée par au moins un échange réel avec un prospect |
| **Prouvée** | Confirmée par un résultat mesuré — un rendez-vous obtenu, une objection levée, une vente |

Ce n'est pas de la bureaucratie : c'est ce qui permet à la campagne suivante de partir de ce qui a marché plutôt que de tout réinventer. Une hypothèse qui reste une hypothèse après trente appels est une hypothèse fausse.

## Déroulé de l'entretien

Poser les questions par groupes, dans l'ordre ci-dessous. Confirmer chaque groupe avant de passer au suivant. Quinze questions d'affilée font décrocher l'interlocuteur.

### Groupe A — Cadrage et momentum

- Quelle offre ou quel sujet la campagne pousse-t-elle ?
- Pourquoi maintenant ? Un momentum particulier justifie-t-il ce lancement : actualité, tendance marché, sujet qui remonte chez les clients, évolution réglementaire ?
- Qui porte la demande (nom du partenaire ou du manager) ?
- À quoi se mesurera l'utilité de la campagne : quelques rendez-vous qualifiés, une vente, autre chose ?

Repères pour cadrer une attente réaliste, à proposer si la personne n'a pas d'ordre de grandeur en tête : environ 10 % de décrochage sur les appels, 5 % des appels aboutissant à une opportunité, 7 à 10 interactions par prospect avant de conclure, et une hypothèse maison de 10 % de conversion d'un premier rendez-vous vers une vente. Un rendez-vous qualifié se définit comme un échange avec une personne ayant la capacité d'acheter.

### Groupe B — Cible entreprise

- Quels secteurs d'activité sont visés ?
- Quelle zone géographique ?
- Quelle taille d'entreprise : chiffre d'affaires, effectif, minimum et maximum si pertinent ?

Ces critères recoupent ceux de la skill `prospection-entreprise-cible`. Ils servent ici à construire l'argumentaire, pas à refaire la recherche.

### Groupe C — Cible interlocuteur

- Quel rôle ou quelle fonction vise-t-on chez le prospect : DSI, RH, direction générale ?
- Cette personne décide-t-elle de l'achat ou l'influence-t-elle ? Un contact pris au hasard dans l'entreprise ne convient pas.
- Vise-t-on le décideur final (N) ou le prescripteur opérationnel (N-1) ? Les deux se travaillent différemment : le N valide et paie, le N-1 doit être convaincu pour porter le sujet en interne — et peut freiner s'il se sent contourné.

### Groupe D — Argumentaire de l'offre

- Que livre concrètement l'offre au client ?
- Quels arguments la différencient de la concurrence ?

Ce groupe se remplit en deux temps. Ce qui décrit l'offre — livrables, arguments différenciants — se récupère dans le document d'offre existant : proposer de s'appuyer dessus plutôt que de tout redemander à l'oral. Ce qui relève du momentum et du contexte du moment ne peut venir que de la personne qui lance la campagne.

Les offres NDA ne sont pas encore centralisées dans Notion : elles vivent sur SharePoint et le document doit être fourni ou localisé par la personne. Une table des offres est en projet ; vérifier son existence avant de conclure à l'absence de source.

### Groupe E — Objections anticipées

- Quelles objections les prospects soulèveront-ils en appel ou en message : « on a déjà des cas d'usage », « pas de budget cette année » ?
- Quelle réponse apporter à chacune ?

Si la personne peine à anticiper, poser la question en mise en situation : « si un prospect disait X, que répondriez-vous ? ». Une case vide vaut moins qu'une réponse imparfaite.

**Si la personne ne fournit aucune objection, ne pas laisser le groupe vide : en construire.** Ce n'est pas une contradiction avec la règle « ne rien inventer ». Inventer, c'est attribuer à un prospect une objection qu'il n'a pas formulée. Construire, c'est dériver méthodiquement les objections qu'une offre appelle par nature. Balayer les six familles ci-dessous et retenir celles qui s'appliquent réellement à cette offre et à cette cible :

| Famille | Question que se pose le prospect |
|---|---|
| Budget | Combien, et sur quelle ligne ? |
| Timing | Pourquoi maintenant plutôt que l'an prochain ? |
| Existant | Nous avons déjà un prestataire, ou nous le faisons en interne |
| Compétence | Mes équipes savent-elles absorber ça ? |
| Risque et conformité | Données, réglementation, dépendance |
| Preuve | Qu'est-ce qui me dit que ça marche chez quelqu'un comme moi ? |
| Autorité | Ce n'est pas moi qui décide |

Chaque objection ainsi construite entre au statut **Hypothèse**, jamais autrement, et se présente comme telle à la personne : « voici ce que le terrain renverra probablement, confirmez ou corrigez ». La réponse associée, elle, doit venir d'elle — c'est elle qui connaît l'offre.

Commencer par les objections déjà entendues sur le terrain plutôt que par des objections imaginées. La plus fréquente à ce jour : « on a déjà des cas d'usage », à laquelle NDA répond « vos cas d'usage sont en production — êtes-vous capables d'en qualifier les gains ? ». Enrichir cette base au fil des campagnes, en distinguant les objections réellement rencontrées de celles qui sont anticipées.

### Groupe F — Exclusions

- Quelles entreprises ou quels contacts exclure d'office : clients en portefeuille, prospects déjà en mission commerciale active, comptes contactés récemment par un autre partenaire ?

Ce groupe évite au prospecteur de travailler des comptes déjà chauds ou déjà grillés. Poser la question même si la personne n'y a pas pensé.

## Format de sortie

Une fois les six groupes remplis, restituer le discours avec ce gabarit exact.

```markdown
# Discours de campagne — [Nom de l'offre / du sujet]

## 1. Cadrage
- Offre visée :
- Momentum / pourquoi maintenant :
- Ce qui justifie de mobiliser le prospecteur sur cette campagne plutôt qu'une autre :
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

## 5. Objections & réponses
| Objection | Statut | Réponse |
|---|---|---|
| … | Hypothèse / Validée / Prouvée | … |

## 6. Exclusions
- Comptes / contacts à exclure :
```

## Limites

Cette skill cadre la demande, rien d'autre. Elle ne lance aucune recherche d'entreprises : c'est le rôle de la skill 1.

## Enchaînement

Une fois le discours validé par son auteur, signaler ses deux destinations : la skill `prospection-entreprise-cible` (Skill 1) pour lancer la recherche, et le prospecteur pour le brief de campagne.

Le momentum et la cible interlocuteur définis aux groupes A et C servent aussi de base au Trigger Playbook que construit `veille-signaux-affaires` (Skill 3), une fois par campagne. Les redéfinir à cette étape est inutile.

La base d'objections du groupe E alimente directement l'arbre de qualification d'appel que construit `suivi-relance-discours-prospection` (Skill 4), lui aussi une seule fois par campagne. Plus cette base est fournie ici, moins il y a à improviser au téléphone.

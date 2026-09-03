---
name: ranking-entreprises-cibles
description: >-
  Skill 3.5 de la prospection NDA : recroise le classement initial de
  pertinence/maturité d'une entreprise cible (Top 20 de
  prospection-entreprise-cible) avec les signaux d'affaires trouvés
  (veille-signaux-affaires) et les contacts identifiés
  (recherche-contacts-entreprise) pour produire un classement ajusté par
  "actionnabilité" réelle — la priorité effective de contact, pas seulement
  la pertinence théorique. Déclencher dès qu'un collaborateur NDA veut
  "prioriser" ou "reclasser" une liste d'entreprises cibles, veut savoir
  "par qui commencer" dans un Top 20, demande un "ranking" ou une
  "priorisation" combinant fit et signaux/contacts, ou a déjà en main un
  Top 20 + des signaux + des contacts sur les mêmes entreprises et veut une
  seule liste ordonnée pour agir. Vient après prospection-entreprise-cible
  (Skill 1), recherche-contacts-entreprise (Skill 2) et
  veille-signaux-affaires (Skill 3) ; produit l'ordre de priorité que
  suivi-relance-discours-prospection (Skill 4) utilise ensuite.
---

# Ranking des entreprises cibles par actionnabilité (Skill 3.5)

**Entrée** : le Top 20 (Skill 1), les signaux (Skill 3) et les contacts (Skill 2) sur la même liste.
**Sortie** : une liste unique ordonnée par actionnabilité, en attente de validation humaine.

## Objectif

Le Top 20 de la Skill 1 classe les entreprises par pertinence théorique : fit sectoriel et maturité technologique. Une entreprise très pertinente sur le papier peut n'avoir aucun signal récent ni contact identifiable. Ce n'est pas une opportunité actionnable, c'est un dossier à laisser mûrir. À l'inverse, une entreprise moyennement pertinente qui cumule un signal Tier 1 récent et plusieurs contacts qualifiés se contacte cette semaine.

Cette skill ne remplace ni la Skill 1, ni la Skill 2, ni la Skill 3. Elle les recombine pour répondre à une autre question : par qui commencer, concrètement, cette semaine.

## Étape 0 — Rassembler les trois entrées

Pour chaque entreprise :

1. son rang ou score de pertinence initial — sortie de `prospection-entreprise-cible` ;
2. les signaux trouvés et leur tier — sortie de `veille-signaux-affaires`, avec effet de cumul ;
3. les contacts identifiés et leur qualité — sortie de `recherche-contacts-entreprise` : nombre, rôle, coordonnées disponibles.

Si une entrée manque pour une entreprise, le classement continue. Noter le manque explicitement dans la sortie, par exemple « signaux non recherchés », plutôt que d'attribuer un 0 : l'absence de recherche n'équivaut pas à l'absence de signal.

Si aucune des trois skills amont n'a tourné sur la liste, le dire et proposer de les lancer. Ne pas improviser de scores.

## Étape 1 — Calculer les trois scores, sur 10

Ramener chaque entrée à un score comparable. Les seuils ci-dessous sont une hypothèse de travail, pas une règle validée : ils n'ont été arrêtés par aucune décision d'équipe. Le préciser dans la sortie et proposer de les ajuster dès que l'usage réel donne matière à comparer.

**Règles disqualifiantes, appliquées avant tout calcul.** Une entreprise qui remplit l'une de ces conditions sort du classement, quel que soit son score :

- elle figure déjà dans la liste des clients NDA ;
- c'est une ESN, une SSII ou un cabinet de conseil ;
- elle est en procédure collective ;
- elle a été contactée il y a moins de trois mois, par qui que ce soit chez NDA.

Les nommer explicitement dans la sortie, avec leur motif.

**Score Fit** — dérivé du rang dans le Top 20 (Skill 1).

| Rang initial | Score Fit |
|---|---|
| 1 à 5 | 10 |
| 6 à 10 | 7 |
| 11 à 15 | 5 |
| 16 à 20 | 3 |

**Score Signal** — dérivé du tier le plus haut atteint et du cumul (Skill 3).

| Situation | Score Signal |
|---|---|
| Aucun signal trouvé | 0 |
| 1 signal Tier 3 seulement | 2 |
| 1 signal Tier 2 | 5 |
| 2 signaux ou plus, tiers mélangés, ou 1 signal Tier 1 isolé | 8 |
| 2 signaux ou plus dont au moins un Tier 1 | 10 |

**Récence du dernier contact** — lue dans la base de suivi.

| Situation | Effet |
|---|---|
| Jamais contactée | Aucun ajustement |
| Contactée il y a plus de 12 mois | Aucun ajustement — mentionner l'historique dans la sortie |
| Contactée il y a 3 à 12 mois | Signaler, et reprendre le fil précédent plutôt que repartir de zéro |
| Contactée il y a moins de 3 mois | Disqualifiée pour cette vague |

**Score Contact** — dérivé du nombre et de la qualité des contacts (Skill 2).

| Situation | Score Contact |
|---|---|
| Aucun contact identifié | 0 |
| 1 contact, rôle générique ou coordonnées incomplètes | 4 |
| 1 contact qualifié : rôle pertinent, email ou LinkedIn | 7 |
| 2 contacts qualifiés ou plus, dont un décideur (CTO/CDO/RSSI/DG) | 10 |

## Étape 2 — Pondérer et combiner

```
Score d'actionnabilité = (Fit × 0,3) + (Signal × 0,4) + (Contact × 0,3)
```

Le signal pèse le plus lourd parce qu'il porte le « pourquoi maintenant ». Un bon fit sans signal ni contact n'est pas actionnable cette semaine : c'est un candidat pour une prochaine vague.

Indiquer toujours cette pondération dans la sortie et proposer de l'ajuster. Si le facteur bloquant côté NDA est le manque de contacts plutôt que le manque de signaux, le poids du Score Contact augmente.

## Étape 3 — Classer et signaler les mouvements

Trier par score d'actionnabilité décroissant pour obtenir le rang ajusté.

Tout écart de plus de 3 places entre rang initial et rang ajusté se signale et s'explique. Exemple : « Entreprise X : rang initial 12 → rang ajusté 2, portée par un signal Tier 1 récent et 2 contacts qualifiés. »

Traiter à part, dans une section **« À laisser mûrir »**, les entreprises à fit fort (rang initial 1 à 5) mais score d'actionnabilité inférieur à 4. Ce n'est pas une exclusion mais un report à une prochaine vague de veille ou de recherche de contacts. Le préciser comme tel.

## Format de sortie

Ouvrir par une synthèse d'une ou deux phrases : les 3 à 5 entreprises à traiter en priorité cette semaine, et pourquoi.

| Entreprise | Rang initial | Fit /10 | Signal /10 | Contact /10 | Actionnabilité /10 | Palier | Dernier contact | Rang ajusté | Mouvement |
|---|---|---|---|---|---|---|---|---|---|
| … | … | … | … | … | … | Chaud / Tiède / Froid | Jamais · ou AAAA-MM-JJ | … | ↑ / ↓ / = |

Paliers, alignés sur ceux de la Skill 1 : **Chaud** au-dessus de 7, **Tiède** entre 4 et 7, **Froid** en dessous de 4.

Ajouter ensuite la section « À laisser mûrir », si elle s'applique.

Terminer par trois éléments :

- la pondération utilisée et son caractère ajustable ;
- la liste des entreprises pour lesquelles une des trois entrées manquait, plutôt que de laisser deviner l'origine d'un score bas ;
- la liste des entreprises disqualifiées, avec le motif ;
- le statut **`🔴 En attente de validation`**.

## Limites

Cette skill ne recherche ni le fit, ni les signaux, ni les contacts. Si une entrée manque, elle le signale et propose de lancer la skill correspondante plutôt que d'inventer un score.

Le classement produit exige une validation humaine avant que la Skill 4 ne rédige le moindre message. Produire le tableau ne vaut jamais validation.

## Enchaînement

Cette skill s'utilise après `prospection-entreprise-cible` (Skill 1), `recherche-contacts-entreprise` (Skill 2) et `veille-signaux-affaires` (Skill 3), une fois leurs trois sorties disponibles pour la même liste.

Le rang ajusté fixe l'ordre de priorité que suit `suivi-relance-discours-prospection` (Skill 4) — mais seulement une fois le statut passé de « en attente de validation » à validé.

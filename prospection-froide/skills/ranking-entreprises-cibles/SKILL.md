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

## Pourquoi ce skill existe

Le Top 20 de prospection-entreprise-cible classe les entreprises par pertinence théorique (fit sectoriel, maturité technologique) — mais une entreprise très pertinente sur le papier peut n'avoir aucun signal récent et aucun contact identifiable : ce n'est pas encore une opportunité actionnable, c'est un dossier à laisser mûrir. À l'inverse, une entreprise moyennement pertinente peut avoir un signal Tier 1 tout chaud et plusieurs contacts déjà qualifiés — c'est elle qu'il faut contacter cette semaine.

Ce skill ne remplace ni la Skill 1 (fit), ni la Skill 3 (signaux), ni la Skill 2 (contacts) : il les recombine pour répondre à une question différente — « par qui je commence, concrètement, cette semaine ? »

## Étape 0 — Rassembler les trois entrées

Ce skill a besoin, pour chaque entreprise, de :
1. Son rang ou score de pertinence initial (sortie de **prospection-entreprise-cible** — le Top 20).
2. Les signaux trouvés et leur tier (sortie de **veille-signaux-affaires** — Tier 1/2/3, avec effet de cumul).
3. Les contacts identifiés et leur qualité (sortie de **recherche-contacts-entreprise** — nombre de contacts, rôle, coordonnées disponibles).

S'il manque une des trois entrées pour une entreprise, ne bloque pas tout le classement : note-le explicitement dans la sortie (par exemple « signaux non recherchés ») plutôt que de le noter à 0 — l'absence de recherche n'est pas équivalente à l'absence de signal réel. Si aucune des trois skills en amont n'a été lancée sur la liste, dis-le et propose de les lancer plutôt que d'improviser des scores.

## Étape 1 — Calculer les trois scores par entreprise (sur 10)

Ramène chaque entrée à un score comparable sur 10. Les seuils ci-dessous sont une première version raisonnable et volontairement simple — dis explicitement dans la sortie que ce sont des hypothèses de départ, à ajuster avec l'utilisateur si l'usage réel montre qu'elles ne reflètent pas bien la réalité du terrain.

**Score Fit** (dérivé du rang dans le Top 20 de la Skill 1) :

| Rang initial | Score Fit |
|---|---|
| 1 à 5 | 10 |
| 6 à 10 | 7 |
| 11 à 15 | 5 |
| 16 à 20 | 3 |

**Score Signal** (dérivé du tier le plus haut atteint et de l'effet de cumul, Skill 3) :

| Situation | Score Signal |
|---|---|
| Aucun signal trouvé | 0 |
| 1 signal Tier 3 uniquement | 2 |
| 1 signal Tier 2 | 5 |
| 2+ signaux cumulés (tiers mélangés), ou 1 signal Tier 1 isolé | 8 |
| 2+ signaux dont au moins un Tier 1 | 10 |

**Score Contact** (dérivé du nombre et de la qualité des contacts, Skill 2) :

| Situation | Score Contact |
|---|---|
| Aucun contact identifié | 0 |
| 1 contact, rôle générique ou coordonnées incomplètes | 4 |
| 1 contact qualifié (rôle pertinent + email ou LinkedIn) | 7 |
| 2+ contacts qualifiés, dont au moins un décideur (CTO/CDO/RSSI/DG) | 10 |

## Étape 2 — Pondérer et combiner

```
Score d'actionnabilité = (Score Fit × 0,3) + (Score Signal × 0,4) + (Score Contact × 0,3)
```

Le signal pèse le plus lourd (0,4) parce que c'est lui qui justifie le « pourquoi maintenant » : un bon fit sans signal ni contact n'est pas actionnable cette semaine, c'est un bon candidat pour une prochaine vague, pas pour celle-ci. Indique toujours cette pondération dans la sortie, et propose de l'ajuster si l'utilisateur a une priorité différente (par exemple si le vrai facteur bloquant côté NDA est le manque de contacts plutôt que le manque de signaux, monter le poids du Score Contact).

## Étape 3 — Classer et signaler les mouvements

Trie les entreprises par score d'actionnabilité décroissant pour obtenir le rang ajusté.

Pour toute entreprise dont le rang ajusté diffère de plus de 3 places par rapport au rang initial, signale-le explicitement et explique pourquoi (exemple : « Entreprise X : rang initial 12 → rang ajusté 2, portée par un signal Tier 1 récent et 2 contacts déjà qualifiés »).

Traite à part, dans une section **« À laisser mûrir »**, les entreprises à fit fort (rang initial 1 à 5) mais score d'actionnabilité faible (< 4) : ce n'est pas une exclusion, c'est un report à une prochaine vague de veille ou de recherche de contacts, à préciser comme tel.

## Étape 4 — Format de sortie

Ouvre par une courte synthèse : les 3 à 5 entreprises à traiter en priorité cette semaine, en une ou deux phrases, avec pourquoi.

Tableau principal :

| Entreprise | Rang initial (Fit) | Score Fit /10 | Score Signal /10 | Score Contact /10 | Score Actionnabilité /10 | Rang ajusté | Mouvement |
|---|---|---|---|---|---|---|---|
| … | … | … | … | … | … | … | ↑ / ↓ / = |

Puis, si applicable, la section « À laisser mûrir » (voir Étape 3).

Termine toujours par : un rappel de la pondération utilisée (Étape 2) et de son caractère ajustable ; la liste explicite des entreprises pour lesquelles une des trois entrées (fit, signal, contact) manquait, plutôt que de laisser deviner d'où vient un score bas ; et un statut explicite **`🔴 En attente de validation`** — ce classement doit être approuvé par un humain avant que suivi-relance-discours-prospection (Skill 4) ne commence à rédiger le moindre message. Ne jamais considérer implicitement que produire le tableau vaut validation.

## Enchaînement avec les autres skills

Ce skill s'utilise après **prospection-entreprise-cible** (Skill 1), **recherche-contacts-entreprise** (Skill 2) et **veille-signaux-affaires** (Skill 3), une fois que leurs trois sorties existent pour la même liste d'entreprises. Le rang ajusté qu'il produit est l'ordre de priorité que **suivi-relance-discours-prospection** (Skill 4) doit suivre pour décider par quelle entreprise commencer — mais seulement une fois le statut passé de « en attente de validation » à validé par un humain.

## Ce que ce skill ne fait pas

Il ne recherche ni le fit, ni les signaux, ni les contacts lui-même — si une des trois entrées manque pour une entreprise, il le signale et propose de lancer la skill correspondante plutôt que d'inventer un score.

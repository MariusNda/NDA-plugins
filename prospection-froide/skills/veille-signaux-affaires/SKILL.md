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

# Veille de signaux d'affaires sur des entreprises cibles

## Pourquoi cette méthode en particulier

Un signal d'affaires est un événement observable et daté (levée de fonds, recrutement, nomination, incident, appel d'offres...) qui révèle qu'une entreprise a, ou va bientôt avoir, un besoin concret — plutôt qu'une simple ressemblance sectorielle avec les clients NDA. C'est la différence entre "cette entreprise pourrait théoriquement avoir besoin de nous" (déjà couvert par la skill prospection-entreprise-cible) et "cette entreprise a un événement récent qui justifie de la contacter cette semaine".

Deux principes structurent tout le travail :

- **La fraîcheur prime.** Un signal se périme. Une levée de fonds ou une nomination de DSI se traite en jours ou semaines ; un mouvement de fond (recrutement en hausse, migration cloud annoncée) se traite en semaines ; un signal isolé sans actualité récente n'a presque plus de valeur commerciale. Toujours dater précisément chaque signal trouvé et le classer selon sa fraîcheur (voir Étape 4).
- **L'effet de cumul (stacking).** Un seul signal isolé est un indice faible. Deux ou trois signaux convergents sur la même entreprise (ex : nomination d'un nouveau DSI + recrutements Data en cours + levée de fonds récente) forment un dossier bien plus solide qu'un signal unique. Cherche systématiquement plusieurs catégories de signaux par entreprise avant de conclure qu'il n'y a "rien à signaler".

## Étape 0 — Clarifier la demande

Récupère la liste d'entreprises à traiter. Elle peut arriver sous forme de tableau collé dans le chat (par exemple la sortie de la skill prospection-entreprise-cible), de fichier, ou simplement de noms cités dans le message.

Précise deux choses avant de lancer la recherche :

1. **Fenêtre temporelle** — via AskUserQuestion, propose : 3 derniers mois / 6 derniers mois / 12 derniers mois (par défaut) / pas de limite. Un signal vieux de plus d'un an n'est en général plus actionnable, sauf recherche volontairement large.
2. **Catégories à prioriser** — il y a 7 catégories (voir Étape 2), donc plus de 4 : liste-les en clair dans le chat plutôt que d'utiliser AskUserQuestion, et demande lesquelles privilégier. L'utilisateur peut répondre "toutes" ou "passer" pour tout couvrir sans filtrer.

Ne lance la recherche qu'une fois ces deux points clarifiés (ou si l'utilisateur dit explicitement de tout couvrir / de lancer maintenant).

## Étape 1 — Vérifier les connecteurs disponibles (à chaque exécution)

Avant de partir sur la recherche manuelle, appelle `SearchMcpRegistry` avec des mots-clés comme "Crunchbase", "Pappers", "Societe.com", "BODACC", "Kaspr", "veille économique", "intent data", "news monitoring". Les connecteurs disponibles évoluent selon la session et l'organisation ; ne pars jamais du principe qu'aucun outil n'est branché sans avoir vérifié à ce moment précis.

Si un connecteur pertinent est disponible (base légale, presse spécialisée, intent data), utilise-le en complément des recherches web — il est en général plus fiable et plus à jour qu'une recherche Google seule. Si rien n'est disponible, dis-le clairement dans le résultat final et procède avec WebSearch/WebFetch (et le navigateur si le bridge Chrome est connecté, pour consulter des pages précises comme LinkedIn ou le site de l'entreprise).

## Étape 2 — Les 7 catégories de signaux à rechercher

Pour chaque entreprise, balaie systématiquement ces catégories plutôt que de s'arrêter au premier résultat trouvé. Chacune a ses propres sources et formulations de recherche type ; le détail des requêtes est dans `references/typologie-signaux-requetes.md`.

1. **Financier / corporate** — levée de fonds, résultats en forte croissance, procédure collective, fusion-acquisition, changement d'actionnariat. Sources : presse économique (Les Echos, La Tribune, Challenges), Bodacc, Pappers/Société.com, Crunchbase.
2. **Dirigeants & organisation** — nomination DG, DSI, CTO, CDO, RSSI, changement de comité de direction. Un nouveau dirigeant réévalue souvent ses prestataires dans ses 90 premiers jours. Sources : LinkedIn, communiqués de presse, Bodacc (mandataires sociaux).
3. **Recrutement & croissance** — hausse des offres d'emploi sur des postes Data/IA/Cyber/DSI, ouverture de nouveaux bureaux ou filiales, croissance d'effectif. Sources : LinkedIn Jobs, Welcome to the Jungle, Indeed, pages carrières.
4. **Technologie & transformation** — migration cloud, projet IA annoncé, refonte de SI, adoption de nouveaux outils, partenariat technologique. Sources : presse spécialisée (Usine Digitale, LeMagIT, Journal du Net), offres d'emploi mentionnant la stack technique, communiqués de partenaires tech.
5. **Cyber & conformité** — incident de sécurité, fuite de données, sanction ou mise en demeure CNIL, mise en conformité réglementaire (NIS2, DORA, RGPD), certification ISO 27001 en cours. Sources : CNIL (sanctions), presse cyber (LeMagIT, ZATAZ), communiqués officiels.
6. **Commande publique** — appel d'offres ou marché public en cours touchant à la Data/IA/Cyber (pertinent surtout si l'entreprise cible travaille avec le secteur public ou est elle-même un acteur public/parapublic). Sources : BOAMP, marches-publics.gouv.fr.
7. **Actualité stratégique générale** — nouveau produit, expansion géographique, partenariat commercial, changement de positionnement. Sources : Google News, site de l'entreprise (rubrique presse/actualités).

Ne force pas une catégorie qui ne s'applique manifestement pas (ex : commande publique pour une PME purement privée sans marché public) — précise-le plutôt que d'inventer un signal.

## Étape 2bis — Compiler le Trigger Playbook du segment (une fois par campagne, pas par entreprise)

Avant de scanner les entreprises une par une, synthétise **une seule fois pour tout le segment de la campagne** — pas entreprise par entreprise — un Trigger Playbook : pour chaque catégorie retenue à l'Étape 2, explicite pourquoi ce type de signal justifie un contact, pas seulement qu'il existe.

| Catégorie | Logique métier (pourquoi ça crée un besoin) | Fenêtre par défaut | Persona visée | Angle de message par défaut |
|---|---|---|---|---|
| ex : Dirigeants & organisation | Un nouveau DSI réévalue ses prestataires dans ses 90 premiers jours | Tier 1 | DSI/CTO entrant | Point de contexte avant qu'il fige ses choix |
| … | … | … | … | … |

Ce tableau sert ensuite de grille de lecture pour chaque entreprise scannée à l'Étape 3 : tu n'as plus à réinventer la logique métier ou l'angle à chaque nouvelle entreprise, seulement à vérifier si le signal concret existe et à le dater. Si la campagne a été cadrée par **discours-campagne-prospection** (Skill 0), reprends le momentum et la cible interlocuteur qui y ont été définis (Groupes A et C) comme base de ce playbook plutôt que de repartir de zéro.

## Étape 3 — Méthodologie de recherche

Pour chaque entreprise et chaque catégorie retenue à l'étape 0 :

- Multiplie les recherches plutôt que de te contenter d'une requête générique : le nom de l'entreprise seul remonte rarement un signal précis. Combine toujours le nom exact de l'entreprise (entre guillemets) avec des mots-clés de la catégorie visée (voir `references/typologie-signaux-requetes.md` pour des exemples de formulations prêtes à l'emploi).
- Varie les angles : recherche généraliste (Google News), recherche ciblée par site (`site:linkedin.com/company/...`, `site:welcometothejungle.com`), recherche par source spécialisée (nom du média + entreprise).
- Filtre mentalement par date à chaque résultat trouvé : un article non daté ou ancien de plus d'un an sort du périmètre sauf mention contraire de l'utilisateur.
- Privilégie la source primaire (communiqué officiel, page LinkedIn de l'entreprise, article de presse spécialisée) à un blog ou agrégateur secondaire qui reprend l'info sans la dater précisément.
- N'invente jamais un signal à partir d'une simple déduction sectorielle ("ce secteur est en général en transformation IA en ce moment") : un signal doit être rattaché à un événement concret, daté, et sourcé. Si rien de concret n'est trouvé pour une entreprise, dis-le clairement plutôt que de forcer un résultat.

## Étape 4 — Prioriser les signaux trouvés

Classe chaque signal détecté dans un des trois niveaux, en t'inspirant de la logique du signal-based selling (les signaux les plus "chauds" se périment vite, les signaux de fond durent plus longtemps) :

| Priorité | Fenêtre d'action | Exemples de signaux |
|---|---|---|
| **Tier 1 — Agir sous 48h** | Se périme très vite | Levée de fonds récente, nomination DSI/CDO/RSSI, appel d'offres ouvert, incident cyber/sanction CNIL récente |
| **Tier 2 — Agir sous 1 semaine** | Se périme en semaines | Hausse des recrutements Data/IA/Cyber, migration technologique annoncée, résultats financiers en forte croissance, changement d'actionnariat |
| **Tier 3 — À surveiller** | Se périme en mois | Expansion géographique, actualité stratégique générale, certification en cours, mention de presse isolée sans suite |

Applique l'effet de cumul : si une même entreprise cumule 2 signaux ou plus (même de tiers différents), remonte-la en tête de liste et signale explicitement la combinaison — c'est elle qui mérite le contact prioritaire, pas nécessairement l'entreprise avec le signal isolé le plus spectaculaire.

## Étape 5 — Format de sortie

Ouvre toujours par une courte synthèse : les entreprises à contacter en priorité (celles qui cumulent plusieurs signaux ou un signal Tier 1), en une ou deux phrases.

Puis un tableau, une ligne par signal (une entreprise avec plusieurs signaux occupe plusieurs lignes) :

| Entreprise | Signal détecté | Catégorie | Date | Source | Priorité | Angle d'approche NDA |
|---|---|---|---|---|---|---|
| ... | ... | ... | ... | (lien) | Tier 1/2/3 | Pourquoi ce signal ouvre une conversation Data/IA/Cyber |

La colonne "Angle d'approche NDA" est importante : ne te contente pas de rapporter le fait, explique en une phrase pourquoi il justifie un contact et quel besoin potentiel il révèle (ex : "Nouveau DSI arrivé en poste il y a 3 semaines → réévalue probablement les prestataires en place").

Termine par la liste des sources consultées (liens) et un bref rappel des limites (Étape 6).

## Étape 6 — Limites à toujours mentionner explicitement

Rappelle dans la sortie, sans être lourd : que la recherche s'appuie sur des sources publiques (et des connecteurs si disponibles), donc que l'absence de signal trouvé ne veut pas dire absence de signal réel — seulement qu'il n'est pas visible publiquement au moment de la recherche ; que la fraîcheur et la complétude dépendent de la couverture presse de chaque entreprise (une PME peu médiatisée aura structurellement moins de signaux visibles qu'un grand groupe, sans que cela reflète son potentiel réel) ; et que la disponibilité de données d'intention propriétaires (visites de site, recherches d'outils) dépend des connecteurs actifs au moment de l'exécution.

## Enchaînement avec les autres skills

Cette skill s'utilise naturellement après **prospection-entreprise-cible** (pour prioriser le Top 20 obtenu) et avant **recherche-contacts-entreprise** (une fois les entreprises prioritaires identifiées, on cherche qui contacter chez elles). Si l'utilisateur enchaîne les trois, garde la même liste d'entreprises d'une skill à l'autre plutôt que de redemander le contexte depuis zéro.

Les tiers de priorité produits à l'Étape 4 (et l'effet de cumul) sont l'une des deux entrées directes de **ranking-entreprises-cibles** (Skill 3.5), qui les recroise avec les contacts trouvés par recherche-contacts-entreprise pour produire un classement final par actionnabilité, ensuite utilisé par suivi-relance-discours-prospection (Skill 4). Si l'utilisateur a aussi lancé recherche-contacts-entreprise sur la même liste, propose d'enchaîner sur ranking-entreprises-cibles plutôt que de s'arrêter au tableau de signaux seul.

## Pour aller plus loin

- `references/typologie-signaux-requetes.md` : exemples de requêtes de recherche prêtes à l'emploi pour chacune des 7 catégories de signaux, à adapter au nom de l'entreprise recherchée.

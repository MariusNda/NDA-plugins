# prospection-froide

Plugin Claude regroupant le pipeline complet de prospection commerciale NDA Partners : du cadrage d'une campagne jusqu'à la relance des contacts, en passant par la recherche de cibles, de contacts et de signaux d'affaires.

## Skills incluses

| Ordre | Skill | Rôle |
|---|---|---|
| 0 | `discours-campagne-prospection` | Cadre la demande de campagne : cible, argumentaire, objections, momentum |
| 1 | `prospection-entreprise-cible` | Recherche des entreprises cibles par look-alike (data.gouv.fr, French Tech 120, clients NDA) |
| 2 | `recherche-contacts-entreprise` | Identifie les interlocuteurs à contacter dans les entreprises cibles |
| 3 | `veille-signaux-affaires` | Recherche les signaux d'affaires qui justifient un contact |
| 3.5 | `ranking-entreprises-cibles` | Recombine fit, signaux et contacts en un classement d'actionnabilité |
| 4 | `suivi-relance-discours-prospection` | Séquence multicanale, message, brief d'appel et arbre de qualification, sparring, suivi de pipeline |

La skill `prospection-froide` affiche le message d'accueil du plugin. Elle ne produit aucun livrable de prospection.

## Comment ça marche

Chaque skill se déclenche automatiquement quand une demande y correspond. « Lance-moi une campagne de prospection sur X » déclenche `discours-campagne-prospection`. Les skills s'enchaînent dans l'ordre du tableau, chaque sortie alimentant la suivante.

```
0. Cadrage de campagne
        │
        ▼
1. Entreprises cibles
        │
   ┌────┴────┐
   ▼         ▼
2. Contacts   3. Signaux d'affaires
   │             │
   └──────┬──────┘
          ▼
3.5. Ranking (validation humaine requise)
          ▼
4. Suivi / relance / séquence (jamais d'envoi automatique)
```

## Structure d'une skill

Les SKILL.md du plugin suivent une ossature commune, pour rester lisibles autant par un humain que par le modèle. Les sections non pertinentes pour une skill donnée sont omises, jamais renommées.

| Section | Contenu |
|---|---|
| En-tête `Entrée` / `Sortie` | Ce que la skill consomme et ce qu'elle produit, en deux lignes |
| `## Objectif` | À quoi sert la skill, et ce qui la distingue des voisines |
| `## Principes` | Les règles de fond qui gouvernent le travail |
| `## Étape N — …` | Le déroulé opératoire |
| `## Format de sortie` | Le gabarit exact du livrable |
| `## Limites` | Ce que la skill ne fait pas, et ce qu'elle rappelle en sortie |
| `## Enchaînement` | Place dans le pipeline, amont et aval |
| `## Références` | Fichiers `references/` et sources externes |

Convention de rédaction : ton de documentation, formulations à l'infinitif, phrases courtes. Le texte ne s'adresse ni au modèle ni au lecteur en particulier.


## Installation

Installer ce plugin dans Claude Desktop depuis ce repo. Une fois installé, la commande `/prospection-froide` affiche un message d'accueil qui résume le fonctionnement.

## Mises à jour

Aucune synchronisation automatique. Après une modification poussée sur ce repo, chaque utilisateur doit relancer l'installation du plugin pour récupérer la dernière version.

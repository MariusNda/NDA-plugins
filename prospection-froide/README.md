# prospection-froide

Plugin Claude regroupant le pipeline complet de prospection commerciale NDA Partners : du cadrage d'une campagne jusqu'à la relance des contacts, en passant par la recherche de cibles, de contacts et de signaux d'affaires.

## Skills incluses

| Ordre | Skill | Rôle |
|---|---|---|
| 0 | `discours-campagne-prospection` | Cadre la demande de campagne (cible, argumentaire, objections, momentum) avec la personne qui la lance |
| 1 | `prospection-entreprise-cible` | Recherche des entreprises cibles par look-alike (data.gouv.fr, French Tech 120, clients NDA) |
| 2 | `recherche-contacts-entreprise` | Identifie les bons interlocuteurs à contacter dans les entreprises cibles |
| 3 | `veille-signaux-affaires` | Recherche les signaux d'affaires (trigger events) qui justifient un contact |
| 3.5 | `ranking-entreprises-cibles` | Recombine fit, signaux et contacts en un classement d'actionnabilité |
| 4 | `suivi-relance-discours-prospection` | Suivi de pipeline, messages personnalisés et préparation aux objections |

## Comment ça marche

Chaque skill se déclenche automatiquement quand une demande y correspond (ex. "lance-moi une campagne de prospection sur X" déclenche `discours-campagne-prospection`). Elles s'enchaînent dans l'ordre du tableau ci-dessus, chaque sortie alimentant la skill suivante.

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
4. Suivi / relance (jamais d'envoi automatique)
```

## Installation

Installer ce plugin dans Claude Desktop depuis ce repo. Une fois installé, taper `/prospection-froide` affiche un message d'accueil qui résume le fonctionnement.

## Mises à jour

Aucune synchronisation automatique : après une modification poussée sur ce repo, chaque utilisateur doit relancer l'installation du plugin pour récupérer la dernière version.

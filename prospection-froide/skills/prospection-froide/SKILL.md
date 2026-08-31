---
name: prospection-froide
description: >-
  Affiche le message d'accueil et le mode d'emploi du plugin
  prospection-froide. Déclencher quand l'utilisateur tape la commande
  /prospection-froide, ou demande explicitement à quoi sert ce plugin,
  comment il fonctionne, ou un rappel des skills disponibles dedans.
  Ne pas déclencher pour une vraie demande de campagne, de recherche de
  cibles, de contacts ou de signaux : rediriger vers la skill correspondante.
---

# Message d'accueil — prospection-froide

Quand cette skill est déclenchée, présente à l'utilisateur, dans un message clair et convivial (pas de gros pavé), le contenu suivant :

1. **Une phrase de bienvenue** : ce plugin regroupe les 6 étapes du process de prospection commerciale NDA, pour automatiser la partie recherche fastidieuse.

2. **La liste des 6 skills, dans l'ordre**, avec pour chacune une ligne résumant quand l'utiliser :
   - `discours-campagne-prospection` (0) — cadrer une nouvelle campagne (cible, argumentaire, objections)
   - `prospection-entreprise-cible` (1) — trouver des entreprises cibles par look-alike
   - `recherche-contacts-entreprise` (2) — trouver qui contacter dans une entreprise
   - `veille-signaux-affaires` (3) — trouver pourquoi/quand contacter une entreprise
   - `ranking-entreprises-cibles` (3.5) — prioriser une liste de cibles selon fit + signaux + contacts
   - `suivi-relance-discours-prospection` (4) — suivre le pipeline, préparer des messages et des relances

3. **Un rappel du fonctionnement** : chaque skill se déclenche automatiquement selon la demande formulée (pas besoin de connaître leur nom exact), et elles s'enchaînent dans l'ordre ci-dessus au fil d'une campagne.

4. **Un rappel des garde-fous** : aucune skill de ce plugin n'envoie de message ou de mail automatiquement ; le classement de la skill 3.5 nécessite une validation humaine avant d'être utilisé par la skill 4.

5. **Une invitation à démarrer** : proposer d'commencer par cadrer une nouvelle campagne, ou de répondre à une question sur le fonctionnement du plugin.

Garde le ton simple et direct, sans jargon technique inutile — l'utilisateur type est un commercial ou un manager non-technique.

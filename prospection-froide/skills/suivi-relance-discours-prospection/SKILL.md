---
name: suivi-relance-discours-prospection
description: >-
  Skill 4 de la prospection NDA, après le premier contact. Trois usages :
  rapport de suivi de la base Notion Pipeline prospection (qui relancer,
  par quel canal, sans jamais rien envoyer soi-même) ; fiche de contact
  en tableau (message personnalisé, contrainte potentielle, insights)
  pour une ou plusieurs entreprises cibles, basée sur les signaux
  trouvés ; sparring approfondi (toutes les contraintes/objections
  d'une entreprise + réponses). Déclencher pour : qui relancer en
  prospection, état des lieux de la pipeline, message ou fiche de
  contact pour une ou plusieurs cibles à partir d'un signal récent, ou
  anticiper les objections avant un appel. Vient après
  prospection-entreprise-cible, veille-signaux-affaires, le Skill 0
  discours-campagne-prospection, et ranking-entreprises-cibles (Skill
  3.5) quand un classement ajusté existe pour la liste traitée.
---

# Suivi, discours et sparring de prospection (Skill 4)

## Pourquoi ce skill existe

Une fois qu'une campagne est lancée et que les premiers contacts sont partis, il reste trois besoins récurrents que personne ne traite de façon structurée aujourd'hui : savoir qui relancer sans avoir à éplucher la base à la main, savoir quoi dire de personnalisé à une entreprise précise plutôt qu'un message générique, et anticiper les blocages propres à cette entreprise avant d'appeler. Ce skill couvre les trois, comme trois modes distincts — utilise celui qui correspond à la demande, pas besoin de faire les trois à chaque fois.

Quand plusieurs entreprises sont à traiter en Mode 2 ou Mode 3 et qu'un classement ajusté par actionnabilité existe (skill **ranking-entreprises-cibles**, Skill 3.5), suis cet ordre de priorité pour décider par quelle entreprise commencer, plutôt que l'ordre brut du Top 20 de prospection-entreprise-cible — c'est justement ce que ce classement ajusté sert à trancher. S'il n'existe pas encore et que la liste comporte plusieurs entreprises avec des niveaux de signaux/contacts très différents, propose de le lancer avant de rédiger les messages. Si ce classement existe mais porte encore le statut « 🔴 En attente de validation », dis-le et attends la validation humaine avant de rédiger le moindre message — ne pars pas d'un classement non validé.

## Mode 1 — Rapport de suivi (lecture seule, aucun envoi)

**Règle absolue : ce mode ne fait strictement que lire et rapporter. Il n'envoie jamais de message, de mail ou de notification à qui que ce soit — ni au prospect, ni en interne (pas de Teams, pas d'email). Il ne rédige même pas de brouillon. Il dit uniquement qui est en attente d'une action, et laisse la personne agir elle-même.** C'est un choix explicite : l'envoi réel vers de vrais prospects est une action à trop fort enjeu pour être automatisée sans validation humaine à chaque étape.

Étapes :
1. Cherche dans Notion la base **"Pipeline prospection"** (elle vit dans la page "PoC Prospection"). Si sa localisation a changé, recherche-la par son nom plutôt que de supposer une URL figée.
2. Pour chaque prospect, regarde la séquence à trois étapes et ses dates : `#1 - Status` / `#1 - Date d'envoi` (message LinkedIn), `#2 - Status` / `#2 - Date d'envoi` (mail de relance), `#3 - Status` / `#3 - Date du dernier appel` (appel).
3. Applique la cadence observée dans le workflow de la page (à ajuster si la personne te donne d'autres délais) : si `#1` est "Envoyé" depuis 3 jours ou plus et `#2` est encore "To-do", l'étape mail de relance est due ; si `#2` est "Envoyé" depuis 5 jours ou plus et `#3` est encore "To-do", l'appel est dû ; au-delà de 10 jours sans réponse après le dernier canal utilisé, signale que c'est la dernière relance ou la fin de cycle à envisager.
4. Restitue un rapport simple, trié par urgence (le plus en retard d'abord) :

```markdown
## Rapport de suivi — Pipeline prospection [date]

| Entreprise | Prospect | Étape due | En attente depuis | Action à faire |
|---|---|---|---|---|
| … | … | Mail de relance (#2) | 5 jours | Envoyer le mail de relance |
```

Si une donnée manque pour juger (pas de date d'envoi renseignée par exemple), indique-le comme tel dans le rapport plutôt que de l'ignorer ou de deviner une échéance.

## Mode 2 — Fiche de contact en tableau, message personnalisé basé sur les signaux

Pour une ou plusieurs entreprises cibles, le livrable de ce mode est un **tableau**, une ligne par contact — pas un message isolé en texte libre. Chaque ligne doit rester exploitable telle quelle (copiable dans Notion), donc reste concis dans chaque colonne plutôt que de délayer.

**Prérequis bloquants (par entreprise) :**
- Contact + rôle connus (skill recherche-contacts-entreprise) — sinon dis-le et propose de la lancer, plutôt que de deviner un rôle.
- Signal daté et sourcé sur l'entreprise (skill veille-signaux-affaires) — sinon dis-le et propose de la lancer, plutôt que d'inventer un signal.

**Rédaction du message (colonne "Message").** LinkedIn plafonne une note de connexion à 300 caractères ; un message direct technique peut aller jusqu'à 8000, mais un message court convertit nettement mieux (environ deux fois mieux sous 200 caractères qu'entre 500 et 1000). Vise 300-500 caractères pour un message direct, précise si c'est une note de connexion ou un message direct. Structure : (1) constat factuel tiré du signal, pas une généralité sectorielle ; (2) défi implicite en une phrase ; (3) référence courte à une mission NDA comparable, sans détailler ; (4) proposition d'échange courte, sans pitch complet. N'invente jamais référence client, chiffre ou détail de signal — demande plutôt que de combler l'espace. Registre direct et factuel, jamais de tournure IA lisse ("j'espère que vous allez bien"), ouverture sous 60 mots.

**Adapter au rôle (influence le contenu du message et la colonne "Insights") :**
- **CTO / DSI** : angle technique — scalabilité, dette technique, charge de l'équipe interne.
- **RSSI / CISO** : angle risque/conformité (NIS2, DORA, RGPD), pas de ton anxiogène.
- **CDO / Directeur Data-IA** : angle valeur métier — cas d'usage, ROI comparable.
- **PDG / Direction générale** : angle stratégique — positionnement concurrentiel, transformation à l'échelle.
- Rôle inconnu ou ambigu : angle business générique, sans deviner.

Pour aller plus loin : [Selling to C-Suite Decision-Makers](https://reply.io/selling-to-c-suite/) et [Tailoring Messaging for Different Buyer Personas](https://blog.segment8.com/posts/messaging-persona-specific/).

**Colonne "Contrainte potentielle".** L'objection la plus probable pour *cette* entreprise en une phrase (voir logique du Mode 3) — pas une liste, juste la plus probable. Si l'utilisateur veut approfondir une entreprise précise avec plusieurs contraintes et leurs réponses, renvoie-le vers le Mode 3.

**Colonne "Insights".** 2 à 4 puces courtes (`• …`, séparées par `<br>` dans la cellule) : le signal exact utilisé et sa fraîcheur, pourquoi il ouvre une conversation, l'angle choisi pour le rôle du destinataire. Pas de généralité — chaque puce doit être spécifique à l'entreprise ou au contact.

**Relecture avant de livrer (8 vérifications).** Avant de figer la colonne "Message", relis-le contre ces 8 règles et corrige tout ce qui échoue plutôt que de livrer un brouillon :
1. Pas de tiret cadratin (—) — casse le ton conversationnel.
2. Pas de question rhétorique ("Vous galérez avec... ?") — ça sent le template.
3. Pas de flatterie générique — un compliment doit citer un fait vérifiable, sinon l'enlever.
4. Pas de jargon ("leverage", "synergies", "best-in-class"...).
5. Le premier mot n'est jamais "Je" — démarre sur le contexte du prospect, pas sur soi.
6. Pas de demande de RDV dans le premier message — la valeur doit venir avant.
7. Limites de mots respectées : note de connexion ≤ 300, message direct 300-500, cohérent avec la règle de longueur ci-dessus.
8. Objet de mail (si applicable) : max 6 mots, spécifique, jamais "Question rapide".

**Format de sortie :**

```markdown
| Entreprise (domaine) | Personne (rôle) | LinkedIn | Message | Contrainte potentielle | Insights |
|---|---|---|---|---|---|
| … | … (…) | (lien) | … | … | • … <br> • … |
```

**Avant d'envoyer.** Rappelle à l'utilisateur de vérifier dans Notion que chaque contact n'a pas déjà été contacté, et de mettre la ligne à jour une fois le message envoyé — pour éviter un double contact.

## Mode 3 — Sparring approfondi : toutes les contraintes et objections d'une entreprise

Pour aller plus loin que la colonne "Contrainte potentielle" du Mode 2 sur une entreprise précise, liste toutes les contraintes ou objections que *cette entreprise en particulier* est susceptible de soulever — pas des objections génériques comme dans le Skill 0, mais celles qui tiennent à son secteur, son contexte réglementaire ou sa situation connue (par exemple une contrainte de conformité sectorielle, une dépendance à un système existant, un cycle de décision long). Pour chacune, propose une réponse. Si tu manques d'information sur le contexte réel de l'entreprise pour anticiper des contraintes crédibles, dis-le et propose de faire une recherche web rapide sur son secteur plutôt que d'inventer des contraintes plausibles mais non vérifiées.

```markdown
## Sparring — [Entreprise]

- Contrainte : … → Réponse proposée : …
- Contrainte : … → Réponse proposée : …
```

## Ce que ce skill ne fait pas

Il ne lance pas de recherche d'entreprises (c'est prospection-entreprise-cible), il ne cherche pas les signaux lui-même s'ils ne sont pas fournis (c'est veille-signaux-affaires), et il n'envoie jamais rien à personne. Si la demande dépasse un de ces trois modes, dis-le clairement plutôt que d'improviser.

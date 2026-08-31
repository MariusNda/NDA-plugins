---
name: recherche-contacts-entreprise
description: >-
  Identifie les bons interlocuteurs à contacter dans une ou plusieurs
  entreprises cibles déjà identifiées (prospection B2B), et fournit une liste
  de contacts avec rôle, profil LinkedIn, email et téléphone quand c'est
  trouvable, avec sources et rappel RGPD/CNIL. Déclencher dès qu'un
  collaborateur NDA demande qui contacter chez une entreprise, veut trouver
  des contacts ou identifier les décideurs chez une entreprise donnée,
  demande l'email ou le téléphone de quelqu'un chez une entreprise, veut
  savoir par qui passer pour entrer en contact avec une entreprise cible, ou
  fournit une liste d'entreprises et veut savoir à qui s'adresser dans
  chacune. S'applique aussi bien à une seule entreprise qu'à une liste. Ne
  pas confondre avec la skill prospection-entreprise-cible, qui sert à
  trouver de nouvelles entreprises cibles par look-alike : cette skill-ci
  part d'une ou plusieurs entreprises déjà connues et cherche les personnes
  à contacter à l'intérieur.
---

# Recherche de contacts dans une entreprise cible

## Pourquoi cette méthode en particulier

Le piège classique de ce genre de recherche est de chercher un titre de poste unique ("le DSI", "le directeur achats") sans tenir compte de la taille de l'entreprise. Dans une startup, c'est souvent le fondateur qui tranche seul ; dans une PME, un responsable de service ; dans un grand groupe, la décision passe par plusieurs personnes (souvent 6 à 10 sur une vente complexe). Raisonner par **rôle fonctionnel** (qui tient le budget, qui évalue techniquement, qui utilisera la solution) plutôt que par intitulé figé évite de rater le bon interlocuteur simplement parce que son titre exact diffère de ce qu'on avait en tête.

De la même façon, il vaut mieux épuiser les sources publiques et gratuites avant de chercher un email ou un téléphone via un outil payant : la plupart du temps, le site de l'entreprise, LinkedIn et les registres légaux suffisent à identifier les bonnes personnes ; l'outil payant sert ensuite à confirmer ou compléter, pas à découvrir.

## Étape 0 — Clarifier la demande

Récupère le ou les noms d'entreprise à traiter. Si l'utilisateur précise déjà un rôle recherché (ex : "le DSI", "la personne en charge des achats IT", "le responsable Data/IA"), garde ce rôle tel quel comme fil conducteur de la recherche.

S'il ne précise rien, ne te limite pas à un seul poste : propose toi-même 2 à 4 rôles plausibles en fonction de la taille et du secteur de l'entreprise (par exemple pour une mission de conseil Data/IA/Cyber : DSI ou CTO, directeur/responsable Data, RSSI, directeur des opérations — à adapter). Explique brièvement ce choix à l'utilisateur plutôt que de l'imposer silencieusement.

## Étape 1 — Vérifier les connecteurs disponibles (à faire à chaque exécution, pas seulement une fois)

Avant de commencer la recherche manuelle, appelle `SearchMcpRegistry` avec des mots-clés comme "LinkedIn Sales Navigator", "Apollo.io", "Hunter.io", "Kaspr", "Lusha", "Cognism", "Clearbit", "ZoomInfo", "RocketReach", "Dropcontact". Les connecteurs disponibles pour une session évoluent dans le temps et selon l'organisation ; ne pars jamais du principe qu'aucun outil n'est branché sans avoir vérifié à ce moment précis.

Si un connecteur pertinent est disponible et activé, utilise-le pour rechercher directement les contacts et/ou vérifier email et téléphone : c'est plus fiable que la déduction manuelle. Si rien n'est disponible, dis-le clairement à l'utilisateur dans le résultat final et propose de connecter l'outil s'il en utilise un en interne.

## Étape 2 — Sources publiques et gratuites (toujours en premier)

Pour chaque entreprise, cherche dans cet ordre (WebSearch / WebFetch, et navigateur si disponible — voir Étape 3) :

1. Le site web de l'entreprise : page "Équipe", "À propos", "Direction", "Presse".
2. Les mentions légales du site, qui indiquent souvent le représentant légal.
3. Pour une entreprise française : Société.com ou Pappers, qui donnent l'identité des dirigeants inscrits au RCS.
4. Les communiqués de presse et la rubrique presse de l'entreprise.
5. Les offres d'emploi publiées par l'entreprise : elles révèlent l'organigramme et parfois le nom du manager recruteur.
6. Les interventions publiques (conférences, webinars, podcasts, tribunes) où des cadres de l'entreprise sont cités nommément.
7. La page entreprise LinkedIn (liste des employés, filtrable par fonction).

Ces sources suffisent en général à construire une première liste de 2 à 5 candidats plausibles par entreprise, avant même de chercher un email.

## Étape 3 — Navigateur (si le bridge Chrome est connecté)

Si les outils `mcp__claude-in-chrome__*` sont disponibles, utilise-les pour naviguer vers les pages publiques identifiées à l'étape 2 (site de l'entreprise, page LinkedIn publique de l'entreprise) et en extraire les informations affichées. Reste sur des pages publiques et consultées une par une : ne fais jamais de scraping en masse de profils LinkedIn ni de contournement des CGU de la plateforme — au-delà du risque de blocage du compte, ce n'est pas nécessaire pour ce cas d'usage, qui ne demande que quelques profils par entreprise.

## Étape 4 — Email et téléphone

Si un connecteur de sales intelligence (étape 1) a permis de trouver directement email et/ou téléphone vérifiés, indique-le comme tel.

Sinon, si aucun email n'est trouvé publiquement mais qu'un ou plusieurs emails de la même entreprise sont déjà connus (par exemple un contact déjà en base, ou une adresse générique visible sur le site), déduis la convention d'adresse probable (prenom.nom@domaine, p.nom@domaine, initiale+nom@domaine, etc.) et applique-la au nom recherché. Présente toujours ce résultat comme une **estimation non vérifiée**, jamais comme un email confirmé — la nuance compte pour l'utilisateur qui va s'en servir.

Si aucune base de comparaison n'existe et qu'aucun outil de vérification n'est disponible, dis simplement qu'aucun email fiable n'a pu être identifié plutôt que d'inventer une adresse.

**Si ni email ni téléphone n'ont pu être trouvés ou estimés pour une personne**, ne laisse jamais la colonne Contact vide : mets à la place le lien vers son profil LinkedIn public (celui repéré à l'étape 2 ou 3), pour que l'utilisateur ait au moins un moyen de l'identifier et de le solliciter (message LinkedIn, demande de mise en relation). Précise que c'est un lien LinkedIn faute de coordonnées directes trouvées, pour que la différence avec un email/téléphone confirmé reste claire.

## Étape 5 — Format de sortie

Présente le résultat sous la forme d'**un seul tableau**, avec une ligne par personne identifiée, même quand plusieurs entreprises sont traitées en une fois (la colonne Entreprise permet de s'y retrouver) :

| Entreprise | Personne | Contact |
|---|---|---|
| ... | Nom — Rôle | Email (trouvé / estimé — non vérifié) · Téléphone si trouvé |
| ... | Nom — Rôle | Lien LinkedIn (aucun email/téléphone trouvé) |

Garde la colonne "Personne" concise (nom, rôle) et regroupe les coordonnées dans la colonne "Contact" en précisant toujours si l'email est confirmé ou seulement estimé par déduction de pattern — cette nuance doit rester visible même dans ce format condensé. Quand ni email ni téléphone n'existent pour une personne, la colonne "Contact" contient son lien LinkedIn à la place (voir étape 4) plutôt que d'être laissée vide.

Termine systématiquement par : la liste des sources consultées (liens), et un rappel bref du cadre RGPD/CNIL applicable — voir `references/rgpd-cnil.md` pour le texte de référence à reprendre.

## Étape 6 — Limites à toujours mentionner explicitement

Rappelle dans la sortie, sans être lourd : que la skill ne fabrique jamais un email ou un téléphone sans base (source publique ou déduction de pattern signalée comme telle) ; qu'elle ne contourne pas les CGU des plateformes consultées ; et que la disponibilité d'un email/téléphone directement confirmé (plutôt qu'estimé) dépend des connecteurs actifs au moment de l'exécution — donc que le résultat peut être plus ou moins complet d'une session à l'autre selon les outils connectés.

## Enchaînement avec les autres skills

Cette skill s'utilise sur la même liste d'entreprises que **veille-signaux-affaires** (Skill 3). Les deux sorties — contacts et signaux — sont les entrées directes de **ranking-entreprises-cibles** (Skill 3.5), qui priorise qui contacter en premier. Les contacts trouvés ici remplissent ensuite la colonne "Personne (rôle)" du tableau produit par **suivi-relance-discours-prospection** (Skill 4).

## Pour aller plus loin

- `references/outils-sales-intelligence.md` : comparatif des outils (Kaspr, Lusha, Apollo.io, Cognism, Hunter.io, Dropcontact, LeadIQ, RocketReach) à consulter si l'utilisateur demande plus de détails sur un outil en particulier ou hésite entre plusieurs.
- `references/rgpd-cnil.md` : texte de référence sur les règles RGPD/CNIL applicables à la prospection B2B, à reprendre pour le rappel de conformité en fin de sortie.

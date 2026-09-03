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

# Accueil du plugin prospection-froide

**Entrée** : la commande `/prospection-froide` ou une question sur le plugin.
**Sortie** : un message d'accueil court présentant les six skills.

## Objectif

Cette skill présente le plugin et son mode d'emploi. Elle ne lance aucune recherche et ne produit aucun livrable de prospection.

## Contenu du message

Restituer les cinq blocs ci-dessous, dans cet ordre, en un message court.

### 1. Objet du plugin

Le plugin couvre les six étapes de la prospection commerciale NDA. Il automatise la partie recherche, la plus fastidieuse du process.

### 2. Les six skills, dans l'ordre

| Ordre | Skill | Quand l'utiliser |
|---|---|---|
| 0 | `discours-campagne-prospection` | Cadrer une nouvelle campagne : cible, argumentaire, objections |
| 1 | `prospection-entreprise-cible` | Trouver des entreprises cibles par look-alike |
| 2 | `recherche-contacts-entreprise` | Trouver qui contacter dans une entreprise |
| 3 | `veille-signaux-affaires` | Trouver pourquoi et quand contacter une entreprise |
| 3.5 | `ranking-entreprises-cibles` | Prioriser une liste de cibles selon fit, signaux et contacts |
| 4 | `suivi-relance-discours-prospection` | Construire la séquence, rédiger le message, préparer l'appel, suivre le pipeline |

### 3. Fonctionnement

Chaque skill se déclenche sur la demande formulée. Connaître son nom exact n'est pas nécessaire. Les skills s'enchaînent dans l'ordre du tableau au fil d'une campagne.

### 4. Garde-fous

Aucune skill du plugin n'envoie de message ni de mail : elles rédigent et rapportent, l'envoi reste humain. Le classement produit par la skill 3.5 exige une validation humaine avant d'être utilisé par la skill 4.

### 5. Prérequis à vérifier

Deux vérifications avant de lancer quoi que ce soit.

- **Connexion Notion.** Les skills 2, 3.5 et 4 lisent la base de suivi de prospection. Si le connecteur Notion n'est pas actif, le dire et indiquer où l'activer — la connexion n'est jamais automatique.
- **Qui utilise le plugin.** Demander le prénom au premier échange : sans lui, le contrôle anti-doublon entre collaborateurs ne peut pas fonctionner.

### 6. Point de départ

Proposer deux suites : cadrer une nouvelle campagne, ou répondre à une question sur le fonctionnement du plugin.

## Ton

Message court, sans pavé ni jargon technique. Le lecteur type est un commercial ou un manager non technique.

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

# Recherche de contacts dans une entreprise cible (Skill 2)

**Entrée** : une ou plusieurs entreprises déjà identifiées.
**Sortie** : un tableau de contacts, avec rôle, coordonnées, sources et rappel RGPD.

## Objectif

Identifier les personnes à contacter dans des entreprises cibles connues, puis fournir leurs coordonnées quand elles sont trouvables légalement.

## Principes

**Raisonner par rôle, pas par intitulé.** Chercher un titre unique — « le DSI », « le directeur achats » — ignore la taille de l'entreprise. Dans une startup, le fondateur tranche seul ; dans une PME, un responsable de service ; dans un grand groupe, six à dix personnes interviennent sur une vente complexe. Raisonner par rôle fonctionnel — qui tient le budget, qui évalue techniquement, qui utilisera la solution — évite de rater le bon interlocuteur parce que son titre diffère de celui attendu.

**Épuiser le gratuit avant le payant pour identifier les personnes.** Le site de l'entreprise, les registres légaux et l'index du moteur suffisent le plus souvent. L'outil payant confirme et complète, il ne découvre pas.

Nuance arbitrée en interne : sur **l'enrichissement du numéro de téléphone**, le recours à un outil payant est accepté et n'est pas un frein budgétaire. C'est l'identification des entreprises et des personnes qui doit rester indépendante de toute API payante.

**Décideur et prescripteur ne se travaillent pas pareil.** Le **N** valide et paie ; il répond peu par écrit mais prend plus volontiers le téléphone, et redirige souvent vers son N-1 avec une semi-introduction exploitable. Le **N-1** est le prescripteur opérationnel : il doit être convaincu pour porter le sujet, et peut freiner s'il se sent contourné. Identifier les deux quand c'est possible, et le dire dans la sortie.

**LinkedIn ne s'ouvre jamais depuis la skill.** Deux raisons, l'une technique et l'autre de risque.

Techniquement, le robots.txt de LinkedIn interdit l'accès automatisé : une tentative de chargement d'une page LinkedIn échoue en `ROBOTS_DISALLOWED`. Ce qui reste accessible, c'est **l'index du moteur de recherche**, qui n'est pas LinkedIn : une requête `site:linkedin.com/in "Entreprise" DSI` renvoie des titres du type « Prénom Nom - Data Analyst chez Entreprise », donc un nom, une société et souvent une fonction, sans qu'aucune requête ne parte vers LinkedIn.

Côté risque, ce sont les extensions de navigateur et les sessions automatisées qui font restreindre puis supprimer un compte — celui du collaborateur, pas celui de l'éditeur. Kaspr a par ailleurs été sanctionné 240 000 € par la CNIL en décembre 2024 pour ce modèle exact, et a cessé toute collecte LinkedIn en mars 2026. Détail dans `references/outils-sales-intelligence.md`.

**Règle : recherche par moteur autorisée, ouverture de LinkedIn interdite.** Aucun compte, aucune extension, aucun navigateur pointé sur linkedin.com.

## Étape 0 — Clarifier la demande

Récupérer le ou les noms d'entreprise à traiter.

Si un rôle est précisé — « le DSI », « la personne en charge des achats IT », « le responsable Data/IA » — le garder tel quel comme fil conducteur.

Sinon, proposer 2 à 4 rôles plausibles selon la taille et le secteur. Expliquer brièvement ce choix plutôt que l'imposer en silence.

Les intitulés varient d'une entreprise à l'autre et c'est la première cause de contact manqué : un même poste s'appelle Head of AI ici, Directeur Intelligence Artificielle là, AI Factory ailleurs. Raisonner par fonction, pas par libellé.

Titres réellement occupés chez les clients NDA, à utiliser comme référentiel plutôt que de deviner :

| Fonction | Intitulés observés |
|---|---|
| Architecture SI | Enterprise IT Architect, Chief Enterprise Architect Officer, Directeur IT Architecture |
| Data et IA | Group Chief Data Officer, Chief Data Officer, Responsable Data & IA, Responsable LABs IA et Innovation |
| Direction SI | CIO, DSI, Directeur de la Transformation Digitale |
| Métier et produit | Product Manager, Digital Strategy Director |

**Plafond : deux personnes par entreprise au maximum.** Au-delà, le risque de collision interne dépasse le gain — deux collaborateurs NDA contactant trois personnes de la même société décrédibilisent le cabinet.

### Contrôle anti-doublon, avant toute livraison

Vérifier dans la base de suivi si l'entreprise ou la personne y figure déjà. Un contact déjà sollicité ne se repropose pas : indiquer qui le suit et depuis quand. Une entreprise déjà travaillée par un autre collaborateur se signale avant de proposer un second interlocuteur.

Ce contrôle est bloquant. Sans lui, un prospect reçoit deux messages presque identiques de deux personnes différentes, et le cabinet perd sa crédibilité en un envoi.

## Étape 1 — Vérifier les connecteurs disponibles

À faire à chaque exécution, pas une fois pour toutes.

Avant toute recherche manuelle, appeler `SearchMcpRegistry` avec des mots-clés comme « Dropcontact », « Hunter.io », « Cognism », « LinkedIn Sales Navigator », « Pappers », « INPI ». Les connecteurs disponibles varient selon la session et l'organisation.

Si un connecteur pertinent est actif, l'utiliser pour vérifier email et téléphone : c'est plus fiable que la déduction manuelle. Si aucun n'est disponible, le signaler dans le résultat final et poursuivre par les sources publiques.

Ne pas proposer d'outil reposant sur une extension qui agit sur LinkedIn (Kaspr, Lusha, LeadIQ), ni Clearbit, qui n'existe plus comme produit autonome depuis son absorption par HubSpot. Le comparatif vérifié et les motifs figurent dans `references/outils-sales-intelligence.md`.

## Étape 2 — Sources publiques et gratuites

Pour chaque entreprise, chercher dans cet ordre, via WebSearch et WebFetch :

1. le site de l'entreprise : pages « Équipe », « À propos », « Direction », « Presse » ;
2. les communiqués de presse — les nominations y sont annoncées nommément, avec la date ;
3. la presse spécialisée, très productive en interviews de DSI et de CDO : LeMagIT, Le Monde Informatique, Journal du Net ;
4. les mentions légales, qui indiquent le représentant légal ;
5. les registres légaux : [data.inpi.fr](https://data.inpi.fr/) (RNE — actes, statuts, dirigeants ; gratuit, compte requis) ou [Pappers](https://www.pappers.fr/) (consultation web gratuite) ;
6. les offres d'emploi, qui révèlent l'organigramme et parfois le manager recruteur — [API France Travail « Offres d'emploi »](https://francetravail.io), compte développeur requis ;
7. les rapports annuels et documents d'enregistrement universel, pour le comité exécutif des sociétés cotées ;
8. les interventions publiques — conférences, webinars, podcasts, tribunes — citant des cadres nommément ;
9. **en dernier, l'index du moteur sur LinkedIn** : `site:linkedin.com/in "Entreprise" [fonction]`. Lire les titres de résultats, ne jamais ouvrir les pages.

**Limite à annoncer, pas à contourner.** Les registres légaux ne donnent que les représentants légaux — président, directeur général, gérant, administrateurs. Jamais un DSI, un CDO ou un RSSI. Aucune source publique gratuite française ne liste les cadres opérationnels. Sans LinkedIn ouvert, le taux de couverture sur ces fonctions est structurellement plus faible : le dire dans la sortie plutôt que de rendre une liste courte sans explication.

Ces sources suffisent en général à constituer 2 à 5 candidats plausibles par entreprise, avant toute recherche d'email.

## Étape 3 — Navigateur, si un bridge est connecté

Le navigateur sert à consulter les pages qui ne se laissent pas lire autrement : site de l'entreprise, article de presse, rapport annuel. Une page à la fois, au rythme d'une lecture humaine.

**Jamais sur linkedin.com.** Le navigateur utiliserait la session connectée du collaborateur, et c'est le seul chemin qui expose réellement son compte. Pour LinkedIn, s'en tenir à l'index du moteur (étape 2, point 9).

Il n'existe aucune API LinkedIn publique pour ce besoin. Un outil qui promet un accès « API » aux profils opère hors cadre.

## Étape 4 — Email et téléphone

Trois cas.

**Connecteur disponible.** Si un outil de sales intelligence a fourni un email ou un téléphone vérifié, l'indiquer comme tel.

**Déduction de pattern.** Si aucun email n'apparaît publiquement mais qu'une adresse de la même entreprise est connue — contact déjà en base, adresse générique du site — en déduire la convention (prenom.nom@domaine, p.nom@domaine, initiale+nom@domaine) et l'appliquer au nom recherché. Présenter toujours ce résultat comme une **estimation non vérifiée**. La nuance compte pour qui va s'en servir.

**Rien de fiable.** Sans base de comparaison ni outil de vérification, indiquer qu'aucun email fiable n'a été identifié. Ne jamais inventer une adresse.

Quand ni email ni téléphone n'existent pour une personne, la colonne Contact ne reste pas vide : y placer le lien vers son profil LinkedIn public, repéré à l'étape 2 ou 3, et préciser qu'il remplace des coordonnées directes introuvables.

## Format de sortie

Un seul tableau, une ligne par personne, même quand plusieurs entreprises sont traitées ensemble.

| Entreprise | Personne | Persona | Niveau | Contact | Source | Vérifié le | Déjà en base |
|---|---|---|---|---|---|---|---|
| … | Nom — Poste | Data / SI / Sécurité / Métier / Direction | N ou N-1 | Email (confirmé / estimé, non vérifié) · Téléphone | (lien) | AAAA-MM-JJ | Non · ou Oui, suivi depuis le [date] |
| … | Nom — Poste | … | … | Lien LinkedIn (aucune coordonnée trouvée) | (lien) | AAAA-MM-JJ | … |

La colonne **Persona** sert directement à la Skill 4 : c'est elle qui détermine l'angle du message. La colonne **Source** et la date de vérification ne sont pas décoratives — l'article 14 du RGPD impose de pouvoir dire d'où vient une coordonnée, et une donnée vieille de six mois n'a pas la même valeur qu'une donnée du jour.

Garder la colonne « Personne » concise : nom et poste exact tel qu'il est écrit chez le prospect.

Terminer par la liste des sources consultées, avec liens, et un rappel bref du cadre RGPD/CNIL. Le texte de référence figure dans `references/rgpd-cnil.md`.

## Limites

Rappeler dans la sortie, sans insister :

- la skill ne fabrique jamais un email ou un téléphone sans base — source publique, ou déduction signalée comme telle ;
- elle ne contourne pas les conditions d'utilisation des plateformes consultées ;
- aucune source publique française ne fournit d'email nominatif ni de mobile : c'est structurel, pas une lacune de la recherche ;
- l'index du moteur sur LinkedIn donne le nom et l'entreprise de façon fiable, la fonction de façon inégale, et il peut avoir plusieurs mois de retard : un dirigeant arrivé récemment n'y figure pas encore ;
- la disponibilité de coordonnées confirmées dépend des connecteurs actifs au moment de l'exécution, donc le résultat varie d'une session à l'autre.

**Deux pratiques circulent dans les retours d'expérience commerciaux et sont proscrites ici** : prétendre détenir un email qu'on n'a pas pour faire corriger l'interlocuteur, et refuser d'indiquer d'où vient une coordonnée en invoquant le CRM. Toutes deux contredisent l'obligation d'information de l'article 14 du RGPD. Si un utilisateur les évoque, le dire et proposer la formulation conforme.

Rappeler aussi le cadre RGPD : le premier message doit indiquer d'où vient l'adresse (art. 14), identifier l'émetteur et offrir un refus simple. Appeler un professionnel sur un **numéro personnel** relève du régime consommateur, donc du consentement préalable obligatoire depuis le 11 août 2026. Détail dans `references/rgpd-cnil.md`.

## Enchaînement

Cette skill s'applique à la même liste d'entreprises que `veille-signaux-affaires` (Skill 3). Les deux sorties — contacts et signaux — alimentent `ranking-entreprises-cibles` (Skill 3.5), qui détermine qui contacter en premier.

Les contacts trouvés ici alimentent la fiche de contact que produit `suivi-relance-discours-prospection` (Skill 4).

## Références

- `references/outils-sales-intelligence.md` — comparatif vérifié des outils : gratuité réelle, prix, exposition au blocage LinkedIn, position RGPD, et chaîne gratuite alternative.
- `references/rgpd-cnil.md` — règles RGPD/CNIL applicables à la prospection B2B, à reprendre pour le rappel de conformité en fin de sortie.

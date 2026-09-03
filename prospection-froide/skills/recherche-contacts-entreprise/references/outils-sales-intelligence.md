# Outils de recherche de contacts — état vérifié

Document de référence de la skill `recherche-contacts-entreprise` (Skill 2).

Les prix et les quotas changent vite : revérifier avant tout engagement budgétaire.

## Trois règles avant d'ouvrir ce tableau

1. **Aucune source publique française ne fournit d'email nominatif ni de mobile.** C'est structurel. Les outils payants n'y arrivent qu'en agrégeant des données que les personnes n'ont pas fournies pour cet usage — le raisonnement exact qui a valu à Kaspr une sanction CNIL.
2. **Toute extension de navigateur qui extrait des données depuis LinkedIn viole ses conditions d'utilisation.** Le risque porte sur le compte du collaborateur, pas sur l'éditeur de l'outil.
3. **Le gratuit sérieux existe, mais en amont** : registres légaux pour identifier les dirigeants, déduction de format d'email, vérification de délivrabilité. Voir la dernière section.

## Le risque LinkedIn, à connaître avant de choisir un outil

Les conditions d'utilisation de LinkedIn interdisent explicitement les extensions de navigateur qui copient des profils :

> « Develop, support or use software, devices, scripts, robots or any other means or processes (including crawlers, browser plugins and add-ons or any other technology) to scrape the Services or otherwise copy profiles and other data from the Services »

En avril 2026, LinkedIn a été identifié comme scannant les navigateurs de ses visiteurs pour détecter environ 6 236 extensions, Apollo, Lusha et ZoomInfo nommément. Des mises en demeure ont été envoyées à des utilisateurs d'outils tiers. En mars 2026, LinkedIn a supprimé la page entreprise et les profils des dirigeants de HeyReach, éditeur d'automatisation.

L'arrêt *hiQ Labs v. LinkedIn* ne protège de rien. Il n'a tranché qu'un point de droit pénal américain (le CFAA). Sur le terrain contractuel, hiQ a perdu : injonction permanente, 500 000 $ de dommages, destruction du code et des données en décembre 2022.

Il n'existe **aucune API LinkedIn publique** permettant de récupérer des profils, une liste d'employés ou des coordonnées. Les API Talent et Sales Solutions sont réservées à des partenaires validés.

## Outils déconseillés ou hors service

### Kaspr — à ne pas utiliser en l'état

Sanctionné **240 000 € par la CNIL le 5 décembre 2024** pour ce cas d'usage exact : extension collectant les coordonnées des profils LinkedIn visités, y compris quand la personne avait restreint sa visibilité à ses relations de 1er et 2e niveau. Manquements retenus : base légale (art. 6), conservation de 5 ans renouvelée à chaque mise à jour (art. 5-1-e), information des personnes quatre ans après le lancement et en anglais seulement (art. 12 et 14), réponses évasives aux demandes d'accès (art. 15).

Le **4 mars 2026**, la CNIL a clôturé l'injonction en actant que Kaspr *« a choisi d'effacer sa base de données et de cesser toute collecte de données sur LinkedIn »*.

L'offre commerciale reste en ligne (gratuit : 15 crédits email et 5 crédits téléphone par mois ; Starter 45 €/mois en annuel), et la politique de confidentialité cite toujours LinkedIn parmi ses sources. Cette contradiction n'est pas résolue. Ne pas souscrire sans réponse écrite de l'éditeur sur l'origine actuelle de ses données.

- [CNIL — sanction Kaspr](https://www.cnil.fr/fr/aspiration-de-donnees-sanction-de-240-000-euros-lencontre-de-la-societe-kaspr)
- [CNIL — clôture de l'injonction](https://www.cnil.fr/fr/cloture-de-linjonction-prononcee-lencontre-de-la-societe-kaspr)

### Clearbit — n'existe plus

Racheté par HubSpot fin 2023, les API autonomes sont dépréciées et le produit est devenu Breeze Intelligence, accessible aux seuls clients HubSpot. Sans abonnement HubSpot, aucun accès aux données Clearbit. À ne plus citer.

### ZoomInfo — à proscrire dans un contexte français

Pas de tarif public, devis annuel. Le plan gratuit « Community Edition » exige de **téléverser son carnet d'adresses et ses signatures d'emails** : c'est un transfert de données personnelles de clients et de partenaires vers un tiers américain, sans base légale évidente et sans information des personnes concernées. Aucune position RGPD documentée sur le site.

### Indeed et Crunchbase — API fermées

L'API publique Indeed est arrêtée depuis 2023 (partenaires uniquement, sur validation). Crunchbase a supprimé son offre API gratuite ; le premier plan est à 99 $/mois, ou 588 $/an.

## Les autres outils

Classement par risque croissant d'exposition du compte LinkedIn. Les quatre derniers reposent sur une extension qui agit sur LinkedIn : ils sont documentés ici pour que personne ne les choisisse sans connaître ce risque, pas pour être proposés.

| Outil | Gratuit réel | Prix d'entrée | Agit sur LinkedIn | Position RGPD |
|---|---|---|---|---|
| **Dropcontact** | Non — 50 crédits d'essai | 79 €/mois, 500 crédits | Non | Aucune base de contacts stockée, traitement algorithmique |
| **Hunter.io** | Oui — 50 crédits/mois, API incluse | 34 $/mois en annuel | Non | Serveurs en Belgique, DPA, clauses contractuelles types |
| **Cognism** | Non, ni essai | Devis | Extension existante, usage principal hors LinkedIn | Intérêt légitime documenté, notification des personnes, filtrage des listes Do Not Call de 12 pays dont la France |
| **LinkedIn Sales Navigator** | Non | 99,99 €/mois (Core) | Natif, c'est LinkedIn | Cadre Microsoft, pas de revente de coordonnées |
| ⚠️ **Lusha** | Oui — 40 crédits/mois | 49,90 $/mois | Oui, extension | ISO 27701, notification art. 14 revendiquée |
| ⚠️ **Apollo.io** | Oui — 10 exports/mois | 49 $/utilisateur/mois en annuel | Oui, extension | Se dédouane explicitement : conformité à la charge du client |
| ⚠️ **LeadIQ** | Oui — 50 crédits, soit 5 téléphones | 200 $/mois | Oui, extension | Non documentée |
| ⚠️ **RocketReach** | Oui — environ 5 recherches | Non vérifiable, sources contradictoires | Extension optionnelle | Non documentée |

**Recommandation NDA** : Dropcontact ou Hunter.io. Ce sont les deux seuls du panel qui ne touchent pas à LinkedIn — Hunter travaille sur les noms de domaine, Dropcontact sur des algorithmes sans base stockée. Ils ne donnent pas de téléphone. Pour du téléphone conforme, Cognism est le seul du panel à filtrer les listes d'opposition françaises, mais il faut un devis.

## La chaîne gratuite, sans risque LinkedIn

Elle ne produit pas de mobile, mais elle produit un nom de décideur et un email nominatif plausible, légalement.

1. **Cibler** — [API Recherche d'entreprises](https://recherche-entreprises.api.gouv.fr) : ouverte, sans authentification, 7 appels/seconde, gratuite. Maintenue par la DINUM avec l'INSEE et l'INPI.
2. **Identifier les dirigeants légaux** — [data.inpi.fr](https://data.inpi.fr/) (RNE) : gratuit, compte requis, actes et statuts depuis 1993, comptes annuels depuis 2017, mise à jour quotidienne, accès SFTP pour le volume. [Pappers](https://www.pappers.fr/) reste gratuit en consultation web ; son API ne l'est pas au-delà de 100 crédits offerts.
3. **Compléter par les sources publiques de l'entreprise** — page Équipe, mentions légales, communiqués, offres d'emploi, interventions publiques.
4. **Déduire le format d'email** (prenom.nom@, p.nom@, initiale+nom@) à partir d'une adresse connue de la même entreprise.
5. **Vérifier la délivrabilité** — [check-if-email-exists / Reacher](https://github.com/reacherhq/check-if-email-exists) : open source, AGPL-3.0, auto-hébergeable, vérification SMTP sans envoi. Ou les 50 crédits mensuels gratuits de Hunter.io.

Les registres légaux ne donnent que les représentants légaux : gérant, président, directeur général, administrateurs. Jamais les cadres opérationnels.

# Cadre RGPD/CNIL pour la prospection B2B

Document de référence de la skill `recherche-contacts-entreprise` (Skill 2). À reprendre pour le rappel de conformité en fin de sortie, reformulé si besoin mais sans en dénaturer le sens.

Les pages CNIL citées ont été mises à jour le 10 juin 2026.

## Email : B2B et B2C ne suivent pas le même régime

En B2C, un consentement préalable explicite est obligatoire avant tout envoi commercial.

En B2B, la prospection peut se fonder sur l'**intérêt légitime** (RGPD art. 6.1.f), à trois conditions cumulatives :

1. la sollicitation est en lien avec l'activité professionnelle de la personne contactée ;
2. la personne est informée de l'origine de ses données et de la finalité du message, **lors de la collecte** ;
3. elle peut s'y opposer simplement et gratuitement, au moment de la collecte et à chaque sollicitation.

## Obligations systématiques

Chaque message doit permettre au destinataire d'identifier l'organisation émettrice et de refuser facilement les sollicitations suivantes. Toute demande d'opposition se respecte immédiatement.

**Obligation souvent manquée : citer la source des données dès le premier message.** Quand les coordonnées n'ont pas été collectées auprès de la personne elle-même — cas de toute prospection à froid — l'article 14 du RGPD impose de l'informer, source comprise, au plus tard lors de la première communication.

## Adresses génériques

Verbatim CNIL : *« Les adresses génériques de type info[@]nomsociete.fr, contact[@]nomsociete.fr ou commande[@]nomsociete.fr, qui concernent de personnes morales, ne sont pas soumises aux principes »*.

La ligne de partage n'est pas « professionnelle contre personnelle » mais **nominative contre non nominative**. `prenom.nom@societe.fr` reste une donnée personnelle et relève du régime ci-dessus.

## Téléphone : changement de régime au 11 août 2026

La loi n° 2025-594 du 30 juin 2025 inverse le régime du démarchage téléphonique. Depuis le **11 août 2026**, un consommateur ne peut plus être démarché sans consentement préalable exprès, valable un an sans reconduction automatique. Bloctel est supprimé. Sanctions : jusqu'à 75 000 € pour une personne physique, **375 000 € pour une personne morale**.

**Le B2B n'est pas concerné** : le nouveau régime figure à l'article L223-1 du code de la consommation, qui protège le consommateur, c'est-à-dire la personne physique agissant hors activité professionnelle. Appeler un professionnel reste possible sur le fondement de l'intérêt légitime, avec information et droit d'opposition.

**Réserve opérationnelle décisive** : appeler un professionnel **sur son numéro personnel** fait basculer l'appel dans le champ consommateur, donc sous consentement préalable obligatoire. Un mobile récupéré via un outil d'enrichissement est exactement le cas à risque.

## Collecte depuis LinkedIn ou un site web

La CNIL traite ce cas explicitement et sa position est plus restrictive que ce que supposent la plupart des méthodes de prospection.

- **Les conditions du site source s'imposent.** Verbatim CNIL : *« Certains logiciels extraient ces informations à partir de sites web dont les conditions générales d'utilisation (CGU) interdisent l'aspiration »* — ces pratiques ne sont pas autorisées. LinkedIn interdit l'aspiration dans ses CGU : une collecte automatisée de profils LinkedIn ne peut donc pas se prévaloir valablement de l'intérêt légitime.
- **L'attente raisonnable des personnes fait limite.** Lorsque les personnes ne s'attendent pas raisonnablement à être démarchées par une autre société, la réutilisation à des fins commerciales exige leur consentement.
- La fiche CNIL du 19 juin 2025 sur l'intérêt légitime et le moissonnage impose notamment d'exclure les sites qui s'y opposent via robots.txt, CAPTCHA ou conditions d'utilisation.

## Ce que la CNIL a sanctionné

| Organisme | Montant | Date | Motif |
|---|---|---|---|
| Kaspr | 240 000 € | 5 décembre 2024 | Extension collectant les coordonnées de profils LinkedIn, y compris à visibilité restreinte ; conservation excessive ; information tardive et en anglais |
| Solocal Marketing Services | 900 000 € | 15 mai 2025 | Consentement recueilli via des formulaires trompeurs de courtiers en données ; incapacité à en prouver la validité |
| Caloga | 80 000 € | 15 mai 2025 | Intérêt légitime invoqué à tort là où le consentement était requis ; désinscription impraticable |

Enseignement de l'affaire Solocal : **acheter un fichier n'externalise pas la responsabilité**. L'utilisateur final des données répond de la qualité du consentement en amont, quelles que soient ses garanties contractuelles.

## Formulation courte à réutiliser

« Contacter un email professionnel nominatif obtenu légalement — site de l'entreprise, registre légal, outil d'enrichissement conforme — est licite en B2B au titre de l'intérêt légitime, à condition de se présenter clairement, d'indiquer d'où vient l'adresse et d'offrir un moyen simple de refus dès le premier message. »

## Sources

- [CNIL — Prospection par courrier électronique, SMS-MMS et automate d'appel](https://www.cnil.fr/fr/la-prospection-commerciale-par-courrier-electronique-sms-mms-et-automate-dappel)
- [CNIL — Prospection commerciale par téléphone](https://www.cnil.fr/fr/prospection-commerciale-par-telephone-hors-automate-dappel-quelles-sont-les-regles)
- [CNIL — Réutilisation des données publiquement accessibles à des fins de démarchage](https://www.cnil.fr/fr/la-reutilisation-des-donnees-publiquement-accessibles-en-ligne-des-fins-de-demarchage-commercial)
- [CNIL — Intérêt légitime et collecte par moissonnage](https://www.cnil.fr/fr/focus-interet-legitime-collecte-par-moissonnage)
- [CNIL — Sanctions prononcées](https://www.cnil.fr/fr/les-sanctions-prononcees-par-la-cnil)
- [economie.gouv.fr — Réglementation du démarchage téléphonique](https://www.economie.gouv.fr/entreprises/developper-son-entreprise/innover-et-numeriser-son-entreprise/professionnels-comment-respecter-la-reglementation-sur-le-demarchage)

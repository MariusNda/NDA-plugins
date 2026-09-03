# Sources de veille — état vérifié

Document de référence de la skill `veille-signaux-affaires` (Skill 3).

Gratuité, accès sans compte, API et restrictions d'usage automatisé. Revérifier avant de câbler une veille automatique.

## Le socle gratuit et ouvert

| Source | URL | Accès | À utiliser pour |
|---|---|---|---|
| **API Recherche d'entreprises** | `https://recherche-entreprises.api.gouv.fr` | Ouverte, **sans authentification**, 7 appels/seconde, gratuite | Résoudre un nom en SIREN, filtrer par secteur, taille, géographie |
| **BODACC** | `https://www.bodacc.fr` — API : `/api/explore/v2.1/catalog/datasets/annonces-commerciales/records` | Gratuite, sans clé, Licence Ouverte 2.0 | Créations d'établissement, cessions, **augmentations de capital**, procédures collectives |
| **INPI / RNE** | `https://data.inpi.fr` | Gratuit, **compte requis**, accès SFTP pour le volume | Actes et statuts depuis 1993, comptes annuels, dirigeants |
| **API Sirene INSEE** | `https://portail-api.insee.fr` | Gratuite, compte requis, 30 requêtes/minute | Historique d'établissements, successions |
| **BOAMP** | `https://www.boamp.fr` — API : `/api/explore/v2.1/catalog/datasets/boamp/records` | Gratuite, sans clé | Appels d'offres publics |
| **DECP consolidées** | `https://www.data.gouv.fr/datasets/donnees-essentielles-de-la-commande-publique-consolidees-format-tabulaire` | Gratuit, Parquet/CSV/JSON, mise à jour quotidienne | Marchés attribués |
| **PLACE** | `https://www.marches-publics.gouv.fr` | Consultation gratuite | Marchés de l'État |
| **CERT-FR (ANSSI)** | `https://www.cert.ssi.gouv.fr` — `/avis/`, `/alerte/`, `/cti/` | Gratuit, sans compte | Vulnérabilités et incidents, identifiants normalisés `CERTFR-AAAA-TYPE-NNNN` |
| **Cybermalveillance** | `https://www.cybermalveillance.gouv.fr/tous-les-fils-d-infos` | Gratuit | AlerteCyber, bulletins de vigilance |
| **CNIL — sanctions** | `https://www.cnil.fr/fr/les-sanctions-prononcees-par-la-cnil` | Libre. **Pas d'API ni de flux dédié** — seul le RSS global `https://www.cnil.fr/fr/rss.xml` existe, à filtrer | Sanctions et mises en demeure |
| **France Travail — Offres d'emploi v2** | `https://francetravail.io` | Compte développeur requis, OAuth2 | Signal recrutement, ~300 000 offres, code ROME et NAF |
| **BALO** | `https://www.journal-officiel.gouv.fr/pages/balo/` | Gratuit | Sociétés cotées : opérations sur capital, AG |
| **Info-financière** | `https://www.info-financiere.gouv.fr` | Gratuit, API exposée | Communiqués réglementés des sociétés cotées |
| **TED** | `https://ted.europa.eu` | Accès anonyme aux avis publiés | Marchés européens au-dessus des seuils |

Flux RSS gratuits, sans paywall, pour la couche presse : `https://www.lemagit.fr/rss`, `https://www.lemondeinformatique.fr/flux-rss/`, `https://www.journaldunet.com/rss.shtml`, `https://www.zataz.com/rss/zataz-news.rss`.

**Astuce sous-exploitée** : une augmentation de capital publiée au BODACC est un proxy gratuit et daté d'une levée de fonds, souvent disponible avant ou après la couverture presse.

## Sources payantes ou fermées — ne pas les présenter comme gratuites

| Source | Statut réel |
|---|---|
| **Crunchbase** | Offre API gratuite **supprimée**. Pro à 99 $/mois ou 588 $/an. Le site est une application JavaScript, illisible sans navigateur. |
| **API Pappers** | 100 crédits offerts à l'inscription, puis payant, tarifs non publics. Le **site** `pappers.fr` reste gratuit en consultation. |
| **API Societe.com** | Payante : 99 € les 5 000 crédits. Redondante avec BODACC et Sirene, qui sont gratuits. |
| **L'Usine Digitale** | Freemium avec paywall (groupe Infopro Digital). |
| **Les Echos, Challenges** | Paywall. La Tribune est mixte. À réserver à la lecture humaine. |
| **Indeed** | API publique **fermée depuis 2023**, partenaires uniquement. À retirer de toute chaîne automatisée. |
| **Google News** | **Aucune API.** Les flux RSS fonctionnent encore mais ne sont ni documentés ni supportés, plafonnés à 100 articles, et `news.google.com/robots.txt` en interdit l'accès. Source d'appoint, jamais un socle. |

## Restrictions d'usage automatisé à respecter

- **LinkedIn** : conditions d'utilisation et robots.txt interdisent le crawl et l'extraction. Consultation humaine uniquement.
- **Welcome to the Jungle** : `robots.txt` interdit `*/jobs?query=*` et toute URL à query string. Le sitemap `https://www.welcometothejungle.com/sitemaps/index.xml.gz` est le canal autorisé.
- **BODACC et BOAMP** : leur `robots.txt` porte `Disallow: /api/` pour les agents génériques, alors que les conditions de l'API autorisent l'usage programmatique. L'appel API est légitime au titre des conditions d'utilisation ; la contradiction est connue et tracée ici.
- **CNIL** : rappelle que réutiliser des données d'un site dont les conditions interdisent l'aspiration n'est pas couvert par l'intérêt légitime.

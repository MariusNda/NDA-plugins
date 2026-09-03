# Exemples de requêtes par catégorie de signal

Document de référence de la skill `veille-signaux-affaires` (Skill 3).

Remplacer `"NomEntreprise"` par le nom exact de l'entreprise, guillemets compris, pour une recherche exacte. Combiner plusieurs formulations par catégorie plutôt qu'une seule requête : chaque moteur et chaque source remontent des résultats différents selon la formulation.

## 1. Financier / corporate

- `"NomEntreprise" levée de fonds`
- `"NomEntreprise" tour de table OR "série A" OR "série B" OR "série C"`
- `"NomEntreprise" résultats OR chiffre d'affaires 2026`
- `"NomEntreprise" rachat OR acquisition OR fusion`
- `"NomEntreprise" redressement judiciaire OR procédure collective`
- Consulter directement : **bodacc.fr** (annonces légales, API gratuite sans clé), pappers.fr (consultation web gratuite), data.inpi.fr (RNE). Crunchbase n'a plus d'offre gratuite : ne pas le proposer par défaut.

## 2. Dirigeants & organisation

- `"NomEntreprise" nomme OR nomination directeur général OR DSI OR DAF`
- `"NomEntreprise" "nouveau directeur" OR "prend la direction"`
- `"NomEntreprise" "Chief Data Officer" OR "Chief Information Officer" OR "RSSI"`
- `site:linkedin.com/in "NomEntreprise" DSI OR CTO OR CDO OR RSSI` — repérer un changement de poste récent. S'en tenir aux titres et extraits renvoyés par le moteur : les pages LinkedIn ne s'ouvrent pas, leur robots.txt l'interdit.
- Consulter : page « Direction » ou « Équipe » du site, communiqués de presse, bodacc.fr et data.inpi.fr (mandataires sociaux)

## 3. Recrutement & croissance

- `"NomEntreprise" recrute Data OR IA OR intelligence artificielle OR cybersécurité`
- `"NomEntreprise" offre d'emploi DSI OR "data engineer" OR "data scientist" OR RSSI`
- `site:welcometothejungle.com "NomEntreprise"`
- `site:linkedin.com/company "NomEntreprise" emplois` — lire les résultats du moteur, sans ouvrir les pages
- API France Travail « Offres d'emploi v2 » (`francetravail.io`) : gratuite, filtrable par SIREN, code ROME et NAF — la voie outillable pour ce signal
- `"NomEntreprise" ouverture bureau OR nouvelle filiale OR implantation`

## 4. Technologie & transformation

- `"NomEntreprise" migration cloud OR "transformation digitale" OR "projet IA"`
- `"NomEntreprise" partenariat OR intègre (nom d'un éditeur/cloud provider connu : AWS, Azure, GCP, Salesforce, SAP...)`
- `"NomEntreprise" refonte système d'information OR "nouvelle plateforme"`
- Rechercher dans la presse spécialisée : `"NomEntreprise" site:usine-digitale.fr`, `site:lemagit.fr`, `site:journaldunet.com`

## 5. Cyber & conformité

- `"NomEntreprise" cyberattaque OR piratage OR "fuite de données" OR ransomware`
- `"NomEntreprise" CNIL sanction OR "mise en demeure"`
- `"NomEntreprise" NIS2 OR DORA OR conformité RGPD`
- `"NomEntreprise" certification "ISO 27001"`
- Consulter directement : **cert.ssi.gouv.fr** (avis et alertes ANSSI), **cybermalveillance.gouv.fr**, cnil.fr rubrique sanctions, presse cyber (LeMagIT, ZATAZ, Le Monde Informatique — flux RSS libres)

## 6. Commande publique

- `"NomEntreprise" appel d'offres OR "marché public"`
- Rechercher sur **boamp.fr** (API gratuite : `https://www.boamp.fr/api/explore/v2.1/catalog/datasets/boamp/records`) et sur PLACE (`www.marches-publics.gouv.fr`), avec le nom de l'entreprise comme émetteur du marché ou son secteur
- Marchés déjà attribués : DECP consolidées sur data.gouv.fr. Échelon européen : ted.europa.eu
- Catégorie pertinente seulement si l'entreprise cible émet elle-même des marchés publics : établissement public, grand groupe avec appels d'offres SI. Ne pas la forcer pour une PME purement privée.

## 7. Actualité stratégique générale

- `"NomEntreprise" actualité 2026`
- `"NomEntreprise" lance OR lancement nouveau produit`
- `"NomEntreprise" expansion OR international`
- Consulter directement la rubrique "Presse" / "Actualités" / "Newsroom" du site officiel de l'entreprise

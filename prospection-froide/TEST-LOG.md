# Test bac à sable — 2 septembre 2026

Test à blanc des skills 1 et 3 sur la verticale agroalimentaire, sans intervention humaine, pour trouver ce qui casse avant un usage réel.

## Protocole

- **Skill 1** — appel réel de l'API Recherche d'entreprises : `activite_principale=10.51D,10.13B,10.71D,10.39A,10.85Z`, `categorie_entreprise=ETI`, `etat_administratif=A`, 25 résultats.
- **Skill 3** — deux recherches de signaux sur Sodebo, l'une avec le gabarit de requête actuel, l'autre avec restriction `site:`.

## Anomalies relevées

### A1 — Le filtre `categorie_entreprise=ETI` ne filtre pas la taille · **bloquant**

Le résultat contient Pâtisserie François (2,5 M€ de CA), Délicecook (2,7 M€) et Aux Merveilleux Lyon (3,1 M€), toutes étiquetées ETI. La catégorie est portée par l'unité légale rattachée à un groupe : une filiale de dix personnes appartenant à une ETI est classée ETI.

Conséquence : le plancher de 200 à 300 salariés de la méthode terrain n'est pas obtenu par ce filtre. Une longlist ainsi constituée contient des entreprises trop petites pour porter un projet.

Second effet du même mécanisme : plusieurs entités d'un même groupe occupent plusieurs lignes. Le test a rendu SILL et SILL DAIRY INTERNATIONAL — même activité, même département, même groupe. Sur vingt places, le gaspillage est réel, et le risque de contacter deux fois le même groupe aussi.

**Correction appliquée** : la skill 1 avertit que `categorie_entreprise` ne mesure pas la taille de l'entité, impose de recouper avec le chiffre d'affaires et l'effectif, et ajoute une règle de dédoublonnage par groupe avant constitution du Top 20.

### A2 — Les données financières sont hétérogènes et souvent périmées · **sérieux**

Les millésimes de chiffre d'affaires vont de 2014 à 2025 selon les entreprises. Sodebo affiche 409,6 M€ au titre de 2014, Les Crudettes 99,6 M€ au titre de 2016. Cinq des vingt-cinq entreprises n'ont aucun chiffre d'affaires publié.

Conséquence : `ca_min` et `ca_max` excluent silencieusement toute entreprise dont les comptes ne sont pas déposés ou sont anciens — sans que rien ne le signale.

**Correction appliquée** : ne plus filtrer sur le chiffre d'affaires par défaut, mais le récupérer et l'afficher **avec son millésime**, puis trancher après coup.

### A3 — `tranche_effectif_salarie` est un code, pas un nombre · **piège de lecture**

La valeur « 32 » ne signifie pas 32 salariés mais la tranche 250 à 499. « NN » signifie non renseigné, et revient souvent. La valeur porte de plus sur l'établissement siège, pas sur l'entreprise.

**Correction appliquée** : table des codes ajoutée dans la skill 1.

### A4 — Le gabarit de requête produit du bruit · **sérieux**

La requête générique `"Sodebo" 2026 IA OR recrutement data OR nomination` a rendu **un seul résultat pertinent sur huit** — le reste étant des articles SEO génériques sur l'IA et le recrutement, sans rapport avec l'entreprise.

La même recherche avec restriction de site a rendu **huit résultats pertinents sur huit**.

**Correction appliquée** : les requêtes de signaux imposent désormais une restriction `site:` ou un second ancrage propre à l'entreprise.

### A5 — Les sources presse sont IT-centrées · **lacune**

La skill 3 cite LeMagIT, Le Monde Informatique et le Journal du Net. Sur l'agroalimentaire, la presse qui parle réellement des entreprises est **LSA Conso** et **L'Usine Nouvelle** — absentes de la liste.

**Correction appliquée** : consigne d'ajouter la presse de la verticale traitée, avec exemples.

## Ce qui a bien fonctionné

- L'API répond, sans clé, et les filtres combinés sont acceptés.
- La règle LinkedIn tient : une offre d'emploi Sodebo est remontée dans les résultats du moteur, lisible par son titre, sans qu'aucune page LinkedIn soit ouverte.
- L'exclusion des sociétés de services fonctionne : aucun faux positif de ce type dans les vingt-cinq résultats.

## Reste à tester par un humain

Le déclenchement des skills sur une demande formulée naturellement, le rendu de l'arbre Mermaid dans l'application, et l'utilité réelle du brief d'appel en situation.


---

# Test 2 — cas réel La Poste, 2 septembre 2026

Entrée : la proposition « Gouvernance IA » du Groupe La Poste (cadre de référence Data/IA, 3 mois, 60 k€ HT, références Crédit Agricole, CMA CGM, MGEN, France Travail, Savencia).

Consigne : passer la skill 0 puis lancer la skill 1 **sans filtre**, avec les seuls critères issus du cadrage de campagne.

## A6 — Sans filtre sectoriel, la skill 1 ne produit rien d'exploitable · **bloquant**

`categorie_entreprise=GE` seul renvoie **10 000 résultats**, plafond de l'API, non classés par pertinence commerciale. Les vingt-cinq premiers sont un échantillon arbitraire : La Poste, EDF, Elior, Ville de Paris, Société Générale, SNCF Réseau, Croix-Rouge, BNP Paribas, Orange, Compass, Lidl, OGF pompes funèbres, SNCF Voyageurs, Carrefour Proximité, LCL.

Ce n'est pas un look-alike, c'est un tirage. Une collectivité territoriale, une association humanitaire et un opérateur funéraire y côtoient des banques et des télécoms.

**Correction appliquée** : la skill 1 exige désormais au moins un filtre de secteur ou d'activité, et refuse de lancer sans, en renvoyant vers le groupe B du discours de campagne. Elle exclut par défaut administrations, collectivités et associations, sauf campagne visant le secteur public. Elle précise que les résultats ne sont pas classés par pertinence.

## A7 — Le dédoublonnage par groupe se confirme sur un second jeu

SNCF Réseau et SNCF Voyageurs occupent deux lignes de la même page. La règle ajoutée au test précédent tient.

## Faux positif de ma part, signalé pour mémoire

Une première lecture du résultat m'a fait conclure à 16 résultats seulement. Contrôle par pagination : le champ `total_results` vaut 10 000. L'erreur venait de ma lecture, pas de l'API. Aucune anomalie de source à retenir.

## Verdict

La chaîne fonctionne techniquement. La skill 1 sans filtre sectoriel ne fonctionne pas méthodologiquement — c'était précisément l'objet du test, et le garde-fou manquait.

---

# Test 3 — La Poste, skill 1 utilisée correctement

Filtres issus du brief : transport et entreposage, grande entreprise, hors administrations et associations. 26 résultats.

## Résultat : la skill fait ce qu'on lui demande

Le vivier est cohérent — DSV, FedEx, DPD, CEVA, Daher Logistics, Autoroutes du Sud de la France, Natran, Chronopost. Ce sont de vrais comparables de La Poste, avec des enjeux Data/IA plausibles.

## Ce que le test valide

**Le dédoublonnage par groupe est indispensable.** Sur vingt lignes, la moitié appartient à deux groupes : SNCF en compte cinq (Réseau, Voyageurs, Gares & Connexions, Société Nationale, Hexafret) et EFFIA trois. Sans la règle, le Top 20 contiendrait dix fois deux entreprises. Avec elle, il tombe à une dizaine de groupes réels — et la skill livre alors une liste plus courte plutôt que du remplissage, comme prévu.

**Les millésimes financiers hétérogènes se confirment** : Chronopost 2020, CEVA 2022, FedEx 2023, les autres 2024.

**La checklist capacité d'investissement sert** : Hexafret affiche 0 € de chiffre d'affaires en 2023.

**La Poste elle-même remonte en première position.** Normal pour un look-alike : la règle d'exclusion des clients et de la cible d'origine s'applique.

## Verdict

La skill 1 fonctionne comme prévu dès lors qu'un secteur est renseigné. Les corrections issues des tests 1 et 2 se vérifient sur un troisième jeu de données indépendant.

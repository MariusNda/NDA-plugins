# Construire un arbre de qualification d'appel

Document de référence de la skill `suivi-relance-discours-prospection` (Skill 4), mode 4.

Il répond à une question : sur quoi se fonde un arbre de qualification, et que dit la méthodologie établie. Les sources sont citées et distinguées selon leur solidité — recherche, analyse de praticien, ou contenu marketing d'éditeur.

## Sur quoi l'arbre se construit

Ni sur l'entreprise appelée, ni sur l'offre seule. Sur quatre niveaux, dont **trois sont mutualisables et un seul est individuel**.

| Niveau | Contenu | Portée |
|---|---|---|
| **0 — Avant l'appel** | Filtre du profil de client idéal : critères de fit et critères rouges d'exclusion | Mutualisé par campagne |
| **1 — La douleur et la métrique** | Ce que l'offre soigne, et ce qui se mesure | Mutualisé **par offre** |
| **2 — La formulation** | Même douleur, mots différents selon l'interlocuteur | Mutualisé **par persona** |
| **3 — Le motif d'appel** | Une phrase adossée à un fait daté sur ce compte | **Individuel** |

C'est le seul point sur lequel la littérature est explicite : le fit doit être qualifié avant tout le reste, parce que les cadres de qualification d'opportunité « deviennent inefficaces quand le prospect n'a pas d'alignement organisationnel fondamental » ([Inflexion-Point](https://www.inflexion-point.com/blog/no-fit-no-deal-why-icp-fit-must-be-the-first-thing-you-qualify-in-complex-b2b-sales)).

Le profil de client idéal se décrit en quatre couches : firmographique, structurelle, culturelle, et priorités actuelles ([Inflexion-Point](https://www.inflexion-point.com/blog/profiling-your-ideal-customers)). Les deux premières se vérifient avant l'appel, sur données publiques. Les deux dernières sont précisément ce que l'appel doit aller chercher.

**Sans offre définie, pas d'arbre.** Un Top 20 sans campagne cadrée ne permet de construire que le niveau 0. Dans ce cas, le dire et renvoyer vers `discours-campagne-prospection` (Skill 0) plutôt que de produire un arbre creux.

## Les critères de disqualification

C'est le point le mieux étayé de tout le dossier, et le plus contre-intuitif : **savoir sortir vite vaut mieux que qualifier finement**.

La méthode documentée est celle des feux tricolores : des critères rouges désignent les organisations qui ne deviendront jamais de bons clients, et **un seul drapeau rouge suffit à disqualifier** ([Inflexion-Point](https://www.inflexion-point.com/blog/profiling-your-ideal-customers)). Côté MEDDIC, la consigne est de « célébrer les deals qu'on quitte », la disqualification précoce étant une victoire et non un échec ([MEDDICC](https://meddicc.com/resources/lessons-ive-learnt-since-implementing-meddic)).

Rouges plausibles pour un cabinet de conseil français : hors panel fournisseur sans voie d'entrée, direction informatique en gel budgétaire, acheteur public déjà lié par un accord-cadre non échu, cabinet interne captif, taille hors cible.

## Le concurrent réel : l'indécision

Une analyse de **2,5 millions de conversations commerciales** montre que **40 à 60 % des affaires perdues le sont sans décision** — pas au profit d'un concurrent — et qu'un niveau d'indécision moyen à élevé apparaît dans **87 % des affaires**. Face à une indécision forte, le taux de succès tombe à 6 % ([The JOLT Effect](https://challengerinc.com/losing-to-customer-indecision/), Dixon & McKenna).

Le moteur dominant n'est pas la peur de rater une opportunité, mais la **peur de se tromper**. Sur un achat de conseil en IA — nouveau, risqué pour la carrière du sponsor, difficile à défendre en comité — c'est le facteur numéro un.

Aucun cadre classique n'intègre cela. Trois questions à insérer en fin de découverte :

- qui, précisément, signe ?
- avez-vous déjà lancé puis arrêté un projet de ce type ?
- que se passe-t-il pour vous si ça échoue ?

## Quel cadre retenir, et à quel moment

Aucun cadre unique ne couvre le besoin. Trois étages.

| Étage | Cadre | Rôle |
|---|---|---|
| Ciblage | Profil de client idéal + feux tricolores | Décider qui on appelle et qui on refuse |
| Appel à froid (4 à 9 min) | **FAINT**, conduite **SPIN** | Obtenir la découverte, pas la vente |
| Découverte et gouvernance | **SPICED** en entretien, **MEDDPICC** en revue | Structurer, puis arbitrer |

**FAINT** (Funds, Authority, Interest, Need, Timing) cherche la **capacité financière** et non le budget alloué. C'est le seul cadre conçu pour une demande créée, c'est-à-dire un acheteur qui ne cherchait rien — la situation par défaut en prospection à froid sur l'IA ([RAIN Group](https://www.rainsalestraining.com/blog/how-to-qualify-sales-leads)).

**SPIN** (Situation, Problème, Implication, Need-payoff) est issu de la seule recherche d'ampleur du domaine : 35 000 appels analysés dans plus de 20 pays sur 12 ans, par l'équipe de Neil Rackham ([Routledge](https://www.routledge.com/SPINr--Selling/Rackham/p/book/9781003073024)).

**MEDDPICC**, né chez PTC au milieu des années 1990, apporte le « Paper process » — référencement fournisseur, achats, juridique. Indispensable face aux panels fermés français ([MEDDICC](https://meddicc.com/resources/who-created-meddic)).

**BANT est à écarter comme grille d'entretien.** Son premier critère, le budget, disqualifie précisément les bons prospects d'un marché émergent : une ligne « conseil IA » n'existe souvent pas encore. Forrester le confirme : « il est déraisonnable d'attendre que des critères budgétaires détaillés soient identifiés tôt dans le processus » ([Forrester](https://www.forrester.com/blogs/isbantstillrelevantpartii)).

## Quatre erreurs de conception à éviter

**Confondre appel à froid et découverte.** Ce sont deux régimes opposés. En appel à froid, les appels qui aboutissent comportent presque toujours un pitch, et la parole du commercial y domine légèrement. En découverte, l'optimum observé se situe autour de 11 à 14 questions réparties sur tout l'entretien ([Gong](https://www.gong.io/blog/nailing-your-sales-discovery-calls)). Un arbre qui transforme l'appel à froid en interrogatoire fait fuir.

**Croire que les questions ouvertes sont supérieures.** La recherche fondatrice du domaine dit l'inverse : les questions ouvertes ne sont pas nécessairement plus efficaces que les questions fermées. Ce qui discrimine, c'est la **séquence** — faire formuler au client l'implication puis le gain — pas la forme grammaticale ([Routledge](https://www.routledge.com/SPINr--Selling/Rackham/p/book/9781003073024)).

**Sur-outiller le traitement d'objection.** Cinq objections représentent **74 %** des cas en appel à froid : pas intéressé (17 %), doute sur l'adéquation (17 %), pas de budget (16 %), pas mon périmètre (13 %), raccroché (11 %) ([30MPC](https://www.30mpc.com/interactive-resources/how-to-master-cold-calls-data-from-300m-calls-30mpc)). Un arbre à trente branches d'objection est du sur-travail. Et Rackham montre que dans la vente de valeur élevée, le traitement d'objection compte moins que sa **prévention** : mieux vaut investir dans la pertinence du motif d'appel.

**Dérouler l'arbre comme une checklist.** L'auteur de MEDDICC met lui-même en garde : c'est ce malentendu qui a donné mauvaise réputation aux cadres de qualification, les commerciaux juniors croyant devoir cocher chaque case à chaque échange. L'arbre est un filet de sécurité, pas un script à réciter.

## Ce que la France change

**Le circuit d'achat, d'abord.** Les panels fournisseurs des grands comptes sont largement fermés, avec une préférence documentée pour les relations existantes plutôt que les nouvelles prospections ([LittleBigConnection](https://www.littlebigconnection.com/fr/blog/entreprise/achat-de-prestation-intellectuelle-8-etapes-pour-maitriser-le-processus)). Une affaire gagnée techniquement mais bloquée neuf mois aux achats est une affaire perdue. Question de qualification de premier rang : **êtes-vous référencé, y a-t-il un panel, quel est le délai ?**

**Le secteur public change la nature de l'appel.** L'objectif n'y est pas de prendre un rendez-vous commercial mais d'entrer dans le sourcing amont, que l'article R.2111-1 du code de la commande publique autorise expressément, sous réserve de ne pas fausser la concurrence ([marche-public.fr](https://www.marche-public.fr/ccp/R2111-01-etudes-echanges-prealables-avec-operateurs-economiques.htm)). Les seuils de procédure formalisée pour les services au 1er janvier 2026 : 140 000 € HT pour l'État, 216 000 € pour les collectivités et établissements publics, 432 000 € pour les entités adjudicatrices ([DAJ Bercy](https://www.economie.gouv.fr/daj/commande-publique-nouveaux-seuils-europeens-applicables-au-1er-janvier-2026)). Les deux questions deviennent : où en est la définition du besoin, et existe-t-il déjà un accord-cadre ?

**La structure hiérarchique explique le barrage.** La France combine une distance hiérarchique élevée et un évitement de l'incertitude très fort ([The Culture Factor](https://www.theculturefactor.com/country-comparison-tool?countries=france)). Deux conséquences concrètes : les dirigeants sont difficiles à joindre par construction, et l'information écrite est attendue **avant** la réunion. « Envoyez-moi un mail » n'est donc pas toujours une esquive — c'est parfois une demande cohérente. Prévoir une branche « document plus créneau proposé » plutôt qu'une branche « refuser le mail ».

**Le cadre légal.** La prospection téléphonique B2B reste possible sur le fondement de l'intérêt légitime, avec information et droit d'opposition. Le régime du consentement préalable entré en vigueur le 11 août 2026 vise le consommateur, pas le professionnel — mais appeler un professionnel sur son numéro personnel fait basculer dans le régime consommateur. Détail dans `recherche-contacts-entreprise/references/rgpd-cnil.md`.

## Fiabilité des sources citées

- **Recherche ou source officielle** : SPIN (Rackham), The JOLT Effect, textes de la commande publique, CNIL, données culturelles Hofstede.
- **Analyse de praticien argumentée** : Inflexion-Point sur le fit et la disqualification, MEDDICC, RAIN Group, Forrester sur BANT.
- **Données d'éditeur, à traiter comme ordre de grandeur** : Gong et 30MPC. Ce sont de vraies analyses sur données réelles, mais non auditables, produites par des acteurs intéressés, et sur une population dominée par le logiciel nord-américain à cycle court. Utilisables pour la forme d'une ouverture d'appel, jamais comme objectif de performance pour de la vente de conseil à des ETI françaises.

L'origine de BANT chez IBM, universellement répétée, n'a pas de source primaire vérifiable : ne pas l'affirmer comme un fait daté.

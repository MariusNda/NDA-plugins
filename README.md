# 🧩 NDA Plugins

Bienvenue ! Ce repo regroupe les plugins Claude de NDA Partners. Chaque dossier ci-dessous est un **plugin indépendant** — tu n'installes que celui qui te concerne.

## 📦 Plugins disponibles

| Dossier | Ce qu'il fait |
|---|---|
| [`prospection-froide/`](./prospection-froide) | Automatise le process de prospection commerciale : cibles, contacts, signaux, relances |

*(d'autres plugins viendront s'ajouter ici avec le temps)*

---

## 🙋 Jamais utilisé GitHub ? Voici comment récupérer un plugin

Pas besoin de rien installer, tout se fait à la souris.

**1. Télécharger le repo**
- En haut de cette page, clique sur le bouton vert **`Code`**
- Clique sur **Download ZIP**
- Un fichier `NDA-plugins-main.zip` arrive dans tes téléchargements → double-clique pour le décompresser

**2. Repérer le plugin qui t'intéresse**
- Ouvre le dossier décompressé
- Entre dans le sous-dossier voulu, par exemple `prospection-froide`

**3. En faire un fichier installable**
- Clic droit sur le dossier `prospection-froide` → **Compresser** (Mac) ou **Envoyer vers > Dossier compressé** (Windows)
- Renomme le fichier obtenu : remplace `.zip` par **`.plugin`**
  → tu dois obtenir `prospection-froide.plugin`

**4. Installer**
- Ouvre Claude Desktop
- Glisse le fichier `prospection-froide.plugin` dans une conversation
- Clique sur le bouton d'installation qui apparaît

**5. Vérifier que ça marche**
- Tape `/prospection-froide` dans une nouvelle conversation → le message d'accueil doit s'afficher

---

## 💻 Tu es à l'aise avec un terminal ?

```bash
git clone https://github.com/MariusNda/NDA-plugins.git
cd NDA-plugins/prospection-froide
zip -r prospection-froide.plugin .
```

Puis glisse le fichier `prospection-froide.plugin` obtenu dans Claude Desktop (étape 4 ci-dessus).

---

## 🔄 Mettre à jour un plugin

Aucune synchronisation automatique pour l'instant. Pour récupérer une nouvelle version : refais les étapes 1 à 4 ci-dessus, et réinstalle par-dessus l'ancienne version.

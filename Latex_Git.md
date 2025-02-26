
# 📘 Travail collaboratif sur des documents avec Git  

Git est un outil puissant pour gérer efficacement le travail collaboratif sur des documents, qu'ils soient en **Word**, **LaTeX** ou **Markdown**. Il permet d'éviter les **copier-coller incessants**, les fichiers du type `Document_v1_final_corrigé_definitif.docx`, et garantit que **tout le monde travaille sur une seule version** tout en offrant la possibilité de **revenir à une version antérieure** sans perdre les modifications ultérieures.

Pour les utilisateurs LaTeX, il permet notamment de palier aux **limitations de la version gratuite d'Overleaf**, ne limitant pas à 2 utilisateurs ni à une taille de fichier limitée.

---

## 1️⃣ Travailler à plusieurs sur un document avec Git  

### ✅ Pourquoi utiliser Git pour la rédaction ?  

- **Un seul fichier de référence** : Plus besoin d’envoyer des versions par mail (et fini les document_V1, document_V2, ..., document_V50).  
- **Historique des modifications** : Chaque changement est enregistré et peut être **restauré** sans perdre les nouvelles modifications.  
- **Travail en parallèle** : **Plusieurs contributeurs** peuvent travailler sans écraser le travail des autres.  
- **Gestion des conflits** : Git aide à identifier et résoudre les conflits si deux personnes modifient la même section.  
- **Accès distant** : Les fichiers sont stockés en ligne et accessibles de partout (GitHub, GitLab…), tout en **travaillant localement**.  

### 📌 Bonnes pratiques générales  

✔ **Faire des commits fréquents** avec des messages clairs.  
✔ **Utiliser des branches** pour chaque nouvelle section ou correction ou collaborateur.  
✔ **Se synchroniser régulièrement** avec `git pull`.  
✔ **Ne pas versionner les fichiers temporaires ou générés** (comme `.log`, `.aux`, `.pdf`).  

---

## 2️⃣ Application à Word  

### 🔹 Limitations avec Word et Git  

- Word génère des fichiers **binaires** (`.docx`), rendant difficile la visualisation des différences.  
- La gestion des conflits est compliquée car les fichiers ne sont pas lisibles en texte brut.  

### 🏆 Bonnes pratiques pour utiliser Git avec Word  

1. **Activer le suivi des modifications** dans Word.  
2. **Éviter de modifier le même fichier simultanément**.  
3. **Convertir en `.txt` ou `.md`** lorsque c'est possible et écrire un README.md qui permet de suivre les modifications.  
4. **Utiliser Git LFS (Large File Storage)** pour mieux gérer les fichiers `.docx`.  

```sh
git lfs install
git lfs track "*.docx"
git add .gitattributes
git commit -m "Ajout de Git LFS pour Word"
git push origin main
```

---

## 3️⃣ Application à LaTeX  

### 📌 Pré-requis
Pour pouvoir réaliser un travail collaboratif LaTeX, il faut avoir une installation latex de TexLive par exemple et un éditeur pour la compilation. Quelques suggestions:
   - Emacs (https://www.gnu.org/software/emacs/)
   - VSCode (https://github.com/James-Yu/LaTeX-Workshop)
   - TeXworks (http://www.tug.org/texworks/)
   - Sublimetext(https://packagecontrol.io/packages/LaTeXTools)
   - Autres (https://www.guru99.com/fr/best-latex-editors-window-mac.html)

Par exemple, l'utilisation de Visual Studio (installation: https://www.youtube.com/watch?v=Mty0vHb0knI&feature=youtu.be) permet aussi d'autres pluggins tels que la visualisation simplifiée du graphe Git: https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph.

### 📌 Organisation du projet  

1. **Créer un dépôt Git**.  
2. **Structurer le projet** :  
   - 📁 `main.tex` *(document principal)*  
   - 📁 `sections/` *(chapitres en fichiers séparés)*  
   - 📁 `figures/` *(images, schémas…)*  
   - 📁 `bibliography.bib` *(bibliographie)*  
   - 📁 `.gitignore` *(exclusion des fichiers inutiles)*  

### Exemple de `.gitignore`  

```gitignore
*.aux
*.log
*.bbl
*.blg
*.out
*.toc
*.synctex.gz
*.pdf
**/un_dossier_a_eviter
```

### 🚀 Workflow collaboratif  

```sh
git init
git remote add origin https://github.com/utilisateur/projet-latex.git
git pull origin main
git switch -c nouvelle-branche
# Modifier des fichiers
git add .
git commit -m "Ajout du chapitre 1"
git push origin nouvelle-branche
git switch main
git merge nouvelle-branche
git push origin main
```

### ⚠️ Gérer les conflits  

```sh
git status
# Modifier les fichiers conflictuels
git add fichier-conflit.tex
git commit -m "Résolution du conflit"
git push origin main
```

---

## 4️⃣ Ensemble des commandes Git utiles  

### 📂 Gestion du dépôt  

```sh
git init  # Initialiser un dépôt
git clone URL  # Cloner un dépôt existant
git remote add origin URL  # Associer un dépôt distant
git pull origin main  # Récupérer les dernières modifications
git push origin main  # Envoyer ses modifications
```

### 🔄 Gestion des modifications  

```sh
git add fichier.txt  # Ajouter un fichier à l'index
git commit -m "Message clair"  # Enregistrer les modifications
git status  # Vérifier l'état du dépôt
git diff  # Voir les modifications non indexées
git diff main nom-de-la-branche  # Comparer une branche avec main
git diff fichier.tex  # Voir les différences d’un fichier spécifique
```

### 🏗 Gestion des branches  

```sh
git branch  # Voir les branches existantes
git switch -c nouvelle-branche  # Créer et basculer sur une nouvelle branche
git switch main  # Revenir sur la branche principale
git merge nouvelle-branche  # Fusionner une branche dans main
git branch -d ancienne-branche  # Supprimer une branche locale
git branch -a  # Lister toutes les branches locales et distantes
git fetch --prune  # Supprimer les branches distantes obsolètes
```

### 🛑 Annuler et corriger des erreurs  

```sh
git checkout -- fichier.txt  # Annuler des modifications locales
git reset --hard HEAD  # Annuler toutes les modifications non commit
git revert HEAD  # Annuler le dernier commit sans perdre les modifications
git reset --soft HEAD~1  # Annuler le dernier commit mais garder les modifications en staging
```

### 📂 Renommer ou supprimer un fichier  

```sh
git mv ancien-nom.tex nouveau-nom.tex  # Renommer un fichier
git commit -m "Renommage de ancien-nom.tex en nouveau-nom.tex"
git rm fichier-a-supprimer.tex  # Supprimer un fichier
git commit -m "Suppression de fichier-a-supprimer.tex"
git push origin main
```

---

## 5️⃣ Utiliser Markdown pour le suivi des fichiers  

Le format **Markdown (`.md`)** est idéal pour suivre les modifications dans Git, car il est **simple, lisible et diffable** en texte brut.  

### 📌 Formatage usuel de Markdown  

#### Titres  

```markdown
# Titre de niveau 1  
## Titre de niveau 2  
### Titre de niveau 3  
```

#### Texte en gras, italique, souligné  

```markdown
**Gras**  
*Italique*  
~~Texte barré~~  
```

#### Listes  

```markdown
- Élément 1  
- Élément 2  
  - Sous-élément  
  - Sous-élément  
```

#### Liens  

```markdown
[GitHub](https://github.com)  
```

#### Images  

```markdown
![Texte alternatif](https://exemple.com/image.jpg)  
```

#### Blocs de code  

```markdown
```sh
echo "Commande shell"
```
```

---

### 🚀 Exemple d'utilisation avec Git  

Créer un fichier `README.md` pour documenter un projet :  
```sh
echo "# Mon projet" > README.md
git add README.md
git commit -m "Ajout du README"
git push origin main
```

Comparer les modifications :  
```sh
git diff README.md
```

---

## 🏆 Conclusion  

Git est un **outil puissant** pour le travail collaboratif sur des documents, qu'ils soient en **Word**, **LaTeX** ou **Markdown**. En respectant quelques **bonnes pratiques**, il est possible d'améliorer la productivité et d'assurer une **meilleure gestion des versions**.  

**🚀 Prêt à collaborer efficacement avec Git ?**  
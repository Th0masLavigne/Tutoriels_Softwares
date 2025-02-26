# 🐍 Création de Packages Python 📦

## 🚀 1. Intérêt de travailler avec des modules et packages

L'organisation du code en modules et packages permet :

- ✅ **Réutilisabilité** : Un même module peut être utilisé dans plusieurs projets sans avoir à dupliquer du code.
- 📖 **Lisibilité et maintenance** : Un projet bien structuré en modules et packages facilite la compréhension et la modification du code.
- ⚠️ **Éviter les erreurs** : Utiliser des packages plutôt que de simples fichiers `.py` réduit les risques de conflits, d'erreurs de sélection de fichiers ou de copier-coller inadaptés.
- 📦 **Facilité de distribution** : Un package peut être partagé et installé facilement via un gestionnaire de paquets comme `pip`.
- 🏗 **Modularité** : Cela permet d'organiser le code en sous-unités logiques, facilitant la collaboration entre développeurs.

### 📜 Importance du fichier `README.md`

Un fichier `README.md` est essentiel pour accompagner un package. Il doit contenir :

- 📝 Une **description claire** du package et de ses fonctionnalités.
- 🔧 Des **instructions d'installation**.
- 🏗 Des **exemples d'utilisation**.
- 📌 Une **liste des dépendances**.
- 🔑 Les **licences et informations de contact**.

Un `README.md` bien écrit permet aux utilisateurs et développeurs de comprendre et utiliser le package plus facilement.


---

## 🏗 2. Création d'un module

Un module est simplement un fichier Python (`.py`) contenant du code réutilisable.

Exemple d'un module `math_utils.py` :

```python
# math_utils.py
def addition(a, b):
    return a + b

def soustraction(a, b):
    return a - b

def readme_maths():
    return "Module math_utils: contient des fonctions d'opérations mathématiques."

if __name__ == "__main__":
    print("Le module math_utils a été exécuté directement.")
```

📌 **Explication de `if __name__ == "__main__"`** :
Ce bloc de code permet d'exécuter des instructions spécifiques uniquement lorsque le fichier est exécuté directement et non lorsqu'il est importé comme module. Cela évite d'exécuter du code involontairement dans un autre script.

Ce module peut être utilisé dans un autre fichier :

```python
import math_utils

resultat = math_utils.addition(2, 3)
print(resultat)  # Affiche 5
```

---

## 📦 3. Création d'un package

Un package est un répertoire contenant plusieurs modules et un fichier spécial `__init__.py` qui indique que le répertoire est un package.

### 📂 Structure d'un package

```
mon_package/
│── __init__.py
│── math_utils.py
│── string_utils.py
│── string_utils.py
│── other_utils.py
```

### 🛠 Contenu du `__init__.py`

Le fichier `__init__.py` peut être vide ou contenir du code pour initialiser le package. Il peut aussi exposer certains modules pour simplifier les imports :

```python
# __init__.py
from .math_utils import readme_maths
from .string_utils import readme_string
from .other_utils import readme_other

__all__ = ["math_utils", "string_utils", "other_utils"]

def readme():
    return "Ce package contient des modules de mon_package."

if __name__ == "__main__":
    print("The package 'mon_package' was successfully loaded")
```

Les trois premières lignes permettront d'exécuter `mon_package.module_name`:
```python
import mon_package

resultat = mon_package.math_utils.addition(2, 3)
```

L'utilisation de `__all__ = ["math_utils", "string_utils", "other_utils"]` permet de réaliser `from mon_package import *`. 

Enfin comme les packages classiques, on peut exécuter:
```python
from mon_package import math_utils

resultat = math_utils.addition(2, 3)
```

📌 **Explication de `if __name__ == "__main__"` dans un package** :
Dans un package, ce bloc permet d'afficher un message ou d'exécuter un comportement spécifique si le package est exécuté directement comme un script, plutôt que d'être simplement importé dans un autre projet.

Ainsi, on pourra importer directement des fonctions depuis le package :

```python
import mon_package
print(mon_package.readme())
```

### 📝 Ajout du fichier `pyproject.toml`

Le fichier `pyproject.toml` permet de définir les métadonnées du package et sa configuration d'installation.

Exemple :

```toml
[build-system]
requires = ["setuptools>=61.0"]
build-backend = "setuptools.build_meta"

[project]
name = "mon_package"
version = "0.1.0"
authors = [
  { name="Auteur", email="auteur@example.com" },
]
description = "Un package d'exemple"
readme = "README.md"
requires-python = ">=3.8"
classifiers = [
    "Programming Language :: Python :: 3",
    "Operating System :: OS Independent",
]
license = {file = "LICENSE"}
dependencies = [
    "numpy>=2.2.2"
]

[project.optional-dependencies]
dev = [
    "csv>=3.13.1",
    "pandas>=2.2.3",
]

[project.urls]
Homepage = "https://github.com/mon_package/homepage"
Issues = "https://github.com/mon_package/issues"
```

### 🔗 Importance des dépendances avec versions spécifiées

Le fichier `pyproject.toml` permet de gérer les dépendances avec des versions précises. Cela garantit :

- 🏗 **Compatibilité** : Assurer que le package fonctionne avec les bonnes versions des bibliothèques.
- 🔄 **Stabilité** : Éviter des erreurs dues à des mises à jour inattendues.
- 🔁 **Reproductibilité** : Permettre aux utilisateurs d'installer le package avec les mêmes versions de dépendances.

Exemple dans `pyproject.toml` :

```toml
dependencies = [
    "package_name>=version",
    "numpy>=2.2.2",
    "matplotlib>=3.10.0",
    "pandas>=2.2.3"
]
```

---

## ⚙️ 4. Installation et exécution du package

### 📥 Installation locale

Dans le dossier contenant `pyproject.toml`, exécutez :

```sh
python3 -m pip install .
```

### 📦 Installation depuis un archive

Créez un package sous forme d'archive :

```sh
python -m build
```

Puis installez-le :

```sh
pip install dist/mon_package-0.1.0.tar.gz
```

### 🚀 Chargement du package

Après installation, vous pouvez utiliser le package dans n'importe quel script Python :

```python
import mon_package
print(mon_package.readme())
```

---

🎯 **En suivant ces étapes, vous pourrez créer, organiser et distribuer efficacement vos packages Python !** 🐍📦

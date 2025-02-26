# Guide d'initiation à WSL, Ubuntu et Python sous Windows

Ce document va vous aider à installer **Ubuntu** via **WSL (Windows Subsystem for Linux)** sur votre machine Windows et à commencer à exécuter des scripts Python. 📜

## Pré-requis avant d'installer WSL 🛠️

Avant d'installer **WSL (Windows Subsystem for Linux)** et d'exécuter Ubuntu, il y a quelques étapes préparatoires à suivre. Ces étapes assurent que votre système est prêt à fonctionner correctement avec WSL.

### 1. Système d'exploitation compatible ✅

- **Windows 10 version 1903 (build 18362) ou supérieure** ou **Windows 11**.
- Si vous avez une version plus ancienne de Windows, vous devrez peut-être mettre à jour votre système pour pouvoir utiliser WSL.

#### Lien officiel pour l'installation de WSL : 
- [Installation de WSL sur Windows](https://learn.microsoft.com/fr-fr/windows/wsl/install)

### 2. Activer la virtualisation et l'hyperviseur 🔧

Pour que WSL fonctionne correctement, la virtualisation matérielle doit être activée sur votre machine. Voici comment procéder :

1. **Activer la virtualisation dans le BIOS/UEFI** :
   - Redémarrez votre ordinateur et entrez dans les paramètres BIOS/UEFI (généralement en appuyant sur la touche `Del` ou `F2` au démarrage de votre PC).
   - Recherchez une option appelée **Intel VT-x** ou **AMD-V** (en fonction de votre processeur).
   - Activez cette option si elle est désactivée.
   - Sauvegardez et quittez le BIOS/UEFI.

2. **Activer l'hyperviseur Windows** :
   WSL nécessite l'activation de l'hyperviseur Windows. Pour cela, suivez ces étapes :
   
   - Ouvrez **PowerShell** en mode administrateur (clic droit sur l'icône PowerShell et choisir "Exécuter en tant qu'administrateur").
   - Exécutez la commande suivante pour activer la fonctionnalité **Hyper-V** et **Virtual Machine Platform** :
     ```bash
     dism.exe /Online /Enable-Feature /All /FeatureName:Microsoft-Hyper-V-All /NoRestart
     dism.exe /Online /Enable-Feature /All /FeatureName:VirtualMachinePlatform /NoRestart
     ```
   - Ensuite, exécutez cette commande pour activer le **Windows Hypervisor Platform** :
     ```bash
     dism.exe /Online /Enable-Feature /All /FeatureName:Windows-Subsystem-Linux /NoRestart
     ```

3. **Activer le sous-système Windows pour Linux (WSL)** :
   Toujours dans **PowerShell** en mode administrateur, activez WSL avec la commande suivante :
   ```bash
   wsl --install
   ```
   Cette commande installera WSL 2, qui est la version recommandée pour de meilleures performances et une meilleure compatibilité.

4. **Redémarrer votre PC** 🔄

Une fois ces étapes terminées, redémarrez votre machine pour appliquer les changements.

## 1. Qu'est-ce que WSL et Ubuntu ? 🖥️

### WSL (Windows Subsystem for Linux) 🔧

WSL est une fonctionnalité de Windows qui permet d'exécuter une distribution Linux (comme Ubuntu) directement sur Windows, sans avoir besoin d'une machine virtuelle ou d'un dual-boot. Cela permet aux utilisateurs de profiter des outils Linux tout en étant sous Windows.

### Ubuntu 🐧

**Ubuntu** est une distribution Linux populaire, facile à utiliser et idéale pour les débutants. En utilisant Ubuntu sous WSL, vous pouvez bénéficier d'un environnement Linux tout en étant dans un environnement Windows.

## 2. Installation de WSL et Ubuntu 🚀

### Étapes d'installation 🛠️

1. **Activer WSL sur Windows** 
   - Ouvrez **PowerShell** en mode administrateur.
   - Exécutez la commande suivante pour installer WSL :
     ```bash
     wsl --install
     ```
   - Cette commande va activer WSL et installer la dernière version d'**Ubuntu**.

2. **Redémarrer votre PC 🔄**
   Une fois l'installation terminée, redémarrez votre ordinateur pour finaliser l'activation de WSL.

3. **Configurer Ubuntu 🖱️**
   - Ouvrez **Ubuntu** depuis le menu Démarrer.
   - Configurez Ubuntu en créant un nom d'utilisateur et un mot de passe.

4. **Vérifier l'installation ✅**
   Une fois Ubuntu ouvert, tapez la commande suivante pour vérifier que tout fonctionne correctement :
   ```bash
   lsb_release -a
   ```
   Cela affichera les informations sur votre version d'Ubuntu.


#### Problèmes possibles ⚠️ :
- **Erreur "WSL non reconnu"** : Cela signifie que WSL n'est pas activé sur votre machine. Exécutez PowerShell en tant qu'administrateur et essayez à nouveau.
- **Problèmes de version** : Si vous avez une ancienne version de Windows, il vous faudra peut-être une mise à jour pour activer WSL.

## 3. Installation d'Ubuntu WSL et de packages 📦

### Installer Ubuntu WSL 🐧

Si vous avez déjà activé WSL mais n'avez pas encore installé Ubuntu, voici comment procéder :

1. Ouvrez **Microsoft Store**.
2. Recherchez **Ubuntu**.
3. Cliquez sur "Installer" pour télécharger et installer Ubuntu sur votre machine.

### Installer un package Ubuntu 🔥

Pour installer des packages sous Ubuntu via WSL, utilisez **apt**, le gestionnaire de paquets.

1. Ouvrez Ubuntu.
2. Mettez à jour les listes de paquets avec :
   ```bash
   sudo apt update
   ```
3. Installez un package avec :
   ```bash
   sudo apt install nom_du_package
   ```

Exemple pour installer **git** :
   ```bash
   sudo apt install git
   ```

### Installer un package Python 🐍

1. Si vous n'avez pas encore installé Python, exécutez :
   ```bash
   sudo apt install python3
   ```
2. Ensuite, pour installer un package Python avec **pip** :
   ```bash
   python3 -m pip install nom_du_package
   ```

Exemple pour installer **numpy** :
   ```bash
   python3 -m pip install numpy
   ```

## 4. Accéder aux fichiers Linux dans l'explorateur de fichiers Windows 🗂️

Pour accéder à vos fichiers Linux dans l'explorateur Windows, tapez `\\wsl$` dans la barre d'adresse de l'explorateur, puis sélectionnez la distribution Ubuntu.

### Se déplacer entre différents dossiers avec la ligne de commande 🧑‍💻

Sous Ubuntu, vous pouvez utiliser les commandes suivantes pour naviguer dans votre système de fichiers :

- **`cd`** : Change le répertoire courant. Exemple :
  ```bash
  cd /home/votre_nom_utilisateur/Documents
  ```
- **`ls`** : Liste les fichiers dans le répertoire courant. Exemple :
  ```bash
  ls
  ```

### Commandes classiques Linux 📂

- **`pwd`** : Affiche le répertoire courant.
- **`mkdir nom_du_dossier`** : Crée un nouveau dossier.
- **`rm`** : Supprime un fichier. Exemple :
  ```bash
  rm fichier.txt
  ```

## 5. Exécuter un code Python 🧑‍💻

1. Ouvrez Ubuntu.
2. Créez un fichier Python avec un éditeur de texte (comme **nano**) :
   ```bash
   nano mon_script.py
   ```
3. Écrivez votre code Python. Exemple :
   ```python
   print("Hello, World!")
   ```
4. Sauvegardez et quittez l'éditeur (dans **nano**, appuyez sur `Ctrl+X`, puis `Y` pour sauvegarder et `Entrée` pour confirmer).
5. Exécutez le script Python :
   ```bash
   python3 mon_script.py
   ```
   Cela affichera `Hello, World!` dans le terminal.

## 6. Utiliser des forums comme Stack Overflow 🌍

### Rechercher une solution sur Stack Overflow 🧐

Si vous rencontrez un problème, **Stack Overflow** est un excellent endroit pour trouver des solutions. Avant de poser une question, effectuez une recherche pour voir si quelqu'un a déjà résolu le même problème.

![Stack Overflow Logo](https://upload.wikimedia.org/wikipedia/commons/0/0e/Stack_Overflow_logo.svg)

**Conseils** :
- Soyez précis dans vos questions pour obtenir des réponses de qualité.
- Vérifiez les réponses et assurez-vous de bien comprendre les solutions proposées.
- N'appliquez jamais une solution sans comprendre ce qu'elle fait, surtout si elle modifie ou supprime des fichiers.

### Prudence avant d'appliquer une commande ⚠️

Avant de lancer une commande trouvée sur un forum, assurez-vous de comprendre ce qu'elle fait. Par exemple, une commande comme `sudo rm -rf /` peut **effacer tout votre système**. 

Toujours vérifier les commandes avant de les exécuter pour éviter tout dommage potentiel à votre système.

---

Avec ce guide, vous êtes maintenant prêt à utiliser Ubuntu sur Windows avec WSL et exécuter des scripts Python. N'hésitez pas à explorer davantage et à poser des questions sur les forums si vous avez besoin d'aide. Bonne chance et amusez-vous ! 🎉
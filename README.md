# Instructions de l'interface AiKit UI

**Appareils compatibles :**
- myPalletizer 260 for M5
- myCobot 280 for M5
- ultraArm P340
- mechArm 270 for M5
- myCobot 280 for Pi
- mechArm 270 for Pi
- myCobot 280 for JN
- myPalletizer 260 for Pi
- myCobot 280 RISCV

---

## I. Environnement requis

Systèmes compatibles : Raspberry Pi Ubuntu 20.04, Windows 10 ou Windows 11, Jetson Nano Ubuntu 20.04.

---

## II. Dépendances Python

### 1. Appareils standards

Concerne les modèles : myPalletizer 260 M5, myCobot 280 M5, ultraArm P340, mechArm 270 M5, myCobot 280 Pi, mechArm 270 Pi, myCobot 280 JN, myPalletizer 260 Pi.

Avant utilisation, assurez-vous que les bibliothèques suivantes sont installées. Les versions d'`opencv-python` et `opencv-contrib-python` doivent impérativement être la **4.6.0.66** :

```
opencv-python==4.6.0.66
opencv-contrib-python==4.6.0.66
pymycobot==3.6.3
PyQt5==5.15.10
```

Si elles ne sont pas installées, exécutez les commandes suivantes :

```bash
pip install pymycobot
pip install opencv-python==4.6.0.66
pip install opencv-contrib-python==4.6.0.66
pip install pyqt5
```

#### Installation du projet

```bash
git clone https://github.com/elephantrobotics/AiKit_UI.git
```

---

### 2. Appareil RISCV

Concerne le modèle : myCobot 280 RISCV.

#### Création d'un environnement virtuel

```bash
sudo apt install python3-virtualenv
virtualenv elephantics-venv
source elephantics-venv/bin/activate
```

#### Installation des dépendances système

```bash
sudo apt install libopenblas-dev
```

#### Installation du projet

```bash
git clone https://github.com/elephantrobotics/AiKit_UI.git
```

#### Installation des bibliothèques Python

```bash
cd AiKit_UI/libraries/yolov8File
pip install -r requirements.txt
```

---

## III. Démarrage

Depuis le répertoire du projet :

```bash
cd AiKit_UI
python main.py
```

> **Remarque :** Pour le modèle myCobot 280 RISCV, la reconnaissance par algorithme YOLO utilise désormais **YOLOv8** (et non plus YOLOv5). Lorsque l'appareil est de type RISCV, seul YOLOv8 peut être sélectionné dans la liste déroulante des algorithmes. YOLOv8 est plus simple d'utilisation : il n'est plus nécessaire de délimiter manuellement la zone de reconnaissance, celle-ci est détectée automatiquement, de la même façon que pour la reconnaissance par couleur.

---

## IV. Fonctionnalités

### Changement de langue

Cliquez sur le bouton situé en haut à droite de la fenêtre pour basculer entre le chinois et l'anglais.

---

### Connexion de l'appareil

1. Sélectionnez le port série, l'appareil et le débit en bauds.
2. Cliquez sur le bouton **CONNECT** pour établir la connexion. En cas de succès, le bouton devient **DISCONNECT**.
3. Cliquez sur **DISCONNECT** pour déconnecter le bras robotique.
4. Une fois le bras connecté, les boutons grisés s'activent et deviennent cliquables.

---

### Activation de la caméra

1. Définissez le numéro de série de la caméra (par défaut : **0**). Sous Windows, il vaut généralement **1** ; sous Linux, **0**.
2. Cliquez sur **Open** pour ouvrir la caméra. En cas d'échec, modifiez le numéro de série.
   > Avant utilisation, positionnez la caméra directement au-dessus du tableau blanc QR, avec la ligne droite orientée vers le bras robotique.
3. Une fois la caméra ouverte, cliquez sur **Close** pour la fermer.

---

### Contrôle des algorithmes

1. **Mode automatique** : Cliquez sur **Auto Mode** pour activer la reconnaissance, la saisie et le dépôt en continu. Cliquez à nouveau pour désactiver ce mode.

2. **Retour au point initial** : Cliquez sur **Go** pour interrompre l'opération en cours et revenir au point de départ.

3. **Mode pas à pas :**
   - *Reconnaissance* : Cliquez sur **Run** pour démarrer la reconnaissance. L'algorithme actif est affiché.
   - *Saisie* : Cliquez sur **Run** pour saisir l'objet. Une fois la saisie effectuée, la reconnaissance et la saisie se désactivent automatiquement ; il faudra cliquer à nouveau pour une prochaine utilisation.
   - *Dépôt* : Cliquez sur **Run** pour déposer l'objet. Les cases **BinA**, **BinB**, **BinC** et **BinD** correspondent aux 4 bacs de stockage disponibles ; sélectionnez le bac souhaité.

4. **Ajustement du point de saisie** : Les décalages X, Y et Z correspondent aux positions sur chacun des axes du bras robotique. Modifiez-les selon vos besoins, puis cliquez sur **Save** pour enregistrer. Le bras utilisera ensuite ce nouveau point de saisie.

5. **Accès aux fichiers sources** : Le code est open source et modifiable. Cliquez sur **Open File** pour accéder à l'emplacement des fichiers, puis ouvrez `main.py` pour le modifier.
   > Le fichier `main.py.bak` est une sauvegarde de `main.py`. Pour le restaurer, supprimez `main.py`, renommez `main.py.bak` en `main.py`, puis créez une nouvelle sauvegarde. Vous pouvez aussi re-télécharger le projet.

6. **Sélection de l'algorithme** : Choisissez parmi la reconnaissance par couleur, par forme, par QR code ou par points clés (Keypoints). L'algorithme sélectionné sera appliqué lors de la reconnaissance.

7. **Utilisation de YOLOv5 :**
   - Connectez le bras robotique et sélectionnez **yolov5** dans la liste des algorithmes.
   - Activez la caméra.
   - Placez l'image à reconnaître et cliquez sur **Cut**.
   - Délimitez la zone du tableau blanc QR, puis appuyez sur **Entrée** pour confirmer (l'opération est répétable).
   - Lancez ensuite la reconnaissance et la saisie.

8. **Ajout d'images pour Keypoints :**
   - Cliquez sur **Add** ; la caméra s'ouvre avec une invite.
   - Cliquez sur **Cut** pour capturer l'image actuelle ; une invite vous demandera d'appuyer sur **Entrée** pour valider.
   - Délimitez la zone à enregistrer, puis appuyez sur **Entrée** pour choisir le bac de destination (**BinA**, **BinB**, **BinC** ou **BinD**).
   - L'image capturée s'affiche dans l'interface.
   - Pour consulter les images enregistrées, accédez au chemin indiqué dans l'interface.
   - Cliquez sur **Exit** pour quitter l'ajout d'images.
   > Si une capture est en cours, attendez qu'elle soit terminée avant de quitter. Vous pouvez choisir de ne pas enregistrer les images capturées.

---

### Affichage des coordonnées

1. **Coordonnées en temps réel** : Cliquez sur le bouton **Coordonnées actuelles** pour afficher la position courante du bras.
2. **Coordonnées de reconnaissance** : Cliquez sur **Coordonnées image** pour afficher les coordonnées issues de la reconnaissance visuelle.

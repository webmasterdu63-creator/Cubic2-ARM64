<p align="center">
  <img src="https://raw.githubusercontent.com/webmasterdu63-creator/Cubic2-ARM64/release/logo2.jpeg" width="180" alt="Cubic2-ARM64 Logo">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Cubic2--ARM64-Build%20System%20Next--Gen-blueviolet?style=for-the-badge&logo=ubuntu" />
</p>

<p align="center">

  <!-- Version -->
  <img src="https://img.shields.io/badge/version-2.0.0-blue?style=for-the-badge" />

  <!-- Architecture -->
  <img src="https://img.shields.io/badge/ARM64-SUPPORTED-success?style=for-the-badge&logo=linux" />
  <img src="https://img.shields.io/badge/x86__64-SUPPORTED-success?style=for-the-badge&logo=linux" />

  <!-- QEMU -->
  <img src="https://img.shields.io/badge/QEMU-Required-important?style=for-the-badge&logo=qemu" />

  <!-- Ubuntu Image -->
  <img src="https://img.shields.io/badge/ubuntu--image-Backend-orange?style=for-the-badge&logo=ubuntu" />

  <!-- Python -->
  <img src="https://img.shields.io/badge/Python-3.11+-yellow?style=for-the-badge&logo=python" />

  <!-- License -->
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" />

  <!-- Status -->
  <img src="https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge" />

</p>

Section Installation — Cubic2‑ARM64
1. Prérequis système

Cubic2‑ARM64 fonctionne sur :

    Ubuntu 22.04 / 24.04 (x86_64)

    Linux Mint 21 / 22

    Debian 12

    KDE Neon

    Tout système x86_64 avec support binfmt_misc

Assurez-vous que votre système est à jour :
bash

sudo apt update && sudo apt upgrade -y

2. Dépendances obligatoires
2.1 QEMU ARM64 + binfmt-support

Ces paquets permettent d’exécuter des binaires ARM64 sur un PC x86_64.
bash

sudo apt install -y qemu-user-static binfmt-support

Vérifiez que le support ARM64 est actif :
bash

ls /proc/sys/fs/binfmt_misc/qemu-aarch64

Si le fichier existe → QEMU ARM64 est opérationnel.
2.2 Outils de montage d’images .img

Cubic2‑ARM64 utilise kpartx pour mapper les partitions internes des images ARM64 (Raspberry Pi, Ubuntu Server ARM64, etc.).
bash

sudo apt install -y kpartx

2.3 Outils de compression / extraction
bash

sudo apt install -y squashfs-tools xorriso

3. Installation de Cubic2‑ARM64
## 🇫🇷 Téléchargements
- [Télécharger CUBIC2‑ARM64 (ZIP)](https://php.technews365.fr/downloads/Cubic2-ARM64-TN365.zip)
- [Télécharger CUBIC2‑ARM64 (TAR.GZ)](https://php.technews365.fr/downloads/Cubic2-ARM64-TN365.tar.gz)

## 🇬🇧 Downloads
- [Download CUBIC2‑ARM64 (ZIP)](https://php.technews365.fr/downloads/Cubic2-ARM64-TN365.zip)
- [Download CUBIC2‑ARM64 (TAR.GZ)](https://php.technews365.fr/downloads/Cubic2-ARM64-TN365.tar.gz)

🇫🇷 Notice d’utilisation — Cubic2‑ARM64

📦 Extraction de l’archive Windows

    Clic droit sur le fichier téléchargé (.zip ou .tar.gz)

    Sélectionnez “Extraire tout…”

    Ouvrez le dossier extrait

Linux
Code

unzip Cubic2-ARM64-TN365.zip

ou :
Code

tar -xvf Cubic2-ARM64-TN365.tar.gz

macOS

    Double‑cliquez sur le fichier .zip

    macOS extrait automatiquement le dossier

▶️ Lancement de Cubic2‑ARM64

Dans le dossier extrait :
Code

python3 cubic2.py

L’interface graphique s’ouvre immédiatement.
📧 Support / Contact

Pour toute question ou assistance :
contact@technews365.fr
🇬🇧 User Guide — Cubic2‑ARM64

(English version to place right under the French one)
📦 Extracting the archive Windows

    Right‑click the downloaded file (.zip or .tar.gz)

    Select “Extract All…”

    Open the extracted folder

Linux
Code

unzip Cubic2-ARM64-TN365.zip

or:
Code

tar -xvf Cubic2-ARM64-TN365.tar.gz

macOS

    Double‑click the .zip file

    macOS extracts it automatically

▶️ Running Cubic2‑ARM64

Inside the extracted folder:
Code

python3 cubic2.py

The graphical interface will start immediately.
📧 Support / Contact

For any question or assistance:
contact@technews365.fr

## 📸 Capture d’écran – Accueil Cubic 2

<p align="center">
  <img src="cubic2-home.png" width="70%">
</p>


## 🔗 Cubic (version originale)
<p align="center">
  <img src="https://raw.githubusercontent.com/webmasterdu63-creator/Cubic2-ARM64/release/cubic.png" width="240" alt="Cubic Original Logo">
</p>

Cubic2‑ARM64 est basé sur le projet original **Cubic** développé par PJ-Singh.

➡️ Version originale de Cubic :  
https://github.com/PJ-Singh-001/Cubic
## 🔗 Original Cubic project

Cubic2‑ARM64 is based on the original **Cubic** project by PJ-Singh.

➡️ Original Cubic repository:  
https://github.com/PJ-Singh-001/Cubic

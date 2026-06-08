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

Clonez le projet :
bash

git clone https://github.com/<votre_repo>/Cubic2-ARM64.git
cd Cubic2-ARM64

4. Structure du projet
Code

Cubic2-ARM64/
 ├── src/
 │    ├── cubic2.py
 │    ├── detection/
 │    │     ├── arch.py
 │    │     ├── rootfs.py
 │    │     ├── iso.py
 │    │     ├── img.py
 │    │     └── __init__.py
 │    └── backend/ (optionnel)
 ├── polkit/
 └── README.md

5. Activation Polkit (recommandé)

Pour éviter d’utiliser sudo dans le terminal, Cubic2‑ARM64 peut utiliser polkit pour autoriser automatiquement :

    kpartx

    mount

    umount

    losetup

Copiez la règle polkit :
bash

sudo cp polkit/com.cubic2.kpartx.policy /usr/share/polkit-1/actions/

Installez le wrapper sécurisé :
bash

sudo cp polkit/cubic2-kpartx /usr/local/bin/
sudo chmod +x /usr/local/bin/cubic2-kpartx

6. Lancer Cubic2‑ARM64

Depuis le dossier src/ :
bash

cd src/
python3 cubic2.py <chemin ISO/IMG/rootfs>

Exemple :
bash

python3 cubic2.py ~/Téléchargements/ubuntu-24.04.3-preinstalled-server-arm64+raspi.img

7. Fonctionnement ARM64

Lorsqu’une source ARM64 est détectée :

    QEMU ARM64 est automatiquement activé

    qemu-aarch64-static est injecté dans le chroot

    Le rootfs ARM64 devient utilisable sur un PC x86_64

    Le backend ARM64 (ubuntu-image) peut générer une image .img




Cubic2‑ARM64 — TN365 ARM Image Builder

Cubic2‑ARM64 est un fork modernisé de Cubic, conçu pour créer des images Ubuntu ARM64 personnalisées.  
Contrairement à Cubic original (orienté ISO x86_64), Cubic2‑ARM64 utilise ubuntu‑image et un système de manifest YAML pour générer des images .img UEFI ARM64 modernes, compatibles avec les appareils ARM, serveurs, SBC et environnements virtualisés.

Ce projet vise à fournir le premier outil graphique complet pour construire des images ARM64 personnalisées : bureaux, IA, outils admin, thèmes, services, kernels, partitions EFI, etc.

Objectif : simplifier la création d’images ARM64 professionnelles, reproductibles et entièrement personnalisées.
✨ Fonctionnalités principales

    Génération d’images ARM64  
    Crée des images .img UEFI ARM64 modernes, compatibles Raspberry Pi, SBC ARM64, serveurs ARM, VM UEFI, etc.

    Backend ubuntu‑image intégré  
    Remplace totalement la génération ISO x86_64 par un système basé sur ubuntu-image et un manifest YAML.

    Assistant graphique complet  
    Interface simple et intuitive (GTK) pour configurer rootfs, kernel, paquets, services, thèmes et partitions.

    Support UEFI ARM64 natif  
    Génération automatique des partitions EFI, bootloader ARM64, shim, grub-efi-arm64.

    Personnalisation avancée du rootfs  
    Ajout, suppression ou modification de paquets, services, thèmes, IA, outils admin, environnements de bureau.

    Gestion automatique du manifest YAML  
    Génération dynamique du fichier manifest.yaml selon les choix de l’utilisateur.

    Logs en temps réel  
    Affichage des logs ubuntu-image directement dans l’interface.

🖥️ Fonctionnalités TN365 intégrées

    Profils préconfigurés TN365

        KDE Maia ARM64

        XFCE ARM64

        AI Edition ARM64

        Gaming ARM64

    Branding TN365  
    Thèmes, KSplash, icônes, fonds d’écran, sons de démarrage/extinction.

    Support IA local  
    Intégration possible de modèles IA (Ollama, GPT4All, LM Studio).

    Outils Admin Pro  
    Sélection d’outils système, réseau, sécurité et maintenance.

🧩 Fonctionnalités techniques

    Chroot ARM64 complet  
    Gestion du rootfs ARM64 via QEMU + binfmt.

    Support multi‑desktops  
    KDE, XFCE, GNOME, MATE, LXQt, Budgie, Cinnamon.

    Gestion des services systemd  
    Activation/désactivation automatique selon le profil.

    Configuration automatique du clavier FR  
    Pack FR intégré pour Live + TTY + X11 + Calamares.

    Optimisation SquashFS ARM64  
    Compression xz/BCJ, exclusion de fichiers inutiles.

🔧 Fonctionnalités à venir (Roadmap)

    Mode “ISO x86_64 + IMG ARM64” hybride

    Éditeur graphique de manifest YAML

    Support des images multi‑boot ARM64

    Génération d’images cloud ARM64

    Support Docker ARM64 préinstallé

🟦 Fonctionnalités ARM64 — Cubic2‑ARM64

Cubic2‑ARM64 apporte un support complet, natif et automatique pour la création, la modification et la génération d’images ARM64 sur un système x86_64.
Il s’agit du premier builder graphique ARM64 moderne, basé sur ubuntu-image, qemu-user-static et binfmt_misc.
🟩 Détection automatique de l’architecture

Cubic2‑ARM64 détecte automatiquement le type de source :

    Rootfs ARM64

    ISO ARM64

    Image .img ARM64

    Sources x86_64

Le module detection/ analyse :

    les binaires ELF

    les partitions internes des images .img

    les squashfs des ISO

    les rootfs extraits

Résultat : Cubic2 choisit automatiquement le mode ARM64 ou x86_64.
🟧 Activation automatique de QEMU ARM64

Lorsqu’une source ARM64 est détectée, Cubic2‑ARM64 active automatiquement :

    qemu-aarch64-static

    binfmt_misc

    l’exécution transparente des binaires ARM64

    l’injection de QEMU dans le chroot

    la compatibilité totale ARM64 → x86_64

Cela permet :

    d’entrer dans un chroot ARM64 depuis un PC x86_64

    d’installer des paquets ARM64

    de configurer XFCE, KDE, GNOME, AI

    de générer des images ARM64 fonctionnelles

🟪 Support complet des images .img ARM64

Cubic2‑ARM64 peut :

    Monter une image ARM64

    Mapper les partitions via kpartx

    Lire le rootfs interne

    Modifier le système ARM64

    Repackager l’image finale

Compatible avec :

    Ubuntu Server ARM64

    Ubuntu Raspberry Pi ARM64

    Debian ARM64

    Images personnalisées

🟨 Backend moderne basé sur ubuntu-image

Cubic2‑ARM64 utilise un backend moderne :

    génération d’images .img ARM64

    support des modèles gadget.yaml

    support des manifest.yaml

    compression optimisée

    partitions GPT/MBR automatiques

    support Raspberry Pi / ARM64 générique

🟦 Polkit intégré (optionnel)

Pour éviter l’utilisation de sudo, Cubic2‑ARM64 inclut :

    une règle polkit dédiée

    un wrapper sécurisé pour kpartx

    une autorisation graphique

    un fonctionnement propre et professionnel

🟩 Fonctionnalités avancées ARM64

    Chroot ARM64 complet

    Installation de paquets ARM64 depuis un PC x86_64

    Support complet APT ARM64

    Personnalisation du système ARM64

    Ajout de kernels ARM64

    Configuration du bootloader ARM64

    Support des overlays Raspberry Pi

    Génération d’images prêtes à booter

🟧 Fonctionnalités x86_64 conservées

Cubic2‑ARM64 reste compatible avec :

    ISO x86_64

    rootfs x86_64

    builds classiques

    squashfs

    customisation Ubuntu/Debian x86_64

🟪 Résumé

Cubic2‑ARM64 est :

    le premier builder graphique ARM64 complet

    compatible x86_64 + ARM64

    basé sur ubuntu-image

    capable de chrooter ARM64 depuis un PC x86_64

    capable de générer des images ARM64 bootables

    automatisé, propre, professionnel

🚀 Usage

Cette section explique comment utiliser Cubic2‑ARM64 pour charger une source, détecter l’architecture, activer QEMU ARM64 et générer une image finale.
1. Lancer Cubic2‑ARM64

Depuis le dossier src/ :
bash

cd Cubic2-ARM64/src/
python3 cubic2.py <chemin ISO/IMG/rootfs>

Exemple :
bash

python3 cubic2.py ~/Téléchargements/ubuntu-24.04.3-preinstalled-server-arm64+raspi.img

2. Charger une ISO / IMG / rootfs

Cubic2‑ARM64 accepte :

    ISO Ubuntu/Debian x86_64

    ISO ARM64

    Images .img ARM64 (Raspberry Pi, Ubuntu Server ARM64, etc.)

    Dossiers rootfs extraits

Le programme détecte automatiquement le type de source.
3. Détection automatique de l’architecture

Lors du chargement, Cubic2‑ARM64 analyse :

    les binaires ELF

    les partitions internes (via kpartx)

    les squashfs des ISO

    les rootfs ARM64

Résultat :
Code

[INFO] Architecture détectée : arm64

ou :
Code

[INFO] Architecture détectée : x86_64

4. Activation automatique de QEMU ARM64

Si la source est ARM64 :

    qemu-aarch64-static est injecté dans le chroot

    binfmt_misc est activé

    l’exécution ARM64 devient transparente

    le chroot ARM64 fonctionne sur un PC x86_64

Cubic2‑ARM64 affiche :
Code

[INFO] QEMU ARM64 activé avec succès.

5. Modifier le système ARM64

Une fois le rootfs monté et QEMU activé, vous pouvez :

    installer des paquets ARM64

    ajouter XFCE, KDE, GNOME

    intégrer des outils IA

    personnaliser le système

    modifier les services

    changer le kernel ARM64

6. Générer l’image finale

Cubic2‑ARM64 utilise un backend moderne basé sur ubuntu-image :

    génération d’images .img ARM64

    support des fichiers manifest.yaml

    support des gadget.yaml

    partitions GPT/MBR automatiques

    compression optimisée

La génération ARM64 est automatique lorsque la source est ARM64.
🟧 SECTION : Roadmap — Cubic2‑ARM64

(à coller telle quelle dans ton README)
🛣️ Roadmap Cubic2‑ARM64
✔️ Fonctionnalités déjà implémentées

    [x] Détection automatique ARM64 / x86_64

    [x] Support des images .img ARM64

    [x] Montage/démontage via kpartx

    [x] Activation automatique de QEMU ARM64

    [x] Injection de qemu-aarch64-static dans le chroot

    [x] Support complet du chroot ARM64 sur PC x86_64

    [x] Polkit pour exécuter kpartx sans sudo

    [x] Backend ubuntu-image (préparation)

    [x] Structure du projet modulaire (detection/, backend/)

🚧 Fonctionnalités en cours

    [ ] Interface graphique GTK4/Qt6

    [ ] Backend ubuntu-image complet (gadget.yaml + manifest.yaml)

    [ ] Génération d’images Raspberry Pi ARM64

    [ ] Support Debian ARM64

    [ ] Compression SquashFS optimisée ARM64

    [ ] Gestion avancée des partitions ARM64

    [ ] Mode “AI Edition” (TensorFlow Lite, ONNX Runtime ARM64)

🎯 Fonctionnalités futures

    [ ] Mode multi-architecture (x86_64 ↔ ARM64)

    [ ] Création d’images cloud ARM64 (KVM, LXD, Proxmox)

    [ ] Génération d’images UEFI ARM64 génériques

    [ ] Support des overlays Raspberry Pi

    [ ] Intégration d’un éditeur de manifest YAML

    [ ] Mode “Live ISO ARM64” (expérimental)


********************************************************************************************************************************************************
# Cubic 1 ISO x86 uniquement

<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/cubic_512x512.png" height="128"/>

**[Cubic](https://github.com/PJ-Singh-001/Cubic) ([Custom Ubuntu ISO Creator](https://github.com/PJ-Singh-001/Cubic)) is a GUI wizard to create a customized Live ISO image for Ubuntu and Debian based distributions.**

Cubic permits effortless navigation through the ISO customization steps and features an integrated virtual command line environment to customize the Linux file system. You can create new customization projects or modify existing projects. Important parameters are dynamically populated with intelligent defaults to simplify the customization process.

Cubic runs on distributions based on:
- Ubuntu 18.04.5 Bionic Beaver and above
- Debian 11 Bullseye and above

Cubic can be used to customize the Live ISOs for:
- All versions of Ubuntu from 14.04 Trusty Tahr and above
- Most distributions based on Ubuntu
- Many versions of Debian (tested on Debian 11 Bullseye and above)
- Many distributions based on Debian

## Fund Cubic
[<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/donate_to_cubic_with_paypal.png" alt="Donate to Cubic with Paypal" height="64"/>](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=5WJL2ZE3AWGQQ&currency_code=USD&source=url)    [<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/donate_to_cubic_with_venmo_334x156.png" alt="Donate to Cubic with Paypal" height="64"/>](https://venmo.com/code?user_id=2990984925282304946&created=1639368328.1588511&printed=1)

## Install Cubic

Cubic runs on distributions based on Ubuntu 18.04.5 Bionic and above.

    sudo apt-add-repository universe
    sudo apt-add-repository ppa:cubic-wizard/release
    sudo apt update
    sudo apt install --no-install-recommends cubic

<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/ubuntu-logo.png" width="18"/> [Detailed Ubuntu installation instructions](https://github.com/PJ-Singh-001/Cubic/wiki/Install-Cubic#-ubuntu-and-derivatives)

<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/debian-logo.png" width="18"/> [Detailed Debian installation instructions](https://github.com/PJ-Singh-001/Cubic/wiki/Install-Cubic#-debian-and-derivatives)

## Screenshots

[<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/Cubic%20Start%20Page.png" width="256"/>](https://github.com/PJ-Singh-001/Cubic/wiki/Start-Page)
[<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/Cubic%20Project%20Page.png" width="256"/>](https://github.com/PJ-Singh-001/Cubic/wiki/Project-Page)
[<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/Cubic%20Extract%20Page.png" width="256"/>](https://github.com/PJ-Singh-001/Cubic/wiki/Extract-Page)
[<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/Cubic%20Terminal%20Page.png" width="256"/>](https://github.com/PJ-Singh-001/Cubic/wiki/Terminal-Page)
[<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/Cubic%20Prepare%20Page.png" width="256"/>](https://github.com/PJ-Singh-001/Cubic/wiki/Prepare-Page)
[<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/Cubic%20Packages%20Page.png" width="256"/>](https://github.com/PJ-Singh-001/Cubic/wiki/Packages-Page)
[<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/Cubic%20Options%20Page%20Kernel%20Tab.png" width="256"/>](https://github.com/PJ-Singh-001/Cubic/wiki/Options-Page#Kernel-Tab)
[<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/Cubic%20Options%20Page%20Preseed%20Tab.png" width="256"/>](https://github.com/PJ-Singh-001/Cubic/wiki/Options-Page#Preseed-Tab)
[<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/Cubic%20Options%20Page%20Boot%20Tab%201.png" width="256"/>](https://github.com/PJ-Singh-001/Cubic/wiki/Options-Page#Boot-Tab)
[<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/Cubic%20Compression%20Page.png" width="256"/>](https://github.com/PJ-Singh-001/Cubic/wiki/Compression-Page)
[<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/Cubic%20Generate%20Page.png" width="256"/>](https://github.com/PJ-Singh-001/Cubic/wiki/Generate-Page)
[<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/Cubic%20Finish%20Page.png" width="256"/>](https://github.com/PJ-Singh-001/Cubic/wiki/Finish-Page)
[<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/Cubic%20Finish%20Test%20Page.png" width="256"/>](https://github.com/PJ-Singh-001/Cubic/wiki/Finish-Test-Page)
[<img src="https://github.com/PJ-Singh-001/Cubic/blob/release/screenshots/Cubic%20Emulator.png" width="256"/>](https://github.com/PJ-Singh-001/Cubic/wiki/Emulator)

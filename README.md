
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





# Cubic

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

# Create_MacOSX_VM_in_KVM

_Publié par Olivier Fransois: 07-07-2020_

* Un petit tutoriel sur la configuration d’une simple VM macOS dans QEMU, accélérée par KVM.

# Installer macOS Catalina ,High-sierra ,Mojave sur Linux

![logo](https://github.com/chayan91300/create_macosx_vm_in_kvm/blob/master/Images/install-macos-catalina-on-linux-FSMdotCOM.png)

## Un petit tutoriel sur la configuration d’une simple VM macOS dans QEMU, accélérée par KVM.

QU’EST-CE QUE KVM ?

La machine virtuelle basée sur le noyau (KVM) est un module de virtualisation du noyau Linux qui permet au noyau de fonctionner comme hyperviseur.

KVM convertit Linux en hyperviseur de type 1 (métal nu) et nécessite un processeur avec des extensions de virtualisation matérielle, comme Intel VT ou AMD-V.

## DEPENDENCES

* Qemu 3.1 ou version ultérieure.

* Python3.

* pip. Modules KVM activés.

* Un ordinateur Mac n’est PAS requis.


## INSTALL

1. Installez les dépendances. Vous pouvez également installer git (non indiqué dans la capture d’écran ). En fonction de votre distribution :


  * Pour Ubuntu, Debian, Mint et Popos : 
  
  `sudo apt-get install qemu-system qemu-utils python3 python3-pip`
  
  * Pour les distributions basées sur Arch et Arch : 
  
  `sudo pacman -S qemu python python-pip`
  
  * Pour Void : 
  
  `sudo xbps-install -Su qemu python3 python3-pip`
  
  * Pour openSUSE Tumbleweed : `sudo zypper` dans `qemu-tools qemu-kvm qemu-x86 qemu-audio-pa python3-pip`
  
  * Pour Fedora : 
  
  `sudo dnf install qemu qemu-img python3 python3-pip`

2. Clonez ce git https://github.com/chayan91300/create_macosx_vm_in_kvm.git et le cd vers le chemin.

3. Exécutez jumpstart.sh pour télécharger le support d’installation pour macOS (connexion Internet requise).

L’installation par défaut utilise macOS Catalina, mais vous pouvez choisir quelle version obtenir en ajoutant soit --high-sierra, --mojave, ou --catalina.
Par exemple : 

`. /jumpstart.sh --mojave`

4. Créez un disque dur vide en utilisant qemu-img, en changeant le nom et la taille de préférence : 

`qemu-img create -f qcow2 Mydisk.qcow2 64G`

REMARQUE : Remplacez « Mydisk » par votre nom de disque préétabli. Remplacez « 64G » par votre taille de disque préférée (min. 20G).

5.  Modifier basic.sh avec sudo nano basic.sh et ajouter ceci à la fin :
```
-drive id=Systemdisk,if=none,file=Mydisk.qcow2
-device ide-hd,bus=sata.4,drive=Systemdisk
```
Enregistrer les modifications et quitter.

REMARQUE : remplacez « Mydisk » par le nom de disque défini à l’étape précédente.

6.  EXÉCUTER  `. /basic.sh`

7. Démarrer dans macOS Catalina Installer

8. Allez à « Utilitaire disque » et formatez votre disque

9. Une fois que votre disque est prêt, vous pouvez installer macOS Catalina.

10. Vous avez terminé!

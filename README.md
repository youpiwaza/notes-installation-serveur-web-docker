# Notes serveur

Mes notes concernant l'installation de mon serveur


## Tutoriel grafikart / Nginx

[La liste de tutoriels vidéos](https://www.grafikart.fr/tutoriels/nginx-692)

### Rappels linux

[Tutoriel concerné](https://www.grafikart.fr/tutoriels/commandes-base-684)

#### Liste des commandes

| Commande | Options | Kwaksafé | Notes |
|----------|---------|--------------------------------------------------------------------|----------------------|
| `.` |  | Correspond au répertoire courant |  |
| `..` |  | Répertoire parent |  |
| `~` |  | Dossier utilisateur courant (`/home/max/`) |  |
| `cd` |  | Modifie le répertoire courant | `Change directory` |
| `ls` |  | Lister le contenu du dossier (courant) | `List` |
|  | `-a` | Affiche les fichiers et dossiers cachés |  |
|  | `-l` | Affiche des infos supplémentaires (droits, possessions) |  |
|  | `-R` | De manière récursive (avec contenus sous-dossiers) |  |
|  | `-t` | Avec tri par date de modification |  |
|  | `-F` | Indique les dossiers, rajoute un slash |  |
| `mkdir` |  | Création d'un dossier | `Make directory` |
| `rmdir` |  | Supprime un dossier | `Remove directory` |
| `touch` |  | Créer un fichier | `Bah touche` |
| `rm` |  | Supprimer un fichier | `Remove` |
|  | `-r` | De manière récursive |  |
| `mv` |  | Déplacer ou renommer un fichier | `Move` |
| `cp` |  | Copier un fichier | `Copy` |
| `ln` | `-s` | Créer un lien symbolique '~raccourci windows' | `Link` |
| `chmod` |  | Changer les droits (RWX) pour utilisateur/groupe/tous | `Change mod` |
|  | `-r` | Récursif |  |
| `chown` |  | Changer la possession (`utilisateur:groupe`) | `Change owner` |
|  | `-r` | Récursif |  |
| `sudo` |  | Exécuter la commande avec les droits max (`root`) | `Substitute user do` |
|  | `-s` | .. sur plusieurs commandes d'affilée (pour quitter le mode `exit`) |  |
| `clear` |  | Vider le contenu affiché de la console |  |

#### Principaux dossiers

| Dossier | Notes |
|-------------------|-------------------------------------------------------------------------------------------------------|
| `bin/` & `sbin/` | Exécutables (~= /Program files/) |
| `usr/bin/` | Exécutables de l'utilisateur |
| `etc/` | Configuration des logiciels |
| `mnt/` & `media/` | Sources externes (CD, DD, usb, etc.) |
| `root/` | Dossier de l'administrateur |
| `srv/` | Dossier pour serveur ? |
| `boot/` | Tout ce qui concerne le démarrage de la machine |
| `lost+found` | Lorsque le système a des 'ratés' |
| `opt/` | Tout ce qui ne rentre pas dans la structure linux (logiciels propriétaires..) |
| `run/` | Espace mémoire pour certains programmes de boot ? |
| `sys/` | Virtual filesystem ? |
| `proc/` | Infos sur les processus en cours |
| `var/` | Tous les fichiers courants, qui vont être modifiés par l'utilisateur (backups, cache, **logs**, etc.) |
| `home/` | Contiendra les dossiers des différents utilisateurs |

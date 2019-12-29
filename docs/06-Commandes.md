# Liste des commandes

Petite cheat sheet & annotations supplémentaires sur les commandes rencontrées au cours de tout ce joyeux bordel.


## Linux

[Si besoin de plus](https://explainshell.com/)

| Commande | Options | Kwaksafé | Notes |
|----------|---------|--------------------------------------------------------------------|----------------------|
| `Ctrl + C` |  | Arrêter la commande en cours |  |
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
| `usermod` |  | Changer un utilisateur | `User modification` |
|  | `-g` | Changer le groupe d'un utilisateur |  |
| `sudo` |  | Exécuter la commande avec les droits max (`root`) | `Substitute user do` |
|  | `-s` | .. sur plusieurs commandes d'affilée (pour quitter le mode `exit`) |  |
| `wget URI` |  | Récupérer le contenu d'une url | `Get from web` |
| `clear` |  | Vider le contenu affiché de la console |  |
| |  | |  |
| `rsync -avhpz /Source /Sauvegarde` |  | Copie |  |
|  | `-a` | (Archive) Récursive, avec droits, possessions, temps, etc. |  |
|  | `-s` | Avec liens symboliques |  |
|  | `-p` | Avec droits dossiers/fichiers |  |
|  | `-o` | Avec possessions |  |
|  | `-t` | Avec temps dernières modifications |  |
|  | `-h` | Avec infos format humain |  |
|  | `-p` | Avec progression & partiels |  |
|  | `-z` | Avec compression (zip) avant envoi |  |
|  | `-n` | (= `--dry-run`) Diff AVANT exécution |  |
|  | `--exclude-from` | (~= .gitignore) Pattern d'exclusion (fichiers conf, etc.) à partir d'un fichier |  |
|  | `-b` | Backup : Versionning de la copie ~précédente (incr.) |  |
|  | `-e` | Si envoi vers serveur distant (via. SSH) permet de spécifier le port |  |
| `pwd` |  | Linux > Affiche le chemin du répertoire courant |  |
| `whereis` |  | Linux > Chemin vers logiciel ou vide si non installé |  |


### Principaux dossiers

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


### Gestion des paquets

| Commande | Notes |
|----------------------------|--------------------------------------|
| `apt-get -h` | Infos sur le gestionnaire de paquets |
| `sudo apt-get update` | Mettre à jour la liste des dépôts |
| `sudo apt-get install XXX` | Installer le paquet XXX |
| `sudo agpt-get upgrade` | Mettre a jour la distribution linux |


### Paquets recommandés

| Nom du paquet | Notes | Url |
|---------------|--------------------------------------|---|
| `curl` | Installation de logiciels serveurs | |
| `git` | Installation de logiciels serveurs (git clone) | |
| `htop` | Meilleure vue des processus en cours | |
| `rsync` | (Déjà installé) Copies et sauvegardes (incrémentales) | [tuto grafikart](https://www.youtube.com/watch?v=7Hb32v8e8W0) contient également exemple déploirement WP |


## Docker

[Liste des commandes docker](https://youtu.be/fqMOX6JJhGo?t=1276)

`docker ps -a` // liste de l'ensemble des containers + status + plus lisible

| Commande | Argument | Kwaksafé |
|-------------------------------------|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| `docker build` |  | Faire un build de l'image : même chose que run MAIS read only |
| `docker pull IMAGENAME` |  | Récup image sans run |
| `docker run IMAGENAME:TAG` |  | Lancer un container, avec l'image voulue, ainsi que sa version (tag) |
|  | `-i` | (interactive mode) autorise inputs consoles |
|  | `-t` | (attacher au terminal) utiliser -it pour injecter des trucs |
|  | `-p 80:5000` | (lier les ports HOST:CONTAINER), ici si un utilisateur accède au port 80 de l'host, il sera redirigé vers les port 5000 du container |
|  | `-v HOSTDIR:CONTAINERDI` | persistance des données, lier dossiers hôtes/container |
|  | `-e APP_COLOR=BLUE` | (environnement) Ajoute une variable d'environnement |
|  | `--link CONTAINERNAME:NAME` | Lier 2 containers (ex php &amp; sql) sans passer par compose |
| `docker ps` |  | Liste des containers |
|  | `-a` | .. y compris ceux qui ne sont pas en route |
| `docker push CONTAINERID` |  | Envoyer sur le docker hub |
| `docker stop ID` |  | Arrêter un container |
| `docker rm ID` |  | Supprimer un container |
| `docker images` |  | Afficher la liste des images dispos |
| `docker rmi IMAGENAME` |  | Supprimer une image téléchargée |
| `docker exec ID CMD ATTR` |  | Execute une commande sur/a l'intérieur d'un container (souvent utilisée pour lancer le shell d'un os) |
| `docker prune` |  | Vire toutes les images arrétées/inutilisées |
| `docker system prune` |  | ++ |
| `docker inspect CONTAINER` |  | Infos sur le container au format json |
| `docker logs CONTAINER` |  | Infos logs sur le container |
| `docker network ls` |  | Liste des réseaux internes à l'hôte |
| `docker volume create VOLUMENAME` |  | Créer un espace de stockage pour données persistantes, s'utilise avec run -v |
| `docker volume ls` |  | Lister les volumes (données persistantes) |
| `docker search` |  | Afficher repos distants existants |
|  | `-s` | (stars) avec un certain nb d'étoiles |
| `docker cp` |  | (copy) copier un fichier de l'intérieur d'un container docker vers l'hôte |
|  |  |  |
| `docker-compose up` |  | Lancer le groupement de containers |
| `docker service create` |  | Truc d'orchestration |


## Divers

| Commande | Argument | Kwaksafé |
|------------------------|---|------------------------------------------------------|
| `nginx -t` |  | Tester la configuration |
| `systemctl reload nginx` |  | ? Relancer nginx |


### Navigation

La suite, [Technologies avancées](/docs/07-Avance.md), ou retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).
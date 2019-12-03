# Notes serveur

Mes notes concernant l'installation de mon serveur



## Tutoriel grafikart / Nginx

[La liste de tutoriels vidéos](https://www.grafikart.fr/tutoriels/nginx-692)

### Rappels linux

[Tutoriel concerné](https://www.grafikart.fr/tutoriels/commandes-base-684)

#### Liste des commandes

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

#### Gestion des paquets

| Commande | Notes |
|----------------------------|--------------------------------------|
| `apt-get -h` | Infos sur le gestionnaire de paquets |
| `sudo apt-get update` | Mettre à jour la liste des dépôts |
| `sudo apt-get install XXX` | Installer le paquet XXX |
| `sudo agpt-get upgrade` | Mettre a jour la distribution linux |

##### Paquets recommandés

| Nom du paquet | Notes | Url |
|---------------|--------------------------------------|---|
| `curl` | Installation de logiciels serveurs | |
| `git` | Installation de logiciels serveurs (git clone) | |
| `htop` | Meilleure vue des processus en cours | |
| `rsync` | (Déjà installé) Copies et sauvegardes (incrémentales) | [tuto grafikart](https://www.youtube.com/watch?v=7Hb32v8e8W0) contient également exemple déploirement WP |



-------

# TODO

## Configuration du serveur

### One shot

- [Changer port par défaut](https://youtu.be/lXOdDal6qos?t=239) : Meilleure sécurité, plus de mots de passe.
- [Retirer connexion par mot de passe](https://youtu.be/lXOdDal6qos?t=324) : Meilleure sécurité, plus de mots de passe.
- Mise en place de backups automatiques via le CRON (~1 fois / jour, incrémental)
  - [Mise en place Rsync](https://www.youtube.com/watch?v=7Hb32v8e8W0) pour les fichiers
  - mysqldump > bdd sql
  - Ajouter un clean des logs (zip après 2 semaines, suppression après 2 ans)
- Créer un dossier log contenant les liens symboliques EXPLICITES vers les logs des différentes technos
- Ajouter un script/la conf qui envoie un email en cas d'erreur côté serveur
- Ajouter une page par défaut pour le serveur, en cas d'accès via l'IP
- Ajouter des pages personnalisées pour les différentes erreurs serveurs 50X
- Désactiver erreurs (php, etc.) & phpinfo en prod
  - Rendre accessible via page dédiée + pass ? (ou dev. suffisant..)
- Script analyses performances (ex [config mysql](https://www.grafikart.fr/tutoriels/mysql-690))
- Ajouter de la sécurité autant que possible > https://www.hacksplaining.com/lessons
- Installer REDIS, et implementer (node et WP) pour gain de perfs
  - Faire un test avec une base WP et faire un diff des perfs
- Mise en place des ~[certificats SSL](https://www.grafikart.fr/tutoriels/apache-ssl-letsencrypt-746)~ cf. [installation avancée](https://www.grafikart.fr/tutoriels/nginx-ssl-letsencrypt-747)
  - Certifs SSL gratuits [Let's encrypt](https://letsencrypt.org/fr/)
  - Tests certificats SSL [SSL Labs tests](https://www.ssllabs.com/ssltest/)
- Mise en place serveur de mails (postfix)
- Mise en place accès FTP pour utilisateurs existants [ProFTP](https://www.grafikart.fr/tutoriels/proftpd-755)
  - Annuaire simple des accès en place
- MeP parefeu (iptables)

### Procédures

- [Ajouter un utilisateur SSH via clés seulement](https://youtu.be/lXOdDal6qos?t=449) : Remplace le mot de passe.
- Ajouter un utilisateur serveur par site et limiter son accès (docker/ftp/annuaire ?)
- Vérifier les performances des différentes technos (analyse + logs)
- Ajouter/Renouveler les certificats SSL (https)
  - CRON ?
- Envoi de mail + tester templates [mailinator](https://www.mailinator.com/)
- Règles iptables

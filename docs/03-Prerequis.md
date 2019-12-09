# Pré-requis

Histoire de ne pas aller se noyer directement dans du Docker, et vu que ça va être également beaucoup orienté Linux & Serveur, une petite remise à niveau s'impose.


## Connaissances de base

Durée _~1h en x2_

| Source | Titre | Sujet | Lien |
|-----------|------------------------------------------------------------|------------------|---------------------------------------------|
| Grafikart | Mettre en place un serveur Web (3/28) : Commandes de bases | Commandes linux | [Go](https://www.youtube.com/watch?v=OekaaLmwttc) |
|  | Linux File System/Structure Explained! | Dossiers linux | [Go](https://www.youtube.com/watch?v=HbgzrKJvDRw) |
|  | Langage Yaml | Utilisé pour créer les fichiers DockerFile | [Go](https://www.youtube.com/watch?v=cdLNKUoMc6c) |
| Traversy media | Connexion en ssh, clés & ports | Utilisé pour accéder au serveur | [Go](https://www.youtube.com/watch?v=hQWRp-FdTpc) |


Il y a dans ce repo une [doc dédiée](/docs/06-Commandes.md) pour les commandes & un récap de l'arbo linux.


## Installation d'un serveur web

Installation d'un serveur web (Apache ou Nginx)

Durée _~1 journée en x2_

| Source | Titre | Sujet | Lien | Notes |
|-----------|-----------------------|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|------------------|
| Grafikart | Créer son serveur web | Tuto serveur complet, a regarder pour avoir un point de vue global pour UN site | [Go](https://www.grafikart.fr/tutoriels/nginx-692) | ~1 journée en x2 |
| Cocadmin | Ansible + Docker = ? | Intro automatisation d'installation de serveur via Ansible | [Go](https://www.youtube.com/watch?v=yqLPUOsy-8M) |  |


## Gestion de plusieurs sites

Il existe quelques méthodes différentes pour gérer plusieurs sites via un même serveur.

La plus courante étant d'assigner à chaque nom de domaine (ex: masamune.fr) une redirection vers un dossier spécifique (ex: /home/masamune/www/ ) via apache ou autre.

Étant donné que nous allons passer par Docker et que ce dernier fonctionne avec des containers (isolés mais accessibles par des ports), d'après mes recherches le mieux serait de passer par du _reverse proxy_.

EN GROS, Tous les clients arrivent par la même entrée (l'IP du serveur) mais sont redirigés vers les bons sites.

Bref, vidéos, tout ça..

Durée _~10m en x2_

| Source | Titre | Sujet | Lien | Notes |
|--------|--------------------------------------------------------|--------------------------------------------------|---------------------------------------------|-------------------|
|  | Proxy vs. Reverse Proxy (Explained by Example) | Explication en schéma toukon | [Go](https://youtu.be/ozhe__GdWC8?t=299) |  |
|  | Run Multiple Site from one IP with reverse proxy Nginx | **1 ip, redirige vers même ip différents ports** | [Go](https://www.youtube.com/watch?v=x1fnOJsX6wE) | **Indispensable** |


### Notes

Possibilité de passer par Ansible pour automatiser la gestuib des NDD & des technologies déployées.



## Docker / kwaksé

~~Et bien Jammy, c'est très simple~~

On rentre dans le vif du sujet + de plus en plus de tech/concret. Pour enfin comprendre le principe de docker/containers/etc. et commencer à faire le lien avec ce qu'on va mettre en place sur le serveur.

Durée _~2h en x2, mais regarder plusieurs fois si besoin.._


| Source | Titre | Sujet | Lien | Notes |
|------------------|------------------------------------------------------------------------------------------------|-------------------------------------------------|---------------------------------------------|-----------------------------|
| Peter Fischer | The Virtual World vs the Container World | Métaphore simple interêt containers | [Go](https://youtu.be/LQWzAkD_zvM?t=8) |  |
| Grafikart |  | Kwaksé docker + démo simple + dockerhub | [Go](https://www.youtube.com/watch?v=XgKOC6X8W28) |  |
|  | Déployer ou exécuter un site Web statique en tant que conteneur à l'aide du didacticiel Docker | Exemple über simple déploiement index.html | [Go](https://www.youtube.com/watch?v=4PvlcTtaAhw) |  |
|  | Top 5 Reasons To Learn Docker For Web Developers | Justifications docker | [Go](https://www.youtube.com/watch?v=sNTn_ZtRSS8) |  |
| freeCodeCamp.org | Docker Tutorial for Beginners - A Full DevOps Course on How to Run Applications in Containers | Théorie + Commandes + tout | [Go](https://youtu.be/fqMOX6JJhGo) | ♥♥♥ Si 1 seule vidéo, celle la |
| Pentacode | Using Docker to deploy Apache, Nginx, Wordpress and Nodejs containers | 1 serveur 4 containers sur 4 ports différents | [Go](https://youtu.be/1OLyXJJPBSA?t=137) |  |
| Grafikart | Tutoriel Docker : Environnement de développement basé sur Docker | Exemple VHOSTS | [Go](https://youtu.be/F9R1EOaA7EA?t=1577) | Ne pas tt regarder |
| Traversy media | Exploring Docker [2] - Docker Compose With Node & MongoDB | App puis Docker image puis DCompose puis Heberg | [Go](https://www.youtube.com/watch?v=hP77Rua1E0c) | ♥ Cycle complet |


### Navigation

La suite, [Tutos docker : Mettre les mains dedans](/docs/04-Tutoriel-Docker.md), ou retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).
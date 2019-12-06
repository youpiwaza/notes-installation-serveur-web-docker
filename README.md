# Installation d'un serveur web (Docker et autres)

Mes notes concernant l'installation de mon serveur (montée en compétence DevOps).

Le tout compilé, annoté et réorganisé afin de vous permettre d'apprendre tout de manière optimisée.

Le but est de mettre en place une architecture clean & sécurisée à base de Docker, en respectant les bonnes pratiques :)

Bon étant donné la masse d'infos, j'ai tout découpé.


## Table des matières

1. [Lexique](/docs/01-Lexique.md)
	- a. [Définitions](/docs/01-Lexique.md#définitions)
	- b. [Technologies associées](/docs/01-Lexique.md#associations)
	
2. [Hébergement](/docs/02-Hebergement.md)
	- [Gammes](/docs/02-Hebergement.md#gammes)
	- [Mon historique serveur](/docs/02-Hebergement.md#mon-historique-serveur)
	- [Mon serveur actuel](/docs/02-Hebergement.md#mon-serveur-actuel)


### Théorie, apprentissage, tests

Il va y avoir énormément de vidéos, ne pas hésiter à vitesse x2.

3. [Pré-requis](/docs/03-Prerequis.md)
	- a. [Connaissances de base](/docs/03-Prerequis.md#connaissances-de-base)
	- b. [Installation d'un serveur web](/docs/03-Prerequis.md#installation-dun-serveur-web)
	- c. [Gestion de plusieurs sites / Reverse proxy](/docs/03-Prerequis.md#gestion-de-plusieurs-sites)
	- d. [Docker / kwaksé](/docs/03-Prerequis.md#docker--kwaksé)
	
4. Tutos docker : Mettre les mains dedans

5. Rentrer dans le gras (docker++)
	- a. Dockerfile / Création d'images dockers & opti
	- b. Docker compose / multiples containers + communication entre
	- c. Docker persistance des données / volumes & links
	- d. Docker network / Réseau interne (compose)

6. Liste des commandes
	- a. linux
	- b. Docker
	- c. Docker-compose
	
7. Avancé
	- a. Orchestration : plein de hosts & containers docker + masters qui surveillent
	- b. Docker machine / Faire 'run' sur de multiples autres hosts
	- c. Microservices / Tout éclater, 1 container pour 1 table de bdd x)

8. Mes questions


### Pratique

Après tout cet apprentissage, il est temps de mettre en place & monter en stack.

9. Exigences

10. Mise en place concrète


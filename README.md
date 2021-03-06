# Installation d'un serveur web (Docker et autres)

Mes notes concernant l'installation de mon serveur (montée en compétence DevOps).

Le tout compilé, annoté et réorganisé afin de vous permettre d'apprendre tout de manière optimisée.

Le but est de mettre en place une architecture clean & sécurisée à base de Docker, en respectant les bonnes pratiques :)

Bon étant donné la masse d'infos, j'ai tout découpé.

Note : Veille techno faite fin 2019, et vu que j'ai une facheuse tendance à ne pas tenir mes projets à jour, n'hésitez pas à vérifier les sources/versions si ce repo à plus de 6 mois ;)

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
	
4. [Tutos docker : Mettre les mains dedans](/docs/04-Tutoriel-Docker.md)

5. [Rentrer dans le gras (docker++)](/docs/05-Docker.md)
	- a. [Dockerfile / Création d'images dockers & opti](/docs/05a-Dockerfile.md)
	- b. [Docker compose / multiples containers + communication](/docs/05b-Docker-compose.md)
	- c. [Docker persistance des données / volumes & links](/docs/05c-Volume-et-persistance.md)
	- d. [Docker network / Réseau interne (compose)](/docs/05d-Network.md)

6. [Liste des commandes](/docs/06-Commandes.md)
	- a. [Linux](/docs/06-Commandes.md#linux)
	- b. [Docker](/docs/06-Commandes.md#docker)
	- c. [Divers](/docs/06-Commandes.md#divers)
	
7. [Avancé](/docs/07-Avance.md) / Découverte des concepts avancés
	- a. [Orchestration](/docs/07-Avance.md#orchestration) / Config Host & Tâches usuelles & Essains de conteneurs
	- b. [Microservices](/docs/07-Avance.md#microservices-plus-tard) / Tout éclater, 1 container pour 1 service (~= 1 table de bdd x))
	- c. [CI/CD](/docs/07-Avance.md#ci-cd) / Intégration continue
	- d. [Websockets et serveur stream](/docs/07-Avance.md#websockets-et-serveur-stream) / ~Serveur Node avec stream
	- z. [Divers](/docs/07-Avance.md#divers) / Survols de technos

22. Lire la doc officielle, et premiers tests
	- 0. Mise à jour de l'environnement de dev (terminal zsh)
	- a. [Docker](https://docs.docker.com/) / Docker sera utilisé pour tester les autres technos
	- b. [Ansible](https://docs.ansible.com/)
		- [Ansible in depth pdf](https://www.ansible.com/resources/whitepapers/ansible-in-depth)

8. [Mes questions](/docs/08-Questions.md)


### Pratique

Après tout cet apprentissage, il est temps de mettre en place & monter en stack.

9. [Exigences](/docs/09-Exigences.md)

10. [Choix technologiques](/docs/10-Choix-technologiques.md)
	- a. [Architecture](/docs/10a-Architecture.md) / Schémas & évolutions

11. [Mise en place](/docs/11-Mise-en-place.md)

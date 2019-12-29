A RANGER
--------

00. Ajouter cours DevOps dans les trucs à regarder dans la doc avant de rentrer dans le gras, dans les pré-requis (fichier dédié ?)
	- Outils a jour / [Xebialabs periodic table](https://xebialabs.com/periodic-table-of-devops-tools/)

01. Créer la configuration en [IaC](https://www.udemy.com/course/linux-academy-devops-essentials/learn/lecture/13781164#overview)
	- Utiliser Ansible pour mise en place du serveur
	- Veersionner la configuration (cookbook ansible ?) à utiliser


546. Tester terminaux et choisir
	- Possibilité d'en faire un conteneur ? Ex: Alpine > avec interface grpahique

- Critères
	- Onglets et ou écrans multiples
	- Possibilité de cliquer pour déplacer le curseur
	- Redimensionnement correct + multiligne correct
	- Coloration syntaxique
	- Intégration de git status
	- ~theme solarized
	- Se lance rapidement !
	- polices ok
	- performances
- Possibilités
	- Cmder // Pas recommandé par grafikar tmais jeter un oeil
	- Hyper // Nouveau <3 ?
	- bash + zsh + omz
	- powershell (windows de base)
	- MobaXterm // long a se lancer, un peu moche
	- iterm2
	- tmux
	- conemu > un peu moins reco par cocadmin
	- windows terminal (le nouveau) > reco par cocadmin
- Créer/récupérer des alias de commande (docker, !! pour rajouter sudo, etc.)

Faire environnementS de dev Docker

- Site statique (+ gulp)
- Serveur PHP (nginx ou apache)
- Serveur Node

- Chercher si images de bases tranquilou, sinon
- Noter les configurations / rendre réutilisable
	- Affichage des erreurs (phpay)
- Conteneurs montés a la volée en fonction des besoins, données persistées via *volumes*


SE RENSEIGNER AVANT DE GOYER
----------------------------

5. Manger la doc officielle & Tester en local

	1. Docker / Création d'un conteneur
		- OK Dockerfile (hello world from scratch)
		- OK Networking
		- Storage
		- Production
		
	2. Kubernetes / Gestion de conteneurs
		- Note : Plutôt docker swarm ? interfaces graphiques ~auto
	3. Ansible / Configuration et automatisation
		- AWX / Interface ^
	4. Traefik / Reverse proxy sur Nginx multiples
	4.5. [Packer](https://www.packer.io/) / Image build/vm/container automation
	5. OK Nginx / Serveur local, afficher un hello world
	- Créer un HW 2, avec rooting via traefik



2. Docker for web hosting & bonnes pratiques (a ranger.md)

3. Séparation environnement de développement de la mise en ligne ?

	- Possibilité de simplifier les upgrades de technos
	- Possibilité de monter des conteneurs de différentes versions en simultané : ex 2 nginx sur 8080 et 8081 pour tester php6 et php7

> dev (local uniquement) != preprod/prod/debug

123. https://dockerswarm.rocks/project-generators/

4. clean exigence et choix technos

- rsync les deux
- Prioriser : Indispensable, prioritaire, plus tard, pas necessaire + statut : Fait/en cours/ a Faire

6. Répondre à l'ensemble des questions 8

7. Attaquer (enfin)

- ansible galaxy
- Tester
- Valider
- Maj repo 10 & 11


---

Technos a connaitre en surface, pour choix

-	Docker for web hosting
	- AppArmor
	- grsec
	- SELinux 
	- Restrict network access (e.g. egress)
	
- Kubernetes for web hosting

Se manger la doc officielle ACTUALISÉE sur les technos choisies

- Nginx
- Docker
	- Docker from scratch
	- Docker source control

- Kitematic > Docker GUI


Optimisations

- [Utiliser ARG pour stocker les versions](https://www.udemy.com/course/docker-essentials/learn/lecture/12339826#overview)
- [Utiliser ENV](https://www.udemy.com/course/docker-essentials/learn/lecture/12339842#overview)
- Création d'image (docker-compose), faut-il intégrer Nginx à chaque site ? cd. 8-Questions.md
-	docker multi stage build
- ansible++, et ansible galaxy
-	https://github.com/oupala/apaxy
-	dockercon
- Docker keywords > Bonnes pratiques / tips / tricks / security / optimisations
- containers HEALTHCHECK > commande dans docker file ou directement via kube/swarm ?
	- Possibilité d'appeler un script pré-fait en cas d'echec (au lieu de [exit 1](https://www.udemy.com/course/docker-for-beginners/learn/lecture/14002044#overview), go envoyer un mail)

--- 

## (Bien) plus tard

Technos a check

-	node express
-	Netflix Titus
-	codeship
-	axios
-	Migrer de Atom a vscode ? // atom vs vscode / most popular ide
-	Tuto serveur node complet [ici](https://www.youtube.com/watch?v=XCgCjasqEFo&list=PLQlWzK5tU-gDyxC1JTpyC2avvJlt3hrIh&index=2)
- Mails https://www.bluemind.net/
- https://www.opendns.com/

- https://www.form.io/
- PROJEQTOR 
































//
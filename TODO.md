TODO / Clean todo :D / A RANGER

--------

[Gros recap 1 page de swarm](https://www.aquasec.com/wiki/display/containers/Docker+Swarm+101)

--------

[Vidéo Traefik v2 officielle avec un accent horrible, mais je crache pas trop dessus je dois avoir le même)[https://www.youtube.com/watch?v=RP40Iv_0yvA]

---


Caddy vs Nginx (serveur web)

https://www.google.com/search?q=caddy+vs+nginx&oq=caddy+vs+&aqs=chrome.1.69i57j0l7.2745j0j7&sourceid=chrome&ie=UTF-8)

---

Docker for production docs

---

[Traefik canary release](https://youtu.be/RP40Iv_0yvA?t=1891)

---


Healthcheck example

```yml
  daServiceQuiTapeSurDeuxPoints3000:
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000"]
      interval: 5s
      timeout: 1s
      retries: 5 
```


Limiter les ressources allouées

```yml
  daService
    deploy:
      resources:
        limits:
          memory: 128M
        reservations:
          memory: 64M
```

---


Taf
- Cron par site
- set de capabilities pour montage container (cf. security)

1.  Ajouter cours DevOps dans les trucs à regarder dans la doc avant de rentrer dans le gras, dans les pré-requis (fichier dédié ?)
	- Outils a jour / [Xebialabs periodic table](https://xebialabs.com/periodic-table-of-devops-tools/)

005. Avant goyer avec DockerFiles & compose, voir pour git & hub, afin de sauvegarder les images d'exercice sur le hub (bonnes pratiques)

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

# Indexation ressources tests

- server-related-tutorials
  - 01-docker
    - 01-Docker-desktop 
      - 01 // Installation docker & tests de base
      - 02 // Modification image & création d'un build
      - 03 // Installation & tests kube
      - 04 // Installation & tests swarm
    - 02-WLS // Installation docker & docker-compose (SPECIAL) sur WLS, et lien vers Docker desktop (windows) + COMMANDE LIEN WLS DDesktop
    - 03-develop-with-docker
      - 01 // Création de dockerfile, context
      - 02 // Build depuis github, Mise en place des volumes (& bind), Backup & restauration volumes
    - 04-my-tests
      - 01 // Dockerfile			/ Nginx 						/ OK	/ Site statique sans process, , github
      - 02 // Docker compose 		/ Nginx + PHP					/ OK	/ Configuration de Nginx & php-fpm, bash containers, exploration configs
      - 03 // Docker compose		/ Nginx + PHP + SQL + adminer 	/ OK	/ Custom Dockerfile (Php + PDO), bash containers, exploration configs, networks, init SQL, volumes, docker secrets (KO), dockerhub push
      - 04 // Docker compose		/ Traefik						/ OK	/ docker-compose CLI
      - 05 // Swarm 				/ Traefik + consul 				/ KO	/ Faire tourner l'exemple docker rocks > ~KO + traefik outdated
      - 06 // Swarm					/ Traefik + ui					/ OK	/ Mise en place de traefik et de son ui + configuration de services (routes)
      - 07 // Docker compose		/ Traefik						/ OK	/ Exemple dockerhub, routes automatiques pour compose
      - 07.1 // run compose swarm	/ Traefik						/ OK	/ Routes automatiques (avec réécriture) pour run, compose & swarm
      - 07.2 // compose				/ Traefik						/ ~KO 	/ Routes automatiques (avec réécriture) pour projet concret (php + sql) > KO aléatoire 1/2
      - 07.3 // swarm				/ Traefik						/ KO 	/ Routes via labels pour projet concret (php + sql)
      - 08	// swarm				/ swarmprom						/ OK	/ Pack outils de monitoring + conf windows. Tout OK excepté Nodes swarm


POUR LES TRUCS KO :  `docker service logs NOM_DU_SERVICE`


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
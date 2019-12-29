# Docker & Dockerfile propre

Docker, kwaksé un container et création d'images

Juste avant, [Création d'une image et utilisation du build](https://www.katacoda.com/courses/docker/create-nginx-static-web-server).

Au programme : 

- Création de Dockerfile
- Variables d'environnement
- Bonnes pratiques
- Optimisations
- Sécurité
- Cache
- Aperçu docker compose


| Source | Titre | Sujet | Lien | Notes |
|------------------|---------------------------------------------------------------|-----------------------------------|---------------------------------------------|-------------------|
| cocadmin |  | YAML pour docker | [Go](https://www.youtube.com/watch?v=7gmW6vxgsRQ) |  |
| freeCodeCamp.org |  | Création dockerfile (52:45 aussi) | [Go](https://youtu.be/fqMOX6JJhGo?t=2697) |  |
| freeCodeCamp.org |  | Variables d'environnement | [Go](https://youtu.be/fqMOX6JJhGo?t=2542) |  |
| Dockercon | Taking Docker to Production: What You Need to Know and Decide | Bonnes pratiques & anti-patterns | [Go](https://www.youtube.com/watch?v=6jT83lT6TU8) | **Indispensable** |

_^ Focus docker file & docker compose
^ Ubuntu avec dernière version du kernel recommandée, dernière version de docker
^ Reco de technos gratuites ~38:30_

| Source | Titre | Sujet | Lien | Notes |
|-----------|----------------------------------|----------------------------------------------|---------------------------------------------|-------------------|
| Dockercon | Creating Effective Docker Images | BP : Réduire taille images et ^vitesse build | [Go](https://www.youtube.com/watch?v=vlS5EiapiII) | **Indispensable** |

_^ [Image alpine](https://nickjanetakis.com/blog/the-3-biggest-wins-when-using-alpine-as-a-base-docker-image) plutot que ubuntu/debian (selon besoin)
^ Reco nodejs 23:50_

| Source | Titre | Sujet | Lien | Notes |
|------------------|---------------------------------------------------------------------------|------------------------------------------|---------------------------------------------|----------------------------------------|
| kubucation | Drastically reduce the size of your DOCKER images with MULTISTAGE builds | Réduire taille image | [Go](https://www.youtube.com/watch?v=KLOdisHW8rQ) |  |
| Docker | Best practices for building secure Docker images | BP sécuritay | [Go](https://www.youtube.com/watch?v=LmUw2H6JgJo) | **user / utilisateur  pas root** |
| kubucation | Proper DOCKER CACHING: Speed up your build with this optimized Dockerfile | Cache pour package.json dans build image | [Go](https://www.youtube.com/watch?v=oZ9nyCWERYc) |  |
| Cocadmin |  | Améliorer perfs réseaux docker | [Go](https://www.youtube.com/watch?v=Z5y7AkOko-o) | à confirmer, potentiellement dangereux |
| udemy |  | Détails instructions commandes DF | [Go](https://www.udemy.com/course/docker-for-beginners/learn/lecture/14002050#overview) | Plus digeste que la doc offi |
| udemy |  | Utiliser ARG pour stocker les versions | [Go](https://www.udemy.com/course/docker-essentials/learn/lecture/12339826#overview) | Bonne pratique |



## Documentation officielle

Docker est basé sur la méthodologie [12 factor app](https://12factor.net/), je recommande donc sa lecture afin de faciliter la compréhension (et l'optimisation) des images Docker.


### docker build

Je reco de se renseigner sur `docker build` avant d'enchaîner sur les Dockerfile. C'plus accesible.

- [Commande docker build](https://docs.docker.com/engine/reference/commandline/build/#extended-description)
- [Dockerfile doc](https://docs.docker.com/engine/reference/builder/) / Ne pas tout lire, aller chercher quand besoin
- [SO / Why build from git repo](https://stackoverflow.com/questions/46636743/why-would-i-want-to-docker-build-from-a-repo-url)


### How to keep your images small

[Doc officielle](https://docs.docker.com/develop/dev-best-practices/)

- Ne pas repartir de ubuntu, mais essayer de voir si des images officielles de la techno voulue existe
- Préférer alpine à ubuntu si les besoins le permettent
- Utiliser un fichier [.dockerignore](https://docs.docker.com/engine/reference/builder/#dockerignore-file)
	- **Ne pas inclure les dépendances dev**, mais uniquement celles nécessaires a la bonne éxécution de l'application

- **RUN**
	- Regrouper les commandes RUN en utilisant `&&` :

```
RUN apt-get -y update
RUN apt-get install -y python
```

devient

```
RUN apt-get -y update && apt-get install -y python
```
	- `-y` s'assure que les dernières majs seront récupérées (cache busting)
	- Si installation de packages multiples, les [ranger par ordre alphanumérique et un par ligne](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#sort-multi-line-arguments) (simplifie lecture de la liste et majs)
	- Utiliser le multi-ligne pour améliorer la lisibilité ( ` \ `)
	- Rajouter ` && rm -rf /var/lib/apt/lists/*` pour clean

- Si utilisation courante d'images redondantes ou composées, préférer la création (et réutilisation) d'une image de base **à partir des composants communs** ; docker mettra en cache les différents 'morceaux' et tout sera plus optimisé
- *dev* > Base les images de debug et de test (surcouche) sur l'image de prod (plutôt que de baser la prod sur le debug en retirant le debug)
- Bien organiser les tags des builds : *prod, test, stability, etc.*, éviter d'utiliser latest


### Best practices for writing Dockerfiles

[Doc officielle / Ref Dockerfile](https://docs.docker.com/engine/reference/builder/)

- Containers/build doivent être "épémères" : autonomes, et possibilité de détruire/re-créer en un minimum d'étapes.
	- stateless / sans état
	- Ne contient aucune données 'variable', elles doivent êtres stockées ailleurs (volumes/database/service)

[Doc officielle / Optimisation](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

- Faire attention au contexte
	- Exclure ce qui n'est pas nécessaire à l'aide de `.dockerignore`
	- Possibilité de lancer des images sans contexte (si besoin d'aucun fichier avoisinant)
- Une image fait une chose : exemple web app : 3 images :
	- Web app
	- Base de données
	- Cache
- Seulement les instructions `RUN, COPY, ADD` rajoutent des couches (~augmentent la taille du build final)
- La commande `RUN` n'invalide pas le cache, peut être problématique pour `RUN apt-get -y update` ou équivalents
- Possibilité d'utiliser des `LABEL`s afin de rajouter des meta-datas a une image
- Utiliser `COPY` plutôt que `ADD`
	- `ADD` uniquement pour auto-extraire archives `.tar`
- `ENTRYPOINT` : définir la commande par défaut
- Ne pas utiliser `RUN cd..` mais `WORKDIR`


#### Multi stage build

Double création d'image dans un seul fichier dockerfile :

- Première image qui récupère les outils et dépendances nécessaires au build, puis build
- Deuxième image FROM SCRATCH qui copie le projet buildé

- Possibilité de rajouter des outils et du debug sur les images intermédiaires, sans influencer le poids de l'image finale

---

[Doc](https://docs.docker.com/develop/develop-images/multistage-build/)

- Nommer images intermédiaires (v "builder") & récupérer les artéfacts via `COPY --from=`

```
FROM golang:1.7.3 AS builder
...

FROM alpine:latest  
COPY --from=builder /go/src/github.com/alexellis/href-counter/app .
```

- Peut être utilisé pour s'arrêter à un certain stage
	- debug avec les outils nécessaires
	- test avec injection de data


#### Optimisation du cache

- Ordonner les couches : le moins de changement en premier, le plus de changement en dernier ; cela permettra une meilleure utilisation du cache. Reco :
	- Installer les outils pour build
	- Installer les dépendances (SANS dépendances dev)
	- Générer l'application
- Utiliser plusieurs instructions `COPY` en fonction des opérations suivantes, afin de ne [pas faire reproc](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#add-or-copy) des opérations suivantes.


#### Utilisateurs & permissions

- Si pas de besoin **indispensable** de permissions spécifiques , il est recommandé de [créer un utilisateur](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#user) différent de root
- Ne pas changer d'utilisateurs fréquemment
	- Installer ce qu'il faut via root
	- Créer et switcher d'utilisateur une fois


### Navigation

La suite, [docker-compose](/docs/05b-Docker-compose.md), ou retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).































//
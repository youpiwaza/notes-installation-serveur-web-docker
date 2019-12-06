# Docker & Dockerfile propre

Docker, kwaksé un container et création d'images

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

_^ Image alpine plutot que ubuntu/debian (selon besoin)
^ Reco nodejs 23:50_

| Source | Titre | Sujet | Lien | Notes |
|------------------|---------------------------------------------------------------------------|------------------------------------------|---------------------------------------------|----------------------------------------|
| kubucation | Drastically reduce the size of your DOCKER images with MULTISTAGE builds | Réduire taille image | [Go](https://www.youtube.com/watch?v=KLOdisHW8rQ) |  |
| Docker | Best practices for building secure Docker images | BP sécuritay | [Go](https://www.youtube.com/watch?v=LmUw2H6JgJo) | **user / utilisateur  pas root** |
| kubucation | Proper DOCKER CACHING: Speed up your build with this optimized Dockerfile | Cache pour package.json dans build image | [Go](https://www.youtube.com/watch?v=oZ9nyCWERYc) |  |
| Cocadmin |  | Améliorer perfs réseaux docker | [Go](https://www.youtube.com/watch?v=Z5y7AkOko-o) | à confirmer, potentiellement dangereux |


### Navigation

La suite, [docker-compose](/docs/05b-Docker-compose.md), ou retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).
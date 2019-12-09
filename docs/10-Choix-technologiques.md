# Choix technologiques

Parce que pour chaque demande il existe plusieurs technologies pour y répondre, ici on fait et justifie nos choix, avant de les appliquer.



## Orchestration

Docker swarm ou Kubernetes ?

https://vexxhost.com/blog/kubernetes-vs-docker-swarm-containerization-platforms/

dev & preprod > 1 réplique

prod > 2 répliques



## Installation du serveur

Installation de base d'un Ubuntu, pas de véritable distribution linux recommandée pour être l'hôte de Docker.

Utilisation d'Ansible pour faire la configuration de l'hôte

- Installation de terminaux
	- zsh
	- tmux
- Installation de Docker
	- Configuration ?
- Backups ?
	- Intervalle de temps ?
	- Clean après combien de temps ?



## Docker


### Gestion de la persistance des données

- Code source
	- Link en `dev`, quel dossier ?
	- Sans en `preprod` et `prod` ? Build
- Base de données
	- Volumes, quel dossier ?
- Logs
	- Quel dossier ? 
	- CRON de clean



## Déploiement

Jenkins ?

dev/preprod/prod


### Navigation

La suite, [Mise en place sur le serveur](/docs/11-Mise-en-place.md), ou retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).



































//
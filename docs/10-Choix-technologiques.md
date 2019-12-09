# Choix technologiques

Parce que pour chaque demande il existe plusieurs technologies pour y répondre, ici on fait et justifie nos choix, avant de les appliquer.


## Variables d'environnement/globales

todo..

*Prévoir avant les différentes variables possibles, ex: ports, chemins des dossiers, etc.*



## Orchestration

> Installation/Réplication du serveur  
> **Gestion du workflow (dev > preprod > prod)**  
> Gestion des containers  
> Gestion de la scalabilité + No down time (répliques)  

Possibilités : ~~Docker swarm / Kubernetes~~ / Ansible

Choix arrété sur [Ansible dans un premier temps](/docs/07-Avance.md#orchestration), avec son interface graphique [AWX](https://github.com/ansible/awx).

- Pas de répliques ni 'no down time' pendant les déploiements.

Dans l'idéal, plus tard:

- dev, preprod, debug > 1 réplique
- prod > 2 répliques, scale automatique si fort trafic



## Installation du serveur

> Machine hôte du Docker

Possibilités : Ubuntu / ~~Debian / CentOs / Alpine / RanchOS~~

Installation de base d'un Ubuntu, pas de véritable distribution linux recommandée pour être l'hôte de Docker.

Utilisation d'Ansible pour faire la configuration de l'hôte ?

- Installation de terminaux
	- zsh
	- tmux
- Installation de Docker
	- Configuration ?
- Backups ?
	- Intervalle de temps ?
	- Clean après combien de temps ?


### Arborescence / Dossiers

Repomper [tuto grafikart ansible](https://www.youtube.com/watch?v=DwNapBHypE8)



## Load balancer

> Répartition du trafic entrant vers ce qu'il faut

Possibilités : Nginx / ~~Node~~

> Node n'est pas recommandé pour la mise en place de multiples sites (cf. grafikart v)

Nginx, [tuto grafikart](https://www.grafikart.fr/tutoriels/nginx-692) avec MeP + logs + Redirections + Erreurs.




## Docker

> Parce que la containerisation, c'est ~~la vie~~ pas de gestion d'environnement, portable, scalable


### Gestion de la persistance des données

- Code source
	- Link en `dev`, quel dossier ?
	- Sans en `preprod` et `prod` ? Build
- Base de données
	- Volumes, quel dossier ?
- Logs
	- Quel dossier ? 
	- CRON de clean


### Images à utiliser

Vérifier compatibilités avec Kubernetes

- [Nginx](https://hub.docker.com/search?q=nginx&type=image) > Nginx ou Nginx-ingress ? Ou kubernetes direct
	-	INGRESS RECOMMANDE POUR KUBERNETES / https://www.youtube.com/watch?v=SC7lLm6QAb8
- [PHP](https://hub.docker.com/r/bitnami/php-fpm/#Connecting-to-other-containers) ?
- [Node](https://hub.docker.com/_/node)


## Orchestration / Ajout de site

> Création d'utilisateur linux (+ droits) + dossiers (sources, (bdd), logs, etc.) + installation de base

Ansible + role + variables ? [tuto grafikart](https://www.youtube.com/watch?v=DwNapBHypE8)



## Déploiement

> dev > preprod > prod

Possibilités : Ansible /  / Kubernetes ?

Kubernetes peut le faire : [Kubernetes The Easy Way!](https://youtu.be/kOa_llowQ1c?t=863)

Choix plutôt sur Ansible/gulp. Dépend vraiment des technos.

**Environnements à prévoir**

- dev / Développement en cours, tests en ligne
- preprod / Build de l'image, et test client avant mise en prod
- prod / Build, site public
- debug / Possibilité de monter une image ancienne spécifique (rollback)


### CI/CD

> Automatisation du process  
> dev > (ut) > (build) > preprod > prod  

Possibilités : Jenkins / Travis CI

**Plus tard**

Mais [Jenkins](/docs/07-Avance.md#ci-cd).


### Déploiement scalable

> Déployer des conteneurs similaires afin d'éviter les problèmes, et ajouter la possibilité d'optimiser les performances sur différentes machines de manière simplifiée et automatique.

Possibilités : ~Ansible / Kubernetes / Docker swarm ?

**Plus tard**

Kubernetes plus populaire, mais j'ai un meilleur feeling avec le swarm.

Possibilité de gérer les deux via Ansible (exécution des commande via scripts yaml).



### Navigation

La suite, [Mise en place sur le serveur](/docs/11-Mise-en-place.md), ou retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).



































//
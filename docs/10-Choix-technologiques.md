# Choix technologiques

Parce que pour chaque demande il existe plusieurs technologies pour y répondre, ici on fait et justifie nos choix, avant de les appliquer.

[IaC Infrastructure as Code](https://www.udemy.com/course/linux-academy-devops-essentials/learn/lecture/13781156#overview) / DevOps > Versionner la configuration de tout et faire exécuter via automatisation.

- Respecter l'arborescence des containers lors de l'override de la configuration

Pages dédiées : 

- [Architecture](/docs/10a-Architecture.md) / Schémas & évolutions

**Activer buildkit de docker !** & swarmkit



## Variables d'environnement/globales

todo..

docker config & secrets + backups

*Prévoir avant les différentes variables possibles, ex: ports, chemins des dossiers, etc.*



## ~~Orchestration~~ Installation et Automatisation

> Installation/Réplication du serveur  
> **Gestion du workflow (dev > preprod > prod)**  
> Gestion des containers  
> Gestion de la scalabilité + No down time (répliques)  

Possibilités : ~~Docker swarm / Kubernetes~~ / Ansible / ~~Chef~~ (reco négative cocadmin)

Choix arrété sur [Ansible dans un premier temps](/docs/07-Avance.md#orchestration), avec son interface graphique [AWX](https://github.com/ansible/awx).

- Pas de répliques ni 'no down time' pendant les déploiements.

Dans l'idéal, plus tard:

- dev, preprod, debug > 1 réplique
- prod > 2 répliques, scale automatique si fort trafic

Utiliser [tuto grafikart](https://www.grafikart.fr/tutoriels/ansible-753) pour installer/réinstaller le serveur de manière clean et automatique (plutôt que d'avoir de la doc partout) & les tâches courantes

## Orchestration des containers

Possibilités : Docker swarm? / Kubernetes? / Mesos

[Docker swarm (1 manager) vs docker-compose](https://devopstuto-docker.readthedocs.io/en/latest/docker_swarm/articles/2018/01__2018_10_17/01__2018_10_17.html) > docker swarm for production !

https://dockerswarm.rocks/

2 interfaces graphiques avec swarm (monitoring ET management) !

+ recommandé avec traefik


## Installation du serveur

> Machine hôte du Docker

Possibilités : Ubuntu / ~~Debian / CentOs / Alpine / RanchOS~~

Installation de base d'un Ubuntu, pas de véritable distribution linux recommandée pour être l'hôte de Docker.

Utilisation d'Ansible pour faire la configuration de l'hôte ?

- Installation de terminaux
	- zsh
	- tmux
	- [grafikart pimp terminal](https://www.grafikart.fr/tutoriels/pimp-my-shell-750)
- Installation de Docker
	- Mise en place d'Ansible
		- run le build
		- Stocker la configuration dans un projet git (backup)
	- Configuration de Docker via Ansible
		- Logs erreurs en priorité
- Sécurité
	- [Changer port par défaut](https://youtu.be/lXOdDal6qos?t=239)
	- [Retirer connexion par mot de passe](https://youtu.be/lXOdDal6qos?t=324)
		- [Ajouter un utilisateur SSH via clés seulement](https://youtu.be/lXOdDal6qos?t=449) : Remplace le mot de passe. ?
	- Mise en place accès FTP pour utilisateurs existants [ProFTP](https://www.grafikart.fr/tutoriels/proftpd-755)
	  - Annuaire simple des accès en place
		- MeP parefeu (iptables)
		- MeP anti-brute force [fail2ban](https://www.grafikart.fr/tutoriels/fail2ban-698)
- Logs
	- Créer un dossier log contenant les liens symboliques EXPLICITES vers les logs des différentes technos
	- Ajouter un script/la conf qui envoie un email en cas d'erreur côté serveur
- Mails
	- Mise en place serveur de mails (postfix, [mailcow](https://mailcow.email/) ?)
	- Envoi de mail + tester templates [mailinator](https://www.mailinator.com/)
- Backups ?
	- Mise en place de backups automatiques via le CRON (~1 fois / jour, incrémental ?)
	  - [Mise en place Rsync](https://www.youtube.com/watch?v=7Hb32v8e8W0) pour les fichiers
	  - mysqldump > bdd sql
	  - Ajouter un clean des logs (zip après 2 semaines, suppression après 2 ans)
- Monitoring
	- Script analyses performances (ex [config mysql](https://www.grafikart.fr/tutoriels/mysql-690))
	- Bande passante : [iperf3](https://github.com/esnet/iperf)
- Divers
	- Ajouter une page par défaut pour le serveur (ou une redirection), en cas d'accès via l'IP
	- Ajouter des pages personnalisées pour les différentes erreurs serveurs 50X
	

### Arborescence / Dossiers

Repomper [tuto grafikart ansible](https://www.youtube.com/watch?v=DwNapBHypE8)

Pas de soucis de droits (pas de sudo)
- /home/USER
- /var

## Load balancer

> Répartition du trafic entrant vers ce qu'il faut

Possibilités : ~Nginx / ~~Node~~ / **Traefik**

> Node n'est pas recommandé pour la mise en place de multiples sites (cf. grafikart v)

Nginx, [tuto grafikart](https://www.grafikart.fr/tutoriels/nginx-692) avec MeP + logs + Redirections + Erreurs.

[Documentation officielle Nginx](http://nginx.org/en/docs/)

[E-book gratuit officiel](https://www.nginx.com/resources/library/complete-nginx-cookbook/) / Besoin d'inscription


PTET PLUTOT [TRAEFIK](https://containo.us/traefik/)

- Plus récent
- Dédié
- Interface graphique x_x


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

Possibilités : Ansible / Swarm / Kubernetes / [Capistrano](https://github.com/capistrano/capistrano)

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



## Monitoring

- [Udemy devops monitoring tools](https://www.udemy.com/course/linux-academy-devops-essentials/learn/lecture/13781206#overview)
- [Docker swarm rocks](https://dockerswarm.rocks/)



## Migration des sites

- Installer REDIS, et implementer (node et WP) pour gain de perfs
  - Faire un test avec une base WP et faire un diff des perfs
- Mise en place des ~[certificats SSL](https://www.grafikart.fr/tutoriels/apache-ssl-letsencrypt-746)~ cf. [installation avancée](https://www.grafikart.fr/tutoriels/nginx-ssl-letsencrypt-747)
	  - Certifs SSL gratuits [Let's encrypt](https://letsencrypt.org/fr/)
	  - Tests certificats SSL [SSL Labs tests](https://www.ssllabs.com/ssltest/)
- Désactiver erreurs (php, etc.) & phpinfo en prod

### Navigation

La suite, [Mise en place sur le serveur](/docs/11-Mise-en-place.md), ou retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).



































//
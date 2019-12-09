# Questions

Les questions, plus ou moins pertinentes, que je me suis posé.

Ainsi que leurs réponses (ajoutées au fil de l'eau) et les justifications.


**Liste des questions**

- [✓] [Comment gérer plusieurs sites depuis le même serveur ?](#hue) / Reverse proxy
	- [✗] [Mais pour les sites utilisant un serveur NodeJS ? Sont-ils a la suite de Nginx ? Ou ~load balancer](#hue)
	- [✗] [Bref, qui gère la répartition du trafic entrant ?](#hue)
- [✓] [L'orchestration est-elle nécessaire a mon niveau ?](#hue) / Non, mais on va le faire quand même
	- [✗] [Cela peut-il fonctionner avec un seul serveur, un seul hôte ?](#hue)
- [✓] [Dois-je installer Docker directement sur l'hôte, ou passer par Ansible ?](#hue) / Ansible (config auto)
	- [✓] [Pourquoi ne pas utiliser une image ou un build Docker ? Même fait maison](#hue) / Eviter Docker in Docker + sécurité de base
- [✓] [Création d'un container par technologie ? Ou création d'un container par service par site ?](#hue) / Un par service
- [✓] [Comment (bien) gérer les données des conteneurs ? (données persistées)](#hue) / Volumes pour BDD, Link pour sources & logs
- [✗] [tf is a microservice ?](#hue) / ?
- [✓] [Comment maintenir un service permanent, y compris lors de majs/problèmes](#hue) / Orchestration
- [✗] [Sur l'hôte, déploie t-on un seul conteneur Jenkins, ou un par site ?](#hue) / ?
- [✗] [Pour les environnements de preprod & prod, est-il possible de n'avoir d'un build Docker ?](#hue) / ?
	- [✗] [Est-ce que le docker compose est obligatoire ? Jenkins gère t-il tout cela ?](#hue)



## Comment gérer plusieurs sites depuis le même serveur ?

Utiliser Nginx (gestion des requêtes entrantes) avec [reverse proxy](https://github.com/youpiwaza/notes-installation-serveur-web-docker/blob/master/docs/03-Prerequis.md#gestion-de-plusieurs-sites).

Cela permet de rediriger chaque noms de domaine vers même la même IP, mais sur un port différent (ce qui correspondra aux différents containers).


### X Mais pour les sites utilisant un serveur NodeJS ? Sont-ils a la suite de Nginx ? Ou ~load balancer

todo..


### X Bref, qui gère la répartition du trafic entrant ?

todo..



## L'orchestration est-elle nécessaire a mon niveau ?

(Il s'agit de la gestion automatique de multiples containers)

Honnêtement je ne pense pas, mais on va le faire quand même si ça n'est pas trop compliqué.

Cela permettra d'éviter les absences de services (2 répliques par site en prod) et de faire des déploiements invisibles.

Cela permettra également une meilleure migration plus tard, si on doit évoluer.


### X Cela peut-il fonctionner avec un seul serveur, un seul hôte ?

todo.. Je pense que oui, mais à confirmer.



## Dois-je installer Docker directement sur l'hôte, ou passer par Ansible ?

Ansible permet de faire de la configuration automatique, et surtout de la répliquer en cas de problème.

Il sera utilisé pour configurer l'hôte (Ubuntu), et donc installer (et configurer si besoin) Docker.

Tout ce qui sera fait via Ansible sera sauvegardé dans un repo Git.


### Pourquoi ne pas utiliser une image ou un build Docker ? Même fait maison

Pas sûr que cela tourne, vu qu'il faut un hôte pour faire tourner Docker.

Il faudrait un hôte pour faire tourner docker pour monter un container hôte... Docker dans Docker existe mais a priori peu recommandé.

Je préfère également gérer la sécurité dès l'hôte, pas dans une surcouche.



## Création d'un container par technologie ? Ou création d'un container par service par site ?

> Exemple : Est-ce que je ne crée qu'un container mysql qui contiendra l'ensemble des bases de mes sites ? Ou un conteneur mysql par site ?

Un conteneur par service. Si la bdd d'un site tombe ou autre, cela ne doit pas inpacter les autres sites.

Par contre il faudra vérifier que cela peut fonctionner au niveau des performances.



## Comment (bien) gérer les données des conteneurs ? (données persistées)

Les volumes (espace de stockage dans le docker hôte, sur l'hôte `/var/lib/docker/volumes/`) seront utilisés pour les bases de données (container `/var/lib/mysql`), car ils sont plus faciles à utiliser dans les réseaux de containers (donner accès aux données depuis le front). Et cela n'empêche pas les backups.

Les links (Même chose mais dans l'hôte, en dehors du docker) seront utilisés pour les sources des sites de `dev`, car cela permet un genre de HMR.

Links également pour récupérer les logs (apache, autre) depuis les conteneurs et les rapatrier vers l'hôte).



## X tf is a microservice ?

todo.. Ptet un container par truc. Au lieux d'une seule bdd pour tous les sites, et d'une bdd par site, il s'agit d'une bdd par table ?

Comme ça chaque table est indépendante ?



## Comment maintenir un service permanent, y compris lors de majs/problèmes

Grâce à l'orchestration : Utilisation de différents hôtes qui contiennent différents containers (répliqués), ainsi qu'un master qui surveille/répartit.



## X Sur l'hôte, déploie t-on un seul conteneur Jenkins, ou un par site ?

Les deux ne me paraissent pas déconnant, mais dans le but d'isoler je dirais un par site, voir par projet, (voir par dev/preprod/prod !?)..

Besoin d'en savoir plus sur les micro-services et leur implémentation.



## X Pour les environnements de preprod & prod, est-il possible de n'avoir d'un build Docker ?

> Dans la mesure ou les sources ne sont pas censées changer 'en live' mais bien être déployées une fois validées..

Surtout sachan que la bdd peut provenir d'un `volume` dédié..

todo..


### X Est-ce que le docker compose up est obligatoire ? Jenkins gère t-il tout cela ?

> Si mise a jour des sources contenues dans le container php uniquement, et que rien n'a changé dans le container Mysql

todo.. conf jenkins ?



### Navigation

La suite, [Mes exigences](/docs/09-Exigences.md), ou retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).





































//
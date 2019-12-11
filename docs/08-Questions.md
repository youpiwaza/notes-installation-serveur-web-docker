# Questions

Les questions, plus ou moins pertinentes, que je me suis posé.

Ainsi que leurs réponses (ajoutées au fil de l'eau) et les justifications.


**Liste des questions**

- [✓] [Comment gérer plusieurs sites depuis le même serveur ?](#comment-gérer-plusieurs-sites-depuis-le-même-serveur-) / Reverse proxy
	- [✓] [Mais pour les sites utilisant un serveur NodeJS ? Sont-ils a la suite de Nginx ? Ou ~load balancer](#mais-pour-les-sites-utilisant-un-serveur-nodejs--sont-ils-a-la-suite-de-nginx--ou-load-balancer) / Nginx renvoie vers NodeJs
	- [✓] [Bref, qui gère la répartition du trafic entrant ?](#bref-qui-gère-la-répartition-du-trafic-entrant-) / Full Nginx
- [✓] [L'orchestration est-elle nécessaire a mon niveau ?](#lorchestration-est-elle-nécessaire-a-mon-niveau-) / Non, mais on va le faire quand même
	- [✗] [Cela peut-il fonctionner avec un seul serveur, un seul hôte ?](#x-cela-peut-il-fonctionner-avec-un-seul-serveur-un-seul-hôte-)
- [✓] [Dois-je installer Docker directement sur l'hôte, ou passer par Ansible ?](#dois-je-installer-docker-directement-sur-lhôte-ou-passer-par-ansible-) / Ansible (config auto)
	- [✓] [Pourquoi ne pas utiliser une image ou un build Docker ? Même fait maison](#pourquoi-ne-pas-utiliser-une-image-ou-un-build-docker--même-fait-maison) / Eviter Docker in Docker + sécurité de base
- [✓] [Création d'un container par technologie ? Ou création d'un container par service par site ?](#création-dun-container-par-technologie--ou-création-dun-container-par-service-par-site-) / Un par service
- [✓] [Comment (bien) gérer les données des conteneurs ? (données persistées)](#comment-bien-gérer-les-données-des-conteneurs--données-persistées) / Volumes pour BDD, Link pour sources & logs
- [✗] [tf is a microservice ?](#x-tf-is-a-microservice-) / ?
- [✓] [Comment maintenir un service permanent, y compris lors de majs/problèmes](#comment-maintenir-un-service-permanent-y-compris-lors-de-majsproblèmes) / Orchestration
- [✗] [Sur l'hôte, déploie t-on un seul conteneur Jenkins, ou un par site ?](#x-sur-lhôte-déploie-t-on-un-seul-conteneur-jenkins-ou-un-par-site-) / ?
- [✓] [Pour les environnements de preprod & prod, est-il possible de n'avoir d'un build Docker ?](#pour-les-environnements-de-preprod--prod-est-il-possible-de-navoir-dun-build-docker-) / Oui, et il le faut
	- [✗] [Est-ce que le docker compose est obligatoire ? Jenkins gère t-il tout cela ?](#x-est-ce-que-le-docker-compose-up-est-obligatoire--jenkins-gère-t-il-tout-cela-)
- [✗] [Peut-on avoir des images/builds Docker avec uniquement du code source ? Est-ce utile ?](#hey) / ?
- [✗] [!! Création d'image (docker-compose), faut-il intégrer Nginx à chaque site ?](#hey) / ?
- [✗] [Dans l'architecture d'un seul site, y a-t-il un interêt à avoir le dev (ex : dev.client1.com) (ainsi que ses dépendances) en ligne ?](#hey) / ?



## Comment gérer plusieurs sites depuis le même serveur ?

Utiliser Nginx (gestion des requêtes entrantes) avec [reverse proxy](https://github.com/youpiwaza/notes-installation-serveur-web-docker/blob/master/docs/03-Prerequis.md#gestion-de-plusieurs-sites).

Cela permet de rediriger chaque noms de domaine vers même la même IP, mais sur un port différent (ce qui correspondra aux différents containers).


### Mais pour les sites utilisant un serveur NodeJS ? Sont-ils a la suite de Nginx ? Ou ~load balancer

Nginx sert de load balancer, cf. [Load Balancing with NGINX](https://www.youtube.com/watch?v=2X4ZO5tO7Co).


### Bref, qui gère la répartition du trafic entrant ?

Nginx..



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



## Pour les environnements de preprod & prod, est-il possible de n'avoir q'un build Docker ?

> Dans la mesure ou les sources ne sont pas censées changer 'en live' mais bien être déployées une fois validées..

Surtout sachan que la bdd peut provenir d'un `volume` dédié..

Oui, et c'est même le but. cf. [Kubernetes The Easy Way!](https://youtu.be/kOa_llowQ1c?t=863).

Cela ne sert à rien de tester l'image en preprod si ce n'est pas la même qui est poussée en prod..


### X Est-ce que le docker compose up est obligatoire ? Jenkins gère t-il tout cela ?

> Si mise a jour des sources contenues dans le container php uniquement, et que rien n'a changé dans le container Mysql

todo.. conf jenkins ?



## PHP est-il dépendant de Nginx ? (un seul container pour les deux)

Non. Nginx peut être lancé dans un conteneur, et PHP dans un autre.

Par contre, il faut qu'ils soient en réseaux afin de pouvoir être utilisés.

cf. [Image dockerhub PHP-FPM](https://hub.docker.com/r/bitnami/php-fpm/#Connecting-to-other-containers), il y a un exemple de conf composée `Ctrl + F` "Connecting-to-other-containers".



## X Peut-on avoir des images/builds Docker avec uniquement du code source ? Est-ce utile ?

> Injection dans d'autres build Docker (php, etc.) ou dans les dossiers linkés ?

todo...



## X!! Création d'image (docker-compose), faut-il intégrer Nginx à chaque site ?

> Pour des raisons de portabilité / déplacement de site

[Katacoda création de site web statique](https://www.katacoda.com/courses/docker/create-nginx-static-web-server)

C'est tellement simple une fois en place, il suffit de lancer l'image...

Du coup un Nginx proxy, et un Nginx (dans docker-compose) par site afin que chaque site gère sa propre configuration.

Ca parait plus logique...

- ~~[SO / Docker nginx multiple apps on one host](https://stackoverflow.com/questions/49489482/docker-nginx-multiple-apps-on-one-host) / 1 Nginx pour 2 sites~~
- [SO / NGINX and multiple docker-compose](https://stackoverflow.com/questions/48076605/nginx-and-multiple-docker-compose) / **Créer un réseau pour le proxy ouvert vers l'extérieur, et un réseau par (docker-compose) site fermé à l'extérieur hormis port 80/voulu**
- ~~[SO / Is it possible to run multiple nginx docker containers on the same host?](https://stackoverflow.com/questions/47011323/is-it-possible-to-run-multiple-nginx-docker-containers-on-the-same-host) / A priori pas possible mais je pense que cela dépend si Nginx peut écouter sur d'autres ports..~~

Le but serait d'avoir un proxy, qui redirige vers des docker-compose indépendants (chacun un site) disposant de leur propre serveur.

Ce qui parait vachement plus isolé et portable, que d'avoir à déclencher une config spécifique via Ansible pour l'installation d'un site.

_A noter que au pire on peut créer une composition avec ansible qui déploie uniquement la config voulue (utilisation des rôles/cookbook) pour le site.. mais du coup 1 ansible par site >.>_

- ~~[SO / How to start nginx via different port(other than 80)](https://stackoverflow.com/a/12800469/12026487)~~
	- ~~[Doc nginx](https://nginx.org/en/docs/http/server_names.html) / C'est directement dans la conf en fait..~~
	- ~~**A noter qu'il faudra passer le port d'écoute en variable d'environnement**.. vu que si le site est seul c'est 80, mais dans notre cas il faudra un port par site..~~

**Non, c'est le proxy qui se charge d'envoyer le flux vers le bon container. C'est transparent pour l'intérieur du conteneur.**

Réponse : De préférence oui, si c'est possible.



## X Dans l'architecture d'un seul site, y a-t-il un interêt à avoir le dev (ex : dev.client1.com) (ainsi que ses dépendances) en ligne ?

> Le développement peut être fait en local (compose + git), et on ne met en ligne que les builds

Cela permettrait de simplifier grandement l'architecture en ligne (pas de conteneurs dédiés aux technos nécessaires) par site.

Retrait de 

- Jenkins dédié
- ~PHP / SQL (ou autre)

Et ce qui permettrait d'avoir une base commune à l'ensemble des sites (~ Ansible + NDD + Nginx + image preprod + image prod)

Attention ! Il faudra également gérer les `volumes` afin de pouvoir gérer les données utilisateurs (BDD & fichiers).



### Navigation

La suite, [Mes exigences](/docs/09-Exigences.md), ou retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).





































//
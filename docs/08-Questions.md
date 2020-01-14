# Questions

Les questions, plus ou moins pertinentes, que je me suis posé.

Ainsi que leurs réponses (ajoutées au fil de l'eau) et les justifications.


**Liste des questions**

- [Questions](#questions)
	- [Comment gérer plusieurs sites depuis le même serveur ?](#comment-g%c3%a9rer-plusieurs-sites-depuis-le-m%c3%aame-serveur)
		- [Mais pour les sites utilisant un serveur NodeJS ? Sont-ils a la suite de Nginx ? Ou ~load balancer](#mais-pour-les-sites-utilisant-un-serveur-nodejs--sont-ils-a-la-suite-de-nginx--ou-load-balancer)
		- [Bref, qui gère la répartition du trafic entrant ?](#bref-qui-g%c3%a8re-la-r%c3%a9partition-du-trafic-entrant)
	- [L'orchestration est-elle nécessaire a mon niveau ?](#lorchestration-est-elle-n%c3%a9cessaire-a-mon-niveau)
		- [Cela peut-il fonctionner avec un seul serveur, un seul hôte ?](#cela-peut-il-fonctionner-avec-un-seul-serveur-un-seul-h%c3%b4te)
	- [Dois-je installer Docker directement sur l'hôte, ou passer par Ansible ?](#dois-je-installer-docker-directement-sur-lh%c3%b4te-ou-passer-par-ansible)
		- [Pourquoi ne pas utiliser une image ou un build Docker ? Même fait maison](#pourquoi-ne-pas-utiliser-une-image-ou-un-build-docker--m%c3%aame-fait-maison)
	- [Création d'un container par technologie ? Ou création d'un container par service par site ?](#cr%c3%a9ation-dun-container-par-technologie--ou-cr%c3%a9ation-dun-container-par-service-par-site)
	- [Comment (bien) gérer les données des conteneurs ? (données persistées)](#comment-bien-g%c3%a9rer-les-donn%c3%a9es-des-conteneurs--donn%c3%a9es-persist%c3%a9es)
	- [tf is a microservice ?](#tf-is-a-microservice)
	- [Comment maintenir un service permanent, y compris lors de majs/problèmes](#comment-maintenir-un-service-permanent-y-compris-lors-de-majsprobl%c3%a8mes)
	- [X Sur l'hôte, déploie t-on un seul conteneur Jenkins, ou un par site ?](#x-sur-lh%c3%b4te-d%c3%a9ploie-t-on-un-seul-conteneur-jenkins-ou-un-par-site)
	- [Pour les environnements de preprod & prod, est-il possible de n'avoir qu'un build Docker ?](#pour-les-environnements-de-preprod--prod-est-il-possible-de-navoir-quun-build-docker)
		- [Est-ce que le docker compose up est obligatoire ? Jenkins gère t-il tout cela ?](#est-ce-que-le-docker-compose-up-est-obligatoire--jenkins-g%c3%a8re-t-il-tout-cela)
	- [PHP est-il dépendant de Nginx ? (un seul container pour les deux)](#php-est-il-d%c3%a9pendant-de-nginx--un-seul-container-pour-les-deux)
	- [Peut-on avoir des images/builds Docker avec uniquement du code source ? Est-ce utile ?](#peut-on-avoir-des-imagesbuilds-docker-avec-uniquement-du-code-source--est-ce-utile)
	- [Création d'image (docker-compose), faut-il intégrer Nginx à chaque site ?](#cr%c3%a9ation-dimage-docker-compose-faut-il-int%c3%a9grer-nginx-%c3%a0-chaque-site)
	- [Dans l'architecture d'un seul site, y a-t-il un interêt à avoir le dev (ex : dev.client1.com) (ainsi que ses dépendances) en ligne ?](#dans-larchitecture-dun-seul-site-y-a-t-il-un-inter%c3%aat-%c3%a0-avoir-le-dev-ex--devclient1com-ainsi-que-ses-d%c3%a9pendances-en-ligne)
		- [Navigation](#navigation)



## Comment gérer plusieurs sites depuis le même serveur ?

Utiliser Nginx (gestion des requêtes entrantes) avec [reverse proxy](https://github.com/youpiwaza/notes-installation-serveur-web-docker/blob/master/docs/03-Prerequis.md#gestion-de-plusieurs-sites).

Cela permet de rediriger chaque noms de domaine vers même la même IP, mais sur un port différent (ce qui correspondra aux différents containers).


### Mais pour les sites utilisant un serveur NodeJS ? Sont-ils a la suite de Nginx ? Ou ~load balancer

Nginx sert de load balancer, cf. [Load Balancing with NGINX](https://www.youtube.com/watch?v=2X4ZO5tO7Co).

Traefik prend tout le trafic entrant (les urls que requêtent les visiteurs), et le redirige vers les conteneurs appropriés.

Les conteneurs (ou ensembles de conteneurs, via compose/services) font leur popote ; indépendamment les uns des autres, chacun à son propre serveur web ;

La réponse est renvoyée à traefik qui la transmet.


### Bref, qui gère la répartition du trafic entrant ?

Nginx



## L'orchestration est-elle nécessaire a mon niveau ?

(Il s'agit de la gestion automatique de multiples containers)

Honnêtement je ne pense pas, mais on va le faire quand même si ça n'est pas trop compliqué.

Cela permettra d'éviter les absences de services (2 répliques par site en prod) et de faire des déploiements invisibles.

Cela permettra également une meilleure migration plus tard, si on doit évoluer.


### Cela peut-il fonctionner avec un seul serveur, un seul hôte ?

~~todo.. Je pense que oui, mais à confirmer.~~

[Docker swarm (1 manager) vs docker-compose](https://devopstuto-docker.readthedocs.io/en/latest/docker_swarm/articles/2018/01__2018_10_17/01__2018_10_17.html) > docker swarm recommandé, meilleure scalabilité pour le futur (plus managers dispos, cf. docker swarm rocks)

Possibilité de monter des VMS afin d'obtenir 1 manager & 2 workers. Même si on perds l'avantage si la seule machine qui héberge crash.

Possibilité également d'avoir un unique bi-classé manager/worker.



## Dois-je installer Docker directement sur l'hôte, ou passer par Ansible ?

Ansible permet de faire de la configuration automatique, et surtout de la répliquer en cas de problème.

Il sera utilisé pour configurer l'hôte (Ubuntu), et donc installer (et configurer si besoin) Docker.

Tout ce qui sera fait via Ansible (recettes "cookbooks") sera sauvegardé dans un repo Git.

Cela permettra une réinstallation rapide au cas ou le serveur tombe, et de maintenir la configuration en cas de mise à jour.

A noter que cette installation du serveur concernera docker, swarm, les utilisateurs ainsi que la sécurité *mais pas les sites* !

Ces derniers seront des builds d'images, stockés sur dockerhub (et donc indépendants). Swarm servira à les instancier en tant que services.



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



## tf is a microservice ?

~~todo.. Ptet un container par truc. Au lieux d'une seule bdd pour tous les sites, et d'une bdd par site, il s'agit d'une bdd par table ?

Comme ça chaque table est indépendante ?

Edit : Un conteneur avec une image qui contient la réponse à une demande.



## Comment maintenir un service permanent, y compris lors de majs/problèmes

Grâce à l'orchestration : Utilisation de différents hôtes qui contiennent différents containers (répliqués), ainsi qu'un master qui surveille/répartit.



## X Sur l'hôte, déploie t-on un seul conteneur Jenkins, ou un par site ?

Les deux ne me paraissent pas déconnant, mais dans le but d'isoler je dirais un par site, voir par projet, (voir par dev/preprod/prod !?)..

Besoin d'en savoir plus sur les micro-services et leur implémentation.



## Pour les environnements de preprod & prod, est-il possible de n'avoir qu'un build Docker ?

> Dans la mesure ou les sources ne sont pas censées changer 'en live' mais bien être déployées une fois validées..

Surtout sachan que la bdd peut provenir d'un `volume` dédié..

Oui, et c'est même le but. cf. [Kubernetes The Easy Way!](https://youtu.be/kOa_llowQ1c?t=863).

Cela ne sert à rien de tester l'image en preprod si ce n'est pas la même qui est poussée en prod..


### Est-ce que le docker compose up est obligatoire ? Jenkins gère t-il tout cela ?

Swarm sera utilisé pour la prod, et non compose (même si cela reste possible)

Jenkins permet d'automatiser les mises à jour (écoute d'un nouveau commit sur github > lance la création d'un nouveau build > lance le conteneur)

---

> Si mise a jour des sources contenues dans le container php uniquement, et que rien n'a changé dans le container Mysql

Qu'il s'agisse de docker-compose ou de l'instanciation d'un service (montage de conteneurs via swarm), le fait de les relancer les met à jour.

Lors du dev, nous travaillons sur des images, qui sont buildées, et piochent dans les volumes (les données, à part des conteneurs, mais toujours dans l'environnement docker)

La production quand à elle gère des conteneurs : l'instance d'un build.

Que cela soit à la main, ou via un manager (automatique (jenkins ou autre) ou non),

	- Les seuls conteneurs affectés sont seulement ceux dont les builds ont changés
	- (Par service,) un nouveau conteneur est lancé avec le nouveau build et le trafic est redirigé dessus.
    	- L'ancien conteneur est supprimé une fois le trafic en cours dessus est terminé.



## PHP est-il dépendant de Nginx ? (un seul container pour les deux)

Non. Nginx peut être lancé dans un conteneur, et PHP dans un autre.

Par contre, il faut qu'ils soient en réseau afin de pouvoir être utilisés.

cf. [Image dockerhub PHP-FPM](https://hub.docker.com/r/bitnami/php-fpm/#Connecting-to-other-containers), il y a un exemple de conf composée `Ctrl + F` "Connecting-to-other-containers".



## Peut-on avoir des images/builds Docker avec uniquement du code source ? Est-ce utile ?

Oui, grâce à la création d'images depuis "FROM SCRATCH".

Est-ce utile ? Non, il reste recommandé de garder les sources indépendantes.

Elles sont ensuites injectées dans les conteneurs concernés :

- Soit grâce aux volumes
- Soit via la création d'une nouvelle image (Base + modifications)

Exemple : Nginx avec remplacement du contenu dossier source `/usr/share/nginx/html`.

> Injection dans d'autres build Docker (php, etc.) ou dans les ~~dossiers linkés~~ volumes ?

D'après la majeure partie des exemples que j'ai pu voir, l'utilisation des volumes est préférable :

- "bind" pour la configuration, ainsi que pour le développement (la modification d'un fichier sur l'hôte (GENRE TON BUREAU) entraîne la modification dans le conteneur)
- "volume" pour la prod (ça ne bougera pas)

Il est toutefois possible de créer une nouvelle image contenant les sources, voir une image composée :

- Une image est récupérée et éxécute un script sur les sources, par exemple minification du css/js
- Les sources "compilées" sont injectées dans l'image d'un serveur web (ex: Nginx).



## Création d'image (docker-compose), faut-il intégrer Nginx à chaque site ?

Pwah pwah pwah l'ancienne réponse est longue v.

Réponse courte : oui. Chaque site dispose de son propre serveur web (Nginx ou autre).

En dev local, ça se lance tout seul.

En prod, ça lance sur un port spécifique, et Traefik fait les routes (ex: http://client1.fr renverra le contenu de  IP_CONTENEUR:8069)

> > Pour des raisons de portabilité / déplacement de site
> 
> [Katacoda création de site web statique](https://www.katacoda.com/courses/docker/create-nginx-static-web-server)
> 
> C'est tellement simple une fois en place, il suffit de lancer l'image...
> 
> Du coup un Nginx proxy, et un Nginx (dans docker-compose) par site afin que chaque site gère sa propre configuration.
> 
> Ca parait plus logique...
> 
> - ~~[SO / Docker nginx multiple apps on one host](https://stackoverflow.com/questions/49489482/docker-nginx-multiple-apps-on-one-host) / 1 Nginx pour 2 sites~~
> - [SO / NGINX and multiple docker-compose](https://stackoverflow.com/questions/48076605/nginx-and-multiple-docker-compose) / **Créer un réseau pour le proxy ouvert vers > l'extérieur, et un réseau par (docker-compose) site fermé à l'extérieur hormis port 80/voulu**
> - ~~[SO / Is it possible to run multiple nginx docker containers on the same host?](https://stackoverflow.com/questions/47011323/> is-it-possible-to-run-multiple-nginx-docker-containers-on-the-same-host) / A priori pas possible mais je pense que cela dépend si Nginx peut écouter sur d'autres ports..~~
> 
> Le but serait d'avoir un proxy, qui redirige vers des docker-compose indépendants (chacun un site) disposant de leur propre serveur.
> 
> Ce qui parait vachement plus isolé et portable, que d'avoir à déclencher une config spécifique via Ansible pour l'installation d'un site.
> 
> _A noter que au pire on peut créer une composition avec ansible qui déploie uniquement la config voulue (utilisation des rôles/cookbook) pour le site.. mais du coup 1 ansible > par site >.>_
> 
> - ~~[SO / How to start nginx via different port(other than 80)](https://stackoverflow.com/a/12800469/12026487)~~
> 	- ~~[Doc nginx](https://nginx.org/en/docs/http/server_names.html) / C'est directement dans la conf en fait..~~
> 	- ~~**A noter qu'il faudra passer le port d'écoute en variable d'environnement**.. vu que si le site est seul c'est 80, mais dans notre cas il faudra un port par site..~~
> 
> **Non, c'est le proxy qui se charge d'envoyer le flux vers le bon container. C'est transparent pour l'intérieur du conteneur.**
> 
> Réponse : De préférence oui, si c'est possible.



## Dans l'architecture d'un seul site, y a-t-il un interêt à avoir le dev (ex : dev.client1.com) (ainsi que ses dépendances) en ligne ?

Réponse courte : Non, aucun.

- Pour les devs : transmission de l'image (et des configs/volumes/secrets)
- Pour le client : Attente de la mise en preprod
  - Voir des preprods, création à la volée de sous domaine par tag ?

> > Le développement peut être fait en local (compose + git), et on ne met en ligne que les builds
> 
> Cela permettrait de simplifier grandement l'architecture en ligne (pas de conteneurs dédiés aux technos nécessaires) par site.
> 
> Retrait de 
> 
> - Jenkins dédié
> - ~PHP / SQL (ou autre)
> 
> Et ce qui permettrait d'avoir une base commune à l'ensemble des sites (~ Ansible + NDD + Nginx + image preprod + image prod)
> 
> Attention ! Il faudra également gérer les `volumes` afin de pouvoir gérer les données utilisateurs (BDD & fichiers).



### Navigation

La suite, [Mes exigences](/docs/09-Exigences.md), ou retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).





































//
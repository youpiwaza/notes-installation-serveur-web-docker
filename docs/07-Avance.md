# Avancé

Les notions un peu plus avancées, qui vont surement se choper leur propre dossier chacune..

- Orchestration
- Microservices
- CI/CD



## Orchestration

> Installation/Réplication du serveur  
> Gestion des containers  
> Gestion de la scalabilité + No down time (répliques)  
> **Gestion du workflow (dev > preprod > prod)**  

Possibilités : Docker swarm / ~~Kubernetes~~ / Ansible ?


### Ansible

Très accessible, très bons tutos.


[Tuto grafilart Ansible](https://www.youtube.com/watch?v=DwNapBHypE8)

- Installation de modules autos (apt get, etc.)
- Création d'utilisateurs & de dossiers
- Modification de fichiers de conf (édition de lignes en regexp)
- Clonage automatique de repo github

[Doc offi Ansible](https://www.ansible.com/integrations/containers/docker)

- Possibilité de créer les containers via Ansible
	- et gestion de la machine hôte
- Interface graphique ~~[Ansible tower](https://www.ansible.com/products/tower)~~ [Version open source : AWS](https://github.com/ansible/awx)
	- ~~Démo gratuite ? Prix non communiqués~~
		- AWX > [doc tower](https://docs.ansible.com/ansible-tower/index.html)
	- Notifs slack
	- Gestion via API
	- Historique jobs
	- Agenda + ~CRONS


### Kubernetes

Pas assez didactique, ca manque de schéma et de commande simples..

-	[kubernetes](https://kubernetes.io/fr/)
	-	[tuto officiel](https://kubernetes.io/fr/docs/tutorials/kubernetes-basics/) / in browser, nice
	- Déploiement de conteneur dans un cluster
	- Scale du déploiement
	- Workflow (maj conteneur)
	- Débugger
	- Retours
		- C'est lent a boot Kubernetes dans leur demo putaing
		- pas vraiment didactique..


### Docker swarm

Pas pu tester, tuto KO sur windows..

[Gros recap 1 page de swarm](https://www.aquasec.com/wiki/display/containers/Docker+Swarm+101)

A voir, il existe des [configs Ansible](https://blog.ruanbekker.com/blog/2018/06/14/deploy-docker-swarm-using-ansible/) pour déployer le swarm..

- [Tuto udemy](https://www.udemy.com/course/docker-essentials/learn/lecture/12366056#overview) très complet

-	[Docker swarm](https://docs.docker.com/engine/swarm/)
	- [Concepts clés](https://docs.docker.com/engine/swarm/key-concepts/)
		- Un node = 1 docker. Possibilité de plusieurs Nodes sur une seule machine (même si reco machines !=, cloud)
		- Nodes chefs & péons > Managers & workers. Les managers envoient des tasks aux workers
		-	Service : task function (can be called, reused) > Spécifie quel worker & quelle commande y exécuter
		- Le manager utilise INGRESS load balancing et se charge de rendre le service dispo a l'exterieur (il assignera la tâche au worker dispo)
	- [Tutoriel swarm](https://docs.docker.com/engine/swarm/swarm-tutorial/)
		- Comprend
			- initializing a cluster of Docker Engines in swarm mode
			- adding nodes to the swarm
			- deploying application services to the swarm
			- managing the swarm once you have everything running
		- Tuto KO sur Docker desktop windows, les [pré-requis](https://docs.docker.com/get-started/part4/#prerequisites) passent pas, la réplique reste à 0/1

- [Gestion du réseau](https://docs.docker.com/network/overlay/)



### Comparatifs

[kubernetes vs docker swarm](https://vexxhost.com/blog/kubernetes-vs-docker-swarm-containerization-platforms/) / ~pareil

[kubernetes vs ansible](https://stackshare.io/stackups/ansible-vs-kubernetes) / Kube ~^

	- Ansible plus simple, plus rapide a config, et peut tout faire (app deployment, configuration management, workflow orchestration) et tuto grafikart
	- Kube dédié pour gestion serveur multiples, dans le cloud & Dcontainers
	- Kube plus utilisé que Ansible

[ansible vs kubernetes](https://www.simplilearn.com/ansible-vs-kubernetes-article) / Pas le même taf

	- Kube plus pour gestion de multiples serveurs
	- Kube monitoring & storage orchestration
	- Ansible a pas de gestion d'état (state) : lance en séquence jusqu'a fin ou erreur
	- Kube plus difficile à maitriser
	- **In other words, Ansible deploys changes to hosts, while Kubernetes manages containers and keeps them working properly.**


### Choix

Pour la mise en place du serveur, utilisation de Ansible pour la configuration de la machine hôte, et création des tâches usuelles.

Je verrai plus tard pour les répliques et tout le bousin, quand j'aurai plus d'expérience.


### Notes

Possibilité d'utiliser [Docker machine](https://docs.docker.com/machine/overview/) pour installer des dockers sur des VHosts > swarm sur une seule machine ?

#### Proxies pour swarms

-	[Docker flow proxy](https://proxy.dockerflow.com/) / Reconfigure proxy every time a new service is deployed, or when a service is scaled
	- [Ca parle de swarm](https://www.youtube.com/watch?v=oP0_H_UkkGA) / Gestion des IP entre clusters, y compris externes ?
- [Traefik](https://containo.us/traefik/) / The Cloud Native Edge Router
	- [Site offi](https://containo.us/traefik/) / Permet de définir des proxy a la volée : **Mapper des urls à des conteneurs (IP:PORTS)**
	- [Vidéo Docker](https://www.youtube.com/watch?v=RP40Iv_0yvA) / Lien ~routeur entre "l'extérieur" et les services sur le service



## Microservices

Tout découper : une tâche = une fonction (~= un conteneur).

[La vidéo avec l'exemple qui va bien](https://www.youtube.com/watch?v=ucHwp1jUS2w).

Enormément d'API REST (via URL). Trop de trucs à dire.

**Pas du tout utile pour la mise en place du serveur**, mais possibilité plus tard grâce à Docker.

-	[microservice](https://smartbear.com/solutions/microservices/)
	- Grosse séparation de l'ensemble des services, possibilité de maj un service sans toucher aux autres
	- [Tutoriel redhat](https://www.redhat.com/fr/topics/microservices)
	- Gros besoin d'APIs, cf. [swagger](https://swagger.io/tools/swaggerhub/)



## CI/CD

*Continuous Integration / Continuous Développement*

Lors de commits/push, exécution automatique de tests unitaires. Si tout est good, passage en pré-prod.

- [Introduction CI/CD](https://www.youtube.com/watch?v=g0qSsex0Reg)
- [Article plus poussé](https://djangostars.com/blog/continuous-integration-circleci-vs-travisci-vs-jenkins/)

Possibilités : ~~Jenkins / Travis CI~~ / [Docker hub](https://docs.docker.com/docker-hub/builds/) ?

Pas mis en place dans un premier temps.

A voir si implémentation rapide via une image Docker.


### Jenkins

L'une des référence.

[Site officiel](https://jenkins.io/).

- [Tutos officiels](https://jenkins.io/doc/pipeline/tour/getting-started/) // pas faits
- [Image Docker](https://hub.docker.com/r/jenkins/jenkins/)


### Travis CI

Assez connu également.

[travis ci](https://travis-ci.org/)

- Outil de déploiement + déploiement automatiques (UT) + interface graphique ?
	- deploy to GitHub pages
	- send notifications
	- != stages
	
- [Tutoriel](https://docs.travis-ci.com/user/tutorial/)
	- Assez pourri (compile du ruby.. sans code ruby, je comprend pas sur quoi il fait les trucs) mais fonctionne
	- Connexion directe avec github
	- Interface en ligne sur leur site
	- Peut [s'interfacer avec Docker](https://docs.travis-ci.com/user/docker/)


### Ansible ?

Yeah non. Ansible peut être appelé par des softs de CI/CD.

Par exemple, si Jenkins fait passer tous les tests à la release, il peut appeler un script Ansible pour passer en prod.

- [Doc officielle](https://www.ansible.com/use-cases/continuous-delivery)
- [Blog offi, exemple](https://www.redhat.com/en/blog/integrating-ansible-jenkins-cicd-process)


### Comparatifs

- [Stackoverflow](https://stackoverflow.com/questions/32422264/jenkins-vs-travis-ci-which-one-would-you-use-for-a-open-source-project)
	- Jenkins est gratuit et on peut l'héberger, Travis ci en ligne
	-	Travis > Plus facile d'avoir différents tests par branches (config dans projet, fichier .yaml)
	- Travis recommandé pour petits projets, mais généralement Jenkins plus recommandé pour ensemble de projets (un seul setup et/ou possibilité 1 par projet)
- [Autre](https://www.guru99.com/jenkins-vs-travis.html)
	- **/!\ Travis CI gratuit pour les projets non commerciaux uniquement**
	- Jenkins favorisé


### Choix

Jenkins



## Websockets et serveur stream

J'avais noté que cela pouvait être utile lors de la configuration de Nginx. Du coup on jette un oeil.

[Définition mdn](https://developer.mozilla.org/fr/docs/Web/API/WebSockets_API) / ~API de promesses  entre client et serveur

[Vidéo intro websockets](https://www.youtube.com/watch?v=vQjiN8Qgs3c) / Un peu plus graphique.

Du coup, pour simplifier, il s'agit d'un genre de communication en temps réel entre un visiteur et le serveur.

Cela permet de faire de multiples allers-retours, mais sans recharger le navigateur, ce qui ressemble un peu à de l'AJAX.

Pour la culture générale et mieux apréhender la suite, je recommande de lire le [design pattern observer](https://refactoring.guru/design-patterns/observer), sur l'excellent site refactoring guru.

---

Du coup, le rapport avec Nginx vient de ce [tutoriel Grafikart](https://www.grafikart.fr/tutoriels/nodejs-nginx-960).

Au final, cela apprend à configurer Nginx pour héberger des websockets [doc](http://nginx.org/en/docs/http/ngx_http_upstream_module.html), ex : discussion chat en ligne, donc pas pertinent pour le moment.


### PM2

À noter toutefois, la recommandation de [PM2](https://pm2.keymetrics.io/), qui permet la gestion de sripts node en tâche de fond (daemon) et monitoring, avec possibilité d'interface graphique dans le terminal.

Possibilité également de scale les scripts (ex: 4 instances de serveur)



## Divers

Différentes technos remontées lors de la veille.


### Rex-ray

[Rex-ray](https://rexray.readthedocs.io/en/stable/)

Permet de gérer la gestion des espaces de stockages des conteneurs (et swarms).

Mais cette fonctionnalité existe déjà via Docker ; du coup je ne vais pas pousser pour le moment..


### Vessel

[Vessel](https://vessel.shippingdocker.com/)

Environnement de dev/workflow pour travailler avec Docker et Laravel. Pas nécessaire pour le moment.


### Navigation

La suite, [Mes questions](/docs/08-Questions.md), ou retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).
































//
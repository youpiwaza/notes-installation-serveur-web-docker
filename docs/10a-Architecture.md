# Architecture

Des petits schémas, afin de s'assurer que la logique est bonne et simple..

## Version actuelle

> Qui évoluera au fil du temps

todo..



## Ebauche v1 / 04/12/19

Un Nginx qui sert de proxy ET de serveur. Les sites disposent de leur compositions de conteneurs pour certaines technologies.

Configuration via Ansible, déploiement via Jenkins.

Les sources (non images/technos) devront provenir de github, les bases de données en backup sur l'hôte.

![Architecture serveur](/docs/images/191204-archi-v1-serveur.jpg)

---

Pour les sites, chaque environnement (dev/preprod/prod) dispose de son docker compose.

https://docs.docker.com/develop/dev-best-practices/#differences-in-development-and-production-environments

Jenkins s'occupe des déploiements en écoutant (webhooks) github.

![Architecture site](/docs/images/191204-archi-v1-site.jpg)


### Problèmes

- Le déplacement d'un site reste problématique (données github/volumes docker)
- La configuration du serveur (de chaque site) se fait au niveau du Nginx de l'hôte, les sites ne sont donc pas isolés
- Les variations entre les différents environnements semblent trop éloignés, et propices aux erreurs/diff.



## Ebauche v2 / 11/12/19

En entrée du serveur, mise en place d'un proxy dédié ; Remplacement de Nginx par Traefik (dédié au proxy, plus simple, interface graphique) 

Ajout de monitoring

Sécurité

- Différents réseaux Docker :
	- Proxy > Un réseau vers l'extérieur
	- Hôte un réseau interne (configuration, monitoring)
	- Hôte un réseau interne (proxy > sites)
	- Site, un réseau par container
- Utilisation des volumes, et aucun link (respect de l'isolation)

[Déclic](https://www.katacoda.com/courses/docker/create-nginx-static-web-server) > Chaque site doit être isolé et indépendant, possibilité de le déplacer/lancer en un clic.

- Chaque site/sous-domaine (preprod/prod) sera un build, et dispose de son propre serveur (Nginx, Node, Wtv), (ainsi que Ansible & Jenkins ?)

Vu au [Paris Open Source summit](https://www.opensourcesummit.paris/), possiblité d'héberger ses DNS (Open DNS).

- Process Ansible d'ajout de redirection DNS

Différences d'environnemts :

- La preprod doit être un build fixe. Si elle est validée, on peut la passer en prod (copie exacte)

![Architecture serveur](/docs/images/191211-archi-v2-serveur.jpg)

---

![Architecture site](/docs/images/191211-archi-v2-site.jpg)


### Problèmes

- Y a-t-il un intérêt à avoir le dev en ligne ? Avant cela servait à s'assurer qu'il n'y avait pas de différence entre le local et en ligne, mais Docker élimine ce problème..
	- Cela simpliferai énormément l'architecture
- Réseaux docker encore un peu brouillons
- Gestion des données utilisateurs (BDD, fichiers) encore un peu floue.
- Ansible & Jenkins sont-ils vraiment nécessaires pour chaque build de site ?
	- S'il s'agit d'un build fini, autant tout faire dans l'image Docker, sans configuration après..
	- Besoin de creuser la différence entre image et build..



## v3 / ?

Todo..



### Navigation

Retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).



































//
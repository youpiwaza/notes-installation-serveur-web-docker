# Docker volume & Persistance des données

Attribuer un espace de stockage pour les données variables des conteneurs (utilisateur ou base de données, par exemple).

Permet également de linker les données d'un projet, concrètement se créer un espace de dev : on modifie sur son bureau, les modifs sont répercutées dans le conteneur.

| Source | Titre | Sujet | Lien | Notes |
|---------------------|------------------------------------------------|------------------------------------------|---------------------------------------------|-------|
| Servers for hackerz | Compose and Volumes | Bonne gestion des données persistantes | [Go](https://www.youtube.com/watch?v=FAI4ZrQRnLU) |  |
| TechSquidTV | Learn Docker-Compose with WordPress | Compose + wp + persistance (mais pas db) | [Go](https://www.youtube.com/watch?v=exmBvjlZr7U) | ♥ |
| freeCodeCamp.org |  | Container + persistance (y compris sql) | [Go](https://youtu.be/fqMOX6JJhGo?t=2430) | ♥ |
| Peter Fischer | Docker Container Tutorial #10 Handling Volumes | Diff 2 types de persistances | [Go](https://www.youtube.com/watch?v=pOGVngLsaX4) |  |
|  |  | ^ Exemple pour backup en MS |  |  |


--- 

`docker run -v HOSTDIR:CONTAINERDIR mysql`

_^ /!\ deux types :_
- _volume dans container (truc@lecontainer>/data),_
- _ou dossier linké (autre emplacement sur machine hôte)_

_^^ /!\ 'volume' (/data du docker hôte) dispo entre != containers ; l'autre (chemin absolu, /data du container) dispo plutôt pour l'extérieur (modifs/backups)_

cf. [ca](https://youtu.be/fqMOX6JJhGo?t=4458).

**Note** :
- Il est plutôt [recommadé d'utiliser exclusivement volumes](https://forums.docker.com/t/shared-web-hosting-with-docker-best-practices/7893?u=youpiwaza) afin d'éviter des failles de sécurité.
- Pour les backups, s'adresser directement **aux volumes** du **docker** hôte, rien ne doit toucher l'OS (respect de l'isolation).
- Utiliser des volumes nommés également, plutôt que `volume_from` pour piocher dans un conteneur.



## Documentation officielle


### Where and how to persist application data

- Eviter autant que possible de stocker de l'info dans le conteneur. Préférer volumes > bind > conteneur storage.
	- Utiliser bind pour le développement uniquement
	- Possibilité en prod de [définir le volume sur le bind du dev](https://docs.docker.com/develop/dev-best-practices/#where-and-how-to-persist-application-data) ?
- Définition des variables :
	- [Docker secrets](https://docs.docker.com/engine/swarm/secrets/) pour les informations sensibles (identifiants, etc.)
		- Usernames and passwords
		- TLS certificates and keys
		- SSH keys
		- Other important data such as the name of a database or internal server
		- Generic strings or binary content (up to 500 kb in size)
		- Peut être utilisé pour différents [credentials](https://stackoverflow.com/questions/48186712/what-does-developer-credentials-exactly-mean-in-the-amazon-cognito-docs) en fonction des différents environnements (dev/preprod/prod), en particulier liés a l'hébergement (google, amazon, etc.)
			- Cela doit être [stocké dans le contexte](https://12factor.net/config), et non dans l'app 
	- [Docker Configs](https://docs.docker.com/engine/swarm/configs/) pour la configuration
		- Configs are mounted into the container’s filesystem directly, without the use of a RAM disk.


### Navigation

La suite, [Docker network](/docs/05d-Network.md), ou retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).
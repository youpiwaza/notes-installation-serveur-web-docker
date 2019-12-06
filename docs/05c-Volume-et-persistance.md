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


### Navigation

La suite, [todo](/docs/06-todo.md), ou retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).
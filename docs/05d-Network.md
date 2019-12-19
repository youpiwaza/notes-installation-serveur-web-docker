# Docker network / Réseau interne (compose)

Comment fonctionne le réseau entre les différents containers d'un docker compose.

| Source | Titre | Sujet | Lien | Notes |
|---------------------|-------------------------------------------------------------|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------|
| Servers for hackerz | Docker in Development - When localhost isn't the Local Host | Cibler container : pas par ip, mais par nom | https://www.youtube.com/watch?v=1cDXJq_RyNc | En cas de crash, pas de perte d'adresse (name = link vers IP courante) |
| Jake Wright | Docker Compose in 12 Minutes | Gestion simplifiée des réseaux de conteneurs | https://www.youtube.com/watch?v=Qw9zlE3t8Ko | &lt; Exemple micro service (php &gt; api python) |
| Peter Fischer | Docker Container Tutorial #9 container hostnames | Nommer hôte (admin@XXX) des conteneurs | https://www.youtube.com/watch?v=0Li9kzb_cJk |  |


## Documentation officielle

[Doc officielle](https://docs.docker.com/network/)

- [Classic (bridge) container network doc](https://docs.docker.com/network/bridge/)
- [Network tutorial](https://docs.docker.com/network/network-tutorial-standalone/)
	- Pour la prod, ne pas utiliser le network `bridge` par défaut, mais un `user defined bridge`

### Réseau pour swarm

[doc officielle](https://docs.docker.com/network/overlay/)



### Navigation

La suite, [Liste des commandes](/docs/06-Commandes.md), ou retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).
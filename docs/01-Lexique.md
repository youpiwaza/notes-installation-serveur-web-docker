# Lexique

Des explications succinctes concernant les termes utilisés.


## Définitions

| Terme | Définition |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Général** |  |
| OS / Operating system | Windows/Linux/Mac. Programme de base permettant de faire tourner un ordinateur |
| Réseau | Ensemble d'ordinateurs pouvant communiquer ensemble |
| (Adresse) IP | Identification d'un ordinateur dans un réseau (ex: 196.24.2.17) |
| Serveur | Ordinateur dédié à la réception de requête de la part d'autres ordinateurs, et qui renvoie des réponses en échange |
| Port | ~Complément d'adresse IP. Ex: 196.24.2.17:3000. _Métaphore_ : Le serveur est une maison, l'IP son adresse postale, le port c'est savoir si tu rentres par la porte, la fenêtre ou la cheminée. |
|  |  |
| **Boulot** |  |
| DevOps | Pseudo-métier : personne chargée de l'infrastructure réseau (installation, maintenance, évolution, etc.) mais également des processus de dev, mise en prod, etc. Se sert beaucoup de l'automatisation. |
| Scale/scalability | ~Mise à l'échelle : Possibilité de déployer un site sur de multiples ordinateurs, sans que ca parte en latte. |
| Orchestration | Gestion de multiples ordinateurs/dockers/containers |
|  |  |
| **Docker** |  |
| Isolation | Donner à un projet son indépendance totale (aucune dépendance d'OS, de version de programme, ou d'autres projets adjacents). |
| Docker | Nom de l'entreprise et de la technologie Docker. Plus d'infos dans les vidéos de connaissance de base. |
| Docker image | Grosso merdo un dossier qui contiendrait un OS, des programmes classique et ton projet. Peut être stocké en ligne (_Docker hub_) et réutilisé partout. |
| Docker build | Docker image compilée (regroupée en un seul fichier, ~zip) |
| Docker container | Instance d'une image, hébergée sur un docker host |
| Docker host | OS de base, sur lequel est installé et tourne Docker, qui permet la mise en place de containers |
| Dockerfile | Fichier de configuration d'une image Docker, si des actions spécifiques sont a faire (rajouter un programme, ajouter de la conf, ajouter des ressources projet, etc.) |
| Docker compose | Assemblage de plusieurs images Docker, souvent reliées par un réseau Docker. Par exemple : un container 'serveur' accueille le visiteur, et communique avec un container 'PHP' qui lui même communique avec un container 'MySQL', ce qui permet d'afficher des infos de la bdd via php au visiteur. |
| Docker network | Réseau interne entre containers dockers (monté via Docker compose). Des adresses IP spécifiques sont utilisées pour chacun des containers. |
| Docker volume | Dossier de stockage des données pouvant être modifiées (ajout du client ou de l'utilisateur). Permet la persistance de modifications (au cas ou le container ou l'hôte à un problème). En (très) gros c'est comme si le container était une clé usb sans droits de modifications, et que tu mets en place un dossier a toi sur ton propre disque dur, mais que les programmes sur la clé vont pouvoir utiliser. |


## Associations

| Terme | Technologie associée |
|-------------------------------------------------|---------------------------------|
| Serveur http (réponse à une url) | Nginx, Apache |
| Gestion de containers/isolation | Docker |
| Gestion des mails | Postfix |
| Serveur DNS | OVH, BindOf |
| Automatisation installation & tâches | Ansible |
| CI/CD | Jenkins |
| Orchestration (gestion auto hosts & containers) | Docker swarm, Kubernetes, Mesos |


### Navigation

La suite, [l'hébergement](/docs/02-Hebergement.md), ou retour à la [table des matières](/).

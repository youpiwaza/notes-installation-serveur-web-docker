# TODO

Répondre à l'ensemble des questions 8

## Doc à ranger

- Docker swarm
  - [Docker swarm 101](https://www.aquasec.com/wiki/display/containers/Docker+Swarm+101)
- Nginx courses
  - https://www.nginx.com/resources/webinars/nginx-basics-best-practices/
  - https://www.nginx.com/resources/library/high-performance-caching-with-nginx-and-nginx-plus/
- Script install ansible .sh
  - Installation de docker pour windows via Ansible, cf. [installation automatique du terminal](https://raw.githubusercontent.com/viasite-ansible/ansible-role-zsh/master/install.sh)
- Traefik
  - [Vidéo Traefik v2 officielle avec un accent horrible, mais je crache pas trop dessus je dois avoir le même](https://www.youtube.com/watch?v=RP40Iv_0yvA)
  - [Traefik canary release](https://youtu.be/RP40Iv_0yvA?t=1891)
- DevOps
  - [IaC / Infrastructure As Code](https://www.udemy.com/course/linux-academy-devops-essentials/learn/lecture/13781164#overview)
  - Outils a jour / [Xebialabs periodic table](https://xebialabs.com/periodic-table-of-devops-tools/)

# Indexation ressources tests

- server-related-tutorials
  - 01-docker
    - 01-Docker-desktop
      - 01 // Installation docker & tests de base
      - 02 // Modification image & création d'un build
      - 03 // Installation & tests kube
      - 04 // Installation & tests swarm
    - 02-WLS // Installation docker & docker-compose (SPECIAL) sur WLS, et lien vers Docker desktop (windows) + COMMANDE LIEN WLS DDesktop
    - 03-develop-with-docker
      - 01 // Création de dockerfile, context
      - 02 // Build depuis github, Mise en place des volumes (& bind), Backup & restauration volumes
    - 04-my-tests
      - 01 // Dockerfile			    / Nginx 						          / OK	/ Site statique sans process, , github
      - 02 // Docker compose 		  / Nginx + PHP					        / OK	/ Configuration de Nginx & php-fpm, bash containers, exploration configs
      - 03 // Docker compose		  / Nginx + PHP + SQL + adminer / OK	/ Custom Dockerfile (Php + PDO), bash containers, exploration configs, networks, init SQL, volumes, docker secrets (KO), dockerhub push
      - 04 // Docker compose		  / Traefik						          / OK	/ docker-compose CLI
      - 05 // Swarm 				      / Traefik + consul 				    / KO	/ Faire tourner l'exemple docker rocks > ~KO + traefik outdated
      - 06 // Swarm					      / Traefik + ui					      / OK	/ Mise en place de traefik et de son ui + configuration de services (routes)
      - 07 // Docker compose		  / Traefik						          / OK	/ Exemple dockerhub, routes automatiques pour compose
      - 07.1 // run compose swarm	/ Traefik						          / OK	/ Routes automatiques (avec réécriture) pour run, compose & swarm
      - 07.2 // compose				    / Traefik						          / ~KO / Routes automatiques (avec réécriture) pour projet concret (php + sql) > KO aléatoire 1/2
      - 07.3 // swarm				      / Traefik						          / KO 	/ Routes via labels pour projet concret (php + sql)
      - 08	// swarm				      / swarmprom						        / OK	/ Pack outils de monitoring + conf windows. Tout OK excepté Nodes swarm

POUR LES TRUCS KO :  `docker service logs NOM_DU_SERVICE`

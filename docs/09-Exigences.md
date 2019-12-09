# Exigences

Liste de ce que doit être capable de faire mon serveur, en français (éviter la technique).


## Sécurité

- Connexions sécurisées (SSH + Clés)
- Sites en https
- Résistance au flood & IP ban
- Load balancer


## Monitoring

- Analyse en temps réel des capacités utilisées de la machine hôte
- Analyse des etats et des capacités des différents containers
- Envoi de mail si problème


## Convénience

- Possibilité d'utiliser simplement n'importe quelle techno (yay Docker)
- Création de sites à la volée
- Lien de nom de domaine à [un] conteneur à la volée


## Développement

- Environnement de développement 'simple' : local/dev/preprod/prod
	- Possibilité de développer en local
	- Possibilité de tester un truc en dev en une étape, voir en HMR
	- Possibilité de passer dev en preprod, preprod en prod, et rollback simplement
	
- Logs
	- Récupération des logs depuis les containers vers l'hôte
	- Envoi de mail si problème
	
- Filets de sécurité
	- Les codes sources seront sur github/lab
	- Les bases de données seront sauvegardées tous les jours (1 semaine max)
		- Cf. serveur de backup fourni
	- Backup des versions des images/build docker

- Gestion des mails


## Confort utilisateur

- www.truc.com, truc.com, https://www.truc.com > tous redirigent vers https://truc.com
- Gestions des pages d'erreurs, possibilité de les customiser (404, 500, etc.)




### Navigation

La suite, [Mes choix technologiques](/docs/10-Choix-technologiques.md), ou retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).






































//
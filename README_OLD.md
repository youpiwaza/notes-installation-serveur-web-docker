# TODO

## Configuration du serveur

Utiliser [Ansible](https://www.grafikart.fr/tutoriels/ansible-753) pour installer/réinstaller le serveur de manière clean et automatique (plutôt que d'avoir de la doc partout)
- Utiliser également pour les tâches courantes

### One shot

- Pimper terminal avec zsh et tmux [grafikart pimp terminal](https://www.grafikart.fr/tutoriels/pimp-my-shell-750)
- [Changer port par défaut](https://youtu.be/lXOdDal6qos?t=239) : Meilleure sécurité, plus de mots de passe.
- [Retirer connexion par mot de passe](https://youtu.be/lXOdDal6qos?t=324) : Meilleure sécurité, plus de mots de passe.
- Mise en place de backups automatiques via le CRON (~1 fois / jour, incrémental)
  - [Mise en place Rsync](https://www.youtube.com/watch?v=7Hb32v8e8W0) pour les fichiers
  - mysqldump > bdd sql
  - Ajouter un clean des logs (zip après 2 semaines, suppression après 2 ans)
- Créer un dossier log contenant les liens symboliques EXPLICITES vers les logs des différentes technos
- Ajouter un script/la conf qui envoie un email en cas d'erreur côté serveur
- Ajouter une page par défaut pour le serveur, en cas d'accès via l'IP
- Ajouter des pages personnalisées pour les différentes erreurs serveurs 50X
- Désactiver erreurs (php, etc.) & phpinfo en prod
  - Rendre accessible via page dédiée + pass ? (ou dev. suffisant..)
- Script analyses performances (ex [config mysql](https://www.grafikart.fr/tutoriels/mysql-690))
- Ajouter de la sécurité autant que possible > https://www.hacksplaining.com/lessons
- Installer REDIS, et implementer (node et WP) pour gain de perfs
  - Faire un test avec une base WP et faire un diff des perfs
- Mise en place des ~[certificats SSL](https://www.grafikart.fr/tutoriels/apache-ssl-letsencrypt-746)~ cf. [installation avancée](https://www.grafikart.fr/tutoriels/nginx-ssl-letsencrypt-747)
  - Certifs SSL gratuits [Let's encrypt](https://letsencrypt.org/fr/)
  - Tests certificats SSL [SSL Labs tests](https://www.ssllabs.com/ssltest/)
- Mise en place serveur de mails (postfix)
- Mise en place accès FTP pour utilisateurs existants [ProFTP](https://www.grafikart.fr/tutoriels/proftpd-755)
  - Annuaire simple des accès en place
- MeP parefeu (iptables)
- MeP anti-brute force [fail2ban](https://www.grafikart.fr/tutoriels/fail2ban-698)

### Procédures

- [Ajouter un utilisateur SSH via clés seulement](https://youtu.be/lXOdDal6qos?t=449) : Remplace le mot de passe.
- Ajouter un utilisateur serveur par site et limiter son accès (docker/ftp/annuaire ?)
- Vérifier les performances des différentes technos (analyse + logs)
  - Bande passante : [iperf3](https://github.com/esnet/iperf)
- Ajouter/Renouveler les certificats SSL (https)
  - CRON ?
- Envoi de mail + tester templates [mailinator](https://www.mailinator.com/)
- Règles iptables

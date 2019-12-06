# Hebergement

Bon il existe 100k possibilités pour l'hébergement. D'expérience OVH reste le meilleur rapport qualité/prox en France (2x moins cher 2x plus puissants).

Après si vous ne voulez pas trop vous prendre la tête il existe également pas mal d'hébergement de ouf cloud (Google, Amazon, BlueOcean, etc.).

Mais perso je préfère tout comprendre et avoir la main tout du long.


## Gammes

Il existe différentes gammes de tarifs pour l'hébergement, selon les besoins et le niveau.

Récapitulatif très rapide OVH :

| Fournisseur | Nom | Type | Cible | Tarifs TTC/mois | Url |
|-------------|-----------------------|---------------------------------|---------------------|-----------------|---------------------------------------------------|
| OVH | Hébergement classique | 1 seul site | Client site vitrine | 2 - 7€ | https://www.ovh.com/fr/hebergement-web/ |
| OVH | OVH VPS | Serveur virtuel | Amateur | 4 - 10€ | https://www.ovh.com/fr/vps/ |
| OVH | Kimsufi | Serveur dédié / Entrée de gamme | Amateur éclairé | 5 - 30€ | https://www.kimsufi.com/fr/serveurs.xml |
| OVH | So you start | Serveur dédié / Moyenne gamme | (Semi) pro | 25 - 85€ | https://www.soyoustart.com/fr/serveurs-essential/ |
| OVH | Ovh serveurs | Serveur dédié / Haut de gamme | Pro | 70 - 250€ | https://www.ovh.com/fr/serveurs_dedies/ |

**Notes**

- Pour du site très classique (vitrine ou faible trafic), pas besoin de prise de tête, prenez un hébergement de base (un par client).
- Pour les VPS je suis mitigé : il s'agit de serveurs dédiés classiques, mais découpés en petites parties (en gros vous avez un "morceau" de serveur dédié).
	- A l'époque (dans les temps anciens) il y avait des problèmes de performance, ou même des problèmes de maintenance si l'un des autres "morceaux" avait des soucis..
	- Mais de nos jours en tout cas le tarif est très attractif.
	- Mais a choisir je partirai sur un kimsufi (ce que j'avais avant..) car les prix sont similaires..


## Mon historique serveur

Au niveau de mon historique, je suis passé de plusieurs hébergements classiques à un kimsufi, puis un plus gros kimsufi, puis sur l'entrée de gamme so you start, et enfin moyenne gamme so you start.

**Hébergement classique** : le meilleur rapport prix/prix, vraiment pas cher pour mettre quelque chose en ligne.
Je n'ai jamais vraiment eu de soucis avec, excepté un peu la lenteur parfois (mis en avant par les outils SEO).
Pratiquement aucune configuration à faire, mais extrêmement limité dès qu'on creuse un peu (cache serveur, etc.).

Ce sont ces deux raisons qui m'ont poussées à avoir mon propre serveur (et le fait d'en avoir vu tourner un prestigieux, pour un gros client, dans l'une des boites ou je travaillais).

**Kimsufi** : Un peu plus cher que l'hébergement classique, mais vu que j'y hébergeai 5-6 sites clients, au final cela revenait moins cher. Légère amélioration de performances, plus de marge de manœuvre côté configuration ; je passais par une interface graphique gratuite _ISPConfig_, qui est très bien.

Mais au final des soucis de performances en fonction des heures de la journée.

**Kimsufi++** : Le même en plus cher, mais surtout avec des **SSD** et une bonne maîtrise du cache serveur.

La différence de performance s'est ressentie directement (retours serveurs qui passent de 1s-1.5s à 0.1s 0.2s !) et qui m'a apporté mes premiers A+ et autres 100/100 sur les analyseurs de site.

Et c'est quand même beaucoup plus confort sur les administrations de type WordPress.

Ca m'allais bien, mais quelques soucis de process et de mémoire sur le long terme..

**So you start** : La cours des (petits) grands. Les tarifs sont pas les même, mais les performances non plus.

En toute objectivité, c'est de l'overkill pour héberger quelques sites vitrines. Mais j'aime bien quand ça pulse, et surtout avec une config maison (Merci à mon copaing [PE](http://fr.viadeo.com/fr/profile/pierre-emmanuel.remy1)).

Une config apache/php/mysql, et tout le monde dans le même bateau.

Au final pas mal de boulot, un peu la flemme de le maintenir, et quelques années plus tard je ne peux plus faire de mises à jour (à cause de _dépendances cycliques_ >.>) et du coup, comme les prix stagnent mais que les configs évoluent, je suis passé sur un autre serveur pour repartir au propre.


## Mon serveur actuel

**So you start++** : Des soldes pour la black friday > un serveur a 50€HT/mois à 35. En gros le double de performances pour le même prix. Beh je me suis lancé.

![Complètement overkill](http://stockage.masamune.fr/images/max/191128-SYS-config-max.jpg)

Du coup nouveau serveur tout propre, avec plein de bonnes résolutions !

Architecture orientée DevOps, avec tout bien séparé dans des conteneurs et tout et tout.

Pour la suite de la doc, d'abord mes recherches, puis mon 'cahier des charges' serveur, puis la mise en place :)


### Navigation

La suite, [les pré-requis](/docs/03-prerequis.md), ou retour à la [table des matières](https://github.com/youpiwaza/notes-serveur).
<a name="1.5.1"></a>
# 1.5.1 (2019-03-20)

### Improvements
 * [**Range Tracking**] Amélioration des performances lors de l'affichage du graph.
 * [**Command**] "Info Recharge" retourne 'Driving' quand la voiture se déplace.

### Fixes
 * [**Range Tracking**] Correctif au niveau de l'unité d'énergie (kW -> kWh).

<a name="1.5.0"></a>
# 1.5.0 (2019-03-14)

### Features
* [**Suivi de l'Autonomie**] Il est maintenant possible de choisir entre l'affichage des kilomètres gagnés ou perdus et l'énergie consommée. Des informations sur la capacité de la batterie sont à renseigner au niveau de la configuration du véhicule.

### Improvements
 * [**Suivi de l'Autonomie**] Live activé par défaut sur les 5 dernières minutes quand la voiture est en marche.
 * [**Suivi de l'Autonomie**] Checkbox "Live" supprimée. Un choix "LIVE OFF" est intégré dans le sélecteur de la "largeur" du live
 * [**Suivi de l'Autonomie**] Mise à jour des min/max des courbes selon les données affichées pour un meilleur rendu visuel.
 * [**Suivi de l'Autonomie**] Dans la version Mobile, sur un écran large, les courbes sont plus épaisses pour un meilleur rendu sur l'écran de la Tesla par exemple.
 * [**Widget**] Fenêtre modale de confirmation sur les boutons d'ouverture de portes et coffres.
  * Ajout d'une Model Y rouge dans les Tesla virtuelles.
 
 
### Fixes:
 * [**Suivi de l'Autonomie**] Quand le chauffage est allumé, seule la ligne change de couleur. Même couleur du fond de courbe si chauffage est on ou off
 * [**Widget**] Sur une Model 3, l'image affiche maintenant la couleur et les jantes qui correspondent au véhicule. Egalement, la gestion du toit ouvrant est supprimés sur la Model 3.

### Tips:
* [**Suivi de l'Autonomie**] Pour accéder directement à la vue `Tesla` depuis la version Mobile sans jongler avec les menus, il est possible de définir `Tesla` comme vue "Mobile" par défaut dans la configuration du profil (Menu `User` -> `Profil Admin` -> Onglet `Interface`)

### Known Issues
* [**Suivi de l'Autonomie**] Sur les journées où il y a eu beaucoup d'aquisition lors de long parcours, l'affichage peut être long, voire ne pas être possible (problème en cours d'analyse).


Un grand merci à `Bob Jouy` (https://twitter.com/bobjouy) pour ses retours et suggestions d'améliorations !


<a name="1.4.2"></a>
# 1.4.2 (2019-02-14)

### Improvements
* [**Suivi de l'Autonomie**] Une nouvelle commande 'Contrôler le suivi de l'autonomie' permet de démarrer/arrêter le suivi de l'autonomie depuis un scénario.
* [**Widget**] Affiche un texte indiquant l'installation d'une mise à jour logicielle et le temps restant, le cas échéant.

### Fixes
* Correctif sur le texte d'info de dernière mise à jour qui pouvait afficher successivement plusieurs valeurs différentes.

<a name="1.4.1"></a>
# 1.4.1 (2019-02-08)

### Improvements
* [**Scenario**] La commande 'Contrôle de la recharge' admet un nouvel argument 'Estimer' qui va: démarrer une charge, attendre 2 minutes, calculer l'heure de départ et arréter la charge. Note: le scénario de départ de charge est simplifié.

<a name="1.4.0"></a>
# 1.4.0 (2019-02-04)

### Features
* [**Scenario**] Ajout de la commande qui va retourner l'heure de départ de la charge, pour qu'elle soit chargée à x% à une heure donnée. Utilisable dans un scénario Jeedom (cf documentation).

<a name="1.3.1"></a>
# 1.3.1 (2019-01-30)

### Improvements
* [**Suivi de l'Autonomie**] En mode live la courbe d'autonomie devient violette quand le chauffage est activée.
* [**Suivi de l'Autonomie**] Il est possible maintenant d'afficher un graph d'exemple sur une voiture virtuelle.
* Augmentation du panel mobile (x2) quand la taille de l'écran le permet.

### Fixes
* Correctifs pour une meilleure stabilité et maintenabilité.

<a name="1.3.0"></a>
# 1.3.0 (2019-01-23)

### Features
* Ajout d'un panneau de '**Suivi de l'Autonomie**' qui permet de visualiser sur un graphique, l'évolution de l'autonomie en fonction de l'état de la voiture : **conduite**, **recharge** et **parking**.

### Known issues
* Le panneau de 'Suivi de l'Autonomie' n'est pas encore traduit en anglais.

<a name="1.2.2"></a>
# 1.2.2 (2019-01-07)

### Improvements
* Ajout d'une indication de la dernière date de mise à jour ("A l'instant", "Mise à jour il y a 2 mintues", ...).

### Fixes
* Suppression du message "Erreur d'accès au Seveur Tesla", lors du réveil de la voiture.

<a name="1.2.1"></a>
# 1.2.1 (2018-12-22)
### Fixes
* Le plugin est maintenant compatible avec PHP 5.6.

<a name="1.2.0"></a>
# 1.2.0 (2018-12-19)
### Features
* Ajout du widget Mobile.
* Ajout d'une commande Info qui remonte la température intérieure (utile pour un scénario de mise en route de la clim par exemple).
* Ajout d'une commande de réveil de la voiture qui effectue 3 tentatives de réveil espacées de 5 secondes (3 et 5 sont configurables au niveau du plugin).
* Lors de la mise à jour du plugin, celui-ci synchronisera vos véhicules configurés.

### Improvements
* Les principales commandes d'actions peuvent être utilisées dans des scénarios.
* Plus de traduction en anglais.

### Fixes
* Correction sur le bouton d'ouverture du toit ouvrant.


### Known issues
* La fonction de reveil marche mieux lorsque le mode **Connexion permanente** est activé dans la voiture.


Un grand merci à `Kim` pour ses retours et suggestions d'améliorations !

<a name="1.1.0"></a>
# 1.1.0 (2018-12-10)
### Features
* Contrôle des températures de climatisation pour le conducteur et le passager.
* Contrôle des ouvrants (coffre avant, coffre arrière, toît ouvrant).
* Contrôle de la limite de recharge via dashboard et scenario.
* Affichage des températures en `°C` ou `°F` selon configuration du véhicule.
* Affichage des distances en `km` ou `miles` selon configuration du véhicule.

### Improvements
* Ajout d'effets sur les boutons cliquables pour les rendre plus visibles.
* Optimisation et nettoyage du code (utilisation d'une feuille de style unique partagée entre les différents templates, ...)

### Known issues
* [Temp settings] A cause d'une limitation sur l'API Tesla, il n'est pas possible de passer de `SYNC` à `Not SYNC`. En conséquence, il n'est possible de configurer la température du passager que si dans la voiture les températures ne sont pas synchronisées (`Not SYNC`)).

<a name="1.0.0"></a>
# 1.0.0 (2018-11-29)
### Highlights
* Ceci est la première version **stable** publiée sur le Jeedom market !
* Les prochaines versions ajouteront de nouvelles fonctionalités (contrôle des temperatures, Contrôle de la limite de charge ...) !

Un grand merci à l'équipe Jeedom  `Loic` and `Alexandre`, et aux béta-testeurs `carfnann` et `philippe` pour leurs tests et commentaires !

<a name="0.3.0"></a>
# 0.3.0 (2018-11-23)
### Bug Fixes
* Rafraichissement du bouton de recharge après avoir cliqué dessus.
* Affichage du pourcentage de la batterie dans le graph.
* Ajout d'un bouton pour supprimer les Tesla virtuelles.
* Ajout de Model 3 et Roadster dans la liste des Tesla virtuelles.
* Amélioration de la phase d'authentification (jeton d'accès et login).

<a name="0.2.0"></a>
# 0.2.0 (2018-11-18)
### Features
* Mise à jour de la documentation
* Ajout de l'anglais comme langue disponible

<a name="0.1.0"></a>
# 0.1.0 (2018-11-10)

### Highlights
* Ceci est la première version **béta** publiée sur le market de Jeedom

### Features
* Contrôle et affichage de la recharge
* Contrôle et affichage de la climatisation
* Contrôle et affichage du vérouillage

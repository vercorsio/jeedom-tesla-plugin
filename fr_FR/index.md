Introduction
===
Bienvenue sur la page de documentation du plugin Jeedom Tesla ! 

Avec ce plugin, l'utilisateur peut accéder à sa voiture Tesla, et intéragir avec les données remontées par l'API proposée par Tesla.

Egalement, ce plugin propose un panneau pour suivre sur un graphique l'évolution de l'autonomie au cours d'une journée, au gré des kilomètres parcourus:


![tracking-graph](../images/consoLow480.gif)


Retrouvez la liste des nouveautés sur le [Change log](!https://vercorsio.github.io/jeedom-tesla-plugin/fr_FR/changelog).


Configuration du plugin
=======================

La configuration est très simple, après téléchargement du plugin, il
vous suffit de l’activer et d'utiliser l'une des deux méthodes indiquées ci-dessous pour accéder à votre compte Tesla.

![config](../images/configPlugin-1.png)

Le plugin va rechercher la ou les Tesla associées à votre compte et créer les équipements automatiquement.

![config](../images/configPlugin-2.png)
> **Tip**
>
> Ce plugin nécessite que votre Tesla soit accessible sur le réseau pour ne pas provoquer d'erreur. 
> Si l'application Tesla sur votre smartphone arrive à se connecter à votre Tesla, le plugin sera à même de configurer correctement votre Tesla dans Jeedom.

Pour accéder au panneaux de suivi de consommation, il suffit de cocher `Afficher le panneau desktop` et `Afficher le panneau mobile`:  
![config](../images/configPlugin-4.png)


Les deux méthodes de connections sont les suivantes:

### 1) Avec vos identifiants de compte Tesla:

- **Email** : l'email que vous utilisez pour vos connecter sur votre compte Tesla
- **Mot de passe** : le mot de passe correspondant
> **Note**
>
> Vos identifiants ne sont utilisés que lors de la phase de connexion pour récupérer un jeton d'accès. 
> 
> De part la nature de Jeedom qui est Self Hosted, vos identifiants sont stockés **localement** sur la machine qui héberge votre Jeedom. Malgré tout, si vous le souhaitez, vous pourriez après la première synchronisation, effacer les champs email/mot de passe.
>
> Néanmoins, le jeton d'accès a une date d'expiration (environ 90 jours) au dela de laquelle il tentera de refaire une connection pour le rafraichir. Il vous appartiendra de remettre vos identifiants et/ou coller un jeton d'accès (cf methode n°2)

### 2) Avec un jeton d'accès:

- **Jeton d'accès** : Jeton que vous pouvez, entre autre, vous procurer en executant le script php fourni avec le plugin:

```
$ php /var/www/html/plugins/tesla/scripts/tokenTesla.php mon.email@FAI.fr mot2passe

Votre jeton d'accès à votre compte Tesla : 49329effb7d381c945fbf7e6b3e02691e746904f47ebdb2a3e54d49c93473e80
```

> **Note**
>
> Cette méthode permet d'éviter d'entrer ses identifiants dans la configuration du plugin.
> Le plugin ne fonctionnera que pendant la durée de validité du jeton d'accès. 
> Un bouton `revoker mon jeton d'accès` permet d'informer le service Tesla que ce jeton ne permettra plus la connexion au service.

Le bouton __"Synchroniser mes voitures"__ permettra d'effectuer la recherche et ajoutera un équipement Jeedom pour chaque véhicule Tesla non encore créé.

Tesla virtuelle
--

Pour tester le plugin sans connexion à votre compte Tesla, ou si vous n'avez pas (encore) de Tesla, le plugin offre la possibilité de créer des équipements virtuels correspondants à des Tesla __Model S__ et/ou __Model X__.

Il suffira de cliquer sur le bouton __"Ajouter des Tesla virtuelles"__. Des jeux de données correspondants à des véhicules réels seront utilisés pour créer des équipements virtuels. Bien entendu toute action (chauffage/charge/dévérouillage) sur ces équipements sera sans effet.

Autres paramètres de configuration
--

- **Coût du kWh** (en euro) : Nécessaire pour calculer approximativement le cout d'une charge, le prix pour parcourir 100km et le nombre de km que l'on peut faire avec 1 euro. La valeur par défaut est `0.14`.
- **Tesla Client ID** et **Tesla Client Secret** : deux clefs publiques qui sont necessaires pour accéder à l'API du serveur des Tesla. Déjà renseignées, ces clefs peuvent être modifiées au cas où l'API requiert de nouvelles valeurs. 




Configuration du véhicule
=======================

Une fois le plugin configuré, le ou les véhicules de votre compte tesla sont ajoutés. Il suffit de cliquer sur chacun pour l'activer, le rendre visible et l'attacher à un objet parent (ici le Garage) :

![config](../images/configPlugin-3.png)

![config](../images/configCar-1.png)


Les commandes d'info et d'action associées à chaque Tesla sont les suivantes

![config](../images/configCar-2.png)

Commandes de type **info**
--

| Commande   |   Description |
| --- | --- |
| **Photo** | Affiche une photo de la Tesla, ainsi que le badge (70D, P85D, ...).
| **Info réveillée** | Indique si le véhicule est en mode veille (0) ou en ligne (1).
| **Info autonomie** | Indique l'autonomie typique (en km ou miles) de la voiture.
| **Info autonomie nominale** | Indique l'autonomie nominale (en km ou miles) de la voiture.
| **Info climatisation** | Indique si la climatisation est allumée ou éteinte.
| **Info température habitacle** | Indique la température à l'intérieur du véhicule.
| **Info recharge** | Indique si la voiture est en train de charger ou non. Les valeurs possibles sont  { `Charging`, `Stopped`, `Disconnected`, `Complete`, `Scheduled` }.
| **Info limite de recharge** | Indique le pourcentage à atteindre à la fin d'un recharge.
| **Info verouillage** | Indique si la voiture est fermée ou ouverte.
| **Info frunk** | Indique si le coffre avant (frunk) est fermé ou ouvert.
| **Info trunk** | Indique si le coffre arrière est fermé ou ouvert.
| **Info toît ouvrant** | Indique si le toit panoramique est ouvert ou fermé.
| **Odomètre** | Indique la valeur du compteur kilométrique (miles ou km).
| **Info véhicule** | Affiche un titre et un sous titre correspondant à l'état actuel de la voiture. Par exemple _Conduite 67km_, _Recharge planifiée à 22h50_, _Stationnée_, _Supercharge_, ...
| **Détail autonomie** | Affiche un graph de la batterie
| **Détail de la recharge** | Affiche les données issues de la recharge.
| **Détail de la climatisation** | Affiche les paramètres de climatisation (conducteur, passager, intérieur et extérieur). 

Commandes de type **action**
--

| Commande   |   Description |
| --- | --- |
| **Contrôler la recharge** | Va permettre de démarrer ou interrompre la charge si le cable de recharge est engagé.
| **Contrôler la limite de charge** | Va permettre dedéfinir un pourcentage de charge a atteindre.
| **Contrôler la climatisation** | Va permettre d'allumer ou d'arreter la climatisation.
| **Contrôler la température** | Va permettre de définir une température dans l'habitacle (conducteur/passager).
| **Contrôler le vérouillage** | Va permettre de vérouiller ou déverouiller la voiture.
| **Contrôler le coffre avant** | Va permettre de vérouiller ou déverouiller le coffre avant (frunk).
| **Contrôler le coffre arrière** | Va permettre de vérouiller ou déverouiller le coffre arrière (trunk).
| **Contrôler le toit ouvrant** | Va permettre d'entrouvrir ou de fermer le toît panoramique.
| **Rafraichir** | Mise à jour de la tuile sur clic de l'icone.
| **Réveiller** | Force le reveil de la voiture (3 tentatives espacées de 5s). Peut-être utile dans un scénario. Met à jour la valeur de **Info reveillée**.

> **Tip**
>
> Chacune de ces actions peut être intégrée dans un scénario Jeedom.


Affichage du véhicule
=======================

La plupart des commandes listées ci-dessus a un template spécifique qui lui est attribué, et qui permet d'obtenir par défaut l'affichage d'un véhicule tel qu'illustré sur l'image:

### Version Desktop:

![config](../images/displayCar-2.png)

### Version Mobile:

![config](../images/mobileWidget.gif)

Par exemple pour ne pas afficher la photo et les détails de climatisation, il suffit pour un véhicule donné de décocher `"Affichage"` dans la ligne correspondante de la configuration de ces commandes.

L'odomètre est historisé, ce qui permet d'obtenir le graphique des km parcourus.

Contrôler la climatisation
--

| Bouton | Description | Un clic sur ce bouton va ... | 
| --- | --- | --: |
| ![clim off](../images/clim_off.png) | La climatisation est éteinte | _... allumer la climatisation_ | 
| ![clim on](../images/clim_on.gif) | La climatisation est allumée | _... éteindre la climatisation_ |

Il est possible de modifier la température cible de la climatisation en utilisant un widget secifique, comme décrit dans l'animation ci-dessous:

![clim on](../images/setTemps.gif)
> **Note**
>
> A cause d'une limitation dans l'API Tesla, il n'est possible de configurer des températures différentes pour le conducteur et le passager que lorsque les températures sont déjà non synchronisées dans le véhicule (SYNC désactivé).
>


Contrôler le vérouillage (portes, coffres et toît ouvrant)
--

| Bouton | Description |  Un clic sur ce bouton va ... |
| --- | --- | --: |
| ![lockOn](../images/locked.png) | La voiture est fermée | _... dévérouiller les portes_ |
| ![lockOff](../images/unlocked.png) | La voiture est ouverte | _... vérouiller les portes_ |
| ![frunkOff](../images/frunk_off.png) | Le coffre avant est fermé | _... dévérouiller le frunk_ |
| ![frunkOn](../images/frunk_on.png) | Le coffre avant est ouvert | _...  être sans effet_ |
| ![trunkOff](../images/trunk_off.png) | Le coffre arrière est fermé | _... ouvrir le coffre_ |
| ![trunkOn](../images/trunk_on.png) | Le coffre arrière est ouvert | _...  fermer le coffre_ |
| ![panoOff](../images/pano_off.png) | Le toît panoramique est fermé | _... ouvrir le toît panoramique_ |
| ![panoOn](../images/pano_on.png) | Le toît panoramique est ouvert | _...  fermer le toît panoramique_ |

Contrôler la charge
--

| Bouton | Description |  Un clic sur ce bouton va ... |
| --- | --- | ---: |
| ![charDis](../images/charging_Disconnected.png) | Le cable de charge n'est pas engagé | _... être sans effet_
| ![charSch](../images/charging_Scheduled.png) | La recharge est programéee | _... démarrer la recharge_
| ![charCha](../images/charging_Charging.gif) | La recharge est en cours | _... stopper la recharge_
| ![charPau](../images/charging_Pause.png) | La recharge a été manuellement arrétée | _... reprendre la recharge_
| ![charCom](../images/charging_Complete.png) | La recharge est terminée | ... _être sans effet_
| ![charNul](../images/charging_Null.png) | Etat de recharge indéterminée | ... _être sans effet_
 


Pour modifier depuis le dashboard la limite de charge, il suffit de délacer le curseur sur le graph de la batterie. Le pourcentage ainsi que le nombre approximatif de kilomètres seront affichés:

![setLimit](../images/setChargingLimit.gif)

Scenario
==

Exemples de scénarios: 

* Modifier le seuil de recharge à son maximum :
  ![setLimit](../images/scenario_setChargeLimit_100.png)

* Reveiller la voiture et mettre le seuil de charge à 90% et activer la climatisation si la température de l'habitacle est inférieur à 14°C :

  ![climate](../images/scenario_Climate.png)


Suivi de consommation
==

Principe
--

Le panneau **suivi de conso** permet au conducteur de comprendre l'influence de sa conduite et de l'environement sur l'autonomie du véhicule, pour chacune des Tesla activées dans votre Jeedom.

Cela permet de comprendre comment évolue l'autonomie restante au fil des trajets, des charges et temps de repos.

Ce 'tracking' s'appuie sur des données acquises depuis les Servers Tesla via un cron qui est démarré et arrêté depuis le panneau. Les données sont stockées en local sur votre serveur Jeedom.

Un graphique retrace l'évolution de l'autonomie au cours d'une journée et un calendrier permet de consulter l'historique des graphiques.

> **Note**
>
> Pratique, la version mobile permet de suivre l'évolution de l'autonomie tout en conduisant !

Mise en place
--
Par défaut, l'acquision n'est pas démarrée.

Un clic sur `Start Recording` va démarrer le cron qui va récupérer à chaque minute les données qui
serviront à afficher des graphiques de suivi, identifier les différentes étapes de la journée et proposer des statistiques.

Un clic sur `Stop Recording` va stopper l'acquisition des données (arrêt du cron).

> **Notes**
>
> Lors de l'acquisition et si le graph affiché est le graph du jour, il est possible de passer en mode `live`, ce qui permet d'afficher en temps réel les dernières données acquises (pratique pour suivre sa consommation lors d'un trajet).
>
> Au premier lancement, il peut se passer plusieurs minutes avant que des données soient
effectivement disponibles pour l'affichage.

Exemple
--
L'exemple ci-dessous retrace un trajet réél effectué le 5 janvier 2019, qui se découpe principalement en 4 segments : 
- <code>km  0</code> à <code>km 15</code>: route départementale sur du plat - _altitude 'en haut': 1100m._
- <code>km 15</code> à <code>km 30</code>: route départementale en descente -  _altitude 'en bas': 250m._
- <code>km 30</code> à <code>km 50</code>: autoroute.
- <code>km 50</code> à <code>km 65</code>: route départementale - _altitude à l'arrivée: 500m._

![tracking-graph](../images/tracking-graph.png)

- En abscisse on trouve le temps
- En ordonnée à gauche en <b>noir</b>, le kilométrage parcouru. <u>Note:</u> l'angle de la courbe est proportionel à la vitesse.
- En ordonnée à gauche en <b style='color:#22C4FF'>bleu</b>, l'autonomie de départ en <b style="color:#3355FF">pointillé</b>, et l'évolution de l'autonomie en <b style='color:#22C4FF'>bleu</b>. Quand la climatisation est allumée, le trait est en <b style='color:blueviolet'>violet</b>.
 - En ordonnée à droite, la différence constatée entre l'<b style="color:#3355FF">autonomie initiale</b> et l'<b style='color:#22C4FF'>autonomie réelle</b> compte tenu des <b>kilomètres parcourus</b>. La courbe est <b style="color:#00FF00">verte</b> quand il y a un gain, <b style="color:#FFA500">orange</b> en cas de perte.



Un tableau récapitulatif par journée est affiché et permet sur selection d'une ligne de zoomer sur le graph correspondant. Un clic sur la ligne "Total" va afficher la journée complète.

![tracking-graph](../images/tracking-table.png)

- L'`efficience` correspond au pourcentage de km gagnés/perdus par rapport à la longueur du trajet, ce qui permet de pondérer les résultats. Les petits trajets sont 'énergivores'.
 - Les trois boutons en haut à droite du tableau permettent de filtrer par type d'étape et de pouvoir par exemple calculer les pertes liées aux seules étapes de type `parking`.
 
> **Notes**
>
> - En dehors des plages de conduite, le graphique affiche l'évolution de l'autonomie à l'arrêt, et permet par exemple de tracer les pertes de type <i>"vampire drain"</i> et de voir les courbes lors des recharges.
> - Activer en continu le recording peut conduire à une consommation d'énergie non souhaitée.

FAQ:
==

1. Comment béneficier des nouvelles fonctionalités après mise à jour du plugin ?

   Lors de la mise à jour, le plugin synchronise automatiquement vos véhicules configurés avec la nouvelle version du plugin. Cependant, il se peut que la mise à jour ne se soit pas faite. Il suffira alors de cliquer sur le bouton `Synchroniser mes voitures` et les nouvelles commandes Info et Action seront ajoutées à l'équipement et visibles sur le dashboard.

2. Comment changer les unités de températures et de distance (°C / °F, km / miles) ?
   
   Le plugin Tesla de Jeedom lit et utilise les paramètres que vous avez configuré dans votre voiture.

   Idem pour l'affichage de l'autonomie typique ou nominale. 

3. La commande 'Réveiller' ne réveille pas la voiture.
  
   Depuis le panneau de configuration du plugin, vous pouvez modifier les deux paramètres `Nombre de tentatives pour reveiller le véhicule` et `Nombre de secondes entre deux tentatives` pour essayer de forcer le reveil. Les chances de succès du réveil sont plus grandes quand le mode **Connexion permanente** est activé dans les paramètres de votre voiture. 


----

Merci d'envoyer toute question à <a href='mailto:vercors.io@gmail.com?subject=About%20Jeedom%20Tesla%20plugin...'>vercors.io@gmail.com</a> !

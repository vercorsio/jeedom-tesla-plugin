# Introduction
Bienvenue sur la page de documentation du plugin Tesla de Jeedom !

Avec ce plugin l'utilisateur peut accéder à sa voiture Tesla et interagir avec les données remontées par l'API proposée par Tesla.

Les informations proposées par Tesla peuvent être utilisées dans votre domotique et des actions peuvent être exécutées dans vos scénarios Jeedom, pour par exemple démarrer une recharge à une heure précise selon l'endroit, fermer les fenêtres s'il pleut, allumer la climatisation le matin s'il fait froid, ajuster l'ampérage de recharge selon la capacité de production de vos panneaux photovoltaïques, ....

Ce plugin propose également un panneau pour suivre sur un graphique l'évolution de l'autonomie et de l'énergie au cours d'une journée, au gré des kilomètres parcourus:


![tracking-graph](../images/consoLow480.gif)

Sur ce même panneau, vous trouverez un tableau récapitulatif des étapes de la journée (conduite, charge, parking). Il détaille les durées, consommation, vitesse, ... de chaque étape, les colonnes sont modifiables et peuvent être triées.

Une carte permet aussi de retracer l'ensemble des trajets d'une journée, de définir des favoris, de suivre à la trace votre voiture depuis l'écran de votre Tesla !

 <img src="../images/tracking-map.png" alt="map" width="804" style="border-radius:8px;"/>

Et parce que ce plugin est une composante de votre système de domotique, votre Tesla rejoint tous les équipements de votre maison. Ce qui vous permettra de les combiner entre eux pour des affichages ou des actions coordonnées.

Retrouvez la liste des nouveautés sur le [Change log](http://tesla.jeedom.free.fr/changelog).


# Connexion au compte Tesla

Après téléchargement du plugin, il suffit de l'activer et de procéder à quelques étapes de configuration:

> Depuis février 2025, Tesla rend obligatoire l'utilisation de ses propres clés pour accéder aux serveurs qui permettent de récupérer des données de ses propres véhicules et pour leur envoyer des commandes (klaxon, démarrage de charge, réveil, ouverture de coffre, ...)

La page de connexion du plugin Tesla sur votre Jeedom vous donne des informations générales et individuelles pour connecter le plugin aux serveurs Tesla

Il convient donc de créer à partir de votre propre compte Tesla un compte "API Fleet" en cliquant sur ce lien : [https://developer.tesla.com](https://developer.tesla.com/fr_FR).

Sur la page **Information sur l'application**, donnez un nom, une description et l'utilisation prévue.  Peu importe, mais évitons que tout le monde indique "Jeedom" :) 

<img src="../images/Fleet_Create1.png" alt="cnx"  style="border-radius:8px;"/>

Dans les **Informations du client** il faudra cocher *"Code d'autorisation et accès de machine à machine"* et renseigner les deux premières URLs.

 - La première est le domaine qui héberge votre jeedom. La page de connexion du plugin vous l'indiquera.
 - La seconde est une page qui vous permettra de récupérer le code d'accès, et sera `https://jeedomteslaplugin.firebaseapp.com/redirect/`
 - La troisième est optionnelle et inutile dans notre cas.

<img src="../images/Fleet_Create2.png" alt="cnx"  style="border-radius:8px;"/>

A l'étape **API et champs d'application**, cochez toutes les cases sauf les deux dernières qui correspondent à l'exploitation des équipements de production d'énergie. Le plugin Tesla a besoin des informations du véhicule, de sa localisation, et des accès aux commandes et gestion de charge. 

> Ces données restent en **local** sur votre serveur Jeedom. En aucun cas elles ne sont transmises à des tiers. En cochant ces cases vous vous autorisez à utiliser vos informations. Vous n'autorisez personne d'autre. 

<img src="../images/Fleet_Create3.png" alt="cnx"  style="border-radius:8px;"/>

Pour les **Informations de facturation**, cliquez simplement sur "Ignorer et soumettre".

> Si votre utilisation dépasse 10€ par mois (qui sont déduits des factures mensuelles) et que vous n'avez pas renseigné de moyen de paiement, Tesla se réserve le droit de désactiver votre compte.
>
> Le plugin permet de limiter l'usage de l'API pour qu'elle ne dépasse pas une certaine somme. Si vous indiquez 10€, le plugin ne contactera plus les serveurs Tesla jusqu'à la fin du mois.

<img src="../images/Fleet_Create4.png" alt="cnx"  style="border-radius:8px;"/>

Suite au remplissage de ce formulaire, vous recevrez un mail de Tesla vous indiquant que votre "application" est activée et disponible. Deux clefs seront alors disponibles à partir de ce compte Fleet API dans les détails de votre "application". Ces clefs seront à renseigner dans le panneau de connexion du plugin Tesla.

<img src="../images/Fleet_Create5.png" alt="cnx"  style="border-radius:8px;"/>

De retour dans le panneau de configuration du plugin Tesla sur votre jeedom, vous renseignerez 
 - votre *ID du client* dans `Client ID`
 - votre *Secret du client* dans `Client Secret`
 - l' *Origine(s) autorisée(s)* dans `URL d'origine autorisé`

> Ces trois données ne doivent en aucun cas être transmises à un tiers.

Après avoir renseigné ces données vous aurez accès au bouton **Récupérer mon code d'authentification** nécessaire pour accéder à votre compte Tesla.


![config](../images/configPlugin-1.png)

Pour permettre au plugin d'interagir avec votre Tesla, un **code d'authentification** doit être renseigné. Ce code est fourni exclusivement par Tesla (depuis janvier 2024). Pour l'obtenir, il faut cliquer sur le lien "Récupérer mon code d'authentification" présent dans la section "Connexion" du panneau de configuration du plugin.

Ce lien vous amène sur le site auth.tesla.com, où vous devrez vous identifier sur votre compte Tesla pour autoriser le plugin Tesla de Jeedom à accéder à vos véhicules, récupérer des informations et jouer des commandes :

<img src="../images/tesla_cnx1.png" alt="drawing"  style="border-radius:8px;"/>

Accordez au plugin Tesla de Jeedom l'accès à vos informations de profil, de véhicule, aux commandes du véhicule et à la gestion de la recharge du véhicule. Ne pas cocher l'un de ces éléments peut amener le plugin à ne pas avoir un fonctionnement optimal.

> Note: Jeedom étant hébergé sur votre propre serveur, vous seul aurez accès aux données qui seront stockées localement chez vous.

<img src="../images/tesla_rights.png" alt="drawing"  style="border-radius:8px;"/>

Après avoir accordé les droits au plugin Tesla, "Jeedom Tesla Plugin" sera ajouté à la liste de vos Applications tierces. En cliquant sur "Gérer", vous pourrez supprimer le lien. Dès lors le plugin n'aura plus accès à vos véhicules. Il faudra recliquer sur "Récupérer mon code d'authentification".

<img src="../images/tesla_appTierces.png" alt="drawing"  style="border-radius:8px;"/>

Le code d'authentification est affiché sur une page dédiée qui n'est utilisée que pour ce but. Copiez ce code (en cliquant sur l'icône à droite du code affiché) et collez-le dans le panneau de configuration du plugin sur votre Jeedom.

> Note: Ce code est à usage unique. Il est inutile de le conserver. Le plugin ne l'enregistre pas. Il sert simplement à obtenir les premiers jetons d'authentification.

<img src="../images/tesla_code.png" alt="drawing"  style="border-radius:8px;"/>

Cliquez ensuite sur "CONNEXION" et le plugin va obtenir deux jetons :

  * le **jeton d'accès** : il est utilisé par le plugin dans ses échanges avec les serveurs Tesla. Ce jeton est valide 8 heures.
  * le **jeton de rafraichissement** : il permettra au plugin de remplacer automatiquement le **jeton d'accès** quand il expire, et d'obtenir un nouveau jeton de rafraichissement.


![config](../images/configPlugin-2.png)

> **Note**
>
>  - Le plugin nécessite que votre Tesla soit accessible sur le réseau pour que la configuration se passe correctement. Assurez-vous que la voiture soit réveillée au moment de l'activation du plugin.
>  - Si l'application Tesla sur votre smartphone arrive à se connecter à votre Tesla, le plugin sera à même de configurer correctement votre Tesla dans Jeedom.
>  - Le plugin Tesla de Jeedom **ne nécessite pas** les identifiants de votre compte Tesla. Ne les transmettez à personne.


## Appairage (requis pour les Tesla récentes)

Tesla a mis à jour début 2024 ses serveurs en introduisant les *Commandes Signées*. C'est un nouveau mode de connexion qui augmente encore la sécurisation des commandes envoyées au véhicule. Si les commandes ne s'exécutent pas depuis Jeedom et/ou que vous trouvez un message d'erreur dans les logs contenant `unsigned_cmds_hardlocked`, il est probable que vous ayez à démarrer le Serveur Proxy.


La mise en œuvre est simple. 
   1. Depuis le panneau de configuration du véhicule, démarrez ce Serveur Proxy sur un port défini (4443 par défaut).
   2. Cliquez sur le bouton "Appairage de la Tesla". Un QR Code sera affiché, celui-ci, après avoir été scanné ouvrira l'application Tesla de votre smartphone (iOS ou Android) et vous demandera de choisir un véhicule compatible avec les commandes signées pour y ajouter la clef qui permettra de sécuriser l'envoi des commandes.
   3. Envoyez des commandes (ouverture de coffre, activation de la climatisation, klaxon, ....), celles-ci seront transmises au Serveur Proxy démarré localement qui les signera avant de les envoyer à la voiture via les serveurs Tesla. 


![config](../images/configCar-pairing.png)

> **Note**
>  - Vous pourrez également arrêter le serveur depuis la page de configuration de la voiture.
>  - Le plugin détecte automatiquement si votre véhicule nécessite l'envoi de commandes signées (et donc le Serveur Proxy). Si au moment où une commande doit être envoyée le serveur est arrêté, Jeedom va tenter de le redémarrer.
>  - Le code du Serveur Proxy est fourni par Tesla
>  - la clef privée ajoutée dans votre Tesla lors de l'appairage peut être supprimée depuis l'écran de votre Tesla (Menu Sécurité, dans la liste des cartes d'accès au véhicule)

Le diagramme ci-dessous est disponible dans la documentation du [Serveur Proxy](https://github.com/teslamotors/vehicle-command). Dans le contexte du plugin Jeedom, il faut lire :
 - `Your Backend`: c'est le code du plugin Jeedom qui envoie des commandes au Serveur Proxy
 - `Vehicule Commands Proxy` est le Serveur Proxy démarré sur le port 4443. Il s'occupe de signer la commande et l'envoie aux Serveurs Tesla.
 - `Fleet API` est le nom de la nouvelle API Tesla présente sur les Serveurs Tesla
 - `Vehicle`, c'est votre Tesla 
![config](../images/request_diagram.png)


## Tesla virtuelles

Pour tester le plugin sans connexion à votre compte Tesla, ou si vous n'avez pas (encore) de Tesla, le plugin offre la possibilité de créer des équipements virtuels correspondant à des Tesla __Model 3__,  __Model Y__, __Model S__ et/ou __Model X__.

Il suffira de cliquer sur le bouton __"Ajouter des Tesla virtuelles"__. Des jeux de données correspondant à des véhicules réels seront utilisés pour créer des équipements virtuels. Bien entendu toute action (chauffage/charge/déverrouillage) sur ces équipements sera sans effet, mais ils feront bonne figure dans votre interface Jeedom.

## Déconnexion

Une fois connecté, le plugin affiche un bouton de déconnexion qui fermera la connexion ouverte. Les jetons d'accès seront revoqués auprès des serveurs Tesla. Le plugin ne sera plus fonctionnel. Pour reconnecter, il faudra à nouveau récupérer un code d'authentification.

# Configuration du plugin

Après connexion, le plugin pourra se connecter aux serveurs Tesla et récupérera la ou les Tesla associées à votre compte pour créer les "équipements" Jeedom automatiquement.

Le bouton __"Synchroniser mes voitures"__ permet d'effectuer une recherche manuelle et ajoutera un équipement Jeedom pour chaque véhicule Tesla non encore créé. Cela permet également de mettre à jour les équipements associés à vos Tesla après une mise à jour du plugin.

## Démon
Le suivi de l'autonomie repose sur des jeux de données acquises via l'API des serveurs Tesla. L'acquisition de ces données est effectuée par un script qui doit tourner en arrière-plan. Son démarrage se pilote depuis le panneau de contrôle du plugin. Il est recommandé d'activer la **Gestion Automatique** pour que Jeedom le redémarre s'il s'arrête.

![config](../images/tesla-daemon.png)

## Tracking

Pour accéder aux panneaux de suivi de l'autonomie (également appelé "tracking"), il suffit de cocher `Afficher le panneau desktop` et `Afficher le panneau mobile`:

![config](../images/configPlugin-4.png)

Une fois cochées et après rechargement de la page, un sous-menu "Tesla" apparaît dans le menu "Accueil". Il conduit alors au tracking :

![config](../images/tracking-flex-columns.png)



## Autres paramètres de configuration

- **Coût du kWh** (en euro) : Nécessaire pour calculer approximativement le coût d'une charge, le prix pour parcourir 100km et le nombre de km que l'on peut faire avec 1 euro. La valeur par défaut est `0.14`.
- **Client ID** et **Client Secret** : les deux clefs personnelles de votre "application" créée sur [developer.tesla.com](https://developer.tesla.com) (voir [Connexion au compte Tesla](#connexion-au-compte-tesla)). Elles sont nécessaires pour accéder à l'API Fleet de Tesla et ne doivent jamais être partagées.
- **cronHourly** : S'il est activé, une fois par heure, le plugin fait une mise à jour des données du widget. Quand le tracking est actif, les données du widget sont mises à jour au fil de l'eau.
- **Région** : le serveur Tesla régional utilisé par le plugin (Amérique du Nord/Asie, Europe/Moyen-Orient/Afrique, Chine). Il est mis à jour automatiquement à la connexion du compte. À modifier uniquement si l'erreur _Account must be registered in the current region_ apparaît dans les logs.
- **Nombre de tentatives pour réveiller le véhicule** et **Nombre de secondes entre deux tentatives** : 3 tentatives espacées de 5 secondes par défaut. Utilisés par la commande **Réveiller** et par le réveil automatique avant l'envoi d'une commande.
- **Coût du kWh** et **devise** : la devise dans laquelle est exprimé le prix du kWh.
- **Coût mensuel** (API Fleet) : le montant maximal que vous acceptez que Tesla facture chaque mois pour l'usage de ses serveurs. Quand le coût estimé par le plugin atteint ce seuil, l'info **Info seuil mensuel atteint** passe à `1` et le plugin ne contacte plus les serveurs Tesla jusqu'à la fin du mois. Voir aussi la fenêtre [Fleet API](#fleet-api).
- **Encours estimé** : l'encours du mois relevé sur votre [Dashboard Tesla](https://developer.tesla.com/fr_FR/dashboard), à une date et une heure données. Le coût estimé par le plugin part de cet encours et ignore les appels enregistrés avant cette date. Le bouton **Effacer l'encours** le remet à zéro.
- **Clé API Maptiler** : nécessaire pour traduire les lieux de parking en adresses physiques et afficher les cartes (tracking, fenêtre Planifier).
- **Pays par défaut** : sur les adresses résolues, le pays n'est affiché que s'il est différent de cette valeur.
- **Thème sombre** : active un thème sombre pour le panneau de tracking, séparément en Desktop et en Mobile.
- **Suivi d'autonomie** : les intervalles entre deux appels selon le mode du tracking, le temps d'attente au parking et la période du SOMMEIL NUIT. Voir [Configuration et impact du tracking](#configuration-et-impact-du-tracking). Le bouton **Rétablir les valeurs par défaut** remet ces réglages à leur valeur d'origine.
- **Scinder un trajet en deux** : quand la voiture traverse une zone sans réseau (un parking souterrain par exemple) puis se gare, elle peut réapparaître alors qu'elle roule déjà. Le tracking coupe alors le trajet en deux si la durée _et_ la distance entre deux mesures successives dépassent les valeurs configurées.
- **Consolidation des données** : supprime de la base les points et parkings orphelins.


# Outils du plugin

En haut de la page du plugin, à côté des liens **Aide** et **FAQ**, trois boutons ouvrent des fenêtres dédiées.

## Fleet API

La fenêtre **Fleet API** affiche une estimation du coût des appels faits par le plugin aux serveurs Tesla, par année, par mois et par jour, avec des graphiques du coût cumulé par rapport au seuil mensuel configuré. Les appels sont classés par type : données, commandes, sorties de veille et transmission de signaux.

L'**encours estimé** peut aussi être saisi depuis cette fenêtre (voir [Autres paramètres de configuration](#autres-paramètres-de-configuration)).

> **Notes**
>
> - Seules les requêtes envoyées par le plugin Tesla de Jeedom sont comptabilisées. Les appels faits par d'autres applications avec vos clés n'apparaissent pas.
> - L'estimation ne tient pas compte de la remise mensuelle de 10€ accordée par Tesla.
> - Le coût réel est consultable sur votre [Dashboard Tesla](https://developer.tesla.com/fr_FR/dashboard). Ajustez l'encours en conséquence.

## Recharges

La fenêtre **Recharges** liste vos sessions de recharge aux Superchargeurs Tesla :

- regroupement par **année**, par **mois** ou par **jour** ;
- filtres par véhicule, par pays, par période (avant / après une date) et recherche libre (lieu, véhicule...) ;
- totaux, moyennes et extrêmes (session la plus longue, coût et énergie maximum) sur les sessions filtrées ;
- téléchargement de la facture PDF de chaque session.

Les montants facturés dans une autre devise sont convertis et affichés en euros.

## Planifier

La fenêtre **Planifier** permet de gérer, directement depuis Jeedom, les plages programmées de votre Tesla :

- **Recharge** : heure de début et/ou heure de fin de la recharge ;
- **Préconditionnement** : heure à laquelle l'habitacle doit être prêt.

Chaque plage est affichée sous forme de carte, avec son lieu sur la carte en haut de la fenêtre. Pour chaque plage, il est possible de :

- l'activer ou la désactiver ;
- choisir les jours de la semaine et la répéter chaque semaine ;
- modifier ses horaires (icône crayon) ;
- déplacer son marqueur sur la carte pour changer le lieu où elle s'applique ;
- la supprimer (après confirmation).

Les boutons **+ Recharge** et **+ Préconditionnement** ajoutent une nouvelle plage.

> **Note**
>
> Les plages sont lues et écrites directement dans la voiture : elle doit être en ligne. Le plugin vérifie qu'elle l'est avant de rechercher les plages programmées.



# Configuration du véhicule

Une fois le plugin configuré, le ou les véhicules de votre compte Tesla sont ajoutés.

 <img src="../images/configPlugin-3.png" alt="config" width="804" style="border-radius:8px;"/>

 Un lien **Documentation** permet d'afficher cette documentation, et un lien **Aide** apporte un premier niveau d'aide en cas de besoin.

Pour configurer le véhicule, il suffit de cliquer sur son image. Il sera alors possible de l'activer, le rendre visible et l'attacher à un objet parent (ici le Garage) :

 <img src="../images/configCar-1.png" alt="config" width="804" style="border-radius:8px;"/>

 * __Vehicle Identification Number (VIN)__ : Champ obligatoire qui permet d'identifier de manière unique votre véhicule pour interagir avec les serveurs Tesla.
 * __Capacité batterie__ : La capacité "commerciale" de la batterie en kWh
 * __Autonomie__ : le nombre de kilomètres qu'il est possible de parcourir avec 100% d'autonomie. Vous pouvez choisir de laisser le plugin estimer le nombre de kilomètres qu'il est possible de faire avec un 'plein' (cocher alors "estimer").
 * __Consommation typique__ : En théorie, c'est le rapport entre `Capacité batterie x 1000 / Autonomie`. Ajustable selon ses propres constatations.
 * __Affichage__ : L'affichage par défaut du Suivi de l'Autonomie. Choix : `Energie` ou `Distance`.

Et vous pourrez également choisir une image pour votre voiture.


# Liste des commandes et des actions du véhicule
Les commandes d'info et d'action associées à chaque Tesla sont les suivantes

 <img src="../images/configCar-2.png" alt="config" width="804" style="border-radius:8px;"/>

## Commandes de type **info**

| Commande   |   Description |
| --- | --- |
| **Photo** | Affiche une photo de la Tesla, ainsi que le badge (70D, P85D, ...).
| **Info véhicule** | Affiche un titre et un sous titre correspondant à l'état actuel de la voiture. Par exemple _Conduite 67km_, _Recharge planifiée à 22h50_, _Stationnée_, _Supercharge_, ...
| **Info état vehicule** | État de la voiture déterminé par le tracking : `driving`, `charging` ou `parking`.
| **Info réveillée** | Indique si le véhicule est en mode veille (0) ou en ligne (1).
| **Info date dernière mise à jour** | Date des dernières données remontées par la voiture.
| **Dernière mise à jour** | Timestamp de la dernière synchronisation horaire avec les serveurs Tesla.
| **Odomètre** | Indique la valeur du compteur kilométrique (miles ou km).
| **Info vitesse** | La vitesse de la voiture (en km/h). Négative en marche arrière.
| **Info selecteur de vitesses** | Indique P R N ou D.
| **Info autonomie** | Indique l'autonomie typique (en km ou miles) de la voiture.
| **Info autonomie nominale** | Indique l'autonomie nominale (en km ou miles) de la voiture.
| **Info niveau de batterie** | Indique le pourcentage de la batterie.
| **Détail autonomie** | Affiche un graphe de la batterie
| **Info recharge** | Indique si la voiture est en train de charger ou non. Les valeurs possibles sont  { `Charging`, `Stopped`, `Disconnected`, `Complete`, `Scheduled`, `Driving` }.
| **Info cable connecté** | Indique si le câble de recharge est connecté.
| **Info trappe de recharge** | Indique si la trappe de recharge est ouverte (1) ou fermée (0).
| **Info limite de recharge** | Indique le pourcentage à atteindre à la fin d'une recharge.
| **Info puissance de recharge** | Indique la puissance de recharge (en kW).
| **Info tension de recharge** | Indique la tension de recharge (en volts).
| **Info ampérage de recharge** | Indique l'intensité de charge réelle (en ampères).
| **Info ampérage demandé** | Indique l'intensité de charge demandée à la voiture (en ampères). Modifiable avec **Contrôler l'ampérage de la recharge**.
| **Info ampérage maximum** | Indique l'intensité maximale que peut fournir la borne (en ampères).
| **Info durée de recharge estimée** | Indique l'estimation de la durée restante de charge (en minutes).
| **Info heure de départ de recharge** | Indique l'heure (format Hmm) à laquelle la charge est censée débuter.
| **Info heure de fin de recharge** | Indique l'heure (format Hmm) à laquelle la charge est censée se terminer.
| **Détail de la recharge** | Affiche les données issues de la recharge.
| **Info climatisation** | Indique si la climatisation est allumée ou éteinte.
| **Info température habitacle** | Indique la température à l'intérieur du véhicule.
| **Détail de la climatisation** | Affiche les paramètres de climatisation (conducteur, passager, intérieur et extérieur).
| **Info verrouillage** | Indique si la voiture est fermée ou ouverte.
| **Info frunk** | Indique si le coffre avant (frunk) est fermé ou ouvert.
| **Info trunk** | Indique si le coffre arrière est fermé ou ouvert.
| **Info fenêtres** | État des 4 fenêtres (avant conducteur, avant passager, arrière passager, arrière conducteur) : une lettre par fenêtre, `F` si elle est fermée, `P` si elle est partiellement ouverte (entrouverte), `O` si elle est ouverte. Exemples : `FFFF` toutes fermées, `PPPP` toutes entrouvertes. _Uniquement si le véhicule remonte l'état de ses fenêtres._
| **Info toît ouvrant** | Indique le pourcentage d'ouverture du toit panoramique. _Uniquement pour les véhicules équipés._
| **Info sentinelle** | Indique si le mode sentinelle est activé (1) ou non (0). _Uniquement pour les véhicules équipés._
| **Info mise à jour logicielle** | Statut de la mise à jour logicielle en attente (par exemple `available`, `scheduled`, `downloading`, `installing`). Vide si aucune mise à jour n'est proposée.
| **Détail logiciel** | Version logicielle actuelle de la voiture et mise à jour proposée.
| **Info latitude** / **Info longitude** | Position GPS de la voiture.
| **Info date de géolocalisation** | Timestamp de la dernière position GPS connue.
| **Info s'approche de** | Nom du favori duquel se rapproche la voiture.
| **Info s'éloigne de** | Nom du favori duquel s'éloigne la voiture.
| **Info date dernier franchissement** | Timestamp qui indique l'heure à laquelle la frontière du dernier favori a été franchie.
| **Info éloigné de** | Favori choisi avec l'action **Calculer la distance**.
| **Info distance** | Distance (en mètres) entre la voiture et le favori choisi avec l'action **Calculer la distance**. Mise à jour à chaque changement de position.
| **Info suivi d'autonomie** | Indique si le suivi de l'autonomie (tracking) est démarré (1) ou arrêté (0).
| **Info mode du tracking** | Mode actuel du tracking : `NORMAL`, `ADJUST`, `PARKING_DAY` (SOMMEIL JOUR), `PARKING_NIGHT` (SOMMEIL NUIT), `DATA` (voiture hors ligne), `SYNC`, `OFF`, ou `REACHED` quand le seuil mensuel de coût de l'API est atteint.
| **Info seuil mensuel atteint** | Passe de `0` à `1` quand le coût estimé de l'API Fleet atteint le seuil mensuel configuré dans le plugin. Le plugin ne contacte alors plus les serveurs Tesla jusqu'à la fin du mois.
| **Détail data** | Pour debug - affiche un buffer encodé en base64 débarrassé de toute info personnelle (VIN/id/GPS/...). Renseigné uniquement quand les logs du plugin sont en niveau `debug`.

## Commandes de type **action**

| Commande   |   Description |
| --- | --- |
| **Contrôler la recharge** | Va permettre de démarrer, interrompre, permuter ou estimer la charge si le câble de recharge est engagé. Valeurs : `Arrêter`, `Démarrer`, `Permuter`, `Estimer`.
| **Contrôler la limite de recharge** | Va permettre de définir un pourcentage de charge à atteindre.
| **Contrôler la trappe de charge** | Va permettre d'ouvrir/fermer la trappe de recharge.
| **Contrôler l'ampérage de la recharge** | Va permettre de préciser l'intensité du courant de charge (min 5A).
| **Contrôler l'heure de fin de recharge** | Va permettre de définir l'heure (format Hmm) à laquelle la charge devra se finir.
| **Contrôler la climatisation** | Va permettre d'allumer ou d'arrêter la climatisation.
| **Contrôler la température** | Va permettre de définir une température dans l'habitacle (conducteur/passager).
| **Contrôler le chauffage du siège conducteur** / **passager** | Va permettre de régler le chauffage du siège : `Arrêter`, `Faible`, `Moyen`, `Fort`. _Uniquement pour les véhicules équipés._
| **Contrôler le chauffage du siège arr gauche** / **arr central** / **arr droit** | Idem pour les sièges arrière. _Uniquement pour les véhicules équipés._
| **Contrôler le chauffage du siège coffre gauche** / **coffre droit** | Idem pour la troisième rangée de sièges. _Uniquement pour les véhicules équipés._
| **Contrôler le chauffage du volant** | Va permettre d'allumer ou d'éteindre le volant chauffant. _Uniquement pour les véhicules équipés._
| **Contrôler le verrouillage** | Va permettre de verrouiller ou déverrouiller la voiture.
| **Contrôler le coffre avant** | Va permettre d'ouvrir le coffre avant (frunk).
| **Contrôler le coffre arrière** | Va permettre d'ouvrir ou fermer le coffre arrière (trunk).
| **Contrôler les fenêtres** | Va permettre d'entrouvrir ou fermer les fenêtres. `Permuter` ferme les fenêtres si elles sont toutes entrouvertes (`PPPP`), et les entrouvre sinon.
| **Actionner les phares** | Va actionner les phares
| **Actionner le klaxon** | Va actionner l'avertisseur sonore
| **Contrôler le mode sentinelle** | Va permettre de démarrer/arrêter le mode sentinelle. _Uniquement pour les véhicules équipés._
| **Contrôler le toît ouvrant** | Va permettre d'entrouvrir ou de fermer le toit panoramique. _Uniquement pour les véhicules équipés._
| **Contrôler le suivi de l'autonomie** | Va permettre de démarrer ou arrêter le suivi de l'autonomie. Valeurs : `Arrêter`, `Démarrer`, `Permuter`, `Accélérer` (repasser en mode NORMAL), `Ralentir` (passer en mode SOMMEIL).
| **Contrôler le tracking** | Bouton du widget pour le tracking. Si la **Gestion Automatique** du démon est activée, il accélère ou ralentit le tracking ; sinon il le démarre ou l'arrête.
| **Calculer la distance** | Va permettre de choisir un favori. La distance entre la voiture et ce favori est alors remontée dans **Info distance**.
| **Rafraichir** | Mise à jour de la tuile sur clic de l'icone.
| **Réveiller** | Force le réveil de la voiture (par défaut 3 tentatives espacées de 5s, configurable dans le panneau de configuration du plugin). Met à jour la valeur de **Info réveillée**. Inutile avant une commande d'action : le plugin réveille automatiquement la voiture si nécessaire.

> **Tip**
>
> Chacune de ces actions peut être intégrée dans un scénario Jeedom.
>
> Le format **Hmm**, est utilisé dans les blocs d'action des scénarios qui permettent de programmer une heure de début d'action. Exemples:
>  - `2305` indique 23h05,
>  - `18` indique 00h18,
>  - `1200` indique 12h00,
>  - `1210` indique 12h10,
>  - `121` indique 1h21
>

# Affichage du véhicule

La plupart des commandes listées ci-dessus a un template spécifique qui lui est attribué, et qui permet d'obtenir par défaut l'affichage d'un véhicule tel qu'illustré sur l'image:

### Version Desktop

![config](../images/displayCar-2.png)

### Version Mobile

![config](../images/mobileWidget.gif)

Par exemple pour ne pas afficher la photo et les détails de climatisation, il suffit pour un véhicule donné de décocher `"Affichage"` dans la ligne correspondante de la configuration de ces commandes.

L'odomètre est historisé, ce qui permet d'obtenir le graphique des km parcourus.

Par défaut, le widget est mis à jour toutes les heures. Il est possible de désactiver cette mise à jour en décochant "Activer" en face de "cronHourly"

![cronHourly](../images/widget-cronHourly.png)

## Contrôler la climatisation, les sièges et le volant chauffants

| Bouton | Description | Un clic sur ce bouton va ... |
| --- | --- | --: |
| ![clim off](../images/clim_off.png) | La climatisation est éteinte | _... allumer la climatisation_ |
| ![clim on](../images/clim_on.gif) | La climatisation est allumée | _... éteindre la climatisation_ |
| ![heaters on](../images/seat_heaters_on.png) | Le volant ou un des sièges chauffants est allumé | _... ouvrir le panneau de contrôle des sièges chauffants_ |
| ![heaters off](../images/seat_heaters_off.png) | Aucun des sièges chauffants ni le volant n'est allumé | _... ouvrir le panneau de contrôle des sièges chauffants_ |

Il est possible de modifier la température cible de la climatisation en utilisant un widget spécifique, comme décrit dans l'animation ci-dessous:


![clim on](../images/setTemps.gif)

Après avoir cliqué sur l'icône de siège, il est possible de contrôler le niveau de chauffage des sièges et du volant. Le nombre de rangées affiché dépend de la configuration du véhicule. Également, si le volant est chauffant, il est activable via ce panneau de contrôle.

Le bouton OFF permet de tout éteindre. Le bouton OK permet de valider les choix faits pour chacun des sièges et du volant:


![heaters](../images/SeatHeaters.gif)


> **Notes**
>
> A cause d'une limitation dans l'API Tesla, il n'est possible de configurer des températures différentes pour le conducteur et le passager que lorsque les températures sont déjà non synchronisées dans le véhicule (SYNC désactivé).
>
> L'accès aux sièges chauffants n'est possible que si la climatisation est allumée.


## Contrôler le verrouillage (portes, coffres, toit ouvrant et sentinelle)

| Bouton | Description |  Un clic sur ce bouton va ... |
| --- | --- | --: |
| ![lockOn](../images/locked.png) | La voiture est fermée | _... déverrouiller les portes_ |
| ![lockOff](../images/unlocked.png) | La voiture est ouverte | _... verrouiller les portes_ |
| ![frunkOff](../images/frunk_off.png) | Le coffre avant est fermé | _... ouvrir le frunk_ |
| ![frunkOn](../images/frunk_on.png) | Le coffre avant est ouvert | _... être sans effet_ |
| ![trunkOff](../images/trunk_off.png) | Le coffre arrière est fermé | _... ouvrir le coffre_ |
| ![trunkOn](../images/trunk_on.png) | Le coffre arrière est ouvert | _... fermer le coffre_ |
| ![panoOff](../images/pano_off.png) | Le toit panoramique est fermé | _... ouvrir le toit panoramique_ |
| ![panoOn](../images/pano_on.png) | Le toit panoramique est ouvert | _... fermer le toit panoramique_ |
| ![sentryOff](../images/sentry_off.png) | Le mode sentinelle est désactivé | _... activer le mode sentinelle_ |
| ![sentryOn](../images/sentry_on.gif) | Le mode sentinelle est activé | _... désactiver le mode sentinelle_ |

## Contrôler la charge

| Bouton | Description |  Un clic sur ce bouton va ... |
| --- | --- | ---: |
| ![charDis](../images/charging_Disconnected.png) | Le câble de charge n'est pas branché | _... être sans effet_
| ![charSch](../images/charging_Scheduled.png) | La recharge est programmée | _... démarrer la recharge_
| ![charCha](../images/charging_Charging.gif) | La recharge est en cours | _... stopper la recharge_
| ![charPau](../images/charging_Pause.png) | La recharge a été manuellement arrêtée | _... reprendre la recharge_
| ![charCom](../images/charging_Complete.png) | La recharge est terminée | _... être sans effet_
| ![charNul](../images/charging_Null.png) | État de recharge indéterminé | _... être sans effet_
| ![trappe](../images/trappe.png) | Trappe de recharge | _... fermer/ouvrir la trappe de recharge_ |

## Contrôler le suivi de l'autonomie

| Bouton | Description |  Un clic sur ce bouton va ... |
| --- | --- | ---: |
| ![track](../images/tracking_off.png) | Le suivi de l'autonomie est arrêté | _... démarrer le suivi de l'autonomie_
| ![track](../images/tracking_on.gif) | Le suivi de l'autonomie est démarré | _... arrêter le suivi de l'autonomie_
| ![track](../images/tracking_sommeil_jour.gif) | Le suivi de l'autonomie est démarré en mode SOMMEIL jour| _... arrêter le suivi de l'autonomie_
| ![track](../images/tracking_sommeil_nuit.gif) | Le suivi de l'autonomie est démarré en mode SOMMEIL nuit| _... arrêter le suivi de l'autonomie_

> **Note**
>
> - Si dans la configuration du plugin la **Gestion Automatique** du démon est activée, Jeedom cherchera à redémarrer le démon s'il est arrêté. Vous pouvez donc laisser Jeedom garantir que le `tracking` est actif en permanence (**Gestion Automatique**) ou le démarrer et l'arrêter manuellement.
> - Si la **Gestion Automatique** du démon est désactivée, il suffit de tenir appuyé sur le bouton du tracking au moins 5 secondes pour voir apparaître le bouton __STOP__.

Pour modifier depuis le dashboard la limite de charge, il suffit de déplacer le curseur sur le graphe de la batterie. Le pourcentage ainsi que le nombre approximatif de kilomètres seront affichés:

![setLimit](../images/setChargingLimit.gif)

# Santé

Pour s'assurer que le plugin Tesla est bien configuré, un ensemble de vérifications est joué lorsqu'on ouvre l'écran **Santé** (menu Analyse / Santé).

![setLimit](../images/sante.png)

> **Note**
>
> Si un problème de permission est détecté, il sera corrigé.


# Scénarios

Exemples de scénarios:

* Modifier le seuil de recharge à son maximum :
  <img src="../images/scenario_setChargeLimit_100.png" alt="scenario set limit" width="804" style="border-radius:8px;"/>


* Réveiller la voiture et mettre le seuil de charge à 90% et activer la climatisation si la température de l'habitacle est inférieure à 14°C :

  <img src="../images/scenario_Climate.png" alt="scenario climate" width="804" style="border-radius:8px;"/>

  > Depuis la version 3.3.12, le plugin réveille automatiquement la voiture avant d'envoyer une commande. L'action **Réveiller** reste utile pour lire des infos à jour (ici la température de l'habitacle) avant de décider d'une action.

* Programmer le départ de la charge pour que la voiture ait 90% de batterie à 7h00 !
  <img src="../images/scenario_getStartTime.png" alt="scenario startTime" width="804" style="border-radius:8px;"/>

> **Note**
>
> Pour connaître l'heure de début de la recharge, il faut démarrer la charge avec l'action 'estimer' qui va démarrer une courte charge pour estimer le temps nécessaire pour la recharge.
>
> Si la voiture n'est pas prête pour la charge, la commande **Info heure de départ de recharge** retourne `N/A`.
>
> Si le temps estimé est inférieur au temps qui sépare le moment où la commande est lancée et l'heure de fin de recharge, la commande **Info heure de départ de recharge** retourne l'heure au format `Hmm` à laquelle la charge pourra être lancée.
>
> S'il n'y a pas assez de temps pour atteindre le pourcentage voulu à l'heure programmée, la commande **Info heure de départ de recharge** indique l'heure de départ précédée du signe `-`.
>
> Exemples si l'on souhaite avoir la voiture chargée à **90%**  pour **7h du matin** :
> - il est 22h30, le scénario est lancé, la recharge demande **5 heures et 30 minutes** : la commande **Info heure de départ de recharge** retourne `130`  (soit démarrage de la charge conseillé à 1h30).
> - il est 22h30, le scénario est lancé, la recharge demande **12 heures** : la commande **Info heure de départ de recharge** retourne `-1900`  (soit démarrage de la charge conseillé à 19h, mais il est trop tard !)

# Suivi de l'autonomie

Note: Le *Suivi de l'autonomie* est aussi appelé *Range Tracking* ou simplement *tracking*.

## Principe

Le panneau **suivi de l'autonomie** permet au conducteur de comprendre l'influence de sa conduite et de l'environnement sur l'autonomie du véhicule, pour chacune des Tesla activées dans votre Jeedom.

Cela permet de comprendre comment évolue l'autonomie restante au fil des trajets, des charges et temps de repos, ou de voir l'énergie consommée lors des trajets, et l'énergie emmagasinée lors de recharges.

Ce 'tracking' s'appuie sur des données acquises depuis les serveurs Tesla via un démon qui est démarré et arrêté depuis le panneau. Les données sont stockées en **local** sur votre serveur Jeedom.

Un graphique retrace l'évolution de l'autonomie ou de l'énergie au cours d'une journée et un calendrier permet de consulter l'historique des graphiques.

> **Notes**
>
> * Pratique, la version mobile permet de suivre l'évolution de l'autonomie ou de l'énergie tout en conduisant !
>
> * Pour accéder directement à la vue `Tesla` depuis la version Mobile sans jongler avec les menus, il est possible de définir `Tesla` comme vue "Mobile" par défaut dans la configuration du profil (Menu `User` -> `Profil Admin` -> Onglet `Interface`)
>
> * Le suivi de l'autonomie peut être programmé via un scénario.



## Configuration et impact du tracking

![tracking-graph](../images/tracking-settings.png)

Lorsque le véhicule roule ou est en charge, les graphs permettent de donner une idée très précise de l'évolution de l'autonomie. En revanche, à l'arrêt au parking, il n'est pas nécessaire de monitorer aussi finement l'état de la voiture.

Passé un certain laps de temps (`temps d'attente au parking`) le tracking ralentit son rythme et espace les différents appels, passant par défaut d'un appel toutes les 60 secondes lors du roulage (180 secondes lors des recharges) à un appel toutes les 15 minutes (`SOMMEIL JOUR`) laissant la possibilité à la voiture d'entrer en veille. La nuit, ce rythme décroit encore plus puisqu'il passe à un appel toutes les trente minutes (`SOMMEIL NUIT`).
Ces intervalles de temps sont configurables, ainsi que les heures de début et de fin de la période de `SOMMEIL NUIT`

Quand la voiture se remet à rouler/charger, le prochain appel va détecter ce changement d'état et fera passer le tracking en mode `NORMAL`, pour garantir un suivi régulier du tracking.

### Considérations techniques
Tesla propose sur son API deux appels d'interrogation du véhicule:
 - un appel nommé `vehicle` qui indique simplement l'état de la voiture : `online`, `offline`, `asleep`, `waking` et `unknown`. Cet appel n'est pas intrusif, il ne rentre pas en contact avec la voiture. `online` indique que la voiture roule, charge, télécharge une mise à jour, effectue une opération interne de service.... Mais elle peut tout à fait être `online` au parking. Et, sans être sollicitée pendant un certain temps au parking, elle pourra automatiquement rentrer dans une phase de sommeil (`offline`/`asleep`). Hélas, sur cet appel, il n'y a pas de distinguo entre un `online "actif"` (roulage, charge, ...), et un `online "inactif"` (au parking en attente d'un prochain sommeil), ce qui permettrait de détecter la phase de pré-sommeil.
- un appel nommé `data` qui remonte toutes les données pertinentes et à jour sur le véhicule. Cet appel `data` n'est possible que lorsque la voiture est `online`. Solliciter trop fréquemment cet appel `data` empêche la voiture de passer `offline`.

Avant chaque appel `data` le tracking effectue un appel `vehicle`. Si ce dernier remonte un état `offline` ou `asleep`, le tracking laisse la voiture dans son sommeil et ne va pas effectuer d'appel `data`. Dans le cas contraire (`online`) le tracking effectue l'appel `data` et stocke un nouveau jeu de données qui sera utilisé pour les graphs et les statistiques.


## Mise en place
Par défaut, l'acquisition n'est pas démarrée.

Un clic sur `Start Recording` va démarrer le démon qui va récupérer à intervalles réguliers les données qui serviront à afficher des graphiques de suivi, identifier les différentes étapes de la journée et proposer des statistiques.

Un clic sur `Stop Recording` va stopper l'acquisition des données (arrêt du démon).

Lorsque le démon est en mode **Gestion Automatique**, il n'est pas possible d'interagir manuellement pour arrêter/démarrer le démon.

> **Notes**
>
> Lors de l'acquisition et si le graphe affiché est le graphe du jour, l'affichage bascule automatiquement en mode `live`, et affiche en temps réel les dernières données acquises.
>
> Au premier lancement, il peut se passer plusieurs minutes avant que des données soient effectivement disponibles pour l'affichage.

## Exemple affichage __distance__
L'exemple ci-dessous retrace un trajet réel effectué le 5 janvier 2019, qui se découpe principalement en 4 segments :
- <code>km  0</code> à <code>km 15</code>: route départementale sur du plat - _altitude 'en haut': 1100m._
- <code>km 15</code> à <code>km 30</code>: route départementale en descente -  _altitude 'en bas': 250m._
- <code>km 30</code> à <code>km 50</code>: autoroute.
- <code>km 50</code> à <code>km 65</code>: route départementale - _altitude à l'arrivée: 500m._

 <img src="../images/tracking-graph.png" alt="tracking graph" width="804" style="border-radius:8px;"/>


- En abscisse on trouve le temps
- En ordonnée à gauche en <b>noir</b>, le kilométrage parcouru. <u>Note:</u> l'angle de la courbe est proportionnel à la vitesse.
- En ordonnée à gauche en <b style='color:#22C4FF'>bleu</b>, l'autonomie de départ en <b style="color:#3355FF">pointillé</b>, et l'évolution de l'autonomie en <b style='color:#22C4FF'>bleu</b>. Quand la climatisation est allumée, le trait est en <b style='color:blueviolet'>violet</b>.
 - En ordonnée à droite, la différence constatée entre l'<b style="color:#3355FF">autonomie initiale</b> et l'<b style='color:#22C4FF'>autonomie réelle</b> compte tenu des <b>kilomètres parcourus</b>. La courbe est <b style="color:#00FF00">verte</b> quand il y a un gain, <b style="color:#FFA500">orange</b> en cas de perte. Et la <b style="color:#E74C3C">puissance de charge</b> quand la voiture est en cours de recharge.



Un tableau récapitulatif par journée est affiché et permet, sur sélection d'une ligne, de zoomer sur le graphe correspondant. Un clic sur la ligne "Total" va afficher la journée complète.

 <img src="../images/tracking-table.png" alt="tracking table" width="804" style="border-radius:8px;"/>


- L'`efficience` correspond au pourcentage de km gagnés/perdus par rapport à la longueur du trajet, ce qui permet de pondérer les résultats. Les petits trajets sont 'énergivores'.
 - Les trois boutons en haut à droite du tableau permettent de filtrer par type d'étape et de pouvoir par exemple calculer les pertes liées aux seules étapes de type `parking`.


## Exemple affichage __énergie__
Depuis la version `1.5.0` du plugin, il est possible de permuter entre mode `distance` et `énergie` en cliquant sur le sélecteur.
Dans ce mode, la courbe <b style="color:#00FF00">verte</b>/<b style="color:#FFA500">orange</b> laisse place à une courbe qui décrit le cumul de l'énergie consommée/produite avec trois zones pour identifier :
 * la <b style="color:#FF0000">sur-consommation</b> lorsque l'on dépasse l'autonomie typique (ici `220Wh/km`) ,
* la <b style="color:#FFA500">sous-consommation</b>
*  et la <b style="color:#00FF00">production</b> lorsque le cumul de l'énergie est négatif.

![tracking-graph](../images/tracking-graph-wh.png)

Le tableau retranscrit les informations d'énergie. Les données sont affichées en <b style="color:darkgreen">vert</b> lorsque le voyage a consommé en moyenne moins que le typique et en <b style="color:#FF0000">rouge</b> sinon.

> **Notes**
>
> - En dehors des plages de conduite, le graphique affiche l'évolution de l'autonomie à l'arrêt, et permet par exemple de tracer les pertes de type <i>"vampire drain"</i> et de voir les courbes lors des recharges.
> - Activer en continu le recording peut conduire à une consommation d'énergie non souhaitée.


# Cartographie

La version 2.0.0 du plugin introduit la cartographie qui permet :
 - de traduire les lieux de parking en adresses physiques,
 - d'afficher sur le tableau du tracking les lieux de départ et d'arrivée,
 - de définir un lieu de parking en favori,
 - d'utiliser, dans un scénario, les événements émis lorsque la voiture entre ou sort d'un favori,
 - d'afficher les trajets effectués sur une carte chacun étant d'une couleur spécifique,
 - de suivre la voiture sur la carte lors des déplacements,
 - de rejouer un trajet effectué en suivant la pastille sur la carte et sur le graphe d'autonomie.

## Éditer un favori
Le menu en haut à droite permet d'afficher sur la carte tous les lieux de parking et/ou ces lieux s'ils ont été transformés en favori.

Le marqueur du parking peut être déplacé pour le positionner au bon endroit.

Un clic sur ce marqueur, puis sur le "coeur" permet de le transformer en favori.

On voit sur la carte ci-dessous qu'un arrêt a été fait au Col du Lautaret (trajet rouge puis trajet vert). On peut donc définir ce lieu comme un favori, et lui indiquer un rayon d'action. La prochaine fois que la voiture entrera ou sortira de cette 'bulle', un événement Jeedom sera émis, pouvant par exemple déclencher un scénario (ouverture de portail, éclairage, ... ).

![map-setfavori](../images/Map-setFavorite.gif)

## Les différentes formes de la pastille
Sur la carte, la pastille qui représente l'emplacement de la voiture prend différentes formes selon son état :

| Pastille | État |
| --- | --- |
| <img style='height:40px' src="../images/map_car_offline.svg"> | la voiture est en veille sur un parking |
| <img style='height:40px' src="../images/map_car_online.svg"> | la voiture est en ligne sur un parking |
| <img style='height:40px' src="../images/map_car_charging.svg"> | la voiture est en cours de recharge |
| <img style='height:40px' src="../images/map_car_driving.svg"> | la voiture roule |



# Liens utiles
 - Le site officiel du plugin : [Tesla Jeedom](http://tesla.jeedom.free.fr/documentation)
 - Les notes de mise à jour : [ChangeLog](http://tesla.jeedom.free.fr/changelog)
 - Le forum officiel du plugin : [Forum Community de Jeedom](https://community.jeedom.com/tags/plugin-tesla)
 - Une mine d'info sur le [Forum Automobile Propre](https://forums.automobile-propre.com/topic/piloter-sa-tesla-avec-jeedom-13412)
 - Une vidéo très démonstrative des possibilités du plugin proposée par XavMax un utilisateur du plugin : [video](https://www.youtube.com/watch?v=4p3vTRY0dNE)
 - Envie de poster un avis sur le plugin ? [Ajoutez le vôtre !](https://market.jeedom.com/index.php?v=d&p=market_display&id=3486)
 - Besoin d'une Tesla pour tester le plugin ? Utilisez mon lien de parrainage !  [http://ts.la/nicolas2320](https://www.tesla.com/fr_fr/referral/nicolas2320)
 - Envie de soutenir le développement du projet :


<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" style='text-align:center'>
<input type="hidden" name="cmd" value="_s-xclick">
<input type="hidden" name="encrypted" value="-----BEGIN PKCS7-----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-----END PKCS7-----">
<input type="image" src="https://www.paypalobjects.com/fr_FR/FR/i/btn/btn_donateCC_LG.gif" border="0" name="submit" alt="PayPal, le réflexe sécurité pour payer en ligne">
<img alt="" border="0" src="https://www.paypalobjects.com/fr_FR/i/scr/pixel.gif" width="1" height="1">
</form>



# FAQ

1. Comment bénéficier des nouvelles fonctionnalités après mise à jour du Plugin ?

   Lors de la mise à jour, le Plugin synchronise automatiquement vos véhicules configurés avec la nouvelle version du Plugin. Cependant, il se peut que la mise à jour ne se soit pas faite. Il suffira alors de cliquer sur le bouton `Synchroniser mes voitures` et les nouvelles commandes Info et Action seront ajoutées à l'équipement et visibles sur le dashboard.

2. Comment changer les unités de températures et de distance (°C / °F, km / miles) ?

   Le Plugin Tesla de Jeedom lit et utilise les paramètres que vous avez configurés dans votre voiture.

   Idem pour l'affichage de l'autonomie typique ou nominale.

3. La commande 'Réveiller' ne réveille pas la voiture.

   Depuis le panneau de configuration du Plugin, vous pouvez modifier les deux paramètres `Nombre de tentatives pour réveiller le véhicule` (3 par défaut) et `Nombre de secondes entre deux tentatives` (5 par défaut) pour essayer de forcer le réveil. Ces paramètres sont aussi utilisés par le réveil automatique effectué avant l'envoi d'une commande.

 4. Est-ce que le tracking du Plugin permet à la voiture de se mettre en veille ?

    Oui, le Plugin cherche à favoriser sa mise en veille dès que possible. La veille est un état dans lequel se met la voiture et qui réduit sa consommation électrique au plus strict minimum. Il n'y a pas de moyen technique de demander à la voiture de se mettre en veille. Dès qu'elle n'est plus sollicitée pendant une période de 15 à 20 minutes, elle passe en mode veille. Elle sortira de veille si elle est ouverte, conduite, en charge (bien qu'elle se remette parfois en veille lors des phases de charge) et/ou sollicitée par une application tierce (y compris l'app officielle Tesla ou le widget iOS). Des besoins internes à la voiture iront la réveiller également (températures hautes/basses, mise à jour de la voiture, ...)

    Exemple:
      - La voiture roule, le tracking enregistre les données au fil de l'eau, le tracking est en mode NORMAL.
      - La voiture se gare, le tracking continue en mode NORMAL pendant 10 minutes prêt à se remettre à enregistrer le prochain trajet.
      - Passées ces 10 minutes, le tracking se met en mode SOMMEIL, arrête l'enregistrement au fil de l'eau et ira interroger la voiture toutes les 15 minutes, laissant à la voiture la possibilité de se mettre en veille.
      - Dès que la voiture passe en veille, le tracking le détecte, arrête tout enregistrement et surveille simplement l'état de la voiture (appel `vehicle`) qui indiquera `offline` toute la durée de la veille.
      - Quand le tracking voit que l'état de la voiture passe `online` il repasse le tracking en mode NORMAL, prêt à enregistrer un trajet, et/ou à commencer une période d'attente de 10 minutes.

    Note: lorsque la voiture est en mode SOMMEIL, le tracking ne peut pas détecter un départ entre deux enregistrements. On peut donc ainsi "perdre" au maximum 14 minutes de trajet. Mais il est tout à fait possible de manuellement remettre le tracking en mode normal en cliquant sur l'icône orange du tracking.

 5. Est-ce qu'il est possible de régler l'intensité depuis le Plugin ?

     OUI ! L'API de Tesla permet cette fonction qui n'était pas disponible à l'origine. Le plugin permet de faire ce réglage qui est très utile pour augmenter ou diminuer la vitesse de charge dans un scénario par exemple.

 6. Le plugin s'est déconnecté tout seul de mon compte Tesla. Pourquoi ?

    Le plugin ferme la session lorsque les serveurs Tesla refusent durablement ses requêtes :
      - après plusieurs tentatives, les erreurs `401` (_Unauthorized_), `405` (_Not allowed_), `421` (_Incorrect region_) ou `423` (_Locked_) ;
      - l'erreur `403 account disabled: EXCEEDED_LIMIT`, qui indique que Tesla a désactivé votre compte API Fleet, en général parce que le plafond de facturation est dépassé sans moyen de paiement renseigné.

    Consultez votre [Dashboard Tesla](https://developer.tesla.com/fr_FR/dashboard) pour vérifier l'état de votre "application" (et ajouter un moyen de paiement si besoin), puis reconnectez le plugin en cliquant sur **Récupérer mon code d'authentification**. Pour éviter un dépassement, configurez un **Coût mensuel** dans les paramètres du plugin.

----

Merci d'envoyer toute question à <a href='mailto:vercors.io@gmail.com?subject=About%20Jeedom%20Tesla%20plugin...'>vercors.io@gmail.com</a> !

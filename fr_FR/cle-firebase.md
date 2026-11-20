# Héberger la clé publique sur Firebase

Tesla doit pouvoir lire la clé publique du plugin à l'adresse `https://<domaine>/.well-known/appspecific/com.tesla.3p.public-key.pem`. Par défaut, ce domaine est celui de votre Jeedom.

Si Tesla refuse le domaine de votre Jeedom, vous pouvez déclarer à la place un site gratuit hébergé par Google Firebase, qui ne contient que cette clé. Votre Jeedom continue de fonctionner comme avant : seule l'adresse de la clé change.

Il vous faut :

 - un compte Google ;
 - un ordinateur (Windows, macOS ou Linux) sur lequel vous pouvez lancer des commandes dans un terminal ;
 - le plugin Tesla en version **3.4.1 ou supérieure** installé sur votre Jeedom. Les versions précédentes régénèrent la clé à chaque connexion, et la clé publiée sur Firebase ne correspondrait plus à celle du plugin ;
 - une "application" créée sur [developer.tesla.com](https://vercorsio.github.io/jeedom-tesla-plugin/fr_FR/#creer-application).

Dans ce guide, le site s'appelle `mon-jeedom-tesla` : remplacez ce nom par le vôtre partout où il apparaît.

## 1. Créer le projet Firebase

 1. Ouvrez la [console Firebase](https://console.firebase.google.com) et connectez-vous avec votre compte Google.
 2. Cliquez sur **Créer un projet** et donnez-lui un nom, par exemple `mon-jeedom-tesla`. Google Analytics est inutile, vous pouvez le désactiver.
 3. Dans le menu de gauche, ouvrez **Hosting** (rubrique *Créer*), cliquez sur **Commencer** et faites défiler les étapes jusqu'au bout sans rien installer : ce guide les détaille plus bas.
 4. Notez l'adresse du site affichée dans **Hosting**, de la forme `https://mon-jeedom-tesla.web.app`, et l'**ID du projet** (roue dentée > *Paramètres du projet*). Ils sont souvent identiques, mais Firebase ajoute parfois un suffixe, par exemple `mon-jeedom-tesla-1a2b3`.

> L'offre gratuite de Firebase (*Spark*) suffit largement : aucun moyen de paiement n'est demandé.

## 2. Installer l'outil Firebase

Le site se publie avec l'outil en ligne de commande `firebase`. Le plus simple est d'installer [Node.js](https://nodejs.org) (version LTS), puis de lancer dans un terminal :

```bash
npm install -g firebase-tools
firebase login
```

`firebase login` ouvre votre navigateur : connectez-vous avec le même compte Google qu'à l'étape 1.

> Sans Node.js, Firebase propose aussi une version autonome de l'outil (fichier `.exe` sous Windows, `curl -sL https://firebase.tools | bash` sous macOS et Linux). Voir la [documentation de Firebase](https://firebase.google.com/docs/cli).

## 3. Récupérer la clé publique de votre Jeedom

Le plugin crée la clé à son installation, dans le fichier `/var/www/html/.well-known/appspecific/com.tesla.3p.public-key.pem` de votre Jeedom. Pour l'afficher, au choix :

 - **depuis la page de connexion du plugin** : renseignez vos clés et, dans `URL d'origine autorisé`, l'adresse de votre site Firebase (`https://mon-jeedom-tesla.web.app`), puis cliquez sur **SUIVANT**. La clé s'affiche dans le cadre **Clé publique lue en local**. À ce stade, il est normal que les vérifications de la clé lue depuis le réseau échouent : le site n'est pas encore publié ;
 - **en SSH sur votre Jeedom** : `cat /var/www/html/.well-known/appspecific/com.tesla.3p.public-key.pem`.

La clé ressemble à ceci :

```
-----BEGIN PUBLIC KEY-----
MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAE...
...
-----END PUBLIC KEY-----
```

> C'est la clé **publique** : elle est faite pour être lue par tous. La clé privée, qui reste dans le plugin, ne doit jamais être copiée sur le site.

## 4. Préparer le site

Sur votre ordinateur, créez un dossier `mon-jeedom-tesla` avec cette arborescence :

```
mon-jeedom-tesla/
├── firebase.json
└── public/
    └── .well-known/
        └── appspecific/
            └── com.tesla.3p.public-key.pem
```

Sous Windows et macOS, l'explorateur de fichiers peut refuser ou masquer un dossier dont le nom commence par un point. Créez les dossiers depuis le terminal, dans `mon-jeedom-tesla` :

```bash
mkdir -p public/.well-known/appspecific      # macOS, Linux
mkdir public\.well-known\appspecific         # Windows
```

Le fichier `com.tesla.3p.public-key.pem` contient la clé copiée à l'étape 3, de `-----BEGIN PUBLIC KEY-----` à `-----END PUBLIC KEY-----` inclus. Le nom du fichier et des dossiers doit être exactement celui-ci, point compris.

Le fichier `firebase.json` contient :

```json
{
  "hosting": {
    "public": "public",
    "ignore": ["firebase.json", "**/node_modules/**"],
    "headers": [
      {
        "source": "/.well-known/appspecific/*.pem",
        "headers": [{ "key": "Content-Type", "value": "application/x-pem-file" }]
      }
    ]
  }
}
```

> Ne générez pas ce fichier avec `firebase init` : la configuration proposée ignore les fichiers et dossiers dont le nom commence par un point, et le dossier `.well-known` ne serait jamais publié.

## 5. Publier le site

Dans le terminal, depuis le dossier `mon-jeedom-tesla`, lancez la commande suivante, en remplaçant `mon-jeedom-tesla` par l'ID de votre projet :

```bash
firebase deploy --only hosting --project mon-jeedom-tesla
```

Vérifiez ensuite que la clé est accessible en ouvrant dans votre navigateur `https://mon-jeedom-tesla.web.app/.well-known/appspecific/com.tesla.3p.public-key.pem` : le navigateur affiche ou télécharge la clé.

## 6. Déclarer le site chez Tesla et dans le plugin

 1. Sur [developer.tesla.com](https://developer.tesla.com/fr_FR/dashboard), dans les détails de votre "application", remplacez l'*Origine autorisée* par `https://mon-jeedom-tesla.web.app`.
 2. Gardez l'URI de redirection `https://jeedomteslaplugin.firebaseapp.com/redirect/`. Dans le plugin, choisissez **Manuelle** pour **Récupération du code** : le mode automatique renvoie vers `https://<domaine>/plugins/tesla/redirect/`, une page qui n'existe pas sur le site Firebase.
 3. Dans le plugin, vérifiez que `URL d'origine autorisé` contient `https://mon-jeedom-tesla.web.app`, puis cliquez sur **SUIVANT**. Toutes les vérifications doivent passer au vert, en particulier « Parfait, les clés sont identiques » et « Parfait, les serveurs Tesla valident la clé publique ».
 4. Poursuivez la [connexion du plugin](https://vercorsio.github.io/jeedom-tesla-plugin/fr_FR/#connecter-plugin) puis l'[appairage de la voiture](https://vercorsio.github.io/jeedom-tesla-plugin/fr_FR/#appairage), comme d'habitude.

## En cas de problème

 - **« Attention, les clés sont différentes »** : la clé publiée ne correspond pas à celle du plugin. Recopiez la clé de l'étape 3 dans `com.tesla.3p.public-key.pem` et republiez le site (étape 5).
 - **La clé ne s'affiche pas dans le navigateur (erreur 404)** : vérifiez le nom exact des dossiers `.well-known` et `appspecific` et du fichier, et que `firebase.json` ne contient pas `"**/.*"` dans `ignore`.
 - **Après « Régénérer les clés »** (configuration avancée du plugin) : republiez la nouvelle clé sur le site Firebase, puis refaites l'appairage de vos Tesla.

> Le site Firebase ne reçoit aucune donnée de vos véhicules : il ne fait que servir la clé publique à Tesla.

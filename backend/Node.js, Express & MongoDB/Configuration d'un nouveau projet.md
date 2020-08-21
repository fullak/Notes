# Configuration d'un nouveau projet

## Installer Angular : 
```
npm install -g @angular/cli
```

## Installer dépandences front-end
Dans le dossier front

```
cd frontend
npm install
ng serve
```

> Avoir toujours un terminal qui exécute ```ng serve``` lorsdu dev. De cette façon, on peut tester le code en temps réel.


## Initialiser un projet

A partir du dossier backend, ```npm init``` pour initialiser le projet.
Le point d'entrée doit être ```serveur.js```

### .gitignore 

Créer un fichier .gitignore contenant ```node_modules``` afin de ne pas l'envoyer sur github.

## Créer un serveur Node

```
const http = require('http');

const server = http.createServer((req, res) => {
    res.end('Voilà la réponse du serveur !');
});

server.listen(process.env.PORT || 3000);
```

Pour démarrer le serveur ```node server```

### nodemon (surveille les modifications en temps réel)

```npm install -g nodemon```

lancer nodemon :

```nodemon server```
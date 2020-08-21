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

## Installer Express

```npm install --save express```

L'application Express doit être créer dans le fichier ```app.js```

```
const express = require('express');

const app = express();

module.exports = app;
```

## server.js

```
const http = require('http');
const app = require('./app');

const normalizePort = val => {
  const port = parseInt(val, 10);

  if (isNaN(port)) {
    return val;
  }
  if (port >= 0) {
    return port;
  }
  return false;
};
const port = normalizePort(process.env.PORT || '3000');
app.set('port', port);

const errorHandler = error => {
  if (error.syscall !== 'listen') {
    throw error;
  }
  const address = server.address();
  const bind = typeof address === 'string' ? 'pipe ' + address : 'port: ' + port;
  switch (error.code) {
    case 'EACCES':
      console.error(bind + ' requires elevated privileges.');
      process.exit(1);
      break;
    case 'EADDRINUSE':
      console.error(bind + ' is already in use.');
      process.exit(1);
      break;
    default:
      throw error;
  }
};

const server = http.createServer(app);

server.on('error', errorHandler);
server.on('listening', () => {
  const address = server.address();
  const bind = typeof address === 'string' ? 'pipe ' + address : 'port ' + port;
  console.log('Listening on ' + bind);
});

server.listen(port);
```
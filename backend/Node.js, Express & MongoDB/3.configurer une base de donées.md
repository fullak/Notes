# Configurer une base de donées 

## MongoDB

mongodb.com

Créer un nouveau cluster

## Connecter l'API au cluster

```npm install --save mongoose```

dans app.js 

```const mongoose = require('mongoose');```

```
mongoose.connect('mongodb+srv://jimbob:<PASSWORD>@cluster0-pme76.mongodb.net/test?retryWrites=true&w=majority',
  { useNewUrlParser: true,
    useUnifiedTopology: true })
  .then(() => console.log('Connexion à MongoDB réussie !'))
  .catch(() => console.log('Connexion à MongoDB échouée !'));
```
récuperer le lien du cluster & remplacer <PASSWORD>
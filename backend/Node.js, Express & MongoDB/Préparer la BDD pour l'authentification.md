# Préparez la base de données pour les informations d'authentification

> NE JAMAIS ENREGISTRER DES MDP NON CRYPTES !!

## Créer un modèle de donées

```
const mongoose = require('mongoose');
const uniqueValidator = require('mongoose-unique-validator');

const userSchema = mongoose.Schema({
    email: { type: String, require: true, unique: true },
    password: { type: String, require: true }
});

userSchema.plugin(uniqueValidator);

module.exports = mongoose.model('User', userSchema);
```

### Installer le package mongoose-unique-validator

Empeche d'utiliser plusieurs fois la même adresse mail pour l'authentification.

```npm install --save mongoose-unique-validator```

## Créer des utilisateurs

### Création des routes : 

Dans le dossier ```routes```
Créer un fichier ```user.js```

```
const express = require('express');
const router = express.Router();

const userCtrl = require('../controllers/user');

router.post('/signup', userCtrl.signup);
router.post('/login', userCtrl.login);

module.exports = router;

```

Import ```const userRoutes = require('./routes/user');``` dans ```app.js```
 
Puis ajouter ```app.use('/api/auth', userRoutes);``` a la fin du fichier ```app.js``` avant le module.export

### Créer une fonction signup

Installer le package ```bcrypt```

```npm install --save bcrypt```

Dans le fichier ```user.js``` dans les ```controllers```

```
exports.signup = (req, res, next) => {
    bcrypt.hash(req.body,paswword, 10)
    .then(hash => {
        const user = new User({
            email: req.body.email,
            password: hash
        });
        user.save()
        .then(() => req.status(201).json({ message: 'Utilisateur créé' }))
        .catch(error => res.status(400).json({ error }));
    })
    .catch(error => res.status(500).json({ error }));
};

```

Documentation de bcrypt https://www.npmjs.com/package/bcrypt

### Créer une fonction login

```
exports.login = (req, res, next) => {
    User.findOne({ email: req.body.email })
    .then(user => {
        if (!user) {
            return res.status(401).json({ error: 'Utilisateur non trouvé' });
        }
        bcrypt.compare(req.body.password, user.password)
        .then(valid => {
            if (!valid) {
                return res.status(401).json({ error: 'Mot de pass incorrect' });
            }
            res.status(200).json({
                userId: user._id,
                token: 'TOKEN'
            });
        })
        .catch(error => res.status(500).json({ error }));
    })
    .catch(error => res.status(500).json({ error }));
};
```

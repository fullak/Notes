# Configurer le routage 

Créer un dossier ```controllers``` dans le dossier ```backend``` & y placer un fichier ```random.js```
pour y intégrer nos routes

```
const express = require('express');
const router = express.Router();

const stuffCtrl = require('../controllers/stuff');

router.get();
router.post();
router.put();
router.delete();
...

module.exports = router;
```

Dans le fichier ```app.js``` remplacer les routes par ```app.use('/api/stuff', stuffRoutes);```

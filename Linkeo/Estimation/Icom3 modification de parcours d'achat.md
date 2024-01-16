---
date: 2023-11-21
shorcode: CLICKCONTA6T0A
site exemple à reproduire: https://www.comptoirdelours.fr/
---
le panier floting sy panier page doivent être modifié pour ne plus afficher 


le contenu d'un bouton ajouter au panier est un link , redirect vers un fichier php 
```
<a class="button addToCartApi" title="Ajouter au panier" data-addtocarturl="//localhost/Icom3/coffrage-france/www/public/catalogues/api/addToCart.php?action=addProduct&amp;stockId=9268&amp;quantity=1&amp;lang=fr_FR">
<span class="icom-spinner"></span></a>
```

template payemen icom3 

```
librairies/extension/ideo3/module/Catalogues/view/paniers/panier_payment.mustache
```

possiblité d'overrider ces partials , regarde dans 

```
librairies/extension/ideo3/module/Catalogues/config/module.config.php
```

on va demander au client de se connecter, 
on remplace le bouton commander par envoi mail pour devis 

relation entre bouton et envoi mail ?
 

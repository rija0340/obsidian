chaque categorie est un url vers une page
puis tous les url des categ sont rediriger par htaccess

```html 
RewriteCond %{REQUEST_FILENAME} (\.html)$
RewriteCond %{REQUEST_FILENAME} \/fiche|/Vente-de|/Categories [NC]
RewriteRule ^.*$ dispatch.php [NC,L]
```

redirigé vers dispatch ,

aveo dispacth mampiasa fonction anaty rout.inc.php

aveo Dispatcher , /home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769/#librairies/extension/ideo3/common_config/Dispatcher.php 

c'est dans la page payment qu'il ya listing adresse livraision et client en cas de successful log in
<span class="remarque" >Après etude</span>
après etude, j'ai constaté que la page payement, après log in est un shortcode
handler du shortcode  : PanierTagHandler
cet handler utilise un fiichier Renderer : PanierRenderer, c'est la fonction renderer dans ce fichier qui rend le template.


template  : les templates utilisés sont dans partials 
/home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769/#librairies/extension/ideo3/module/Catalogues/view/paniers

template qui assemble ces partials 
/home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769/#librairies/extension/ideo3/module/Catalogues/view/paniers/panier_payment.mustache


content_panier_payment = panier_payment

```php

return array(
  'service_manager' => array(
    'invokables' => array(
        'catalogue.renderer' => 'Customize\Service\Renderer\CatalogueRenderer',
    ),
  )
);

```



## frais de port

dans ce site on a deux frais de port  : 
retrait en magasin 
livraison

dans chaque frais de port on peux configurer des calculateur , ces calculateurs peuvent etre en fonction de localisation, nombre de produits, poids produit ...
un frais de port peux associer plusieurs calculateurs.


# declinaison

lorsqu'on crée des declinaison d'un produit dans b.o , ils (les déclinaisons) sont enregistrés dans la tables IC301_catalogues02_stocks 
stock_quatité represente la quantité de chaque déclinaison

le nombre de stock considéré est toujours celui du déclinaison à moindre prix.
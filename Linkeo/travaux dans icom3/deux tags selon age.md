
## Avoir un "Tag" pour definir deux type de produits a afficher selon le choix d'un utilisateur


catégorie est rendu dynamiquement dans home.php

$menuRenderer->renderIcom3("R|useClass=\"dropdown\"");

-pop up choix 
-redirection vers une page avec un short code 
-js met dans une session le choix 
-handler catalogue overridé check du choix dans session 
-retrieve donnée en fonction choix 

relation entre 
* catalogueTagHandler
* catalgueRenderer 
* produit.php

sur page catalogue on a un shortcode qui a un handler,
handler return un code php qui appelle une méthode dans catalogueRenderer.
peut être que dans cette renderer ou handler on ajout un stack js qui envoi appelle produit.php avec paramètre.

url en dur pour redirection vers une catégorie  : 

```php
_PTR_.'/Vente-de-'.$nom.'-9-'.$id.'.html';
```

daans les catégories s'il y avait quelque chose comme , getproductsBytags 

## solutions pour avoir liste catégorie selon tranche age (jeune et adulte )

### 1-créer ces ages en tant que categorie et setter en tant que parents pour les autre cagétorie 

et puis pour avoir les categories childres on utilise cette methode  : 

```php
$result = $elementCategorieRepository->getChildrens(61,$langueId, $defaultLangueId);
```
ou 61 est un ID de categorie parent 

### 2- (en cours) creer tag jeune et adulte 

créer des tags no catégories ( qui sont meme chose au niveau base de données ) 

utiliser method getproduitsbytag et puis looper les produits pour avoir les catégories utilisé par ces produits 


ity izao no zavatra mitsy  : 

```html

<pre class='xdebug-var-dump' dir='ltr'>
<small>/home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769/#librairies/extension/ideo3/public/catalogues/api/produit.php:72:</small>
<b>array</b> <i>(size=8)</i>
  'elementCategorieId' <font color='#888a85'>=&gt;</font> <small>string</small> <font color='#cc0000'>'0'</font> <i>(length=1)</i>
  'categorieId' <font color='#888a85'>=&gt;</font> <small>string</small> <font color='#cc0000'>'0'</font> <i>(length=1)</i>
  'limit' <font color='#888a85'>=&gt;</font> <small>int</small> <font color='#4e9a06'>12</font>
  'offset' <font color='#888a85'>=&gt;</font> <small>int</small> <font color='#4e9a06'>0</font>
  'id' <font color='#888a85'>=&gt;</font> <font color='#3465a4'>null</font>
  'attributs' <font color='#888a85'>=&gt;</font> <font color='#3465a4'>null</font>
  's' <font color='#888a85'>=&gt;</font> <small>string</small> <font color='#cc0000'>''</font> <i>(length=0)</i>
  'lang' <font color='#888a85'>=&gt;</font> <small>string</small> <font color='#cc0000'>'fr-fr'</font> <i>(length=5)</i>
</pre>

```


ampiasaina le getallproduit sy getproduit ao anaty produit.php
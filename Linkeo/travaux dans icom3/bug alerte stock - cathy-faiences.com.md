---
url: http://jira.linkeo.com/browse/IDEO-6816
---

### Bug alerte stock | cathy-faiences.com CATHY FAIENCES | 


exemple produit épuisé en ligne  : 

https://www.cathy-faiences.com/fiche-Mug+en+porcelaine+rouge+gorge+++easy+life-6493.html
exemple epuisé local ordi 
http://localhost/Icom3/cathy-faiences.com_IC301/www/public/fiche-Mug+en+porcelaine+rouge+gorge+++easy+life-6493.html

http://10.99.0.21/index.php?action=fiche&module=site&id=11EF8CED5BFED

coffrage frnace epuisé
http://localhost/Icom3/coffrage-france/www/public/fiche-tee+shirt-291.html

dans le fiche produit, quand celui-ci est épuisé, on a un bouton "m'avertir quand ce produit est disponible " qui apparit

voici le code de ce bouton  : 

```html 
{{#alertStock}}
<p class="warningMsg text-center">{{staticText.alertStockText}}</p>
<div class="block-button full-width">
<a class="button text-center" id="alertStock" data-stockid="{{stockId}}">
<span class="txt">{{staticText.alertStockTextBtn}}</span>
</a>
</div>
{{/alertStock}}
```


voici le fichier js contenant les événement lié à ce template 

```url 
librairies/#librairies/#librairies/extension/ideo3/public/catalogues/js/fiche.js
```

liste des templates dans $config['render_mustache']

```
 0 => string 'content_panier' 
  1 => string 'list'
  2 => string 'home' 
  3 => string 'content_panier_bloc' 
  4 => string 'categorieList'
  5 => string 'fiche' 
  6 => string 'tag' 
  7 => string 'custom_content_panier' 
  8 => string 'custom_list' 
  9 => string 'custom_home' 
  10 => string 'custom_content_panier_bloc'
  11 => string 'custom_categorieList' 
  12 => string 'custom_fiche' 
  13 => string 'custom_tag' 
```


```javascript
$(document).ready(function () {
    // Add this script to remove the 'top' attribute
    $('#smallModal').on('opened.zf.reveal', function () {
        $(this).css('top', '');
    });
});
```
---
tags  : auto_work, CLICKCONTA6NVX
url : http://jira.linkeo.com/browse/IDEO-6708
date : 2023-05-08
---

<span class="remarque">remarque : </span> si on ne met pas de modele le mercedes ne s'affiche pas , 
souci : recherche Audi Q2 et un mercedes apparaît
dans la table IC302_categories01_elementsCategoriesProduits on a une ligne qui associe le mercedes avec la catégorie Q2 (voir details requete en bas, id_categ = 172)

' AND n.produit_id in(9860,38302,75515,75927,76124) AND ( n.produit_puissance_reelle BETWEEN 0 AND 10000)'

bdd est auto  :CLICKCONTA6QCC

résultat de recherche pour Audi Q2 : 

reference:
+38562
+39084 (mercedes)
+220228

id :
+75515
+75927 (mercedes)
+76124

```html
<pre class='xdebug-var-dump' dir='ltr'>
<small>/home/rrakotoarinelina/programming/Linkeo/libraries2/branches/immo-auto/#librairies/extension/ideo3/module/CataloguesAuto/src/CataloguesAuto/Repository/ElementsCategoriesProduitsRepository.php:246:</small><small>string</small> <font color='#cc0000'>' AND n.produit_id in(9860,38302,75515,75927,76124)'</font> <i>(length=50)</i>
</pre>
```


parametre de la recherche  : catauto:1;selMarque:3;selModele:172;

investigation dans la method  : filtreParCategories
enfant  : 172
request  : 

```html
SELECT produit_id FROM IC302_categories01_elementsCategoriesProduits ecp 
 LEFT JOIN `IC302_categories01_elementsCategories` ec ON ecp.elementsCategorie_id = ec.elementsCategorie_id  WHERE ec.elementsCategorie_id = '172' GROUP BY produit_id
```


marque et modèle sont dans la table IC302_categories01_elementsCategories et IC302_categories01_elementsCategories_lang (meme id pour les deux tables mais _lang contient juste des info supplementaire)

on va faire un test de fausse manipulation si cela va etre corrigé après
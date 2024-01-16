---
tags  : icom3_work, CLICKCONTA6CQZ
url : http://jira.linkeo.com/browse/IDEO-6718
date : 2023-05-31
---

produit avec déclinaison 


https://www.medigaservice.fr/fiche-CHANGE+COMPLET+EXTRA+PLUS+LILLE+HEALTHCARE-41.html

http://localhost/Icom3/medigaservice.com_IC301/www/public/fiche-CHANGE+COMPLET+EXTRA+PLUS+LILLE+HEALTHCARE-41.html

/home/rrakotoarinelina/programming/Linkeo/libraries/Icom3/dev/#librairies/extension/ideo3/module/Catalogues/src/Catalogues/Service/CataloguesApi.php 1697 ligne a voir


## requete original pour avoir stock minimal et prix minimal


(SELECT c.stock_id FROM " . getPrefixForDatabaseTable() . "catalogues02_stocks c WHERE c.produit_id = n.produit_id ORDER BY c.stock_prix,c.stock_prixPromo ASC LIMIT 1 ) AS stock_id,

(SELECT c.stock_quantite FROM " . getPrefixForDatabaseTable() . "catalogues02_stocks c WHERE c.produit_id = n.produit_id ORDER BY c.stock_prix,c.stock_prixPromo ASC LIMIT 1 ) AS stock_quantite,


## nouveau requête 

(
SELECT c.stock_id 
FROM " . getPrefixForDatabaseTable() . "catalogues02_stocks c 
WHERE c.produit_id = n.produit_id 
ORDER BY 
CASE 
	WHEN c.produit_quantite  = 0 THEN  0 ELSE c.stock_prix,c.stock_prixPromo END
ASC LIMIT 1 ) AS stock_id,

(SELECT c.stock_quantite 
FROM " . getPrefixForDatabaseTable() . "catalogues02_stocks c 
WHERE c.produit_id = n.produit_id 
ORDER BY 
CASE
	WHEN c.produit_quantite  = 0 THEN  0 ELSE c.stock_prix,c.stock_prixPromo END
ASC LIMIT 1 ) AS stock_quantite,


## requete nandeha 



```sql
(SELECT c.stock_id

FROM " . getPrefixForDatabaseTable() . "catalogues02_stocks c
WHERE c.produit_id = n.produit_id
ORDER BY
CASE WHEN c.stock_quantite = 0 THEN c.stock_prix ELSE 0 END ASC,
c.stock_prixPromo ASC


LIMIT 1 ) AS stock_id,
(SELECT c.stock_quantite
FROM " . getPrefixForDatabaseTable() . "catalogues02_stocks c
WHERE c.produit_id = n.produit_id
ORDER BY
CASE WHEN c.stock_quantite = 0 THEN c.stock_prix ELSE 0 END ASC,
c.stock_prixPromo ASC LIMIT 1) AS stock_quantite,

```
explication pour mieux comprendre le requete utilisé pour modification 

https://chat.openai.com/share/b69ba90d-e797-4537-b269-d345400f5c20

le tri par zero n'est valabque que dans case when 
ces ligne sont tjours placé en bas .


## <span class="titre1">ajouter au panier issue </span>
le prix minimum est égale à zero stock 
le bouton ajouter au panier n'est pas affiché

dans serializerproduit , on chect si disponibilité du produit est 1 (non dispo car stock zero ),  c'est pour cela que le bouton ajoter au panier n'apparait pas 

### concern :
on essaye de forcer de cacher tag "epuiser "
 et afficher ajouter au panier, alors que l'url ajouter au panier pointe vers le stock qui est épuisé ( avec prix minimum ) ???????
ho affichena ihan zany ny bouton ajouter au panier avec id anle min misy stock 

## ancien requete dispobibilite 

```sql 
(SELECT c.disponibilite_id FROM " . getPrefixForDatabaseTable() . "catalogues02_stocks c WHERE c.produit_id = n.produit_id ORDER BY c.stock_prix,c.stock_prixPromo ASC LIMIT 1 ) AS disponibilite_id,
```

new query 

```sql 
(SELECT c.disponibilite_id
FROM " . getPrefixForDatabaseTable() . "catalogues02_stocks c
WHERE c.produit_id = n.produit_id
ORDER BY
CASE WHEN c.stock_quantite = 0 THEN c.stock_prix ELSE 0 END ASC,
c.stock_prix,
c.stock_prixPromo
LIMIT 1) AS disponibilite_id,
```
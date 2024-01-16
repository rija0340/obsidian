---
tags  : icom3_work, LINKDIRECT65UH
url : http://jira.linkeo.com/browse/IDEO-6717
date : 2023-05-22
---

souci de commande qui passe vnant de finlande alors que ne devrait pas 

creation de 3 comptes pour test 

rija Francais : rija0340@gmail.com 

produit :    CHABLIS CUVÉE ÉTAIN TRADITION (10)
deux option de livraision disponible (retrait et livraison 44,44 euro)
redirection sur site paypal pour paiement


Rija Australien : rakotoarinelinarija@gmail.com
produit : MONT DE MILIEU (10)
deux option de livraision disponible (retrait et livraison 44,44 euro)
redirection sur site paypal pour paiement


Rija Finlandais : rija.rakotoarinelina@linkeo.com
produit :  MONTMAINS (20)
deux option de livraision disponible (retrait et livraison 40,44 euro)
redirection sur site paypal pour paiement

test dans liste calculateur  : 

localisation associé : Ain ( dans 19-24) on a le prix  : 59.04


scenario test :

## test 1 : 
creation de compte  adresse de livraision comme suit : 


pays  : finlande 
ville  : Helinksi 
code postal  : 00100 

test achat  : bloqué ( ne livre pas à cette adresse )

## test  2 

creation de compte adresse de livraisoin comme suit  : 

pays : finlande 
ville  : Porvoo (comme la commande qui a passé )
code postal  : 06450 

test achat : commande accepté ( on voit deux options pour livraison : retrait et livraison avec frais de 63.17 euro )


------------------
### test 2.1

attempt to process another bying with this account  : 

commade accepté pour meme adresse de livraision 

### test 2.2 
changement de addresse livraison en turku et commande bloqué ( addresse non accepté)

### test 2.3 
changement adreese par helinski -> commande bloquée (adresse non accepté )

## test 2.4

<span class="remarque">Remarque</span> changement par autre code postal (07750) mais meme ville (PORVOO) , commande non accepté  , 


## test 3
 creation de compte addresse de livraison comme suit : 
mail  : rakotoarinelinarija@gmail.com
pays : finlande
ville  : Turku
postal code  : 20100

test achat  : commande bloqué pour raision addresse de livraison no valide 

## test 4

creation de compte avec ces parametres 

pays : Allemagne
ville : antananarivo 
postal code  : 06450

test achat : commande accepté 

pays : Allemagne
ville : antananarivo 
postal code  : autre

test achat : commande refusé

<span class="titre1">Raison bug : </span> code postal utilisé par client est même que Alpes-maritime, c'est pourquoi il y a un frais de port. 

## test 5 :  check si seulement code postal est checké par code mais pas pays ..

dump dans PanierService  : 

var_dump(pays_client,pays_magasin,datas["listShippingCosts"]);
pour ce compte 
pays : finlande 
ville  : Porvoo (comme la commande qui a passé )
code postal  : 06450 

resultat  : 
pays_client  : FI
pays_magasin : FR 

```php
/home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769/#librairies/extension/ideo3/module/Catalogues/src/Paniers/Service/PanierService.php:2658:string 'FI' _(length=2)_

/home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769/#librairies/extension/ideo3/module/Catalogues/src/Paniers/Service/PanierService.php:2658:string 'FR' _(length=2)_

/home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769/#librairies/extension/ideo3/module/Catalogues/src/Paniers/Service/PanierService.php:2658:
**array** _(size=2)_
  0 => 
    **array** _(size=5)_
      'shippingCostId' => int 5
      'label' => string 'Retrait en magasin' _(length=18)_
      'total' => string '€0,00 EUR' _(length=11)_
      'totalValue' => float 0
      'livraisonMagasin' => boolean true
  1 => 
    **array** _(size=5)_
      'shippingCostId' => int 6
      'label' => string 'Livraison' _(length=9)_
      'total' => string '€63,17 EUR' _(length=12)_
      'totalValue' => float 63.17
      'livraisonMagasin' => boolean false
```


cette fonction dans panier service
```php 
function getDataLivraison($datas) {}
```


utilise cette methode  : 

```php
$listeFraisPort = $fraisPort->getListe($parametre);
```

qui utilise ce paramètre  (pays et codepostal)

```php
//Correction bug unite de mesure kg Jimmy 08/07/2021

$parametre = array(
	'pays_id' => round($commandeEncours -> getObjAdresseLivraison() -> getPays_id()),
	'codePostal' => trim($commandeEncours -> getObjAdresseLivraison() -> getCp()),
	'total' => round(str_replace(',', '.', $total), 2),
	'articles' => $datas['cart']['nbItem'],
	//'poid' => round($datas['cart']['weight']),
	'poid' => $datas['cart']['weight'],
	'volume' => 0,
	'info_client' => $refClient
);
```

dans FraisPortAbstract.class.php, on a 
getliste qui UTILISE SEULEMENT CODEPOSTAL POUR CALCULER FRAIS DE PORT 

table liste departement  :  

## dans fichier FraisPortAbstract

on a ceci  : loadFraisPort qui load les frais de port depuis base , retourne frais port active depuis la table IC301_fraisports01_libelle
```php
/home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769/#librairies/modules/fraisports/01/v9.10/FraisPortAbstract.class.php:581:
**array** _(size=2)_
  5 => 
    **object**(_FraisPortLibelle_)[_1038_]
      _protected_ 'id' => string '5' _(length=1)_
      _protected_ 'libelle' => string 'Retrait en magasin' _(length=18)_
      _protected_ 'enabled' => string '1' _(length=1)_
      _protected_ 'libelle_admin' => string 'Click & Collect' _(length=15)_
      _protected_ 'politique' => string 'cumule' _(length=6)_
      _protected_ 'gratuit' => string '0.00' _(length=4)_
      _protected_ 'minimumCommande' => string '0.00' _(length=4)_
      _protected_ 'listeType' => 
        **array** _(size=0)_
          _empty_
      _private_ 'inAdmin' (FraisPortLibelleAbstract) => boolean false
      _protected_ 'isClickCollect' => boolean false
  6 => 
    **object**(_FraisPortLibelle_)[_1073_]
      _protected_ 'id' => string '6' _(length=1)_
      _protected_ 'libelle' => string 'Livraison' _(length=9)_
      _protected_ 'enabled' => string '1' _(length=1)_
      _protected_ 'libelle_admin' => string 'Livraison' _(length=9)_
      _protected_ 'politique' => string 'cumule' _(length=6)_
      _protected_ 'gratuit' => string '0.00' _(length=4)_
      _protected_ 'minimumCommande' => string '1.00' _(length=4)_
      _protected_ 'listeType' => 
        **array** _(size=0)_
          _empty_
      _private_ 'inAdmin' (FraisPortLibelleAbstract) => boolean false
      _protected_ 'isClickCollect' => boolean false
```

### table  : fraisport01_localisation 

c'est la table qui met en relation libelle (calculateur ) et localisation 


##  <span class="titre3">Table </span>table  : 
fraisports01_libelle -> mitazona ny frais de port rehetra 
fraisports01_type -> mitazona ny type de frais ( calculateur, par nombre produit , par localisation etc )
fraisports01_libelle_has_type -> correspondance entre frais de port et calculateur 

fraisport01_localisation -> correspondance entre localisation et frais de port 
	fraisport_localisation_libelle -> nom du zone inseré depuis backoffice ( manuellement)
	fraisport_localisation_libelle_id-> id du frais  de port ( ici test ou livraison)
	fraisport_localisation_zonage_id -> par departement, par pays etc


<span class="remarque">Remarque</span> supposons que c'est une relation entre pays et localisation  :
fraisports01_localisation_fk (fk_id == pays id)

pourquoi il a une localisation qui a deux pays ? 

supponsons que ce sont des erreurs, 

## test 6 

pays :  afganisthan
code postal  : 01000 (departement Ain france)

<span class="titre2"> Remarque </span> le proble c'est l'enregistrement du localisation dans la table localisation_fk qui double a chaque sauvegarde, sauvant France et autre pays qui s'incremente à chaque ajout de localisation ( donc) si on ajoute beaucoup de localisation , tous les pays peuvent etre compris , 


format du json envoyé pour etre enregistré
localisation par departement  : 

```json 
  
	  fraisport_localisation_id=
      fraisport_localisation_libelle=555
      fraisport_localisation_zonage_id=4 -> fraisport departement (table fraitsport_zonagelocalisation) 
      fp_loc_id =5
      
      fraisport_localisation_libelle_id=1
```

je travaille dans  /home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769/#librairies/modules/fraisports/01/v9.10/class/FraisPortLocalisationAbstract.class.php



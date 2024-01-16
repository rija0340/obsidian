---
tags  : estimation, 
url : http://jira.linkeo.com/browse/SPE-1754
date : 2023-07-21
---

Description  : 

ce qu'on a besoin de faire dans la bdd 

+ ajouter des marques et des modeles 
dans la base de donnée les produits sont dans  : 

http://localhost/phpmyadmin/sql.php?server=1&db=CLICKCONTA6QCC&table=IC302_catalogues02_autoProduits&pos=0&token=cc955ef47af415632be47b9328baeaee
## fonctionnement oscaro.com 

- on la possibilté de voir directement la catégorie d'une pièce et les sous catégorie 
- est ensuite redirigé vers une page ou on a un pop up nous proposons de saisir la marque et le modéle de notre véhicule 

## pour notre part 

on se proopose de construire quelque chose de similaire à la recherche avancée menu gauche. ce qu'on va faire c'est créer aussi les catégorie et puis la possiblité de filterer par des marque et modèle de véhicules

+ il nous faut la liste des pièces ainsi que la marque et modèle des véhicules qui peuvent utiliser les pièces 
+ 
## scenario
+ si le site est hybride, auto est immo, je propose qu'on sépare lé page 
	+ auto : utilise recherche gauche standard
	+ pièces utilise le short code dev spe pour recherche 

url api quand on click sur catégorie 

http://localhost/Auto/est-autos.fr/public/catalogues/api/produit.php?v1%20&%20offset=0&rowcount=12&lang=fr-fr&ecat=0&cat=0&s=catauto:1;eleCat:182;


possibilité  : 

si la profondeur de véhicuele est de 4 -> marque > modele > famille > type (comme sur oscaro)

#### renderer template véhicule 
- construire un renderer et template qui peut faire cela 
- a chaque changement de niveau parent , injecter le children correpondant dans le select sub 
- rubriques en template select
- ajoute un bouton et au click la recherche se lance 


#### handler
utiliser meme que pour RAMGhandler avec des ajustement 

#### fonctionnement

-  IMPORTANT : on prendra id dernier profondeur pour vehicule comme idmodele à envoyer 

les marque modèles sont des selects 
les rubriques (catégories de pièces) seront dans un dropdown 
chaque rubriques contient des selects de sous catégories de pièces

## mail à Yosh

Au cas ou le site est hybride ayant voitures et pièces, il y aura deux pages différentes pour voitures et pièces.

-  recherche pièces

L'intégration de système d'immatriculation risque de compliquer le travail. Il y a des prestataires  qui proposent ce service mais c'est payant. Il faut faire une étude pour la manipulation de données.
Cette estimation considère seulement une recherche de pièces par modèle. 
Nous proposons de créer un nouveau shortcode spécialement dédiée pour recherche de produits pièces.  dans ce shortcode, on aura :

- filtre véhicule  : marque , famille, modèle, type 
- choix de rubrique de pièces

L'utilisateur doit entrer manuellement dans le backoffice les pièces est leurs compatibilités (dans la section organistion).

-  recherche véhicules

On va modifier le template recherche enregistrée menu gauche pour ne pllus afficher les rubriques pièces. 



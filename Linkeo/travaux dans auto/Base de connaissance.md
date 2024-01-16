## generation de template less

même principe que dans ideo 3 [[Base de connaissance IDEO3 et IDEO3.2]]

* garage-betton et murocars n'a pas d'override dans list produits auto 
* est-auto misy override liste auto produits

## importation de produit et catégorie par import csv

+ les deux vont ensemble, il faut télécharger le fichier exemple dans le modal d'importation 
+ importer un zip contenant les deux fichiers 
+ dans le fichier csv produit 
	+ rubrique peut être une liste, il y a les rubrique par défaut dans le site (catégorie > rubrique )   
		+ rubrique 
		+ marque modele 
		+ selection 
	- marque modèle doit aussi etre deux chiffres(des ids ) si un produit a une marque est un modèle (obtenu a partir des données dans le fichier catégories)


 donc par exemple on doit mettre sur le fichier produit un produit modèle


  |   |   |   |   |   |
|---|---|---|---|---|
|REFERENCE_PRODUIT|NOM_PRODUIT|IMAGES|RUBRIQUES|MARQUES|
|39131|VOLKSWAGEN POLO||1|69,165|
|230401|RENAULT KADJAR||75,1,5|49,55|

dans ce tableau : renault a les rubriques suivant  : 
- notre selection 
- nos véhicules
- occasion


## creation de shortcode dans lib auto 



### CategoriesService 

categoriesauto.service  est CategoriesService 

dans cette classe on a 3 methodes qui sont  : 
- getElementsCategoriesRepository() qui retourne une classe elementcategoriesRepository, cette classe hérite de elementsCategoriesRepository
- getAllCatagoriesAndElementsCategories($categorie_id)
- getElementsCategoriesProduitsRepository()


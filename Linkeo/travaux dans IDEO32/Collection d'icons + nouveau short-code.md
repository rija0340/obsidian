---
tags  : ideo32_work,ideo3.2_work
url : https://trello.com/c/TdaHcPnj/250-collection-dicons-nouveau-short-code
date : 2023-02-17
---

comprehension du flow du work  : 

* creation de menu de configuration (select dans la backoffice)
* choix par defaut (outline)
* enregistrement choix dans la base de données
* modifier rendu svg pour considerer choix de collection dans la backoffice

### partie Rija  : 
* modification de SvgTagHandler pour accepter un autre shortcode pattern.
* modification pattern regex dans gestionContenuUtil/module.config.php 

### partie Jonathan

creation html et inserction dans la backoffice 
numero du révision  : r10450
* creation de html du select 
* creation du view iconsCollection qui utilise l'html ainsi que le modele (setting )
	* definition des methodes evenements sur le html 
* insertion du View dans panelparams 

### test
effacement de la valeur dans la base de données : ajout de gestion de ce cas

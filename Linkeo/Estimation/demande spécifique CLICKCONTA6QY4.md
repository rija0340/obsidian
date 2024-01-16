---
code bouton  : CLICKCONTA6QY4
url site  : ### http://delattreimmo.fr/
ticket référence pour intégration passerelle  : http://jira.linkeo.com/browse/IDEO-6238
documentation apimo  : https://apimo.net/fr/api/webservice/
rappel : effacement de tous les produits à chaque insertion de flux de données par passerelle 
---

Demande  : 

- différencier le particulier du professionnel sur le site ainsi que de classer par type de bien (bar, restau, tabac, commerce, etc..)  
- classer les mandats par simple ou exclusif (commentaire dans ticket pas de champ spécifique pour mandat )
## Point numéro 1 : 

Après observation du flux données venant presta Apimo : 

- Il n'y a pas de champs spécifique pour 
	- particulier
	- professionnel 
- Même chose pour type de bien, pas de champs spécifique pour 
	- bar
	- restaurant
	- tabac
	- commerce 
	- etc 

Question : comment catégoriser les produits  sur le site alors ? 

- je ne sais pas si c'est possible de créer des catégories et de les affecter sur les produits selon titre au moment enregistrement dans la base de données. 
## simulation passerelle en local 

```url
http://localhost/immo/delattreimmo/public/catalogues/api/import.php?key=b827de56268f5b46247da0bf8b1c253db4fed633&file-product=apimo&codeSupplier=3220&keyAgency="b73b28078247b2ed6e903c9d533b1ca8d11dcb28"&codeAgency=14784
```
## etude des fichiers  : 

- ImportsApimoAbstract.class.php

les logiques suivi sont dans ce fichier : 
- recupération du json data venant presta
- loop sur le json correspondance entre donnée presta et donnée lib immo 
### type de bien 

le type de bien est défini par cette ligne  : 

```php
$dataProd[array_search("produit_marque", $this->enteteProduits)] = $this->checkType($row['type']);
```
la fonction checkType() retourne un string qui est le nom du type de bien. 
Il check la valeur du champ "type" dans le json et retourne une valeur string selon la correspondance dans  https://apimo.net/fr/api/r%C3%A9f%C3%A9rentiel/property_type 


---

url site  : https://www.elagage-vouhe.com/elagage.php
---
![[image.png]]
* verifier l'erreur et debuger en ligne , utilisant debug = true comme parametre url 
* zone undefined (sur check error en ligne) qui appelle la methode getInitErrors (dans le message slack)
* sync down pour pouvoir tester sur DID
* recuperation de filesystem et ajout de console log pour voir les parametre dans le fichier pageview
	console.log(this.currentZoneID); > undefined
 
	console.log(this.model.main_zone);	 > 200

### instruction  : tonga dia jereo izay anaty base : 
possible cause ? 
compareo ideo302 sy 303
comparaison contenu page sur front et backoffice
zone 191 - 200 ve misy mampiasa ankotran le page 9

SELECT * FROM `ID303_pages` WHERE mainZone IN (191, 192, 193, 194, 195, 196, 197, 198, 199, 200,90)

sql query for updating the page zone  : 
UPDATE `CLICKCONTA667W`.`ID303_pages` SET `mainZone` = '91' WHERE `ID303_pages`.`id` = 9;

<span class="text-danger">Cause erreur</span> : la page dans la base de donnée utilise une référence de zone qui n'existe pas.
la zone n'existe pas dans la table zone. Puis on a vérifié dans la table zone ce qui ont comme page parente la page en question. on a constaté que une autre zone a comme page parente la page en question et on utilisé cette zone pour  la page.

<span style="color : yellow"> pourqoui la reference de zone a changé ? </span> peut etre lp support ????
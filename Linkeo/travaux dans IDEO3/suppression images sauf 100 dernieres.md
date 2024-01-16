---
tags : ideo3_work, CLICKCONTA6KJ5
url : http://jira.linkeo.com/browse/IDEO-6671
date : 2023-03-15
---

[[suppression images CLICKCONTA6KJ5]] ticket de reference

lors export base DID on constate que le nombre de items dans table ressources_collections n'est pas le meme que dans la meme table mais sur un sauvegarde fait au début de traitement du ticket origine. (ticket suppression images avant 2021)

DELETE FROM table_name;
/var/www/html/testCode/csv/restedes100todelete.csv

<span style="font-size : 20px">Mise en pause eo amin'ny creation  requete amafa donnée anaty ressources sy table ressources_collections </span>


situation avant suppression  : 
* nombre de entry dans table ressources  : 1254 (dont 1103 images)
* nombre entry dans table ressources_collections : 688

apres suppression  : 

* nombre entry dans table ressources  : 251 ( 100 images) (1003 deleted)
* nombre entry dans table ressources_collections : 167 (521 deleted)

reto sary telo ireto ao anaty dossier source fa tsy anaty bdd : 

1db4390428c8.jpg
136f567b7ae3.jpg
f2e80de5200d.jpg

comparaison entre les 100 images de la base de données et liste nom images du dossiers sources  : toutes les 100 sont dans le dossier 
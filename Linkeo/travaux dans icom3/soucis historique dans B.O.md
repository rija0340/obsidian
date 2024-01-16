---
tags  : icom3_work, LINKDIRECT69GB
url : 
date : 2023-06-29
---

site en ligne mjcreation -> systeme historique marche
site en ligne https://www.ideo-catalogue-australiia.com -> mandeha

table contenant versionning  : IC301_zone_version

page : homeTop, disparition content confirmé, en train de voir dans la base de donnée en cours


7h49 25 tsy misy ninina, ( dans page test)
7h49 29 misy paragraphe ( dans page test)

Notice: Undefined offset: 3568 in /home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3/module/Gestioncontenu/src/Gestioncontenu/Model/ContentProvider.php on line _461_


### details sur hometop 

page > zone > section > colonne > block

#### page 
id : 2
name  : homeTop
ref  : PAGE_0VANP7FZTA
layout  : LAYOUT_L0Q80BKY42
mainzone : 

#### zone ( type : header, footer, content ...)

id : 7
name : header 
refZoneName : header
ref  : ZONE_6I2G4KV57F
template  : {{{SECTION_XU9GRJ3OL6}}}
parentpage : 2

#### zone version 
id : 629


#### section 
id  : 27319
ref : SECTION_XU9GRJ3OL6
template  : COLUMN_PH6X65FR0M
parentZone : 7

#### colonne
id : 4266,32761
ref  : COLUMN_PH6X65FR0M
template  : BLOCK_ILOXB8W31N

## Fonctionnement versionning
rehefa manova an'ilay version aho dia tokon miova nu template ao anatin'ilay zone, io tamplate io dia section
io version ana section io dia alaina any amin'ny table  zone_version


## JEREO ZAY METY AMINN'IREO

SECTION_XU9GRJ3OL6

UPDATE `LINKDIRECT69GB`.`IC301_column` SET `parentSection` = '27319' WHERE `IC301_column`.`id` = 4266;

ty zavatra ity manao erreura amion'ny front 

Notice: Undefined offset: 3568 in /home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3/module/Gestioncontenu/src/Gestioncontenu/Model/ContentProvider.php




page accueil , manana zone dia reo zone reo misy section lié aminy (9 isany), kanefa reo section reo misy tsy mampiasa column, kanefa itan'ny 

page  : id 18, 
zone id  :  zone 108
section  : parent zone 108 
id parent section  : 27319 ,4266 (ity no mety atao amin'ny block, parent column)


non useful section  : 

SECTION_HQRN90V3YU
SECTION_44XQVMCQJQ

32761


section miasa ao anati'ilay zone
SECTION_XU9GRJ3OL6

reto ny zone version mampiasa ilay 4266 : 1173,910,428
reto kosa no mampiasa io section ambony io  : 

###bdd pages 

http://localhost/phpmyadmin/sql.php?server=1&db=LINKDIRECT69GB&table=IC301_pages&pos=0&token=d1a11bb408a3f698c5387ebb4b151cdc#PMAURL-0:sql.php?db=LINKDIRECT69GB&table=IC301_pages&server=1&target=&token=d1a11bb408a3f698c5387ebb4b151cdc

###bdd zone 

http://localhost/phpmyadmin/sql.php?server=1&db=LINKDIRECT69GB&table=IC301_zone&pos=0&token=d1a11bb408a3f698c5387ebb4b151cdc#PMAURL-0:sql.php?db=LINKDIRECT69GB&table=IC301_zone&server=1&target=&token=d1a11bb408a3f698c5387ebb4b151cdc

### bdd section 

http://localhost/phpmyadmin/sql.php?server=1&db=LINKDIRECT69GB&table=IC301_section&pos=0&token=d1a11bb408a3f698c5387ebb4b151cdc#PMAURL-0:sql.php?db=LINKDIRECT69GB&table=IC301_section&server=1&target=&token=d1a11bb408a3f698c5387ebb4b151cdc

bdd column 

http://localhost/phpmyadmin/sql.php?server=1&db=LINKDIRECT69GB&table=IC301_column&pos=0&token=d1a11bb408a3f698c5387ebb4b151cdc#PMAURL-0:sql.php?db=LINKDIRECT69GB&table=IC301_column&server=1&target=&token=d1a11bb408a3f698c5387ebb4b151cdc
---
tags  : ideo32_work,ideo3.2_work
url : https://trello.com/c/OsYXEURw/278-aria-label-zoom
date : 2023-06-20
revision :
---

check bdd pour voir ce qui change quand on active bouton zoomer : 

pour block image  : type = 4  (zoomer) 
pour grille  : linkAction  = 1 (clickable) (utiise blockAbstractCollectionImage) addActionLink method
pour carroussel  : Action = 1  (utiise blockAbstractCollectionImage) addActionLink method
pour gallerie  : galerieAction = 1 (utiise blockAbstractCollectionImage) addActionLink method

## fichiers concernés

M       module/GestionContenuUtil/src/GestionContenuUtil/Core/BlockModuleHandlers/BlockAbstractCollectionImage.php
M       module/GestionContenuUtil/src/GestionContenuUtil/Core/BlockModuleHandlers/BlockImageHandler.php
M       module/GestionContenuUtil/src/GestionContenuUtil/language/default.php
M       module/GestionContenuUtil/src/GestionContenuUtil/language/en_AU.php
M       module/GestionContenuUtil/src/GestionContenuUtil/language/en_CA.php
M       module/GestionContenuUtil/src/GestionContenuUtil/language/en_FR.php
M       module/GestionContenuUtil/src/GestionContenuUtil/language/en_US.php
M       module/GestionContenuUtil/src/GestionContenuUtil/language/es_CA.php
M       module/GestionContenuUtil/src/GestionContenuUtil/language/es_FR.php
M       module/GestionContenuUtil/src/GestionContenuUtil/language/es_US.php
M       module/GestionContenuUtil/src/GestionContenuUtil/language/fr_CA.php
M       module/GestionContenuUtil/src/GestionContenuUtil/language/fr_FR.php
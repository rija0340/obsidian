---
tags  : ideo32_work,ideo3.2_work
url : https://trello.com/c/3q88Vpx5/214-css-print
date : 2023-02-23
revision :
---

Estimation  : 

* recherche ou est-ce qu'on ajoute le link dans header pour importer ambiance.min.css
* apres utilisation de xdebug visual code sur ideo3.2, ligne 646 dans AmbianceEngineRenderer : $ambianceUrl
* sur la ligne 651 on a dans le debuger la ligne correspondante  : "<link href="<?php echo _PTR_ ?>/css/ambiance.min.css?v=1655875258" rel="stylesheet" type="text/css">" celui qu'on recherche
* comment on peut faire la même chose pour print.min.css
* dans vendor/CoreMoteurDeRendu/config/module.config.php -> on a aussi les ligne suivante  : 
```shell
'zone_prefix' => 'z',

'path_css_minify' => '/css/styles',

'ambiance_path_css_minify' => '/css/ambiance',

'ext_css_minify' => 'min.css'

```

revision sarah sur timestamp : 10005
revision Jonhatan sur google font  :  10400 ^a2ba24

## documentation sur pourquoi ajouter timestamp comme parametre

```text
 If there is no timestamp or version parameter in the URL of a CSS file, the browser will still send a request to the server that includes an "If-Modified-Since" header on subsequent requests.
 The server will use the timestamp in the "If-Modified-Since" header to determine whether the CSS file has been modified since the last request. If the file has not been modified, the server will respond with a "304 Not Modified" status code and no content, indicating to the browser that it should continue to use the cached copy of the file. If the file has been modified, the server will respond with the new version of the file along with a new modification timestamp.

  __However__, if there is no timestamp or version parameter in the URL, the browser may cache the file for a longer period of time, which could lead to users seeing an outdated version of the CSS file.  <span class="text-danger"> By including a timestamp or version parameter in the URL, you can ensure that the browser checks for a new version of the file on each request <span> , rather than relying on its cached copy.

pour savoir quelles fichiers utilisent l'invalidation de page , rechercher la fonction invalidate [[#^a2ba24]]
```

## liste des fichiers modifié  : (normalement semblale aux revisions cités en haut mais avec module.config.php)

module/ConstManager/src/ConstManager/Controller/ConstRestController.php
module/Gestioncontenu/src/Gestioncontenu/Controller/InvalidatePageRestController.php
module/Gestioncontenu/src/Gestioncontenu/Controller/PageRestController.php
module/Gestioncontenu/src/Gestioncontenu/Service/PageApi.php
module/MenuTemplate01/src/MenuTemplate01/Controller/MenuRestController.php
vendor/CoreConfigurationService/config/module.config.php
vendor/CoreConfigurationService/src/CoreConfigurationService/Controller/IndexController.php
vendor/CoreMoteurDeRendu/config/module.config.php
vendor/CoreMoteurDeRendu/src/CoreMoteurDeRendu/Core/AmbianceEngineRenderer.php
vendor/CoreMoteurDeRendu/src/CoreMoteurDeRendu/Core/Resources/LinkResource.php

on a effectué ajout de ressource dans AmbianceEngineRenderer ...

<span class="text-danger">AmbianceEnginerRenderer</span> : pour ajouter des ressources à la page qu'on va generer

## comment gulpfile est utilisé dans lib IDEO3.2
pour rappel , c'est un fichier qui contient des tasks à executer par gulp ( minifying and concatenating files, compiling code, optimizing images, and more.)
* gulpfile contient les tasks à executer 
* GulpHandler contient une fonction qui execute les tasks dans gulpfile , methode  : function compileStylesTemplate()
* PageWriter utilise cette fonction dans une fonction  : recompileLayoutTemplate()
* ConstantManager utilise cette fonction dans une fonction  : checkLayoutTemplate()
* Index controller ainsi que PcoController utilisent cette fonction



confirmation 
*  est ce qu'une fois généré  le print.min.css  garde sa timestamp et ne ce dernier ne sera modifié qu'aprés une autre génération du fichier
* ou après chaque modification ambiance css dans B.O le print.min.css aura un nouveau timestamp

#invalidation_page #invalidation pour ohatra manova zavatra anaty oglet params
manova css anaty design  
miappelle api nanao invalidation de tout les pages



ce 03-04-2023
liste des fichiers dans svn st

```shell
M       #librairies/module/ConstManager/src/ConstManager/Controller/ConstRestController.php
M       #librairies/module/ConstManager/src/ConstManager/Manager/ConstantManager.php
M       #librairies/module/Gestioncontenu/src/Gestioncontenu/Controller/InvalidatePageRestController.php
M       #librairies/module/Gestioncontenu/src/Gestioncontenu/Controller/PageRestController.php
M       #librairies/module/Gestioncontenu/src/Gestioncontenu/Service/PageApi.php
M       #librairies/module/Gestioncontenu/src/Gestioncontenu/Service/PageWriter.php
M       #librairies/module/MenuTemplate01/src/MenuTemplate01/Controller/MenuRestController.php
X       #librairies/public/integration
M       #librairies/vendor/CoreConfigurationService/src/CoreConfigurationService/Controller/IndexController.php
M       #librairies/vendor/CoreCssLess/src/CoreCssLess/Core/Processors/GulpHandler.php
M       #librairies/vendor/CoreMoteurDeRendu/config/module.config.php
M       #librairies/vendor/CoreMoteurDeRendu/src/CoreMoteurDeRendu/Core/AmbianceEngineRenderer.php
M       #librairies/vendor/CoreMoteurDeRendu/src/CoreMoteurDeRendu/Core/Resources/LinkResource.php
M       #librairies/vendor/CoreMoteurDeRendu/src/CoreMoteurDeRendu/Service/ResourceDispatcherService.php

```

ireto mila atao revert

vendor/CoreConfigurationService/src/CoreConfigurationService/Controller/IndexController.php

module/Gestioncontenu/src/Gestioncontenu/Service/PageWriter.php
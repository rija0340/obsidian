---
tags  : ideo32_work,ideo3.2_work
url : https://trello.com/b/h5DP05ns/wishlist-ideo3
date : 2023-05-09
revision :
référence : https://trello.com/c/ztP5TyKm/127-gestion-popup-modale-cms
---
Gestion popup (modale) CMS
https://trello.com/c/ztP5TyKm/127-gestion-popup-modale-cms

pour voir des fonctionnement similaire, voir buttonstyleview sns (Sarah)

dans ideo 3 svn log 

```text
------------------------------------------------------------------------
r9796 | srazanandralisoa | 2022-11-15 12:23:44 +0300 (tlt 15 Nov 2022) | 1 ligne

Wishlist IDEO: gestion popup ajout Style partie PHP 
------------------------------------------------------------------------
r9763 | srazanandralisoa | 2022-11-10 12:00:09 +0300 (lkm 10 Nov 2022) | 1 ligne

Wishlist IDEO popup : retour sur le sessionStorage
------------------------------------------------------------------------
r9757 | jn.harison | 2022-11-09 18:02:38 +0300 (lrb 09 Nov 2022) | 1 ligne

Wishlist IDEO3 POPUP: Updating sessionStorage for the popup
------------------------------------------------------------------------
r9756 | jn.harison | 2022-11-09 16:59:30 +0300 (lrb 09 Nov 2022) | 1 ligne

Wishlist IDEO3 POPUP:not rendering if inactive & setting the default stat to inactive
------------------------------------------------------------------------
r9748 | srazanandralisoa | 2022-11-08 14:51:44 +0300 (tlt 08 Nov 2022) | 1 ligne

retour wishlist gestion popup cms PHP
------------------------------------------------------------------------
r9727 | srazanandralisoa | 2022-11-07 12:17:55 +0300 (lts 07 Nov 2022) | 1 ligne

wishlist IDEO: gestion popup CMS suite
------------------------------------------------------------------------
r9721 | srazanandralisoa | 2022-11-04 12:41:00 +0300 (zom 04 Nov 2022) | 1 ligne

wishlist IDEO3: gestion popup modale CMS partie PHP
------------------------------------------------------------------------
```

## premier commit dans partie php

```shell
r9721 | srazanandralisoa | 2022-11-04 12:41:00 +0300 (zom 04 Nov 2022) | 1 ligne
Chemins modifiés :
   M /branches/dev/#librairies/module/GestionContenuUtil/src/GestionContenuUtil/Services/OptionParserService.php
   M /branches/dev/#librairies/module/Gestioncontenu/src/Gestioncontenu/Model/ContentProvider.php
   M /branches/dev/#librairies/module/Gestioncontenu/src/Gestioncontenu/Model/PreviewerContentProvider.php
   M /branches/dev/#librairies/vendor/CoreMoteurDeRendu/src/CoreMoteurDeRendu/Core/Ambiance/Section.php
   M /branches/dev/#librairies/vendor/CoreMoteurDeRendu/src/CoreMoteurDeRendu/Core/AmbianceEngineRenderer.php

wishlist IDEO3: gestion popup modale CMS partie PHP
```

dans section.php on a un getsetispopu et setIspopup

## estimation 

- ajout de menu dans backoffice  : 1jour (0.5 chercher code existante, 0.5 ajout de code pour nouveaux parametres)
- ajout des paramétre dans base de donnees : 1 jour
- ajustement code pour prendre en compte toast (section, ambiancerenderer .... ) - 2jours
- mise en marche toast (methode pour afficher un toast ) ->2 jours 
- marge de test  - 1 jour

<span class="remarque" > Remarque </span> raha azoko tsara zan dia tsy manao anle partie poup sns tsony fa manampy parametre dia manao traitement mifanaraka amin'iny aty amin'ny front aveo , 
ao anatin'izay traitement aty amin'ny front izay dia tsy maintsy mijery anreo efa vitan Sarah mba hahafahana manampy anle toast


exemple de configuration pour ideo 3 cd eurospa (json pour une section ) : 

```json 

[{"optionType":"popup","activeType":1,"dateDebut":"","dateFin":"","priority":40},{"optionType":"popupStyle","size":"small","priority":60},{"optionType":"advancedCSS","priority":200,"cssClasses":""}]


```

<span class="titre1" > ny ifandaraisan'ny model sy view dia ao amin'ny    </span> 
/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/public/integration/src/js/JEditor/PagePanel/Contents/Ancestors/Content.js

satria rehefa mampiasa anle hoe this.model ao anatin'ny view dia tsy hita oe aiza le model no declaré


## retain all the things you have done and write them 

### deux choices dans option block dans pagepanel 
dans page panel, on a deux différentes sorte de item  : 
les avec pop et les sans pop up durant hover on the element 

ils sont géré differemment car les sans pop up integre un input tandis que l'autre est faite juste de span


### block pour avoir option avec modal on hover 

```html

```html
<!--  gdgdfgdfgdfgdfgdfg-->
<div class="panel-option-container gallery-template-option  animated ">
<!-- Debut Couleur du bloc-->
<article class="panel-option animations">
<header>
   <h3 class="option-name">
      <span class="icon-button-size icon-midsize"></span>
      <%=__("displayPopup")%>
   </h3>
   <span class="panel-content-legend">
   <%=__("displayPopupLegend")%>
   </span>
</header>
<div class="category-content radio-transformed">
   <div>
      <span class="effect-radio display-choice <%=(display==='modal')?'active':''%>" data-value="modal" data-helper="">
      <span class="helper">
      <span class="help">Modal</span>
      <span class="bottom"></span>
      </span>
      <span class="container">
      <span class=" icon-modal">
      </span>
      <span class="switch-container">
      <span class="radio"><span>
      </span>
      </span>
      </span>
   </div>
   <div>
      <span class="effect-radio display-choice <%=(display==='toast')?'active':''%>" id="" data-value="toast" data-helper="">
      <span class="helper">
      <span class="help">Toast</span>
      <span class="bottom"></span>
      </span>
      <span class="container">
      <span class=" icon-toast">
      </span>
      <span class="switch-container">
      <span class="radio"><span>
      </span>
      </span>
      </span>
   </div>
</div>
```

### handler dans view 

```js 
displayChange: function(event) {
    this.$(".display-choice").removeClass("active");
    var $target = $(event.currentTarget);
    $target.addClass("active");
    var value = $target.attr("data-value");
    if (value == "modal") {
        this.$(".alignment-container").css("display", "none");
    } else {
        this.$(".alignment-container").css("display", "block");
    }

    this.model.display = value;
},
```


NB :  ne pas oublier de mettre l' evenement dans view : click, change  etc

### block sans modal 

voir dans popupstyle.html et ceux qui sont avec des input 
handler dans popupstyleview.js


### json apres ajout 


```json
[
   {
      "optionType":"popup",
      "activeType":2,
      "dateDebut":"",
      "dateFin":"",
      "priority":40
   },
   {
      "optionType":"popupStyle",
      "size":"tiny",
      "priority":60,
      "display":"modal",
      "alignment":"bottom-left"
   },
   {
      "optionType":"advancedCSS",
      "priority":200,
      "cssClasses":""
   }
]
```


ajout de css dans ce fichier less  : (car l'ancien abc s'y trouve)

```path
/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/public/integration/src/less/imports/page_panel/module/block-options/advanced-option.less
```


commit des fichiers :  envoyer ou pas le fichier minifié ?


## commit 

vn ci -m "évolution "popup" : ajouter un mode "toast"" vendor/CoreMoteurDeRendu/src/CoreMoteurDeRendu/Core/Ambiance/Section.php vendor/CoreMoteurDeRendu/src/CoreMoteurDeRendu/Core/AmbianceEngineRenderer.php public/integration/src/js/JEditor/PagePanel/Contents/Options/Models/PopupStyle.js public/integration/src/js/JEditor/PagePanel/Contents/Options/Templates/popupStyle.html public/integration/src/js/JEditor/PagePanel/Contents/Options/Views/PopupStyleView.js public/integration/src/js/JEditor/PagePanel/Contents/Options/nls/fr-ca/i18n.js public/integration/src/js/JEditor/PagePanel/Contents/Options/nls/fr-fr/i18n.js public/integration/src/js/JEditor/PagePanel/Contents/Options/nls/i18n.js public/integration/src/less/imports/page_panel/module/block-options/advanced-option.less



commit list pour ajout couleur toast

?       #librairies3
X       public/integration
M       vendor/CoreMoteurDeRendu/src/CoreMoteurDeRendu/Core/AmbianceEngineRenderer.php

Vérification de l'état sur la référence externe en 'public/integration' :
?       public/integration/src/js/JEditor/Commons/libraries/bower_components
M       public/integration/src/js/JEditor/PagePanel/Contents/Options/Models/PopupStyle.js
M       public/integration/src/js/JEditor/PagePanel/Contents/Options/Templates/popupStyle.html
M       public/integration/src/js/JEditor/PagePanel/Contents/Options/Views/PopupStyleView.js
M       public/integration/src/js/JEditor/PagePanel/Contents/Options/nls/fr-ca/i18n.js
M       public/integration/src/js/JEditor/PagePanel/Contents/Options/nls/fr-fr/i18n.js
M       public/integration/src/js/JEditor/PagePanel/Contents/Options/nls/i18n.js



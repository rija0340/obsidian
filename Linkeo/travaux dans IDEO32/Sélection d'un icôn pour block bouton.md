---
date: 2023-10-26
url: https://trello.com/c/C5DJf241/322-s%C3%A9lection-dune-icon-pour-les-boutons
tags:
  - ideo32_work
---
tâche à faire 
- ajout de bouton "afficher l'icone" dans style button (0.25)
- affichage parcourir les iconnes au dessus du button afficher icone si c'est coché (0.25) 
- click sur btn parcourir -> ouverture d'un modal contenant liste des icones (selon config icon à utiliser dans params panel  B.O) (0.25)
- ne sélectionner qu'un seul icon ( radio)
- il faut cliquer sur choisir pour valider choix et fermer modal (0.25)
- affichage apercu de l'icone sélectionnée entre bouton afficher l'icoet et parcourir les icones (0.25)
- il faut cliquer sur btn appliquer du rightpanel pour appliquer les changement(0.25)
- si afficher icone est coché mais pas d'icone sélectionnée, il ne faut pas sauvegarder l'option cochée

rendu front : (0.5)
- chercher le template du bouton et suivre modification dans ticket
- le svg icon est rendu a partir de shortcode 

marge : 1 jour 

## tuto documentation  : 

+ ajout de bouton 
	-> modification dans le fichier template de l'option style .html ( à expliquer plus tard )
	-> j'ai pu trouver un element checkbox depuis le block carroussel 
- ajout de translation dans les fichiers translations  : 
	-> il faut chercher des existant et puis ajouter pour tous les fichiers de translation

azavaina tsara ny marche natao 

eo amle mijer anle template tsika zo 
- listing anle icone 
- aazona anle icon miasa avy any anaty base (jereo ny )



flow de fetch data et affichange dans le modal 

- ajout d'attribut 'icon ' sur modèle




efa mandeha le requete maka svg 
- a faire 
	- mijer anle fomba ametaahana svg au chargememnt 
	- rendu front 

## liste des fichiers impacté  


### dans integration  : 

src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Models/ButtonStyleOption.js
src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Models/Svg.js
src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Models/SvgCollection.js
src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Templates/buttonStyleOption.html
src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Templates/selectIcon.html
src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Views/ButtonStyleOptionView.js
src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Views/SelectIconView.js
src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/nls/fr-ca/i18n.js
src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/nls/fr-fr/i18n.js
src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/nls/i18n.js

src/less/imports/blockButton.less
src/less/main.less

REVISION : r11534
### dans librairies 

module/GestionContenuUtil/src/GestionContenuUtil/Core/BlockModuleHandlers/BlockBoutonHandler.php
module/Gestioncontenu/config/module.config.php
vendor/CoreRessourceManager/src/CoreRessourceManager/Controller/ResourceRestController.php

REVISION : r11533

documentation procédure à ecrire 

fichier modifié pour retour  : 

src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Models/ButtonStyleOption.js
src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Models/SvgCollection.js
src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Templates/buttonBlock.html
src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Templates/buttonStyleOption.html
src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Templates/selectIcon.html
src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Views/ButtonBlockView.js
src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Views/ButtonStyleOptionView.js
src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Views/SelectIconView.js
src/less/imports/button_block/button_block.less
src/less/imports/button_block/styleOptions.less
src/less/main.less

## Ajout de la possiblité de choisir un icon dans l'option style du block button 
https://trello.com/c/C5DJf241/322-s%C3%A9lection-dune-icon-pour-les-


pour le travail on  fait ces choses  : 

- ajout d'un checkbox dans la view style du bouton 

![[Pasted image 20231110101025.png]]

- ajout d'un bouton trigger d'un modal lorsque le  checkbox 'afficher l'icône' est checké 

![[Pasted image 20231110101042.png]]


- ajout d'un modal qui contient liste des icônes (icônes de type selon la configuration collection icône à utlisaler dans params panel ) 

![[Pasted image 20231110101114.png]]


voici aussi des détails sur la fonctionnalité de cette nouvelle option  : 

- à l' ajout d'un block bouton le checkbox "afficher l'icône " est décoché par defaut 
- au moment ou on selectionne un icon et clicker sur le bouton choisir du modale, on a le icon qui sera afficher entre le checkox et le bouton "parcourir ", ainsi qu' afficher sur l'appercu du block dans la pageview 
- si on ne sauvegarde par la modification (qui se fait par click du bouton appliquer du rightpanel ), l'icone choisi n'est pas sauvegardé 

## Ajout des boutons 

l'ajout des deux boutons : 
- afficher l'icone 
- parcourir les boutons 
se fait par la modification du fichier html   : ibrairies/public/integration/src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Templates/buttonStyleOption.html.
Les événements rattachés à ces boutons sont dans le view  : librairies/public/integration/src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/Views/ButtonStyleOptionView.js

## Ajout de modal 

Au click du bouton "parcourir les icones", un modal apparaît. Ce modal est instancié dans le view ButtonStyleOptionView.js. 
Le template html qui est utlisé dans ce view est  : selectIcon.html

Dans la fonction initialize de  ButtonStyleOptionView, on a cette ligne   : 
```js 
this.selectIconDialog = new SelectIconView();
```

La view SelectIconView est un view qui extend un DialogView de backbone. 

## Contenu du modal (obtention de la liste des icônes)

Pour avoir la liste des icônes selon la collection utilisé dans le params panel, on a crée un model svgCollection  : 
Dans ce modèle, on a un url  : 

```js
url: function() {
	return __IDEO_API_PATH__ + "/resources-svgcollection/" + this.name + ( this.svgName != '' ? "/" + this.svgName :'' );
},
```

cette url est utilsé lorsque qu'on fait un fetch sur l'objet svgCollection 

regardons le contenu de la méthode fetchIcons maintenant  : 

```js
fetchIcons: function(callback) {
	var self = this;
	this.params = new Params();
	this.params.fetch().done((function(data) {
		self.name = data.IconsCollection || 'outline';
		self.fetch({
			success: function(collection, response, options) {
				callback(null, response);
			},
			error: function(collection, response, options) {
				callback(new Error('Failed to fetch SVG'));
			}
	
	})).fail(function(error) {
		console.log(error);
},
```

On obtient le nom de la collection par le fetch de l'objet params.
On a comme paramètre de la fonction une fonction callback.  Ce qui est une bonne pratique lorsqu'on fait des opération asychrone comme le fetch de data. 
on peut fetcher soit un seul svg, soit le contenu d'un dossier collection de svg. (les icônes sont des svg) par cette fonction.
#### Moment ou on fetch un ou des svgs

- au chargement deblock bouton  dans la pageview ( se fait dans : ButtonBlockView -> render()) (s'il le block a un icôn)
- au moment de mise a jour apercu de bouton block dans pageview (se fait dans  : ButtonBlockView -> renderOptions())
- au moment render de la view ButtonStyleOptionView (si le block bouton a un icôn)
- ou moment de l'affichage du modal (fetch des svgs) (se fait avec l'appel du modal dans ButtonStyleOptionView)
	- dans cette methode _onClickBrowseIcons
	- on passe un paramètre nom svg utilisé si le bouton a un icon pour qu'on puisse ajouter une classe 'selected-icon' à l'icône utilisé parmi la liste 

## partie php pour le fetch 

on a ajouté une route dans  : 
module/Gestioncontenu/config/module.config.php

```php
	'svgs' => array(
	'type' => 'segment',
	'options' => array(
	'route' => ADMIN_PATH . '/resources-svgcollection/:name[/:svg-name]',
	'constraints' => array(
	'name'=> '[a-zA-Z]*',
	'svg-name'=>'[a-zA-Z]+\d*\.svg$'
	),
	'defaults' => array(
	'controller' => 'CoreRessourceManager\Controller\ResourceRest',
	'action'=>'getSvgCollection'
	),
	),
	'may_terminate' => true,

),
```

et puis une méthode dans ResousceRestController : 

```php
    /**
     * Function pour retourner liste des icônes ou un icône dans un dossier
     * @param name nom 
     */
      public function getSvgCollectionAction($name)
      {
        $name = $this->getEvent()->getRouteMatch()->getParam('name');
        $svgName = $this->getEvent()->getRouteMatch()->getParam('svg-name');
       
        
        if(!is_null($svgName)){
            $path = rtrim(AMBIANCE_FOLDER_PATH, '/') . '/' . AMBIANCE_REF .'/svg/'.$name.'_collection/'.$svgName;
            $svgToReturn = array(
                "name"=>basename($svgName),
                "content"=>(file_get_contents($path) == false ? '':file_get_contents($path))
            );
        }else{
            $svgToReturn = array();
            $path = rtrim(AMBIANCE_FOLDER_PATH, '/') . '/' . AMBIANCE_REF .'/svg/'.$name.'_collection'.'/*.svg';
            $files = glob($path);
            foreach ($files as $file) {
                $svg = array(
                    "name"=>basename($file),
                    "content"=>file_get_contents($file)
                );
              array_push($svgToReturn,$svg);
            }
        }
        return new \Zend\View\Model\JsonModel($svgToReturn);
      }
```


## flow sélection d'un icôn : 

lorsqu'on choisit un icôn dans le modal et puis on click sur le bouton choisir, voici ce qui se passe  :
La méthode onOk du modal est appelée, voici la méthode  : 

```js 
onOk: function() {
var selectedIcon = this.selected;
var svgObj = this.svgCollection.filter(function(item) {
return item.name === selectedIcon;
})[0];
this.trigger(Events.ButtonEvents.SELECT_ICON, svgObj );
this.$el.dialog('close');
},
```

on trigger un event qui est déclaré dans  : ButtonStyleOptionView

```js 
Events.extend({
ButtonEvents: {
SELECT_ICON: 'selectIcon',
},
})
```

cet event est écouté dans ButtonStyleOptionView, dans la fonction initialize 

```js
this.selectIconDialog = new SelectIconView();
this.listenTo( this.selectIconDialog,Events.ButtonEvents.SELECT_ICON,this.onSelectedIcon);
```

la fonction "onSelectedIcon" qui est appelée dans le listner reçoit en paramètre un "event" qui contient le nom du svg selectionné. (ce nom est passé par le trigger  : svgObj)

dans la fonction onSelectedIcon : 
```js
onSelectedIcon:function(event){
this.selectedIconEl.empty();
this.selectedIconEl.append(event.content);
this.model.icon=event.name;
},
```

on vide le container de l'apercu de l'icone en dessous du bouton ckecbox "afficher l'icône",
on append le contenu de l'icôn dans son container et puis on set le nom de l'icon dans le modele. 

NB : il faut cliquer sur appliquer pour enregistrer le modif et puis sur sauvegarder la page pour enregistrer modif dans la base de donnée

si on click annuler de right panel  : on aura le modél remplacé par le dernier saveState, donc annulation du changement et retour vers le dernier état modèle avant modification.

on a cette fonctionnalité dans   AbstractOption qui est extend par les modèles des options : 

```js
revertChanges: function() {
this.set(_.clone(this._savedState));
},
```

comment notre boutton utilise AbstractOption

```js
var ButtonStyleOption = AbstractOption.extend(
```

## Mise à jour de l'apercu du bouton dans pageview
![[Pasted image 20231110121258.png]]
comme le modèle est modifié lors d'une sélection d'un icôn , le renderOptions dans ButtonBlockView sera appelé.
Dans cette méthode on a implementé un systeme qui met à jour le content à afficher le svg dans l'aperçu

```js 
         renderOptions: function(model, options) {
         	this.$(".blk-button__icon").empty();
         	this.$(".blk-button__label").css('margin-top', '');
         	var svgName = this.model.options.ButtonStyleOption.icon;
         	// fetch icon content
         	if (svgName !== "") {
         		var svgCollectionObj = new SvgCollection({
         			"svgName": svgName
         		});
         		svgCollectionObj.fetchIcons(_.bind(function(error, svg) {
         			if (error) {
         				console.error(error);
         			} else {
         				this.$(".blk-button__label").css('margin-top', '-15px');
         				this.$(".blk-button__icon").empty();
         				this.$(".blk-button__icon").append(svg.content);
         			}
         		}, this));
         	}
         	var sizeButton = this.model.options.ButtonStyleOption.size;
         	var alignButton = this.model.options.ButtonStyleOption.buttonAlignment;
         	var alignText = this.model.options.ButtonStyleOption.textAlignment;
         	var color = this.model.options.ButtonStyleOption.color;
         	this.$(".block-button").attr("class", "block-button " + sizeButton + " " + alignButton + " " + alignText + " " + color);
         	var textButton = this.model.options.ButtonOption.text ? this.model.options.ButtonOption.text : translate('button');
         	this.$(".txt span").text(textButton);
         	return this;
         }

}
```

voici le html pour mieux comprendre le code 

```html
<div class="block-button blk-button <%=size%> <%=buttonAlignment%> <%=textAlignment%> <%=color%>">
<a href="#" class="button">
<span class="ico blk-button__icon aria-hidden="true">
<%=icon%>
</span>
<span class="txt blk-button__label"><span><%=text%></span></span>
</a>
</div>
```

on a du forcé l'alignement du texte et du svg icon dans le rendu par l'ajout du margin-top 
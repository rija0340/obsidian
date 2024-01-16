Un document sur la liste des pages dans B.O : [[PagePanel > pageList]]

## Liste de blocs
Dans le PagePanel, quand une page est sélectionnée, un bouton "ajouter du contenu" apparait en haut à droite 

![[Pasted image 20230811151946.png]]
le html de ce bouton a comme id  : "#available-blocks-trigger"

Dans le code de déclaration des événements dans PagePanel.js, la première ligne attache au click de ce bouton une fonction de callback showAvalaibleBlocks
```js
events : {
	'click #available-blocks-trigger' : 'showAvailableBlocks',
	'click #show-zone-version': 'showZoneVersionsPanel',
	'click .addPage,.empty-content-lang':'onAddPageClick'
}
```

la fonction showAvailableBlocks  : 

```js
showAvailableBlocks: function(column) {
    this.renderRightPanel();
    this.rightPanelView.showContent(this.childViews.availableBlocksView);
    this.rightPanelView.showPanel();
    return false;
}
```


le view "this.childViews.availableBlocksView" n'est rien d'autre que AvalaibleView

```js
this.childViews.availableBlocksView = new AvailableView({
	pagePanel : this
});
```


donc lorsque ce bouton est clické, un rightpanel est affiché. 
Ce rightpanel contient un menu des blocs qui peuvent être ajoutés à une page
![[Pasted image 20230811154117.png]]

### ## Affichage du menu
Ce fichier est le responsable de l'affichage du menu des blocs existant : 
```shell
librairies/public/integration/src/js/JEditor/PagePanel/Contents/Blocks/Block/Views/AvailableView.js
```
ceci est le template html utilisé dans cette view : 
```shell
librairies/public/integration/src/js/JEditor/PagePanel/Contents/Blocks/Block/Templates/availableBlocks.html
```
## AvalaibleView.js

ce qu'on trouve dans ce fichier  : 

-  Déclarations événements liés au menu block  et composition
- Liste des blocs existants 
- Construction du template menu pour être et puis ajout dans le html (AvalaibleBlocks.html)
- Déclaration des fonctions callback utilisées dans les événements

### 1- Catégorisation des blocs

Organisation des blocs, ceci sera utilisé dans la construction du menu
```js
blockOrder: {
	'standard': ["TextBlock", "ImageBlock", "ButtonBlock", "SeparatorBlock", "TableBlock"],
	'advanced': ["CarrouselBlock", "GridBlock","GalerieBlock","CompareBlock", "FormBlock", /*"VideoLinkeoBlock",*/ "MapBlock", "VideoBlock", "HtmlBlock"],
	'others': ["LegalsBlock","SiteMapBlock","SocialNetworkBlock"],
	'ignored':['TwitterTimelineBlock']
}
```

### 2- Construction template menu blocs disponible 

![[Pasted image 20230811160040.png]]

### ##  fonciton initialize : 

dans cette fonction un tableau d'objets, plus précisément un tableau de d'objet blocs est construite et puis assigné à la variable "this.modelLib".
Voici le code pour la construction : 

```js
for (var category in this.blockOrder) {
    if (category === 'ignored')
        continue;
    var currentCategory = this.blockOrder[category];
    this.modelLib[category] = [];
    for (var i = 0; i < currentCategory.length; i++) {
        try {
            var type = currentCategory[i].replace('Block', '').toLowerCase();
            var constructor = Blocks[currentCategory[i]];
            var icon = constructor.ICON ? constructor.ICON : '';
            var className = type + '-block';
            if (constructor.ACCESS_CONTROL === true && !this.app.user.can("use" + currentCategory[i], constructor.ACCESS_CONTROL_CRITERIA)) {
                continue;
            }
            this.modelLib[category].push({
                model: constructor,
                class: className,
                icon: icon,
                type: type
            });
        } catch (e) {
            console.error(e.stack);
        }
    }
}
```

c'est dans la fonction render que le template du menu est construit , à partir du tableau d'objet blocs  disponible

### ## function render
```js 
render: function() {
    this.undelegateEvents();
    this.$el.empty();
    var $frag = $(document.createDocumentFragment());
    var zone = new Zone();
    var section = new Section({}, {
        parent: zone
    });
    var col = new Column({}, {
        parent: section
    });
    for (var category in this.modelLib) {
        var currentCategory = this.modelLib[category];
        if (currentCategory.length > 0)
            $frag.append('<h2 class="option-title">' + translate(category) + '</h2>');
        var $catDiv = $(document.createElement('div'));
        for (var i = 0; i < currentCategory.length; i++) {
            var $block = $(document.createElement('div')).addClass('available simple block ' + currentCategory[i].class).append('<div class="container"><span class="icon ' + currentCategory[i].icon + '"></span><span class="text">' + currentCategory[i].model.BLOCK_NAME + '</span></div>');
            var model = new currentCategory[i].model({}, {
                parent: col
            });
            model.dummy = true;
            col.addChild(model);
            $block.data('model', model);
            $block.draggable({
                revert: true,
                appendTo: $("#page-edit"),
                helper: "clone",
                cursor: "move"
            });
            $catDiv.append($block.get(0));
        }
        $catDiv.addClass('items');
        $frag.append($catDiv);
    }
    this.$el.addClass('available-items');
    this.$el.html(this._template({}));
    this.$el.find('.items').append($frag.get(0));
    //ajout de menu pour composition
    this.createTemplateForCompositions();
    this.scrollables();
    this.delegateEvents();

    return this;
}
```

Dans cette fonction, on construit le menu a partir du tableau d'objet blocs, un bouton pour chaque bloc. 
un div (représentant un bouton) avec des classes pour chaque menu : 
```js
     var $block = $(document.createElement('div')).addClass('available simple block ' + currentCategory[i].class).append('<div class="container"><span class="icon ' + currentCategory[i].icon + '"></span><span class="text">' + currentCategory[i].model.BLOCK_NAME + '</span></div>');
```

et puis chaque div a un attribut data-model contenant l'objet bloc correspondant : 

```js
$block.data('model', model);
```

Un bloc est  placé à l'intérieur d'une colonne. Cette colonne est ensuite située au sein d'une section, et chaque section est rattachée à une zone.

bloc ajouté comme child d'une colonne  :
```js
col.addChild(model);
```

une section déclarée comme parente d'une colonne 
```js 
 var col = new Column({}, {
        parent: section
    });
```

et puis la colonne est attaché à une zone. 
### ## Ajout de block dans une page

- ajout par  drag and drop 
- ajout par clic 
### ### draggable

On peut ajouter un bloc à une page par drag and drop. C'est pour permettre cette fonctionnalité qu'on doit ajouter le modèle à l'attribut data-model du div et de setter le div draggable. 

```js
$block.data('model', model);
$block.draggable({revert: true, appendTo: $("#page-edit"), helper: "clone", cursor: "move"});
```

et aussi un événement est déclaré : 
```js
'dragstart .block.simple.available': '_ondragStart'
```
## ### click

c'est géré par l'événement : 
```js
'click .block.simple.available': 'addToCurrentContainer'
```
## Composition de blocs
Le travail consiste à pouvoir créer des compositions de blocs prédéfinis qui se présentent sous forme de sections

## ## Données de composition

les compositions sont dans un json. Ce json est semblable à ce qu'on peut exporter depuis le backoffice avec des propriétés en moins. (pas de id , ref, template ).

```json
{
   "Compo1":{
      "id":331,
      "ref":"SECTION_733AOS3R40",
      "locked":0,
      "editing":false,
      "template":"",
      "columns":[
         {
            "id":336,
            "ref":"COLUMN_HAEZZH8CMQ",
            "width":6,
            "template":"{{{BLOCK_2Z6TEV9ECO}}}",
            "blocks":[
               {
                  "id":370,
                  "ref":"BLOCK_2Z6TEV9ECO",
                  "type":"html",
                  "options":[
                     {
                        "priority":70,
                        "optionType":"html",
                        "html":"<div id=\"configSheet\" class=\"blk-sheet dzone-configsheet\" aria-hidden=\"true\">\n\t\t<div class=\"blk-sheet__header\">\n\t\t\t<h2>Pr\u00e9f\u00e9rences<\/h2>\n\t\t\t<button type=\"button\" id=\"configSheetCloser\" class=\"button tiny blk-button__link\" aria-label=\"Fermer\">\n\t\t\t\t<span class=\"ico blk-button__icon\" aria-hidden=\"true\">\n\t\t\t\t\t[[svg_include:svg\/tabler_collection\/x.svg]]\n\t\t\t\t<\/span>\n\t\t\t\t<span class=\"txt blk-button__label\">\n\t\t\t\t\t<span>Fermer<\/span>\n\t\t\t\t<\/span>\n\t\t\t<\/button>\n\t\t<\/div>\n\t\t<div class=\"blk-sheet__content\">\n\t\t\t\n\t\t\t<div class=\"blk-sheet__section\">\n\t\t\t\t<h3>Langue<\/h3>\n\t\t\t\t<p>Choisir la langue<\/p>\n    \t\t\t<nav class=\"blk-nav blk-nav--language\">\n\t\t\t\t\t\t[[language_link]]\t\t\t\t<\/nav><\/div>\n\t\t\t\n\t\t\n\t\t\t[[settings]]\n\t\t<\/div>\n\t<\/div>\n",
                        "js":{
                           "content":""
                        },
                        "css":""
                     },
                     {
                        "optionType":"advancedCSS",
                        "priority":200,
                        "cssClasses":""
                     }
                  ]
               }
            ],
            "options":[
               {
                  "optionType":"styles",
                  "priority":90,
                  "_id":"c599",
                  "colorOption":"lead1",
                  "shadeWorn":"level-hight",
                  "contentSize":"xxl"
               },
               {
                  "optionType":"advancedCSS",
                  "priority":200,
                  "cssClasses":"col1"
               }
            ]
         },
         {
            "id":337,
            "ref":"test",
            "width":6,
            "template":"",
            "blocks":[
               {
                  "id":370,
                  "ref":"BLOCK_2Z6TEV9ECO",
                  "type":"html",
                  "options":[
                     {
                        "priority":70,
                        "optionType":"html",
                        "html":"<div id=\"configSheet\" class=\"blk-sheet dzone-configsheet\" aria-hidden=\"true\">\n\t\t<div class=\"blk-sheet__header\">\n\t\t\t<h2>Pr\u00e9f\u00e9rences<\/h2>\n\t\t\t<button type=\"button\" id=\"configSheetCloser\" class=\"button tiny blk-button__link\" aria-label=\"Fermer\">\n\t\t\t\t<span class=\"ico blk-button__icon\" aria-hidden=\"true\">\n\t\t\t\t\t[[svg_include:svg\/tabler_collection\/x.svg]]\n\t\t\t\t<\/span>\n\t\t\t\t<span class=\"txt blk-button__label\">\n\t\t\t\t\t<span>Fermer<\/span>\n\t\t\t\t<\/span>\n\t\t\t<\/button>\n\t\t<\/div>\n\t\t<div class=\"blk-sheet__content\">\n\t\t\t\n\t\t\t<div class=\"blk-sheet__section\">\n\t\t\t\t<h3>Langue<\/h3>\n\t\t\t\t<p>Choisir la langue<\/p>\n    \t\t\t<nav class=\"blk-nav blk-nav--language\">\n\t\t\t\t\t\t[[language_link]]\t\t\t\t<\/nav><\/div>\n\t\t\t\n\t\t\n\t\t\t[[settings]]\n\t\t<\/div>\n\t<\/div>\n",
                        "js":{
                           "content":""
                        },
                        "css":""
                     },
                     {
                        "optionType":"advancedCSS",
                        "priority":200,
                        "cssClasses":""
                     }
                  ]
               }
            ],
            "options":[
               {
                  "optionType":"styles",
                  "priority":90,
                  "_id":"c599",
                  "colorOption":"lead2",
                  "shadeWorn":"level-hight",
                  "contentSize":"xxl"
               },
               {
                  "optionType":"advancedCSS",
                  "priority":200,
                  "cssClasses":"col1"
               }
            ]
         }
      ],
      "options":[
         {
            "optionType":"styles",
            "priority":90,
            "_id":"c525",
            "colorOption":"accent1",
            "shadeWorn":"level-medium",
            "contentSize":"xl",
            "sectionWidth":"full-wide",
            "parentSWidth":"screen",
            "childSWidth":"full-wide"
         },
         {
            "optionType":"advancedCSS",
            "priority":200,
            "cssClasses":"test"
         }
      ]
   }
}
```
## ## construction du menu compositions

On a reprit le même principe que pour le menu de blocs existants : 

- looper les données du json et construction de bouton pour chaque composition
- ajout attribut data-model pour chaque bouton ( div ) . Le modèle ici est une section 
- setter draggable chaque bouton (div)
- ajout du menu dans le template html (celui qui est utilisé pour menu bloc) (fait dans la fonction render)

voici la fonction qui crée cette template de menu : 

```js 
createTemplateForCompositions: function() {
    //liste des compositions keys (compo1, compo2 ...)
    var compositionNames = Object.keys(this.compositions);
    var $frag = $(document.createDocumentFragment());
    var $catDiv = $(document.createElement('div'));
    $catDiv.addClass('items');
    $frag.append('<h2 class="option-title">' + translate('compositions') + '</h2>');
    for (var i = 0; i < compositionNames.length; i++) {

        var $block = $(document.createElement('div')).addClass('available block composition ').append('<div class="container"><span class="icon ' + this.compositions[compositionNames[i]]['icon'] + '"></span><span class="text">' + compositionNames[i] + '</span></div>');
        $block.data('composition', compositionNames[i]);
        $block.data('model', this.getSectionByComposition(compositionNames[i])); //model section
        $block.draggable({
            revert: true,
            appendTo: $("#page-edit"),
            helper: "clone",
            cursor: "move"
        });
        $catDiv.append($block.get(0))
        $frag.append($catDiv);
    }
    this.$el.find('.availables > .items:first').append($frag.get(0));
}
```

### ## Construction du composition 

La construction  d'un objet section à partir du donné json  est assurée par la fonction "getSectionByComposition".

Cette fonction prend en paramètre le nom d'une composition et 
- construit les blocs, colonnes , section en ajoutant à ces modèles leurs attributs respectifs 
- construit le structure section > columns > blocs 
- retourne une section 

### ### Attributs objet section et column 

Comme vu dans le json contenant les compositions, tous les objets (blocs, colonnes, section) ont des attributs. 

Pour les objets section et column, on a ces attributs :

```js
"options":[
   {
      "optionType":"styles",
      "priority":90,
      "_id":"c525",
      "colorOption":"accent1",
      "shadeWorn":"level-medium",
      "contentSize":"xl",
      "sectionWidth":"full-wide", 
   },
   {
      "optionType":"advancedCSS",
      "priority":200,
      "cssClasses":"test"
   }
]

```

**REMARQUE** : "sectionWidth":"full-wide", (seulement pour section)

Certains de ces attributs correspondent à des options de  section et de colonne  configurable dans le backoffice. 
Un click sur le bouton Styler d'une section ouvre un rightpanel contenant les styles pouvant être configurés pour cette section 

**REMARQUE** : même chose pour colonne à l’exception de la largeur de section qui n'existe par pour celle-ci
![[Pasted image 20230814111138.png]]

Dans le rightpanel on a deux tabs : 

![[Pasted image 20230814111626.png]]

dans **Styles** on a les options suivantes : 
- couleurs du blocs  - correspond à l'attribut **colorOption**
- ombres portée - correspond à l'attribut **shadeWorn**
- Taille du contenu - correspond à l'attribut **contentSize**
- Largeur de la section - correspond à l'attribut **sectionWidth**

dans **Avancé** : 
* Ajout de classes  - correspond à l'attribut **cssClasses**

Quand la composition est ajoutée à une page, l'attribut de couleur prendra effet immédiatement sur l'aperçu, et les valeurs des attributs seront appliquées aux configurations correspondantes dans le rightpanel.

#### #### Objet option

Les attributs qu'on vient de citer  sont ajoutés aux objets section et column par l'utilisation d'autres objets.

-  **Styles**
les attributs styles vienent de l'objet **StylesOption**.
Dans la fonction **initialize**, les objets column et section ajoutent un objet **StylesOption**

```js
initialize: function() {
    this._super();
    if (this.options.colors)
        this.options.remove(this.options.colors);
    if (this.options.effects)
        this.options.remove(this.options.effects);
    if (!this.options.styles)
        this.options.add(new StylesOption({}, {
            content: this
        }));
},

```

- **Avancée**
L'attribut cssClasses vient de l'objet **Content**.
Utilisation de l'objet **AdvancedOption**, qui a comme attribut "cssClasses"
Section et column extend un objet **Content**, et dans la fonction initialize de cet objet on a cette ligne 

```js
if (!this.options.advancedCSS)
	this.options.add(new AdvancedOption({},{content:this}));
```
### ### Ajout des attributs aux objets (section et column)

Voici comment setter les valeurs des attributs : 

```js
     /**
      * Appliquer des styles pour sections et colonnes
      * @param objetcType  section ou colonne
      * @param liste des options
      */
     setStyleSectionOrColumn: function(objectType, options) {
         for (const option of options) {
             if (option.optionType === "styles") {
                 objectType.attributes.options.styles.colorOption = option.colorOption ? option.colorOption : "";
                 objectType.attributes.options.styles.shadeWorn = option.shadeWorn ? option.shadeWorn : "";
                 objectType.attributes.options.styles.contentSize = option.contentSize ? option.shadeWorn : "";
                 objectType.attributes.options.styles.sectionWidth = option.sectionWidth ? option.shadeWorn : "";
                 objectType.attributes.options.styles.priority = option.priority ? option.priority : "";
             } else if (option.optionType === "advancedCSS") {
                 objectType.attributes.options.advancedCSS.cssClasses = option.cssClasses ? option.cssClasses : "";
                 objectType.attributes.options.advancedCSS.priority = option.priority ? option.priority : "";
             }

         }
         return objectType;
     },
```


### ### Attributs objet bloc

Recherche encore à faire 

## ## Draggable 
Pour que les compositions puissenr fonctionner avec la fonctionnalité drag and drop, il fallait modifié le fichier contentView.js
### ### ContentView.js

```shell
librairies/public/integration/src/js/JEditor/PagePanel/Contents/Ancestors/ContentView.js
```

les événements de drag and drop d'un block ou compositions se trouve dans ce fichier. 
Au début le drop n'acceptait que des objets blocs. 
La méthode onDrop a été modifié pour qu'une section soit acceptée. 

La partie qu'on drop un élément (block ou composition ) est une zone d'une page (zone type :  content)

```js
onDrop: function(event, ui) {
    var model, clone, sensor, parent, parents, futureChild, shouldRemove, ctor, lastParent, current;
    try {
        event.stopPropagation();
        model = ui.draggable.data('model');
        clone = model.clone();
        sensor = $(event.target);
        parent = model.parent;
        parents = [];
        shouldRemove = !model.dummy;
        sensor.removeClass('custom-placeholder');
        this.dom.body.removeClass('drag');
        clone.dummy = false;
        if (parent != null) { // pour composition

            while (!(parent instanceof this.model.constructor)) {
                parents.push(parent.constructor);
                parent = parent.parent;
            }
        }
        if (parents.length > 0) {
            ctor = parents.pop();
            lastParent = new ctor();
            futureChild = lastParent;
            while ((parent = parents.pop()) !== undefined) {
                current = new parent();
                lastParent.addChild(current);
                lastParent = current;
            }
            lastParent.addChild(clone);
            clone = lastParent;
        } else {
            futureChild = clone;
        }
        if (shouldRemove && parents.length > 0) //length  = 0 pour composition
            model.parent.removeChild(model);
        this.model.addChild(futureChild, sensor.data('index'));
        event.stopImmediatePropagation();
    } catch (e) {
        this.error({
            message: translate('cannotAddContent')
        });
    }
    // return false;
},
```

**Modification faite** : Ce qu'on a changé dans cette fonction ce sont les opérations sur l'objet **parent**. 
Pour le fonctionnement initial, qui est l'ajout de bloc, la parent direct est une colonne et puis le parent de cette colonne est une section 
Pour la modification composition qui est une section, elle n'a pas de parent. Donc soit "parent = null". Donc on ne fait des opérations sur '"parent"' quand c'est une section (composition).




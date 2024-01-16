
---
url : 

---

views listes des block disponible 

/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/public/integration/build/js/JEditor/PagePanel/Contents/Blocks/Block/Views/AvailableView.js
## fichiers modifié selon svn st avant commencement prototype 

```html 
M       module/GestionContenuUtil/src/GestionContenuUtil/Core/BlockModuleHandlers/BlockAbstractCollectionImage.php
M       module/GestionContenuUtil/src/GestionContenuUtil/Core/BlockModuleHandlers/BlockGalerieHandler.php
M       module/GestionContenuUtil/src/GestionContenuUtil/Core/BlockModuleHandlers/BlockImageHandler.php
M       module/GestionContenuUtil/src/GestionContenuUtil/Core/HtmlTagHandlers/VideoTagHandler.php
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
X       public/integration

Vérification de l'état sur la référence externe en 'public/integration' :
?       public/integration/src/js/JEditor/Commons/libraries/bower_components
M       public/integration/src/js/JEditor/ParamsPanel/Views/MarqueClientView.js
?       public/integration/src/js/JEditor/ParamsPanel/Views/MarqueClientView_old.js
```

N.B : marque client view est pour la carte refacto 

/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/public/integration/src/js/JEditor/PagePanel/Contents/Blocks/Block/Templates/availableBlocks.html
## Etude sur styles et paramètres

Objet section et colonne partagent les mêmes fichiers pour styles et parametres, ce sont les 3 fichiers en dessous.
Les options sont ce qu'on trouvent dans rigt panel qu'on fait edit section ou colonne 

le View

```path
/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/public/integration/src/js/JEditor/PagePanel/Contents/Options/Views/StylesOptionView.js
```

template html
```path
/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/public/integration/src/js/JEditor/PagePanel/Contents/Options/Templates/stylesOption.html
```

modele 

```path
/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/public/integration/src/js/JEditor/PagePanel/Contents/Options/Models/StylesOption.

```

voici les options pour une section  qu'on voit dans le right panel , qu'on peut voir dans le modèle
### 1) onglet style 
il y a 5 options pour section (4 pour colonne, sans le dernier)
- couleur du bloc - colorOption
- ombre de porté - shadeWorn
- taille contenu - contentSize
- largeur de la section ( qui est propre à section ) - sectionWidth

### 2) onglet Avancé
- nom de classe - cssClasses
## fonctionnalité style section 

### bouton style sur la section 

("click .edition-menu>.style": "edit",) la déclaration de l'évenement se trouve dans le fichier SectionView.js
la définition de la fonction callbac "edit" se trouve dans  ContentView.js
## ce qui se passe lors d'un sauvegarde 

les propriétés se trouvent bien dans attributs avant et après modification dans right panel , mais durant la sauvegarde , le json envoyé se présente sous un autre forme , c'est à dire les proriété qui sont sauvé se trouvrent dans un attribut options
( à étudier plus)

La déclaration des options du modèle SECTION  se trouve dans Section.js (initialize)
```javascript
initialize: function() {
this._super();
if (!this.options.popup) {
	if (this.options.colors)
		this.options.remove(this.options.colors);
	if (this.options.effects)
		this.options.remove(this.options.effects);
	if(!this.options.styles)
		this.options.add(new StylesOption({}, {content: this}));
}
},
```
### colorOption, contentSize, shadeWorn, sectionWidth

la dernière instruction ajoute un modele StyleOption à section, à noter que tous ces options se trouves dans attributs, 
donc pour acceder aux options d'une section il faut écrire  : 
```javascript 
section.attributes.options
```

ces styles se trouvent dans   (ceux qu'on peut modifier dans rightpanel, style d'une section)
se trouvent dans l'attribut de  l'objet options :  

```javascript
section.attributes.options.styles.attributs
```

on peut trouver aussi le paramètre avancé cssClasses dans cet attribut.
la valeur possibles des ces attributs se trouvent dans le même fichier dans StyleOption.

## Etude sur comment utiliser un json similaireà celui exporté dans le b.o

j'ai étudié comment le B.O utiliser les json des pages dans la base de données.
en cliqaut sur une page dans le BO, un api recupère le contenu de la page, toute les zones et l'affiche. 

cette template contient liste des pages  :
```shell 
/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/public/integration/src/js/JEditor/PagePanel/Templates/pageList.html
```
cette view est la logqieu pour liste des pages :

```shell
/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/public/integration/src/js/JEditor/PagePanel/Views/PageCollectionView.js
```

lorsqu'on click une page , dans le view de dessus, un evenement est triggered, avec le contenu de la page choisi en paramètre , dans la methode _onPageClick

```js
this.trigger(Events.ChoiceEvents.SELECT, this, this.collection.get(cid));
```

la methode trigger est fournie par backbone 

#### PagePanel 

PagePanel.js ecoute cette evenement par le biais de cette ligne 

```js 
this.listenTo(this.childViews.pageList, Events.ChoiceEvents.SELECT, this._onPageSelect);
```

ou pageList représente la liste des pages à gauche 

```js
@property {PageCollectionView} pageList La liste des pages sur la
* gauche

```

La fonction listenTo est fourni par backbone.
l'évenemt Events.ChoiceEvents.SELECT est un custom évenement qui est déclaré dans 
```shell
librairies/public/integration/src/js/JEditor/Commons/Events.js
```

Le contenu de la page qui a été récupré dans la pagecollectionview est copité dans 
this.currentPage


-> jereo pageview.js


ligne dans page vie qui rend les section 

```js
this.sectionCollectionView.render();
```

09-08-2023

il faut creer un system qui peut crée des blocs en fonction du json 
les blocks on leur options respectives 

Estimation 4-5 jours avec test.

dernier liste fichier modifié avant de faire un autre dev  : 
```
Vérification de l'état sur la référence externe en 'public/integration' :
?       public/integration/src/js/JEditor/Commons/libraries/bower_components
M       public/integration/src/js/JEditor/PagePanel/Contents/Ancestors/ContentView.js
M       public/integration/src/js/JEditor/PagePanel/Contents/Blocks/Block/Templates/availableBlocks.html
?       public/integration/src/js/JEditor/PagePanel/Contents/Blocks/Block/Templates/availableBlocks_composition_dynamique.html
M       public/integration/src/js/JEditor/PagePanel/Contents/Blocks/Block/Views/AvailableView.js
?       public/integration/src/js/JEditor/PagePanel/Contents/Blocks/Block/Views/AvailableView_composition_dynamique.js
M       public/integration/src/js/JEditor/PagePanel/Contents/Blocks/Block/nls/fr-ca/i18n.js
M       public/integration/src/js/JEditor/PagePanel/Contents/Blocks/Block/nls/fr-fr/i18n.js
M       public/integration/src/js/JEditor/PagePanel/Contents/Blocks/Block/nls/i18n.js
?       public/integration/src/js/JEditor/PagePanel/Contents/Compositions
?       public/integration/src/js/JEditor/ParamsPanel/Views/MarqueClientView_old.js

```




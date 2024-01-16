
documentation officiel  : https://backbonejs.org/#Events

Dans Backbone.js, les événements jouent un rôle central pour permettre aux différents composants de communiquer entre eux de manière souple et dé-couplée. Les événements permettent aux vues, aux modèles et aux collections de réagir à des actions spécifiques, sans nécessiter une forte dépendance entre les différentes parties de l'application.

## 1 - liste 

Backbone.js offre une variété d'événements prédéfinis que vous pouvez écouter sur les modèles, les collections et les vues. Voici une liste des événements prédéfinis les plus couramment utilisés dans Backbone :

**Événements de Modèle (Model Events) :**

1. `"change"` : Déclenché lorsque les attributs d'un modèle changent.
2. `"change:attribute"` : Déclenché lorsque un attribut spécifique du modèle change.
3. `"destroy"` : Déclenché lorsque le modèle est détruit (supprimé).
4. `"sync"` : Déclenché après qu'un modèle a été synchronisé avec le serveur.
5. `"error"` : Déclenché en cas d'erreur lors d'une opération (comme le chargement ou la sauvegarde).
6. `"invalid"` : Déclenché lorsque la validation échoue lors de la sauvegarde d'un modèle.
7. `"add"` : Déclenché lorsqu'un modèle est ajouté à une collection.

**Événements de Collection (Collection Events) :**

1. `"add"` : Déclenché lorsqu'un modèle est ajouté à la collection.
2. `"remove"` : Déclenché lorsqu'un modèle est retiré de la collection.
3. `"reset"` : Déclenché lorsque la collection est réinitialisée.
4. `"sort"` : Déclenché lorsque la collection est triée.
5. `"sync"` : Déclenché après que la collection a été synchronisée avec le serveur.

**Événements de Vue (View Events) :**

1. `"render"` : Déclenché lorsque la vue est rendue.
2. `"remove"` : Déclenché lorsque la vue est supprimée.
3. `"close"` : Déclenché lorsque la vue est fermée.

## 2 - méthodes pour mieux gérer les événements 


En plus des événements courants tels que "click", "change", etc., Backbone.js fournit plusieurs méthodes utiles pour gérer les événements et la communication entre les différentes parties de votre application. Voici quelques-unes de ces méthodes :

### a. **`on(event, callback, [context])`** : 
	
Cette méthode permet d'écouter des événements sur un objet Backbone, comme un modèle, une vue ou une collection. Lorsque l'événement se produit, le callback associé est exécuté.
    
### b. **`off([event], [callback], [context])`** : 

Cette méthode permet de supprimer un écouteur d'événement précédemment défini. Si vous ne spécifiez pas d'événement, elle supprimera tous les écouteurs pour l'objet. Vous pouvez également limiter la suppression à un événement spécifique en le précisant.
    
## c. **`trigger(event, [args...])`** : 

Cette méthode déclenche un événement personnalisé sur l'objet. Vous pouvez également fournir des arguments supplémentaires qui seront passés aux callbacks enregistrés pour cet événement.
    
### d. **`listenTo(other, event, callback)`** : 
Cette méthode permet d'écouter des événements sur un autre objet Backbone (par exemple, un modèle écoutant les changements d'un autre modèle). C'est une méthode plus recommandée que `on` car elle gère automatiquement la suppression des écouteurs lorsque l'objet écouté est détruit.
    
### e. **`stopListening([other], [event], [callback])`** 
Cette méthode permet d'arrêter d'écouter les événements sur un autre objet Backbone. Si aucun objet n'est spécifié, elle arrêtera tous les écouteurs sur tous les objets.
    
### f. **`once(event, callback, [context])`** :
Cette méthode fonctionne de la même manière que `on`, mais le callback est exécuté au plus une fois. Une fois exécuté, l'écouteur est automatiquement supprimé.
    
### g. **`listenToOnce(other, event, callback)`** : 
Cette méthode fonctionne de la même manière que `listenTo`, mais le callback est exécuté au plus une fois.
    

Ces méthodes sont utilisées pour gérer les événements et la communication entre les différentes parties de votre application Backbone, que ce soit pour les modèles, les vues ou les collections. Elles vous permettent de mettre en œuvre un modèle d'interaction souple et réactive entre les composants de votre application. 

## 3 -  événement dans une vue sur un élément html
On déclare un eventlistner comme ceci dans un vue  : 

```js
events: {
  'click .item': 'handleItemClick'
},
```

Explication  : 
- "click" : événement 
- ".item" :  sélécteur css (une classe de l'élément html )
- handleItemClick  :  fonction qu'on exécute au click de l'élement avec une classe ".item"

## 4 - Exemple d'utilisation des méthodes de gestion d'événement 

On peut déclarer des events dans les views et les modèles.

on peut soit : 

- on peut écouter directement des événement sur un attribut de modèle 
- déclencher et écouter des événement personnalisé
### 4-1- evenement sur des attributs de modèles

On peut ecoutér des evenement sur un ou plusieurs attributs de modèles dans backbone. Par exemple : 

```js
book.on("change:title change:author", ...);
```

Explication : 
- séparation de liste : espace
- change  : un événement 
- title : attribut d'un modèle qu'on veut écouter l'événement
Donc à chaque fois que des événement sont fired, la fonction callback bindé est executé.
### 4-1- événement personnalisé 

on peut définir des événement personnalisé comme ce qui est fait dans Ideo3.2 Backbone. 

```shell
librairies/public/integration/src/js/JEditor/Commons/Events.js
```

Ce fichier contient liste des noms d'événement personnalisé qu'on utlise partout dans l'application.

pour  les événement personnalisé, il faut deux choses , un déclencheur et un écouteur 

#### a) déclencheur d'événement 

La méthode fourni par Backbone  :  trigger( ) permet de déclencher  un événement. (voir def en haut) cette fonction passe les params s'il y en aux callback dans le listener de l'event. 

#### a) écouteur d'événement 

on peut écouter en utilisant soit <span class="remarque">listenTo</span>   soit  <span class="remarque" >on</span> 

### listenTo VS on (chatGPT)

`listenTo` et `on` sont deux méthodes de gestion des événements dans Backbone.js, mais elles diffèrent principalement en termes de gestion des écouteurs d'événements et de nettoyage automatique.

##### **`on` :**

La méthode `on` est utilisée pour écouter les événements sur un objet Backbone. Vous pouvez l'utiliser pour définir des écouteurs d'événements et exécuter des fonctions lorsque ces événements se produisent. Cependant, avec `on`, vous êtes responsable de supprimer manuellement ces écouteurs lorsque vous n'en avez plus besoin, afin d'éviter les fuites de mémoire.

**Exemple d'utilisation de "on" :**

```js
myModel.on('change', this.handleModelChange, this);
```
##### **`listenTo` :**

La méthode `listenTo` est similaire à `on`, mais elle a l'avantage de gérer automatiquement la suppression des écouteurs d'événements lorsque l'objet qui écoute est détruit. Cela évite les problèmes de fuites de mémoire où les écouteurs d'événements restent actifs même lorsque l'objet principal n'est plus utilisé.

**Exemple d'utilisation de "listenTo" :**

```js 
this.listenTo(myModel, 'change', this.handleModelChange);
```

En résumé, 
"listenTo" est recommandé dans la plupart des cas, car il facilite la gestion de la mémoire et évite les problèmes potentiels liés aux fuites de mémoire. Cependant, vous pouvez toujours utiliser `on` lorsque vous avez des raisons spécifiques de gérer manuellement la suppression des écouteurs.

##  exemple sur  la méthode on()

voici un exemple comment l'utiliser 

```js
var Order = Backbone.Model.extend({
  placeOrder: function() {
    // Logic to place the order
    this.trigger('orderPlaced');
  }
});

var order = new Order();

//cette ligne ecoute lévenenent et execute la fonction callback lorsque l'evenement "orderPlaced est trigger"
order.on('orderPlaced', function() {
  console.log('Order placed successfully!');
});

order.placeOrder(); // This will trigger the 'orderPlaced' event

```

Explication  : 

this.trigger('orderPlaced') : trigger l'événement orderPlaced 
lorsque cette événement est triggered , la fonction call back est exécutée. 

```js
order.on('orderPlaced', function() {
  console.log('Order placed successfully!');
});
```
## undelegateEvents() 

Bien sûr ! En utilisant Backbone.js, la fonction `this.undelegateEvents();` permet de supprimer toutes les écoutes d'événements qui ont été précédemment mises en place à l'aide de la déclaration `events` dans une Vue Backbone. On l'utilise généralement quand on veut nettoyer les écoutes d'événements avant de détruire ou de supprimer une vue.

En utilisant `this.undelegateEvents();`, on enlève essentiellement toutes les écoutes d'événements associées à la vue. Cela permet d'éviter les fuites de mémoire et les comportements inattendus après que la vue n'est plus nécessaire.

Par exemple, si tu as une Vue Backbone qui écoute différents événements comme des clics ou des changements, tu pourrais appeler `this.undelegateEvents();` avant de détruire la vue pour t'assurer qu'aucune écoute d'événements persiste.
### Exemples dans le lib IDEO3.2

##### listener  : 

dans Pagepanel.js (un View), on a cette ligne 

```js 
this.listenTo(this.childViews.pageList, Events.ChoiceEvents.SELECT, this._onPageSelect);
```

- **this.childViews.pageList** : 

est l'objet sur lequel vous souhaitez écouter un événement. Plus précisément, c'est l'objet que vous écoutez pour l'événement spécifique **Events.ChoiceEvents.SELECT**

- **this._onPageSelect** : 
callback function, si cette fonction a besoin de paramètre, ces paramètres sont passé par le trigger 

```js 
		/**
		 * au changement de page
		 *
		 * @param {Commons.Pages.Models.Page}
		 *            page la page
		 * @param {PageCollectionView}
		 *            view la liste de page
		 * @private
		 */
		_onPageSelect: function(view, page) {
		    if (this.currentPage && this.currentZone && this.currentZone.hasUnsavedChanges()) {
		        this.confirmUnsaved({
		            message: translate("quitWithoutSaving"),
		            title: translate("unsavedChanges"),
		            type: 'delete-not-saved',
		            onYes: _.bind(function() {
		                this.currentZone.save();
		                this.currentPage = page;
		            }, this),
		            onNo: _.bind(function() {

		                this.currentZone.cancel();
		                this.currentPage = page;
		            }, this),
		            options: {
		                dialogClass: 'delete no-close',
		                dontAskAgain: true
		            }
		        });
		    } else
		        this.currentPage = page;
		},

```

##### trigger  :  **`trigger(event, [args...])`** 

```js
this.trigger(Events.ChoiceEvents.SELECT, this, this.collection.get(cid));
```

les paramètre de la méthod trigger : 
- nom événement 
- premier paramètre requis par la fonction "_onPageSelect()"
- deuxième parametre requis par la fonction "_onPageSelect()"


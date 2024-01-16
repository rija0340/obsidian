
## backbone généralités

Voici des faits concernant View dans backbone (chatgpt et documentation officielle):
- un view n'a pas nécessairement besoin d'un modèle
- un view peut avoir des childViews qui peuvent être rendu dedans.

## ## Etude pagepanel (c'est un View)

panel.js est un view 

voici comment Pagepanel extend Backbone.view  : 
```text
PagePanel extend PanelView
panelview extend BabblerView
BabblerView extend View
View extend Backbone.view
```

### childViews dans PagePanel 

ceci est un capture pris au premier chargement de pagepanel, pas de page selectionée par défaut.

![[Capture d’écran du 2023-08-11 08-57-16(1).jpg]]

Vois une de quelques childView qu'on utilise dans backbone : 

- pageList ( view  :PageCollectionView)
- pageListManager ( view  :  PageListManagerView) ( je n'ais pas vraiment étudié en profondeur  )
- pageLpManager ( view  :  PageLpManagerView) ( je n'ais pas vraiment étudié en profondeur  )
- availableBlocksView ( view  : AvailableView)
- AddpageView 
- LanguagesDropDown

Il faut noter que certains n'est pas sur l'mage mais rendu lorsqu'une page est selectionnée (par exemple  : availableBlocksView ... )
### ###  fonction load() dans PagePanel

c'est dans cette fonction que certains childviews sont chargé et puis rendu dans la fonction render()

**function load()**

```js
load: function() {
    var loaded = 0;
    var languagesCount = this.languages.length;
    this.contentModels = ContentModelCollection.getInstance();
    this.pages = PageCollection.getInstance();
    this.pageSupports = PageSupportCollection.getInstance();
    this.layouts = LayoutCollection.getInstance();
    this._byLang = this.pages.groupBy('lang');
    this.currentList = this._byLang[this.currentLang.id];
    this.on(Events.PagePanelEvents.PAGE_CHANGE, this._onPageChange);
    this.childViews.langDropDown = new LanguagesDropDown({
        collection: this.languages,
        _default: this.currentLang,
        defaultLabel: 'language'
    });
    this.childViews.pageList = new PageCollectionView({
        collection: this.pages,
        language: this.currentLang,
        supportCollection: this.pageSupports
    });
    this.childViews.pageListManager = new PageListManagerView({
        collection: this.pages,
        language: this.currentLang,
        listView: this.childViews.pageList,
        languageList: this.languages
    });
    this.childViews.pageLpManager = new PageLpManagerView({
        listView: this.childViews.pageList
    });
    this.childViews.availableBlocksView = new AvailableView({
        pagePanel: this
    });

    this.loadingEnd();
},
```

**render()**

```js
render: function() {
    this.undelegateEvents();
    this.$el.html(this._template({
        empty: this._byLang[this.currentLang.id].length === 0,
        noneSelected: !this.currentPage,
        canAddPage: this.user.can("create_page")
    }));
    this.dom.pagePanel.nothingToDisplay = this.$('.nothing-to-display');

    //this.childViews.addPageView.attach(this.$('.addPage'));
    //this.childViews.addPageView.attach(this.$('.empty-content-lang'));

    this._renderPage();
    this._renderPageList();
    this.setDOM();
    this.renderRightPanel();
    this.lockOverlayArrow();

    // init app intro (tutorial)
    this.appIntro();

    this.delegateEvents();
    this.dom.window.scroll();
    return this;
},
```

### ### ### childview  : pageList (PageCollectionView)
![](listepages.png)
c'est la vue qui affiche la liste des pages sur la coté gauche du tab pagepanel dans B.O. Elle est rendu par la fonction **_renderPageList**  

``` javascript
 * @property {PageCollectionView} pageList La liste des pages sur la gauche
```
#### Événement sur la liste des pages
Du point de vu html, la liste des pages sont des liens dans des  balises li.
Dans la view **PageCollectionView**, on a cet événement sur la liste li html  : 

```js
events: {
'click ul li a[data-cid]': '_onPageClick',
},
```

la fonction de callback **_onPageClick**_
```js
    /**
     * Change La page courante de l'application
     * @argument {jQuery.Event} event Evenement jQuery
     * @private
     */
    _onPageClick: function(event) {
        event.preventDefault();
        var $target = $(event.currentTarget);
        var cid = $target.data('cid');
        this.$('.edit').removeClass('edit');
        $target.parent().addClass('edit');
        if (!this.collection.get(cid)) {
            this.trigger(Events.ChoiceEvents.SELECT, this, this.options.supportCollection.get(cid));
        } else {
            this.trigger(Events.ChoiceEvents.SELECT, this, this.collection.get(cid));
        }
        return false;
    },
```

le contenu de la page sélectionnnée est recupéré par cette ligne, on utilisant sont cid  : 

```js
this.collection.get(cid)
```

Ensuite Il y a un la fonction qui déclenche un événement "Events.ChoiceEvents.SELECT", cet événement est écouté dans PagePanel et est attaché à une fonction callback 

Voici la méthode qui écoute cet événement  : 

```js
this.listenTo(this.childViews.pageList, Events.ChoiceEvents.SELECT, this._onPageSelect);
```

- this.childViews.pageList :  l'objet sur lequel vous souhaitez écouter un événement
- l'événement spécifique **Events.ChoiceEvents.SELECT** écouté
- this._onPageSelect) : callback function,

Voici la définition de cette fonction  **_onPageSelect** : 

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

Remarquer que cette fonction prend en paramètre deux objets, un view et une page. Ces paramètres sont passés à cette fonction par le trigger. 
Donc à chaque click sur une page, la fonction _onPageSelect va être appelée.

Dans cette fonction, on set la valeur du paramètre page dans une variable this.currentPage 
```js 
this.currentPage = page;
```

**this.currentPage** n'est rien d'autre qu'un propriété du prototype de PagePanel, qui est défini en bas du fichier PagePanel.js : 

```js 
Object.defineProperties(PagePanel.prototype,
    /**
     * @lends PagePanel.prototype
     */
    {
        /**
         * La liste de page courante
         *
         * @type{PageCollection}
         */
        currentList: {
            get: function() {
                return this._currentList;
            },
            set: function(currentList) {
                this._currentList = currentList;
                this.trigger(Events.PagePanelEvents.PAGE_LIST_CHANGE, this, currentList, undefined);
            }
        },
        /**
         * La page courante
         *
         * @type{Commons.Pages.Models.Page}
         */
        currentPage: {
            get: function() {
                return this._currentPage;
            },
            set: function(currentPage) {
                if (currentPage !== this._currentPage) {
                    this._currentPage = currentPage;
                    this.trigger(Events.PagePanelEvents.PAGE_CHANGE, this, currentPage, undefined);
                }
            }
        },
        currentZone: {
            get: function() {
                return this.childViews.pageView.currentZone;
            }
        }
    });
```

Dans la définition de currentPage, son setter trigger un événement une fois appelé : 

```js
set: function(currentPage) {
    if (currentPage !== this._currentPage) {
        this._currentPage = currentPage;
        this.trigger(Events.PagePanelEvents.PAGE_CHANGE, this, currentPage, undefined);
    }
}
```

l'écouteur de cet événement est dans la fonction **load()**

```js
this.on(Events.PagePanelEvents.PAGE_CHANGE, this._onPageChange);
```

et une fois l'événement déclenché, la fonction **_onPageChange** est appelé , C'EST DANS CETTE FONCTION QUE LE CONTENU DE LA PAGE EST AFFICHÉ, CELA VEUT DIRE QUE PAGEVIEW EST MISE A JOUR. 

```JS
		/**
		 * met à jour la vue de page (zone du centre de l'écran)
		 */
		_onPageChange: function() {

		    this.dom.body.animate({
		        scrollTop: 0
		    }, 300);
		    var callback = _.bind(function() {
		        this.renderRightPanel();
		        this._checkMessages();
		        if (this.currentPage) {
		            var windowHeight = this.dom.window.height();
		            var offset = this.$('#page-edit').offset().top - this.dom.window.scrollTop();
		            this.$("#page-edit").css('minHeight', (windowHeight - offset) + 'px');
		            this.childViews.pageView = new PageView({
		                model: this.currentPage,
		                pagePanel: this,
		                rightPanelView: this.rightPanelView
		            });
		            this.listenToOnce(this.childViews.pageView, Events.LoadEvents.LOAD_ERROR, this.render);
		            this.childViews.pageView.load();
		            this._renderPage();
		        }
		    }, this);
		    if (this.childViews.pageView) {
		        this.listenToOnce(this.childViews.pageView, Events.ViewEvents.HIDE, function() {
		            this.childViews.pageView.remove();
		            callback();
		        });
		        this.childViews.pageView.hide();
		    } else
		        callback();
		},
```


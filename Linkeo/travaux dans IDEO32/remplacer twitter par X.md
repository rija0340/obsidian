coté admin  : 
+ autoriser le domaine x.com -> public/integration/src/js/JEditor/ParamsPanel/Models/Params.js
    
- Ajouter option network=x pour le shortcode (il faut que l'option network=twitter continue à fonctionner pour les sites existants) -> module/GestionContenuUtil/config/module.config.php
    
- Remplacer l’icon (avec le SVG joint) -> à rechercher template paramspanel
    
- Changer le titre par “X” en majuscule (idem Front) -> à recherche template paramspanel  + rendu shortcode 
    
- Changer la couleur du titre par du noir #000000 -> eo amle misy oe ajouter une page dans paramspanel
    
- Dans la liste, remplacer l’icon et indiquer “**X (Twitter)** -> regarder la carte pour mieux comprendre 


## opérations faites

remplacement shortcode twitter sur liste social network  :  

```
public/integration/src/js/JEditor/ParamsPanel/Views/SocialNetworks.js
changement de twitter en x dans le 

            this.networks = {
                facebookUrl: 'facebook',
                twitterUrl: 'x',
                mybusinessUrl: 'googlemybusiness',
                pinterestUrl: 'pinterest',
                viadeoUrl: 'viadeo',
                linkedinUrl: 'linkedin',
                youtubeUrl: 'youtube',
                instagramUrl: 'instagram',
                skypeUrl : 'skype',
                theforkUrl: 'thefork',
                tiktokUrl: 'tiktok',
                tripadvisorUrl: 'tripadvisor',
                wazeUrl: 'waze',
                whatsappUrl: 'whatsapp',
                slideshareUrl: 'slideshare',
            };

```

view liste social network dans admin  : 

```
public/integration/src/js/JEditor/ParamsPanel/Views/ListSocialNetworks.js
```

template liste social network dans paramspanel :

```
public/integration/src/js/JEditor/ParamsPanel/Templates/ListSocialNetwork.html
```

le shortcode au render de paramspanel est suivant ce qui est enregistré dans la base de données. Les previes twitter seront ceux qui est enregistrée mais les nouveaux seront x.

REMARQUE : misy olana kel zan 

rehefa mampiditra ray dia asina url iny mbola mety "x" ka manampy iray dia mifafa iny le efa teo iny
fa raha ohatra ka twitter no apesaina dia tsy miala le izy fa mijanona eo ian 

jereo maha null anle url x fa io no olana 

ty timesheet : reunion sy X

-------
ny tsy mapandeha anle izy dia izy tsy misy network ankotran x dia lasa tsy mahita izy aveo 

objet utilisé lors de l' jout d'une entrée  : 
```js 
librairies/public/integration/src/js/JEditor/ParamsPanel/Views/SocialNetworks.js

var object={
id: maxId+1,
title:"",
url:"",
type:Type,
network : this.networks[Type],
};
```

type  => sur la liste dropdown du template  
```
data-id="xUrl"
```


donc 
### Questions : 

shortcode network=x    -> fetch existante et nouveau ;
shorcode network=twitter -> fetch only existante (type  = twitterUrl et network  = x);


## correction de Mathieu

fichier impactés  : 

 public/integration/src/js/JEditor/ParamsPanel/Templates/ListSocialNetwork.html
 module/GestionContenuUtil/src/GestionContenuUtil/Core/HtmlTagHandlers/SocialTagHandler.php
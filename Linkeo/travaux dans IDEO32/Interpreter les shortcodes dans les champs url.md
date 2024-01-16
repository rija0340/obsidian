---
date: 2022-12-05
url: https://trello.com/c/MZnQ7D3b/414-interpreter-les-shortcodes-dans-les-champs-url
---

chercher tous les blocs ayant url 
- button 
- image

checker tous les shortcodes existants dans les codes  :

tonga dia soloina miitsy ireo namespace reo dia solona ddouble quote daholo, atao am chatgpt 

#### 07-12-2023

```
url pour contact : 

http://test.com/googlemap=[[contact_googlemap]]&ndd=[[contact_ndd]]&email=[[contact_email]]&tel=[[contact_tel|format=international_none]]  
&mobile=[[contact_mobile|format=international_none]]&calttracking=  
[[contact_calltracking|format=international_none]]

[[contact_googlemap]]   - ok
[[contact_ndd]]  - ok
[[contact_email]]  - ok
[[contact_tel|format=international_none]]  - ok
[[contact_mobile|format=international_none]]  - ok
[[contact_calltracking|format=international_none]] - ok  

----------------------------------------------------------

url pour ptr  : 

http://test.com/?ptr=[[ptr]]  - ok
[[ptr]]  - ok

----------------------------------------------------------
url pour binaries_dir 
http://test.com/?binaries=[[binaries_dir]]  
[[binaries_dir]]- ok

----------------------------------------------------------
url pour accueil  : 

http://test.com/?accueil=[[url_accueil]]&contact=[[url_contact]]&mentions=[[url_mentions]]&plansite=[[url_plansite]]&avis=[[url_avis]]&newsletter=[[url_newsletter]] 

[[url_accueil]]  
[[url_contact]]  
[[url_mentions]]  
[[url_plansite]]  
[[url_avis]]  
[[url_newsletter]]  
//  
[[deliver_link]] (et toutes les variantes [[deliver_link|url=booking]], ....)

test 

[[contact_googlemap]]
[[contact_ndd]]
[[contact_email]]
[[contact_tel|format=international_none]]
[[contact_mobile|format=international_none]]
[[contact_calltracking|format=international_none]]
[[deliver_link]]
[[deliver_link|url=booking]]
[[deliver_link|url=products]]
[[deliver_link|url=offers]]
[[deliver_link|theme=light]]
[[deliver_link|theme=dark]]
[[deliver_link|url=booking|url=products]]
[[deliver_link|url=booking|url=offers]]
[[deliver_link|url=booking|theme=light]]
[[deliver_link|url=booking|theme=dark]]
[[deliver_link|url=products|url=offers]]
[[deliver_link|url=products|theme=light]]
[[deliver_link|url=products|theme=dark]]
[[deliver_link|url=offers|theme=light]]
[[deliver_link|url=offers|theme=dark]]
[[deliver_link|theme=light|theme=dark]]
[[deliver_link|url=booking|url=products|url=offers]]
[[deliver_link|url=booking|url=products|theme=light]]
[[deliver_link|url=booking|url=products|theme=dark]]
[[deliver_link|url=booking|url=offers|theme=light]]
[[deliver_link|url=booking|url=offers|theme=dark]]
[[deliver_link|url=booking|theme=light|theme=dark]]
[[deliver_link|url=products|url=offers|theme=light]]
[[deliver_link|url=products|url=offers|theme=dark]]
[[deliver_link|url=products|theme=light|theme=dark]]
[[deliver_link|url=offers|theme=light|theme=dark]]
[[deliver_link|url=booking|url=products|url=offers|theme=light]]
[[deliver_link|url=booking|url=products|url=offers|theme=dark]]


url mixte 

[[deliver_link]]?url=[[url_accueil]]&binaries=[[binaries_dir]]&ptr=[[ptr]]&contact=[[contact_googlemap]]



[[contact_googlemap]]  
[[contact_ndd]]  
[[contact_email]]  
[[contact_tel|format=international_none]]  
[[contact_mobile|format=international_none]]  
[[contact_calltracking|format=international_none]]  
//  
[[ptr]]  
[[binaries_dir]]  
[[url_accueil]]  
[[url_contact]]  
[[url_mentions]]  
[[url_plansite]]  
[[url_avis]]  
[[url_newsletter]]  
//  
[[deliver_link]] (et toutes les variantes [[deliver_link|url=booking]], ....)

```

<span class='remarque' >Remarque</span>:

subtiliité de gallerie photo  : 

- les images dans le panel fichier peuvent avoir des liens , lorsqu'on ajoute un block gallerie image dans le backoffice et on utilise des photos avec des liens spécifiques et on active l'optiosfn ouvrir le lien quand on click sur l'image.
- ces liens peuvent contenir des shortcodes 
- on utiliser ajax pour charger le contenu de la gallerie dans la page htmldroller.php
	- route  : module/Application/config/module.config.php
- on va modifier le controlleur pour retourner les interprétations des shortcodes.


si on veu directememnt avoir les contenu

- contact
```
     $refApi = $this->getServiceLocator()->get('ref01.api');
            $serviceManager = $this->getServiceLocator();
            $contact = new \Coords01\Invokable\Contact($refApi,$serviceManager);
```

j'ai aussi trouvé ca mais cela ne fonctionnne que pour les contact_* mais pas pour [contact_fsdfsdf|fdfdf]

```
$coordsManager  = $this->getServiceLocator()->get(\Coords01\Services::COORDS_MANAGER);
$content = $coordsManager->replaceTagByValue($content);
```

- ptr

```
return _PTR_
```

- deliver 
c'est directement un url 

- binaries 
```
    public function replaceBinariesDirTagByValue($shortcode){
        $this->tag='binaries_dir';
        $config = $this->serviceLocator->get('configuration');
        $patttern='/'.$config['gestioncontenu.util']['short_code']['pattern']['binaries'].'/';
        $result = preg_replace($patttern,$this->getHtml(), $shortcode);
        return $result;
    }
```

- url 
gethtml pour test 


andramana centralisena ilay code nataontsika 
atao ato : 
module/GestionContenuUtil/src/GestionContenuUtil/Services/ContentTagParserService.php


code miaraka amin'y php echo

```php
  /**
   * Retourne le link en remplacant les shortcodes 
   *  
   */
    // public function checkAndReplaceShortCodes($link)
    // {
    //     $patterns = [
    //         "deliver" =>"\[\[deliver_link(\|(url|theme)=(booking|products|offers|light|dark))*\]\]",
    //         "contact" => "\[\[contact_([a-zA-Z]+)?([\|a-zA-Z0-9=_]+)\]\]",
    //         "ptr" => "\[\[ptr\]\]",
    //         "binaries" => "\[\[binaries_dir\]\]",
    //         "url" =>"\[\[url_(accueil|contact|mentions|plansite|avis|newsletter)\]\]",
            
    //     ];

    //     $handlers = [
    //         "deliver" =>"\GestionContenuUtil\Core\HtmlTagHandlers\DeliverTagHandler",
    //         "contact" =>"\GestionContenuUtil\Core\HtmlTagHandlers\CoordsTagHandler",
    //         "ptr" => "\GestionContenuUtil\Core\HtmlTagHandlers\PtrHandler",
    //         "binaries" =>"\GestionContenuUtil\Core\HtmlTagHandlers\BinaryDirTagHandler",
    //         "url" => "\GestionContenuUtil\Core\HtmlTagHandlers\UrlTagHandler",
    //     ];

    //     foreach ($patterns as $key => $pattern) {
    //         $results = [];
    //         preg_match_all("/" . $pattern . "/", $link, $results);
    //         if (isset($results[0]) && count($results[0]) > 0) {
    //             $handlerClass = $handlers[$key];
    //             $handlerInstance = new $handlerClass($this->serviceLocator);
    //             //boucle sur les resultas dans le url et les remplacer par leur valeurs
    //             foreach ($results[0] as $matche) {
    //                 $tag = str_replace(["[[", "]]"], ["", ""], $matche);
    //                 $handlerInstance->setTag($tag);
    //                 $html = $handlerInstance->getHtml();
    //                 $link = preg_replace("/\[\[" . preg_quote($tag, '/') . "\]\]/", $html, $link, 1);

    //             }
    //         }
    //     }
    //     return $link;
    // }
```

## resumé :

### fichiers impactés:
module/GestionContenuUtil/src/GestionContenuUtil/Core/BlockModuleHandlers/BlockAbstractCollectionImage.php
module/GestionContenuUtil/src/GestionContenuUtil/Core/BlockModuleHandlers/BlockBoutonHandler.php
module/GestionContenuUtil/src/GestionContenuUtil/Services/ContentTagParserService.php
module/MenuTemplate01/src/MenuTemplate01/View/Renderer/DynamicRenderer.php
module/GestionContenuUtil/src/GestionContenuUtil/Core/BlockModuleHandlers/BlockImageHandler.php

centralisation traitemement dans service contentTAgParserService 

shortcode prise en compte  : url, binaires, ptr, contact, deliver

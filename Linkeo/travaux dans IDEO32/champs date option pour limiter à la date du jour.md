---
date: 2024-01-03
url: https://trello.com/c/aYJw2e5u/404-champs-date-option-pour-limiter-%C3%A0-la-date-du-jour
---
formBuilderView.js -> un view qui s'occupe de la construction d'un formulaire 
fieldBuilder;html -> représente chaque champ, contient aussi la fenetre d'édition d'un champ

capture output fieldBuilder.html 

![[Pasted image 20240103145514.png]]

comment : un champ date en mode édition 

+ double vitrification ( sod manao injection ilay olona, ohatra oe manao insertion manuelle izy dia avy eo submitteny) 
+ enregistrement anaty base mety manao ahoana 
+ tokon boolean no anaty base fa le rendu anaty front manao js dynamiquement raha ny tokon ho izy 


dans la classe Form\Renderer, on cette ligne 

```php
$this->helper = new \Formulaire01\View\Helper\FormElement;
```

cette classe retourne une classe en fonction du type de l’élément par sa fonction render.


## lasa tsy mandeh enregistrement page, mila jeren

controller qui enregistre modif depuis B.O

module/Gestioncontenu/src/Gestioncontenu/Controller/ContentRestController.php


l'erreur de sauvegarde se passe au niveau de la ligne 

```php
$zone = $this->getParser()->saveZone($zone, $data);
```
 dont 
```php
 'gestioncontenu.parser' => 'Gestioncontenu\Service\GestionContenuParser',
```

dans la classe GestionContenuParser , c'est cette ligne qui genère l'erreur 

```php
$blockReference = $crud->saveblock($bloc);
```

$crud ici est 

```php
'gestioncontenu.crud' => 'Gestioncontenu\Service\GestionContenuCrud',
```

dans la fonction saveBlock on a encore cette ligne 

```php
$data = $this->saveFormBlock($data, $persist);
```

Gestioncontenu\Service\GestionContenuCrud

dans la fonction saveFormBlock , on a cette ligne qui generer l'erreur 

```php
$formApi->addFieldToForm( $form, $fieldData);
```

$'form01.api' => 'Formulaire01\Services\ModelApi',$

## liste des fichiers impactés 

module/Formulaire01/src/Formulaire01/Form/Form.php
module/Formulaire01/src/Formulaire01/Form/Renderer.php

partie js
public/integration/src/js/JEditor/PagePanel/Contents/Blocks/FormBlock/Models/Field.js
public/integration/src/js/JEditor/PagePanel/Contents/Blocks/FormBlock/Templates/FieldBuilder.html
public/integration/src/js/JEditor/PagePanel/Contents/Blocks/FormBlock/Views/FieldBuilderView.js
public/integration/src/js/JEditor/PagePanel/Contents/Blocks/FormBlock/nls/fr-ca/i18n.js
public/integration/src/js/JEditor/PagePanel/Contents/Blocks/FormBlock/nls/fr-fr/i18n.js
public/integration/src/js/JEditor/PagePanel/Contents/Blocks/FormBlock/nls/i18n.js

---
date: 2024-01-03
url: https://trello.com/c/1HDE53cv/405-form-champs-date-range
---

ao anatin'ity otran misy manao construction d'element , anaty function applyConfig()

librairies/module/Formulaire01/src/Formulaire01/Form/Form.php

```php
$element = $this->factory->create(array(
	'type' => 'Zend\\Form\\Element\\Hidden',
	'name' => 'fideo',
	'attributes' => array(
	'type' => 'hidden',
	'value' => $this->config->id,
	),
	'options' => array(
	'label' => 'fideo',
)
));
```

cette classe (form.php) extends \Zend\Form\Form; qui et une classe responsable de creer des formulaires

### `\Zend\Form\Form` :

Voici quelques-unes des fonctionnalités courantes fournies par la classe `\Zend\Form\Form` :

1. **Création de formulaires**: Vous pouvez créer un formulaire en instanciant cette classe. Le formulaire peut ensuite être configuré en ajoutant des éléments, des filtres, des validateurs, etc.
    
2. **Gestion des éléments de formulaire**: Vous pouvez ajouter des éléments de formulaire tels que des champs de texte, des zones de texte, des boutons radio, des cases à cocher, etc., au formulaire.
    
3. **Validation des données de formulaire**: La classe fournit des fonctionnalités pour valider les données soumises via le formulaire en utilisant des filtres et des validateurs.
    
4. **Rendu du formulaire**: La classe peut générer le code HTML nécessaire pour afficher le formulaire dans une vue.
    
5. **Protection contre les attaques CSRF**: Elle offre des mécanismes intégrés pour protéger les formulaires contre les attaques de type Cross-Site Request Forgery (CSRF).

## blockmoduleformhandler


la page test 
id page : 13
id zone content de la page  : 117
section de la page  : {{{SECTION_N97QE9EB5H}}}
id section  : 3347
id colmum  : 3613

id block  : 3820 
content block  : 
```json
{
  "contentType": "formBlock",
  "form": {
    "name": "test_46548",
    "buttonText": "Envoyer",
    "action": "SendAndSave",
    "successMessage": "Merci, votre message nous a été transmis avec succès",
    "columns": [
      [
        {
          "type": "date",
          "label": "",
          "description": "",
          "placeholder": "",
          "options": [],
          "mandatory": false,
          "underline": false
        },
        {
          "type": "datetime-local",
          "label": "",
          "description": "",
          "placeholder": "",
          "options": [],
          "mandatory": false,
          "underline": false
        }
      ]
    ],
    "recipients": [
      {
        "name": "[[contact_nom]]",
        "email": "[[contact_email]]"
      }
    ],
    "useCaptcha": "google",
    "sendMailToInternaute": false,
    "id": 11,
    "lang": "fr_FR"
  },
  "dummy": true
}

```

type du block  : form 

## blockmoduleformhandler 
### ce qui se passe dans la foction getVariables()
- prend le json du formulaire depuis la base 
- get le id du form 
- créer le formulaire par le factory en lui passant les donnée json comme paramètre 
<span class="remarque">Remarque</span> Le factory se charge de construire un objet Form à partir du json du formulaire 

On passe le json data à la fonction getform de FormFactory.php
```php
$form = $factory->getForm( $blockContent, $this->sourceBlock );
```
## dans le FormFactory (getForm) 
- on instancier un objet Formulaire , c'est comme un sorte de entity pour une formulaire ( ID, name, nombre de colonne ... )
- pour les champs du form, on loop les donnée de l'attribut columns du json en bas dans la fonction get form 

```php
                     foreach ( $jsonContent['form']['columns'] as $col=> $columns) {
                         foreach ( $columns as $key => $field ) {
                             if( 'separator' === $field['type']) {
                                $field['mandatory'] =  $field['underline'];
                             }
                            $fieldData = array(
                                //'id' => $field['id'],
                               'label' => $field['label'],
                               'name' => 'f' . $oForm->getId() . '-c' . $col . '-' . $field['label'].'_'.$key,
                               'type' => $field['type'],
                               'description' => $field['description'],
                               'placeHolder' => $field['placeholder'],
                               'isMandatory' => $field['mandatory'],
                               'formulaire' => $oForm->getId(),
                               'options' => $field['options'],
                                'column' => $col +1,
                                'underline' => $field['underline']
                           );
                            $champ = new \Formulaire01\Model\Champ( $fieldData );
                             
                             $tFields->add($champ);
                             unset($champ);
                         }
                     }
```

- tFields est un arrayCollection 
```php
$tFields = new \Doctrine\Common\Collections\ArrayCollection();
```
- fieldData est un array et on passe cette array contenant key value des données de la column du json à un objet Champ pour en creer un 

```php
$champ = new \Formulaire01\Model\Champ( $fieldData );
```

et puis
```php
$tFields->add($champ);
```

on ajout l'arrayCollection à la formulaire 

```php
$oForm->setFields( $tFields );
```

on on créer un objet Form à partir de l'objet oForm (objet Formulaire )

```php
$oForm = new \Formulaire01\Form\Form($oForm, $translator);
```

 <span class="remarque" >REMARQUE</span> 
 donc le factory return un objet $\Formulaire01\Form\Form$
 $oForm ici est un objet $\Formulaire01\Entity\Formulaire()$
## retour dans blockModuleFormHandler 

cette ligne de code 

```php
$formRendered = $form->getRenderer()->render();
```

$form ici est $Formulaire01\Form$

la fonction getRenderer retourne : $\Formulaire01\Form\Renderer$


```php
public function getRenderer(){
	if ($this->renderer === null) {
		$this->renderer = new \Formulaire01\Form\Renderer($this,$this->formErrors,$this->serviceLocator);
	}
	 return $this->renderer;
}
```

il faut noter que dans la getRendrerer on passe à la classe Rendrerer this qui est la Form propriétaire de getRendrer, 
## dans Form\Rendrerer

le param du contructeur de Rendrer est un objet Form, et on setForm au rendrer
dans constructeur 
```php
$this->setForm($form);
```

et puis dans la fonction setForm , on a cette ligne 

```php
$this->applyConfig();
```

et puis, prépare est une fonction dans ZendForm classe

```php
$this->form->prepare();
```

on get la fonguration de l'objet form 

```php
$formBasicConfig = $this->form->getConfig();
```

on a cette ligne qui instancie le variable $this->helper 

```php
$this->helper = new \Formulaire01\View\Helper\FormElement;
```


dans ce bout de code on loop les fields, les champs du formulaire et construit les champ (html ) par la fonction $prepareFormElement$

```php
foreach ($fields as $field) {

	$renderedElements[($field->column == 2) ? 'second' : 'first'] []= $this->prepareFormElement($field->name,
	$field->type,
	$field->description,
	$field->isHidden,
	$field->isMandatory);

}
```

le factory create ne retourne pas de html, juste des objets 

## <span class="titre2">render des champs en html </span>

dans la fonction $prepareFormElement$ on a cette ligne qui construit le form et render du html 

c'est la ligne dans Renderer qui le fait  :

```php
$helper->render($elt)
```

$helper ici est un objet pour les fields (date etc)

```php
$this->helper = new \Formulaire01\View\Helper\FormElement;
```

cette classe render un objet en fonction de type du field 

voici un extrait de code :

```php
       elseif ('date' == $type)
        	//$renderClass = '\\Zend\\Form\\View\\Helper\\FormDate';
            $renderClass = '\Formulaire01\View\Helper\FormInput';
        
        //if (class_exists($renderClass)) 
        {
	        $render = new $renderClass;
	        $this->usedHelper[$type] = $render;
	        return $render->__invoke($element);
        }
        
```

et ici $\Formulaire01\View\Helper\FormInput$ extends zend\Form  donc au final en return un zend\Form

pour les éléments date et datetimelocal on a ces types d'objet de zend 

```php
Zend\Form\Element\Text Object
```

un exemple de dump d'un objet date 

```
Zend\Form\Element\Text Object
(
    [attributes:protected] => Array
        (
            [type] => date
            [name] => f11-c0-_0
            [id] => f11-c0-_0
        )
    [label:protected] => 
    [labelAttributes:protected] => 
    [messages:protected] => Array
        (
        )
    [options:protected] => Array
        (
            [label] => 
            [value_options] => Array
                (
                )
        )

    [value:protected] => 
)
```
#### <span class="titre3" > override de render zend form  </span>

Dans render on un type custom qui n'est pa géré par zendform 

```php
$helper = $this->helper ;
if ($ctype == 'file'){
	$tConfig = $this->serviceLocator->get('config');
	if(!in_array(CODE_BOUTON,$tConfig['site_corpo'])){
		$helper = new \Formulaire01\View\Helper\FormUpload();
		$helper -> setServiceLocator($this->serviceLocator);
		$helper->setMl($ml);
		$helper->setLang($this->getLang());
	}
}
```

on va etudiier le formUpload pour mettre en place le nouveau type dateRange


## Liste des tâches à faire  : 

### dans le B.O
- dans la liste des champs, ajouter un élément daterange
- dans édition d'un champs, ajout d'autres propriétés en plus de celles d'une date simple 
- ajout d'un option "checkbox" choisir date antérieure
- au sauvegarde, enregistrement du nouveau type dans la base de données ainsi que les attributs 
### front 
- ajout d'une extension de zend form comme FormUpload
- gestion de sélection de date, il faut qu'on ne puisse pas choisir une date fin antérieur à la date début (selon config ) par un script 
### mail 
- gestion affichage label et dates
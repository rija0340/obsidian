
## fichier contenant liste route api Backbone  - zend

librairies/module/ConstManager/config/module.config.php
librairies/module/Gestioncontenu/config/module.config.php

## invalidation de toutes les pages : 

* plusieurs scenario dont enregistrement modif dans design onglet
* voir les  codes en dessous pour faire programmatiquement l'invalidation d'une ou plusieurs page

mot de passe wifi  : Efi(528U+u%S

## invalidation page dans onglet icommerce 

ajout de ce bous de code pour le faire  : 

```php
public function invalidateAllPages(){
$modules = array(
	'CoreZendExtension',
	'CoreException',
	'DoctrineModule',
	'DoctrineORMModule',
	'CoreConnectionService',
	'CoreMoteurDeRendu',
	'CoreAccess',
	'MenuTemplate01',
	'CoreHistory',
	'Catalogues',
	'Gestioncontenu',
);

$globalPath = array(
ABSTRACT_DIR.'/extension/ideo3/common_config/autoload/{,*.}{global,local}.php',
);
$modulePath = array(ABSTRACT_DIR.'/extension/ideo3/module');

$this->setServiceLocator(Common::getIdeo3ServiceManager($modules, $globalPath, $modulePath));

$pagePersister = $this->serviceLocator->get('moteurderendu.persister');
$pageApi = $this->getServiceLocator()->get('gestioncontenu.page.api');
$pages = $pageApi->getAllPages();
foreach ($pages as $page)
{
	$pageUrl = $page->getUrl();
	$pagePersister->deletePageFile($pageUrl);
}
//force suppression home.php
$pagePersister->deletePageFile('home');

}

```

<span class="remarque">remarque : </span> plusieurs tests ont été fait, pour essayer d'utiliser le bout de code suivant qui est utilisé dans IDEO3 et IDEO3.2

```php

//finally invalidate all pages

$pagePersister = $this->getServiceLocator()->get(\CorePagePersister\Services::PAGE_PERSISTER);
$pageApi = $this->getServiceLocator()->get('gestioncontenu.page.api');
$pages = $pageApi->getAllPages();
foreach ($pages as $page)
{
  $pagePersister->invalidate($page);
}

```
Essaye en vain pour essayer d'appeler la classe $pagePersister, 

## generation de template less

cela existe dans ambiance mais dès que le site acceuil se charge pour la premiere fois, on génére un fichier dans public/customization/template.less, c'est ce dernier qui va etre utilisé par le site.

pour regenerer ce fichier, il faut supprimer celui qui est present dans le dossier customization, invalider la page d'accueil et puis rafraichier la page d'accueil (test fait avec cdeurospa)

<span class="remarque">Remarque</span> Classe responsable check et génération du fichier : 
/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3/module/ConstManager/src/ConstManager/Manager/ConstantManager.php


## travail sur refacto marque client (27-04-2023)
telechargement de fichier image logo, logsmalle et favicon

cotroller rresponsable 

```
/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/vendor/CoreConfigurationService/src/CoreConfigurationService/Controller/IndexController.php
```


fichier ou on trouve route et controlleur utilisé dans backoffice : 
```path
/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/vendor/CoreConfigurationService/config/module.config.php
```

fichier contenant route ressources et autres ngamba 

```path 
/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/module/Gestioncontenu/config/module.config.php
```

controlleur utilisé pour upload et listig ressources 

```path
/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/vendor/CoreRessourceManager/src/CoreRessourceManager/Controller/ResourceRestController.php
```

fichier  service  pour crud ressource

```path
/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/vendor/CoreRessourceManager/src/CoreRessourceManager/Service/ResourceCrud.php
```

fichier pour uploader ressource 

```path
/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/vendor/CoreRessourceManager/src/CoreRessourceManager/Service/ResourceUploader.php
```


## comprehension fonctionnnement upload image dans marque client 
le fichier est d'abord crée dans ressources/images puis copié vers logos (ou logosmall ou favicion )

upload dans ressources/images peut etre fait par crud ressources (service utilisé dans controller ResourceRestController.php)

- c'est dans ressourceUploader , createfile( ) qu'on copie le ressource dans dossier public/ressources images et construction d'un thumb ainsi qu'un _lg

### log dans docker 
```shell
docker exec -it apache-php-node bash  
cd ../../  
cd /log

by maitre N
```

## code snippet 

- obtenir langue dans ideo 3.2

```php
$refApi = $this->serviceLocator->get('ref01.api');
$actualLanguageCountry = $refApi->getLocale();
$actualLanguage = explode("-", $actualLanguageCountry);
$defaultContentLang = getLangUrlFromLocale(DEFAULT_CONTENT_LANG);
if($actualLanguage[0] == 'fr')
```

- lien fichier 
```php
<?php echo _PTR_ ?>/ressources/fichiers/77e9218a7132.pdf
```

- page courante (current page )

```php
$url = $_SERVER['REQUEST_URI'];
$pageName = basename($url);
if(strpos($pageName, '.php') > -1){
    $pageName = explode(".php", $pageName);
    $pageName = $pageName[0] . ".php";
}else{
    $pageName = 'accueil.php';
}
```
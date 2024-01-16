---
url : https://trello.com/c/IriO0zgL/346-head-order
date : 2023-08-28
remarque : un peu de débogage sur ideo3 utilisant vscode, var_dump plus lisible dans code source page
---




Etude du fichier  : 

```
librairies/vendor/CoreMoteurDeRendu/src/CoreMoteurDeRendu/Core/AmbianceEngineRenderer.php
```

dans le methode  : 
```php
protected function initAmbiance(ViewModel $viewModel, ServiceManager $serviceManager)
```

le rang existant est défini dans le layout  : 

```php
$layoutTemplate = $this->datasourceProvider->getLayoutTemplateByRef($layoutRef);
```

cette layout est utilisé par une page  , comme dans cette catpure d'une entrée dans bdd  : 

![[Pasted image 20230828101210.png]]

Voici  la relation entre layout et page selon la documentation sur ideo3

![[Pasted image 20230828101254.png]]

cette methode **getLayoutTemplateByRef** se trouve dans le fichier  : 

```
librairies/vendor/CoreMoteurDeRendu/src/CoreMoteurDeRendu/Service/FileSystemAmbianceDataProvider.php
```

output du dump dans cette methode   : 

```php
var_dump($layoutContent,$layoutPath);
die();
```

output : 
```php
string(1358) "%preBlock% %meta% %title%%remoteInlineLess% %remoteInlineCss% %lessResources%  %zheader%
%zhero%%zprecontent% %zcontent%%zprefooter%
%zfooter%
%zcontactsheet% %zconfigsheet% %znavsheet% %remoteInlineJs% %jsResources% " string(78) 
```

```
"/var/www/html/public//AMBIANCE_GFFNYS36T5_framework2022-eco/fr_FR-homeTop.html"
```

output header : actual  

![[Pasted image 20230828105630.png]]

ny tokony ho izy : 


![[Pasted image 20230828110245.png]]


layout  content : (obtention par dump de la line  : layoutContent = file_get_contents($layoutPath);)
dans FileSystemAmbianceDataProvider.php

```html
%preBlock%
<!DOCTYPE html>
<html class="no-js no-io" lang="fr"><head><meta name="theme-color" content="var(--theme-color)"><meta charset="utf-8"><meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover"><meta name="mobile-web-app-capable" content="yes">%meta%
%title%%remoteInlineLess%
%remoteInlineCss%
%lessResources%</head><body class="home layout-home-top">

	<a id="skip-to-content-button" href="[#page-content](view-source:http://localhost:8585/public/#page-content)" class="button blk-button__link blk-button--a11y" aria-label="Aller au contenu">
		<span class="txt blk-button__label">
			<span>Aller au contenu</span>
		</span>
	</a>
	<a id="jump-to-contact-details-button" href="[#contactSheetTrigger](view-source:http://localhost:8585/public/#contactSheetTrigger)" class="button blk-button__link blk-button--a11y" aria-label="Aller aux coordonnées">
		<span class="txt blk-button__label">
			<span>Aller aux coordonnées</span>
		</span>
	</a>
	<!-- ==================================
		Header
	=================================== -->
	%zheader%<main class="wrapper bg-color-layout" id="page-start"><div class="layer-background"></div>
		%zhero%%zprecontent%
		%zcontent%%zprefooter%</main>%zfooter%<div id="modal-overlay" aria-hidden="true"></div>
	<!-- Modals -->
	%zcontactsheet%
	%zconfigsheet%
	%znavsheet%

	<!-- <script src="[[ambiance]]template/js/template.min.js"></script> -->%remoteInlineJs%
%jsResources%</body></html>
```


renderer viewmodel 
```
librairies/vendor/CoreMustache_1_0/src/CoreMustache_1_0/Service/ViewRendererFactory.php
```



```html
%preBlock%
<!DOCTYPE html>
<html class="no-js" lang="fr">
   <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      %meta%
      %title%<!--[if lt IE 9]>
      <script src="[[ambiance]]js/vendor/html5shiv.min.js"></script>
      <![endif]-->%remoteInlineLess%
      %remoteInlineCss%
      %lessResources%
   </head>
   <body itemscope itemtype="http://schema.org/Organization" class="content gridAmbiance">
      <div class="stickyfooter">
         <!-- ==================================
            Tab mobile spacer
            =================================== -->
         <div id="tab-mobile-spacer"></div>
         <!-- ==================================
            Header
            =================================== -->
         %zheader%<!-- ==================================
            Top Nav
            =================================== -->%ztopnav%<!-- ==================================
            Main content
            =================================== -->%zcontent%<!-- ==================================
            Subheader
            =================================== -->%zsubheader%<!-- ==================================
            Side nav
            =================================== -->%zsidenav%<!-- ==================================
            Prefooter
            =================================== -->%zprefooter%<!-- ==================================
            Footer
            =================================== -->%zfooter%<!-- ==================================
            Hero Container
            =================================== -->%zherocontainer%<!-- ==================================
            Mobile Tab-bar
            =================================== -->%ztabmobile%
      </div>
      <!-- ==================================
         Mobile Navigation
         =================================== -->
      %zmobilenav%
      <div id="tinyModal" class="reveal-modal tiny" data-reveal></div>
      <div id="smallModal" class="reveal-modal small" data-reveal></div>
      <div id="mediumModal" class="reveal-modal medium" data-reveal></div>
      <div id="largeModal" class="reveal-modal large" data-reveal></div>
      <div id="xlargeModal" class="reveal-modal xlarge" data-reveal></div>
      %remoteInlineJs%
      %jsResources%
   </body>
</html>

```


Voici donc le rang que nous devons suivre  : 

| Element                    | Description                                                       |
|-------------------------   |-------------------------------------------------------------------|
| meta utf 8                 | ao anaty layout filesystem                                        |
| meta viewport           | ao anaty layout filesystem                                        |
| title                   | viewModel->setVariable(self::TAG_TITRE, $refApi->getTitle());  |
| script pout theme       | themeJS_script= this->getScriptJSTheme($defaultTheme);   (concatené amin'ilay  ld+json io ambany io)      | 
| link ambiance.min.css   | viewModel->setVariable($config[self::AMIBANCE_RENDERER_CONFIG_INDEX][self::LESS_RESOURCE_TAG], $lessAmbianceResource . $lessResource . $lessPrintResource . $IconResources . $listGoogleFonts . $refApi->getLinkRel()); |
| link print.min.css      | viewModel->setVariable($config[self::AMIBANCE_RENDERER_CONFIG_INDEX][self::LESS_RESOURCE_TAG], $lessAmbianceResource . $lessResource . $lessPrintResource . $IconResources . $listGoogleFonts . $refApi->getLinkRel()); |
| meta theme-color        | ao anaty layout filesystem                                        |
| meta mobile-web-app-capable | ao anaty layout filesystem                                    |
| meta keywords           | $viewModel->setVariable(self::TAG_META, $refApi->getMeta());    |
| meta description        | $viewModel->setVariable(self::TAG_META, $refApi->getMeta());   |
| meta robots             | $viewModel->setVariable(self::TAG_META, $refApi->getMeta());   |
| script application/ld+json | $viewModel->setVariable("scriptcustom", $this->getScriptCustom()); |
| noscript                |   css/print dans LinkResource                                                               |
| link alternate fr-fr    |   dans RefApi ligne 483                                                    |
| link alternate en-fr    |     dans RefApi ligne  489                                                              |
| meta google-site-verification | tsy ilaina jerena                                         |


ireo ny toerana ahafahana mahazo ireo element rehetra anaty header 
ireto ary ny modificaiton tokon atao raha oahtra anraha à la lettre izao filaharana izao  : 

- ilay meta efatra par défaut ao anaty layout dia zaraina roa ny toerany araka izao filaharana zao 
- apekaraina ambonin'ny %meta% ny %title%
- zaraina roa ity ligne ity  :  ilay ao arina tokon eo ambany title , ilay getscriptCustom amban meta rehetra
```
$viewModel->setVariable("scriptcustom", $this->getScriptCustom() .$themeJS_script);
```
- layout %lessRessource mande ao ambany title 

raha FINTININA : 

- sarahina  : print.min.css link sy noscript 


TOKONY IZY

```html
%preBlock%
<!DOCTYPE html>
<html class="no-js no-io" lang="fr">
<head>
	<meta name="theme-color" content="var(--theme-color)">
	<meta charset="utf-8">
		%title%
		%remoteInlineLess%
		%remoteInlineCss%
		%lessResources%
	<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
	<meta name="mobile-web-app-capable" content="yes">
	%meta%

	</head>
	<body class="home layout-home-top">

	<a id="skip-to-content-button" href="[#page-content](view-source:http://localhost:8585/public/#page-content)" class="button blk-button__link blk-button--a11y" aria-label="Aller au contenu">
		<span class="txt blk-button__label">
			<span>Aller au contenu</span>
		</span>
	</a>
	<a id="jump-to-contact-details-button" href="[#contactSheetTrigger](view-source:http://localhost:8585/public/#contactSheetTrigger)" class="button blk-button__link blk-button--a11y" aria-label="Aller aux coordonnées">
		<span class="txt blk-button__label">
			<span>Aller aux coordonnées</span>
		</span>
	</a>
	<!-- ==================================
		Header
	=================================== -->
	%zheader%
	<main class="wrapper bg-color-layout" id="page-start"><div class="layer-background"></div>
		%zhero%%zprecontent%
		%zcontent%%zprefooter%
	</main>
	%zfooter%
	<div id="modal-overlay" aria-hidden="true"></div>
	<!-- Modals -->
	%zcontactsheet%
	%zconfigsheet%
	%znavsheet%

	<!-- <script src="[[ambiance]]template/js/template.min.js"></script> -->
	%remoteInlineJs%
%jsResources%
</body>
</html>
```
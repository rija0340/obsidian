---
tags  : ideo32_work,ideo3.2_work
url : https://trello.com/c/RH453kHR/247-shortcode-settings
date : 2023-02-13
---
### liste des fichiers modifiés et crées :  

* dev/#librairies/module/GestionContenuUtil/config/module.config.php
* dev/#librairies/module/GestionContenuUtil/src/GestionContenuUtil/Core/HtmlTagHandlers/SettingsTagHandler.php
* fichiers concernant langue dans : GestionContenuUtil/language/


### logique du fichier settingstaghandler

* recupération liste shortcode et handlers dans settings
* detecter tous les patterns qui ont des handler dans le html et interpreter et remplacer si c'est nécessaire. 
```php
public function getHtml(){
	//get from config patterns and handlers
	$config = $this->serviceLocator->get('configuration');
	$translator = $this->serviceLocator->get('translator');
	$currentPageLang = $this->serviceLocator->get('page.container')->getCurrentPageLang();
	$patterns = $config['gestioncontenu.util']['short_code']['pattern'];
	$handlers = $config['gestioncontenu.util']['short_code']['handlers'];
	$affichageTexte = $translator->translate('Affichage', 'GestionContenuUtil', $currentPageLang);
	$choisissezTexte = $translator->translate('Choisissez le thème clair ou sombre', 'GestionContenuUtil', $currentPageLang);
	$html = '
	<div class="blk-sheet__section">
	<h3>'. $affichageTexte .'</h3>
	<p>
	'.$choisissezTexte.'
	</p>
	<button type="button" role="switch" aria-checked="false" aria-label="'.$choisissezTexte.'" id="theme-switch">
		<span class="ico">[[svg_include:svg/tabler_collection/moon.svg]]</span>
		<span class="ico">[[svg_include:svg/tabler_collection/sun.svg]]</span>
	</button>
	</div>
';

//boucler pattern config et voir si le texte contient
//si contient utiliser handler pour retourner interpretation

	foreach ($patterns as $key => $pattern) {
	$pattern = "/".$pattern."/";
	preg_match_all($pattern, $html, $matches);
	
	// si des patterns sont trouvés, on get handler et interprete shortcode
	if( count($matches[0]) > 0){
	$handlerName = "\\". $handlers[$key];
	$handler = new $handlerName($this->serviceLocator);
	foreach ($matches[0] as $key => $matche) {
	$tagRessource = str_replace(array('[[', ']]'), array('', ''), $matche);
	$handler->setTag($tagRessource);
	$return = $handler->getHtml();
	$html = str_replace($matche,$return,$html);
}
}
}
return $html;

}
```
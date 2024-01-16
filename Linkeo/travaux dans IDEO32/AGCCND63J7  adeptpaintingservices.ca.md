
ajout de google tag (2) pour être précis :
- via B.O 
- via gstat 

ajout B.O est comme suit  : 

- ajout dans le champ : 

et enregistrement dans la table settings de la base de données avec key  : GAKey

## comment est-il utilisé dans la page (celui dans B.O)

Dans le fichier PagePreviewer.php : 
```php
public function getContent()
{
	$this->replaceContactTagByPhp();
	$this -> addTrackingCode() ;
	$pageFormatter = $this->serviceManager->get('moteurderendu.pagecontentformatter');
	$content = $pageFormatter->replacePhpCodeByValue($this->content);
	return $content;
}

```

la fonction **addTrackingCode()** est comme suit dans le même fichier  : 

```php
public function addTrackingCode(){
	$pageFormatter = $this->serviceManager->get('moteurderendu.pagecontentformatter');
	$page = $this->configProvider->getPage();
	$this->content = $pageFormatter -> addTrackingCode($this->content, $page) ;
}
```

on utilise une fonction dans la classe pageFormatter
fonction **addTrackingCode**

```php
/**
* Ajoute le contenu des codes google tracking
* @param string $data
* @param Object $pageAppelant
* @return string
*/
public function addTrackingCode($data, $pageAppelant){
	$gstats = $this->getServiceLocator()->get(\GStats\Services::RENDERER);
	$data = str_replace('<head>','<head>' . $gstats->renderTrackingCode('head','tag_open', $pageAppelant),$data);
	$data = str_replace('</head>',$gstats -> renderTrackingCode('head','tag_close', $pageAppelant). '</head>',$data);
	$data = preg_replace('/<body(.*)>/', '<body$1>' . $gstats->renderTrackingCode('body','tag_open', $pageAppelant),$data,1);
	$data = str_replace('</body>', $gstats->renderTrackingCode('body','tag_close', $pageAppelant) . '</body>', $data);
	/*ajout du meta facebook-domain-verification sur la page d'accueil
	c'est seulement dans cette méthode que icom3 hérite, du coup on met le code ici pour ne pas modifier à 2 endroits*/
	$data = $this->addFbDomainVerification($data, $pageAppelant);
	return $data ;
}

```

dans cette fonction on utilise une méthode de la classe **GStatsRendrer** : 
### fonction renderTrackingCode dans GstatsRenderer : 

```php
public function renderTrackingCode($location, $tagPos, $pageAppelant){
```

paramètres  : 
- location : head or body 
- $tagPos : tag_open or tag_close 
- $pageAppelant : nom de la page qui appelle

cette ligne dans cette fonction recupère la liste des gstas, 

```php
$list = $this ->getServiceLocator() -> get('Configuration') ;
```

voici un extrait de gstats_body qui se trouve dans le fichier /home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/module/GStats/config/module.config.php, on a la liste des gstats selon location et position , 


```php

   'gstats_body' => array(
         
        'tag_open' => array(
            'GTMKey' => array(
               'content' => '
    <!-- Google Tag Manager (noscript) -->
    <noscript><iframe src="https://www.googletagmanager.com/ns.html?id={GTMKey}"
    height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
    <!-- End Google Tag Manager (noscript) -->
',
               'pageHomeOnly' => false,
               'validation' => '/^(GTM)-[a-zA-Z0-9]{1,}/',
           ),
        ),
         
        'tag_close' => array(
            'GA4Key' => array(
                'content' => "<script>Epeius.addTracker( { name: 'Google Analytics 4', id: 'ga4', cookies: ['_ga', '_ga_{GA4Key}'], config: {key: '{GA4Key}'} } );</script>",
                'pageHomeOnly' => false,
                'validation' => '/^G-\w{10}$/'
            ),
            // google analytics
            'GAKey' => array(
                'content' => "<script>Epeius.addTracker( { name: 'Google Analytics', id: 'ga', cookies: ['_ga', '_gat', '_gid'], config: {key: '{GAKey}'} } );</script>",
                'pageHomeOnly' => false,
                'validation' => '/^((UA|YT|MO)-[0-9]+-[0-9]+$)/'
            ),
            'GoogleRemarketingTag' => array(
                'content' => "<script>Epeius.addTracker( { name: 'Google Ads Remarketing', id: 'gawr', config: {key: '985359031', params: {cbtn: 'SITE_CODEBOUTON', dpt: 'SITE_DEPARTMENT', region: 'SITE_REGION', pays:'SITE_PAYS', cat: 'SITE_CAT', souscat: 'SITE_SUBCAT'}} } );</script>",
                'pageHomeOnly' => false,
                'validation' => '//'    
            ),
            'scriptGtag' => array(
                'content' => $sScriptGtag,
                'pageHomeOnly' => false,
                'validation' => '',
            ),
            'scriptConvertTel' => array(
                'content' => $sScriptConvertTel,
                'pageHomeOnly' => false,
                'validation' => '',
            ),
        ),
     ),
```


on boucle le contenut de **$list** et remarquer que pour 

- $key == GAKey on set $keyVal  = callGoogleAnalyticsId()

cette fonction se trouve dans  /home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/common_config/common_function.php

voici le contenu : 
```php
function callGoogleAnalyticsId($checkVHost = true){
	if ($checkVHost && !checkVHost()){
		return null;
	}
	$result = callApiLinkeo('googleAnalytics');
	if (!empty($result['google_analyticsId'])){
		return $result['google_analyticsId'];
	}
	return null;
}
```

REMARQUE : 

Dans cette fonction la ligne ci dessous fait des checks qui ne sont pas satisfaites  : 

```php
if(empty($keyVal) || (!empty($validation) && !preg_match($validation, $keyVal))) continue ;
```

il se trouve que pour

$key == GAKey  callGoogleAnalyticsId() est empty alors qu'on a quelque chose dans la BDD
et puis meme si on parvient a avoir la valeur dans bdd , la validation pour GAKey ne correspondra pas pour le ticket, c'est là le problème 

question  : il faut que GA4Key soit utilisé pour le type de code qui est de format G-xxxx, comment on fait cela dans le B.O ???????
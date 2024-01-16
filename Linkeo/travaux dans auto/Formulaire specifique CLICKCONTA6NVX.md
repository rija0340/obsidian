---
tags : auto_work, CLICKCONTA6NVX
url : http://jira.linkeo.com/browse/IDEO-6656
date : 2023-03-01
---

reference  : http://jira.linkeo.com/browse/IDEO-6272
aussi dans doc in google drive  : ligne 110

<span class="text-danger" style="font-size : 20px">tips : trouver le moyen d'overrider un fichier, par factory or something else </span>

pick the sendmail function in ideo3 and ajust it to send the same information to the customer 


voici comment on get langue (picked dans auto rechercheenregistreesapi)

```php
// default lang

$aDefaultLang = $langueService->getDefaultLangueInfos();
$defaultLangueId = (int) $aDefaultLang['langueId'];
// current langage
$aCurrentLang = $langueService->getCurrentLangueInfos();
$langueId = (int) $aCurrentLang['langueId'];
$catalogueApi = $this->getServiceLocator()->get(getInfoCatalogue('api'));
$translator = $this->getServiceLocator()->get('translator');
$locale = DEFAULT_CONTENT_LANG == $aCurrentLang['langueLocale'] ? getLangUrlFromLocale(DEFAULT_CONTENT_LANG) : getLangUrlFromLocale($aCurrentLang['langueLocale']);

```

information propre au site  : 

// informations propre au site

$refApi = $this->getServiceLocator()->get('ref01.api');

$senderInfo['name'] = $refApi->getClientRef()->getNomSociete();

farany : check numero id formulaire, si iny dia zay vo mandefa mail am customer

#mail #email
<span class="text-danger">sur ngrok </span> : gmail ne marche pas mais mail linkeo marche 
<span class="text-danger"> sur localhost</span> : mail localhost marche ainsi que mail linkeo 

dans l'envoi de mail 
---
tags  : ideo32_work,ideo3.2_work
url : http://jira.linkeo.com/browse/IDEO-6704
date : 2023-05-03
revision :
---

## langue dans filesystem 


```php

$refApi = $this->serviceLocator->get('ref01.api');
$actualLanguageCountry = $refApi->getLocale();
$actualLanguage = explode("-", $actualLanguageCountry);
$defaultContentLang = getLangUrlFromLocale(DEFAULT_CONTENT_LANG);

```


## formula 


M = P [ i(1 + i)^n ] / [ (1 + i)^n – 1]  
  
Where:  
  
M = Monthly payment amount  
P = Principal amount (the amount borrowed)  
i = Monthly interest rate (the annual interest rate divided by 12)  
n = Total number of monthly payments


## liens 

http://10.99.0.21/index.php?action=fiche&module=site&id=120255427BBF6

http://10.99.0.24/_production3/c/courtierhypothequelaval.ca_ID301/www/Customize/Module/GestionContenuUtils

## lien en validation 
http://validation.courtierhypothequelaval.ca/
http://validation.courtierhypothequelaval.ca/admin/#pages/en_CA/37/335

## séparateur de millier 

et deux chiffres après virgule
```javascript
number.toFixed(2).replace(/\d(?=(\d{3})+\.)/g, \'$&,\')
```

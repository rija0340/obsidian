---
tags : ideo3_work, LINKDIRECT68J8
url : http://jira.linkeo.com/browse/IDEO-6699
date : 2023-04-14
---

<span class="remarque">Remarque : </span> the description is not really clear to understand, they talk about stars and after they give an API documentation to read. 

```description

Pour l'intégration des étoiles :  
Widget simple - documentation : Cliquez-ici pour le téléchargement

par widget company ID (par entreprise): 10873

OU  
Intégration avec l'api (modification couleur/bandeau dynamique..):

clé API: 3556fbc63566e9a722bb26269626561b

Documentations API:  
[https://new.api.opinionsystem.fr/v2/![](http://jira.linkeo.com/images/icons/linkext7.gif)](https://new.api.opinionsystem.fr/v2/)  
Intégration api
```

## fetch js from postman 

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Basic Q0xJQ0tDT05UQTZOVlg6Y1A2dEU4alc3ZU43");
var requestOptions = {
method: 'GET',
headers: myHeaders,
redirect: 'follow'
};

fetch("https://api.opinionsystem.fr/v2/client/company/rating?api_key=3556fbc63566e9a722bb26269626561b", requestOptions)
.then(response => response.text())
.then(result => console.log(result))
.catch(error => console.log('error', error));

</script>
```

## fetch php from postman 

```php
<?php
$curl = curl_init();
curl_setopt_array($curl, array(
CURLOPT_URL => 'https://api.opinionsystem.fr/v2/company?api_key=3556fbc63566e9a722bb26269626561b',
CURLOPT_RETURNTRANSFER => true,
CURLOPT_ENCODING => '',
CURLOPT_MAXREDIRS => 10,
CURLOPT_TIMEOUT => 0,
CURLOPT_FOLLOWLOCATION => true,
CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
CURLOPT_CUSTOMREQUEST => 'GET',
CURLOPT_HTTPHEADER => array(
'Authorization: Basic Q0xJQ0tDT05UQTZOVlg6Y1A2dEU4alc3ZU43'
),
));
$response = curl_exec($curl);
curl_close($curl);
echo $response;
?>
```


j'ai un peu chercher sur ce site

https://www.opinionsystem.fr/fr-fr/pro/functionalities "tab : diffusion avis" 

mais je n'ai pas trouvé comment intégrer le widget, la demande de démonstration requiert des informations à soumettre.

finalement on a utilisé un widget pour l'intégration  : 
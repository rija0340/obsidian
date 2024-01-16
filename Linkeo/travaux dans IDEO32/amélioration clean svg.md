---
url: https://trello.com/c/IFmdYIkp/383-am%C3%A9liorer-clean-logo-svg-%C3%A0-lupload
date: 2023-10-18
---
## Résultat de test : 

reto no nivermberenako natao

- scenario Matthieu non reproduit en local, clean svg marche correctement en local
- scenario Mattieu reproduit sur un site DID
- execution code sur local en dehors ideo3.2 -> clean svg marche
- execution code sur un site DID (lancement manuelle ) -> clean svg marche

atreto zan tsy haiko oe inona no tena tokony tsy hapandeha azy, za ko tsy maharaka oe aona ko fomba azo anaovana test anle code amle site HID

site DID de test : 
- lien code php : http://10.99.0.24/_production3/d/djsolutionsmiami.com_ID302/www/public/clean.php
- svg de test dans  : public/ressources/svg

# ce 10-01-2024
site misy bug  : http://10.99.0.24/_production3/j/jhs-isolation.com_ID301/www/public/admin/#params
code bouton  : CLICKCONTA6SWV

bug : 
- on upload puis en efface le fichier image, on a le logo delete qui apparait toujours et le url de l'image dans le code du logosmall (inspection html)

amélioration à apporter :
- pour une raison inconnue, l'image peut être supprimée, afficher rien et ne faire apparaitre le logo remove si fichier non présent  

comportement :
 en supprimant l'image directement depuis le dossier , on a toujours les données url dans la table settings >logosmall
 c'est pourquoi c'est affiché en blanc
- si on supprime by hand ce qui se trouve dans  bdd , table setting > logosmall, on a  plus rien affiché (etat cliquez ici ou deposer...) 

reflexion , 
pourquoi le model genere une erreur sur le site en validation mais pas pour le local sur machine 

ce 11

- doubler checker presence firchier et si non present supprimer logosmall data dans table settings 
- checker aussi en front et si non present supprimer aussi ???

## consigne 

- alohan'ny hanao enregistrement anaty base dia jereo indray mandeh le fichier raha tena ao marina , 
	- au moment upload 
	- au chargment de donnée le maka anle donnée 

## comment se fait l'upload d'un fichier logo 

le controller responsanble est le : 
- ResourceLogoRestController.php

la ligne ci -dessous se trouve dans le controller  : 
```php
$resourceId = $this->getCrud()->saveResource($data, true);
```

la fonction saveRessource se trouve dans le fichier  : $ResourceCrud$

et dans cette la fonction saveRessource, on a ces lignes : 
```php
$msg = '';
$fileData = $uploaderService->createFile($data,null,$msg,$logo);
if($fileData === false){
	echo $msg;
return false;
}
```

la creation de file par la fonction createFile se trouve dans le fichier $ResourceUploader$

après l'upload de fichier logo , on a une requête dans l'onglet réseau qui se lance (on ne trouve pas encore c'est qui l'auteur)
POST  : http://localhost:8585/public/admin/settings/

chemin se trouve dans  : 
```url
vendor/CoreConfigurationService/config/module.config.php
```

```php
'router' => array(

'routes' => array(

'settingsrest' => array(

'type' => 'segment',

'options' => array(

'route' => ADMIN_PATH . '/settings/[:id]',

'defaults' => array(

'controller' => 'settingsControllerRest',

),

'constraints' => array(

'id' => '[a-zA-Z0-9_\.-]+',

),

),

),

),

),

  

'controllers' => array(

'invokables' => array(

'settingsControllerRest' => 'CoreConfigurationService\Controller\IndexController',

),

),

```


finalement, ce qu'on a fait : 
- das ResourceUploader 
	- on check la présence image dans ressources/images et si non présent -> return false (on ne continue pas à enregistrer entity etc)
- dans indexcontroller,
	- durant upload, si fichier image non présent on n'enregistre pas les données dans table settings 
	- durant getlist au chargement de setting panel , si fichier image pas present (pour logo,logosmall et favicon) -> effacer donnée dans tablet ressource  et donnée dans table settings 
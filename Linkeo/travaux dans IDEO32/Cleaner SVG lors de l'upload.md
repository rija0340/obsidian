---
url: https://trello.com/c/3EusGGmF/345-cleaner-svg-lors-de-lupload
date: 2023-08-24
tags:
  - uploadfile, upload
---

fichier declaration route et controller 

```
/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/module/Gestioncontenu/config/module.config.php
```

controller  : 
```
'controller' => 'CoreRessourceManager\Controller\ResourceLogoRest',
```

il y a un fichier centralisé qui prend en charge uploader de tous les ressources  : 

ResourceUploader.php

c'est ce fichier qui a été modifié 

ce 31-08-2023 : 
------------------------------------
ajout de fonctionnalité  : 
+ blocage d'upload si fichier contenant script js 

fichier touché par le changement  : 
- librairies/public/integration/src/js/JEditor/Commons/libraries/jquery-plugins/uploader.js
- ResourcelogorestController
- reousercerestController

## TUTO

Les panels Paramètre et Fichier nous permettent d'uploader des fichiers dans le Backoffice.

La seule différence entre ces deux possiblité, au niveau proccessus c'est que dans le Paramètre on utilise un autre view qui est : FileUploaderView alors que dans le Ficher palel on ne l'utilise pas.

Paramètre et Fichier panels utilisent tous les deux le fichier uploader.js qui est un plugin jquery qui permet de facilter la gestion des téléchargements. 

On va voir le processus de téléchargement du coté Paramètre pour la suite  : 
### 0-MarqueClientView.js
dans ce fichier view on utilise un autre view pour l'upload d'image comme ceci  : 

```js
//logo
this.fileUploader = this.uploadFile(this.currentFileLogo, uploadParams);

uploadFile : function(currentFile, uploadParams) {
return new FileUploaderView({
	currentFile : currentFile,
	collection: this.fileCollection,
	uploadParams,
});

},
```

le chemin de **FileUploaderView** est : 

```
librairies/public/integration/src/js/JEditor/Commons/Files/Views/FileUploaderView.js
```

on a constaté aussi qu'on utilise un autre fichier jquery plugin qui est  : 

```
librairies/public/integration/src/js/JEditor/Commons/libraries/jquery-plugins/uploader.js
```


Voici comment tout est relié d'après ce que j'ai compris : 
### 1- uploader.js

#### a- debogage dans la navigateur:
au moment de l'upload, cette evenement "change" est fired  (dans uploader.js): 
```js
this.$exploreButton.on('change', function(e) {
	that._fetchFromInput.call(that, e);
});
```

je pense que dans FileUploaderView un widget jquery est rendu pour l'upload et le fichier uploader prend en charge les événements liés à ce widget.

```
et puis _fetchFromInput est appelé et puis appele à son tour la fonction _readFiles
```

dans la fonction **_readFiles**_, plusieurs checker de type de fichier sont utilisés comme  : **_isImage** etc, ce sont des fonctions contenant des regex pour checker extensions fichiers

```js
_isImage: function(file) {
	var extPattern = /^.*\.(png|jpg|jpeg|tiff|gif|svg)$/;
	var typePattern = /^image\/.*$/;
	return (extPattern.test(file.name.toLowerCase()) || typePattern.test(file.type.toLowerCase()));
},
```

dans la partie de la fonction readFiles ou on checke si fichier uploadé est image, on a modifier quelques lignes pour checker présence de script dans code source 
```js
var uploadInfos = {
    name: file.name,
    value: file,
    size: file.size,
    preview: preview,
    uploaded: 0,
    code: e.target.result //ligne ajouté
};
if (uploader._isImage(file)) { //modification contenu de ce if 
    var decodedData = atob(uploadInfos.code.split(',')[1]);
    if (decodedData.includes('<script>')) {
        uploader.errors.push('Le fichier semble corrompu');
        console.log("corruption du fichier");
        files.rejected++;
        if (files.length === 1) {
            uploader._onComplete();
        }

    } else {
        realPreview.addClass('imagepreview');
        realPreview.css({
            background: 'url(' + this.result + ') center center',
            backgroundSize: 'cover'
        });
    }
}
```

alors qu'avant la modification, on avait juste ça : 
```js
var uploadInfos = {
    name: file.name,
    value: file,
    size: file.size,
    preview: preview,
    uploaded: 0,
};
if (uploader._isImage(file)) {
        realPreview.addClass('imagepreview');
        realPreview.css({
            background: 'url(' + this.result + ') center center',
            backgroundSize: 'cover'
        });
}
```

REMARQUE : on a eu l'inspiration de modification par l'examination de ce qui se passe quand on importe un video de taille supérieur au maximum acceptable.
Maintenant regardons ce qui se passe dans la fonction **_onComplete**
#### b- fonction onComplete()

ensuite le processus de l'upload passe dans cette fonction. 
La dernière ligne de cette fonction trigger un événement 'complete ' et passe en paramètre un objet 

```js 
this._trigger('complete', null, {filesData: this.uploaded , error: errorMsg });
```
### 2- FileUploaderView.js 

path  : 
```
librairies/public/integration/src/js/JEditor/Commons/Files/Views/FileUploaderView.js
```

après le trigger dans la fonction onComplete() mentionnée en haut, la fonction **_onUpload** est appelé et reçoit deux paramètres  : event et data 

```js
_onUpload: function(event, data) {
    var file = data.filesData[0];
    if (file) {
        this.currentFile = new File(file.response);
        this.collection.add(this.currentFile);
        this.trigger(Events.FileUploaderEvents.UPLOAD, this.currentFile, this.collection);
    } else if (data.error) {
        this.trigger(Events.FileUploaderEvents.TOOBIG, data);
    }
},
```

REMARQUE : je n'ai pas trouvé la liiason entre cette fonction et le trigger dans uploader.js, je pense qu'il y a quelque part un listner qui les lie. par contre il y a cet événement dans FileUploaderView.js

```js
events: {
	'uploadercomplete': '_onUpload',
},
```
le paramètre data ici est l'objet  : 
```js
{filesData: this.uploaded , error: errorMsg }
```

Dans le cas d'importation d'un fichier ayant du script dedans l'objet est comme ceci  : 

```
{filesData: [] , error: "<li>Echec du chargement. Le fichier semble corrompu</li>" }
```

et donc ce qui va nous conduire dans le else if the _onUpload :

```js
this.trigger(Events.FileUploaderEvents.TOOBIG, data);
```
#### 3-MarqueClientView.js

cet évenement **Events.FileUploaderEvents.TOOBIG** est écouté dans ce fichier 

```js
this.listenTo(this.fileUploader, Events.FileUploaderEvents.TOOBIG, this.onError);
```

écoute sur l'objet fileUploader qui est un FileUploaderView, puis le nom de lévénement écouté et une function callback 
j'ai crée la fonction onError pour afficher un message d'erreur et de rerendre les marquesClients 
```js
	onError: function(data){
	var errorMessage = data.error.replace(/<li>/g, "").replace(/<\/li>/g, "");
	//affichage message d'erreur venant de data (trigger dans FileUploaderView)
	this.error({message:errorMessage});
	this.render();
},
```
le data en paramètre est passé par le trigger.
Le message obtenu dans le data a besoin d’être formaté.

REMARQUE : 

dans la fonction readFiles on a cette ligne  : 
uploader._upload.call(uploader);
et la fonction upload est responsable d'envoyer des requetes vers serveur, c'est pour cela que meme le fichier n'est pas accepté il ya toujours ce requête 
## modification des controller Resources et fileUploader

- requête envoyé par uploader.js est traité dans ResourceRestController (Filepanel) et ResourceLogoRestControoler (Marqueclient dans parametrePanel). 
- dans chaque Controller, on fait appel à une méthode de  **saveResource** de ResourceCrud.php

```php
$resourceId = $this->getCrud()->saveResource($data, false);
```
et dans cette méthode, on fait appel à une autre méthode de la classe ResourceUploader

```php
	$msg = '';
	$fileData = $uploaderService->createFile($data,null,$msg,$logo);
	if($fileData === false){
	echo $msg;
	return false;
}
```

la partie de la fonction createFile dans ResourceUploader  : 
```php
if(strpos($fileContent, '<script') !== false){
	unlink($filePath);
	return false;
}else if(preg_match($regexXml, $fileContent) ||preg_match($regexScriptJs, $fileContent)) {
//remplacement du balise xml par rien
	$modifiedContent = preg_replace($regexXml, '', $fileContent);
	//remplacement extra espace
	$minifiedSvgContent = preg_replace('/\s+/', ' ', $modifiedContent);
	$minifiedSvgContent = preg_replace('/<!--.*?-->/', '', $minifiedSvgContent);
	$minifiedSvgContent = preg_replace('/<!--.*?-->/', '', $minifiedSvgContent);
	$minifiedandcleanedSvgContent = preg_replace('/<script\b[^>]*>.*?<\/script>/is', '', $minifiedSvgContent);
	//enregistrement du fichier modifié, ecrasement de l'existant
	file_put_contents($filePath, $minifiedandcleanedSvgContent);
}
```

si contient de script, on return false et donc saveResource on a false, et donc ceci va etre false 

```
$resourceId = $this->getCrud()->saveResource($data, false);
```

et j'ai ajouté cette ligne dans le controlleurs pour retourner directement  une erreur 

```php
if (!is_int($resourceId)) {
	return $this->getResponse()->setStatusCode(\Zend\Http\Response::STATUS_CODE_403)->setContent(self::ERROR_CREATE_MESSAGE);
}
```

## message
pour le panel fichier le message apparait directement dans un popup. 
en parlant de message , il y a beaucoup de type de message qu'on utilise dans le projet qui se trouvent dans  le dossier : 

```
librairies/public/integration/src/js/JEditor/App/Messages
```

RESTE A FAIRE : 

- regarder erreur pour l'affichage message erreur
- différencier message por toobig et fichier corrompu 
- translation message depuis uppload.js
## liste des fichier impactés  : 

```
vendor/CoreRessourceManager/src/CoreRessourceManager/Controller/ResourceLogoRestController.php
vendor/CoreRessourceManager/src/CoreRessourceManager/Controller/ResourceRestController.php
vendor/CoreRessourceManager/src/CoreRessourceManager/Service/ResourceUploader.php
public/integration/src/js/JEditor/FilePanel/nls/fr-ca/i18n.js
public/integration/src/js/JEditor/FilePanel/nls/fr-fr/i18n.js
public/integration/src/js/JEditor/FilePanel/nls/i18n.js
public/integration/src/js/JEditor/Commons/libraries/jquery-plugins/uploader.js
public/integration/src/js/JEditor/ParamsPanel/Views/MarqueClientView.js![[Logo-Mexigrillsvg-0bb0svg_f905.svg]]
```
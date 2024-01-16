---
tags  : ideo32_work,ideo3.2_work
url : https://trello.com/c/DtldMt63/248-gestion-multi-adresse-rendu-block-contact
date : 2023-02-21
extreme development : true
canceled : true
---

tasks  :  
* ajout de formulaire par défaut qui reprend shortcode donnée client 
	* (dans la viewjs, on a valeur par défaut)
	* les champs sont modifiable 
	* formatage du json à stocker dans la base de données
* ajout d'un bouton permettant d'ajouter un autre formulaire de contact
	* texte translated (fonctionnalité déjà existant dans la backoffice)
* ajout d'un autre formulaire de contact si Click sur bouton <span style = "color : yellow">(fonctionnalité déjà existante)</span>
	* les champs sont modifiables et peuvent être mixé avec des short codes 
	* possibilité de supprimé les formulaires # par défaut 
* voir le rendu du shortcode [[contact_block]]

<span style="font-weight : bold; color : red">remarques</span>   :  les données seront stockées sous forme de json dans la table settings.
toutes les données seront dans un seul json car on va utiliser un seul paire key value dans la base.

## Choses faite durant le developpement

### coté backbone
* creation du template pour le premier formulaire par defaut
* creation de view correspondant 
* ajout du key value default value dans models/params.js
* creation de nouveau template pour liste adresse (html)
* creation de view pour liste adresse 
	* click sur le bouton ajouter adresse ajoute un json vide dans la base et render la view Adresse en ajoutant des childs correspondant au nombre de json dans la table 
* gestion des evenement suppression et modification dans chaque view

### coté php
puisque c'est un api donc il fallait modifier aussi un fichier php responsable de l'insertion dans la base du json  : 

```shell
/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/vendor/CoreConfigurationService/src/CoreConfigurationService/Controller/IndexController.php

/home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/vendor/CoreConfigurationService/config/module.config.php

```

<span class="text-danger">Dans indexcontroller : </span>  modification methode __create_or_replace__ et __getlist()__

<span class="text-danger" >Dans module.copnfig.php : </span> ajout d'une ligne dans social link


## sauvegarde des fichiers modifiés 

#### ListAdresses.js

```js

define([

'jquery',

"underscore",

'JEditor/Commons/Ancestors/Views/View',

'JEditor/Commons/Events',

'text!../Templates/ListAdresses.html',

"JEditor/App/Messages/Confirm",

'i18n!../nls/i18n'],

function ($, _, View, Events, template, Confirm, translate) {

var ListAdresses = View.extend({

events: {

  

"click .rigth-delete " :"DeleteOneAdress",

'click .shortcode': 'copyToClipboard'

},

initialize: function () {

this.model=this.options.model;

this.data=this.options.model.toJSON();

this.data=this.data.Adresses;

this._super();

this._template = this.buildTemplate(template, translate);

// this.listenTo(this.model, Events.BackboneEvents.CHANGE, this.onChange);

},

___onInputChange: function ($target) {

var field = $target.attr("name");

var shouldSave = $target.data("autosave") == true;

var output, error;

var $outputTarget = $target;

var pos = !$target.data("error-position") ? "before" : $target.data("error-position");

var filter = $target.data("filter");

filter = _.isFunction(this[filter])?this[filter]:function (val) {

return val?val:null;

};

var value =filter($target.val());

//onError

function onInvalid(model, validationError, options) {

if (validationError.field === field) {

error = validationError;

}

}

//listen to errors

this.listenToOnce(this.model, Events.BackboneEvents.INVALID, onInvalid);

if ($target.attr("type") === "checkbox") {

this.model[field] = $target.data("negate") ? !$target.is(":checked") : $target.is(":checked");

}

else {

  

if(field.includes("_")){

var arraySpliteField=field.split('_');

var propertyName =arraySpliteField[0];

var numAdresse =arraySpliteField[1];

numAdresse = parseInt(numAdresse) - 1;

var listeAdresses =this.model.get("Adresses");

listeAdresses[numAdresse][propertyName] = value;

this.model.set("Adresses", listeAdresses);

}

}

//error_positioning

if (pos !== "after" && pos !== "before") {

if (this.$(pos).length > 0) {

$outputTarget = this.$(pos);

pos = "append";

$outputTarget.children(".input-error." + field).remove();

}

else

pos = "before";

} else {

$outputTarget.siblings(".input-error." + field).remove();

}

if (error) {

output = "<span class=\"input-error " + field + "\"><span class=\"icon icon-warning\"></span>";

if (error.message)

output += "<span class=\"text\">" + error.message + "</span>";

output += "</span>";

$outputTarget[pos](output);

$target.addClass("error");

}

this.stopListening(this.model, Events.BackboneEvents.INVALID, onInvalid);

if (shouldSave && !error)

this.model.save();

  

},

  

confirm: function(params) {

this.app.messageDelegate.set(new Confirm(params));

},

DeleteOneAdress:function(event){

var $target = $(event.currentTarget);

var id = $target.attr("id");

var arraySplitId=id.split('_');

var numAdresse =arraySplitId[1];

  

this.confirm({

// message: translate('confirmDeleteSocial', {'name': $target.attr("name")}),

message: translate('confirmDeleteAdress', {'number': numAdresse}),

title: translate("deleteAction"),

type: 'delete',

onOk: _.bind(function() {

this.trigger("deleteOneAdress", parseInt(numAdresse) - 1);

}, this),

//options: {dialogClass: 'delete no-close', dontAskAgain: true}

options: {dialogClass: 'delete no-close'}

});

  

},

  

render: function () {

  

this.undelegateEvents();

this.$el.html(this._template({ liste: (this.data != null? this.data :0)}));

this.delegateEvents();

return this;

},

  

copyToClipboard : function (e){

var copyText = $(e.currentTarget).text();

const clipboard = navigator.clipboard;

if (clipboard !== undefined && clipboard !== "undefined") {

navigator.clipboard.writeText(copyText.trim()).then(this.successfully($(e.currentTarget)));

}

else

{

if (document.execCommand)

{

const el = document.createElement("input");

el.value = copyText;

document.body.append(el);

el.select();

el.setSelectionRange(0, value.length);

if (document.execCommand("copy"))

{

this.successfully();

}

el.remove();

}

}

},

  

successfully :function (el){

el.before('<div role="alert" aria-live="polite" style="top: auto;position: absolute;" class="toastcopy"><div class="jq-toast-single jq-icon-success" style="text-align: left; /*! display: none; */"><span class="icon icon-check-circle"></span><span>'+translate("copy")+'</span></div></div>')

window.setTimeout(function(){

el.parent().find('.toastcopy').remove();

}, 2000);

}

});

return ListAdresses;

});

```


#### AdresseView.js

```js

define(['jquery',

"underscore",

'JEditor/Commons/Ancestors/Views/View',

'JEditor/Commons/Events',

'JEditor/ParamsPanel/Views/ListAdresses',

'text!../Templates/Adresse.html',

'i18n!../nls/i18n'], function (

$,

_,

View,

Events,

ListAdresses,

template,

translate) {

var AdresseView = View.extend({

events: {

"click .addAdresse":"onClickAddAdresse",

'click .shortcode': 'copyToClipboard'

},

initialize: function () {

this._super();

this._template = this.buildTemplate(template,translate);

this.ChildViews={};

},

___onInputChange: function ($target) {

var field = $target.attr("name");

var shouldSave = $target.data("autosave") == true;

var output, error;

var $outputTarget = $target;

// var pos = !$target.data("error-position") ? "before" : $target.data("error-position");

var filter = $target.data("filter");

filter = _.isFunction(this[filter])?this[filter]:function (val) {

return val?val:null;

};

var value =filter($target.val());

//onError

function onInvalid(model, validationError, options) {

if (validationError.field === field) {

error = validationError;

}

}

//listen to errors

this.listenToOnce(this.model, Events.BackboneEvents.INVALID, onInvalid);

  

//sauvegarde dans modele les changements

var listeAdresses =this.model.get("Adresses");

listeAdresses[0][field] = value;

this.model.set("Adresses", listeAdresses);

  

// error_positioning

// if (pos !== "after" && pos !== "before") {

// if (this.$(pos).length > 0) {

// $outputTarget = this.$(pos);

// pos = "append";

// $outputTarget.children(".input-error." + field).remove();

// }

// else

// pos = "before";

// } else {

// $outputTarget.siblings(".input-error." + field).remove();

// }

if (error) {

output = "<span class=\"input-error " + field + "\"><span class=\"icon icon-warning\"></span>";

if (error.message)

output += "<span class=\"text\">" + error.message + "</span>";

output += "</span>";

$outputTarget[pos](output);

$target.addClass("error");

}

this.stopListening(this.model, Events.BackboneEvents.INVALID, onInvalid);

if (shouldSave && !error)

this.model.save();

},

onClickAddAdresse : function(e){

listeAdresses = this.model.get('Adresses');

  

var nbrAdresses = listeAdresses.length;

var nextNumero = parseInt(nbrAdresses) + 1;

  

var newAdresseObject = {

shortcode:"[[contact_block|"+ nextNumero +"]]",

nom:"",

adresse:"",

cp:"",

ville:"",

lienPlan:"",

telephone:""

}

listeAdresses.push(newAdresseObject);

this.model.set("Adresses",listeAdresses);

this.model.save();

this.$("#liste").remove();

this.render();

},

DeleteOne :function(key){

this.model.get("Adresses").splice(key,1)

console.log("key,this.model");

console.log(key,this.model);

this.model.save();

this.render();

},

render: function () {

  

this.undelegateEvents();

var listeAdresses = this.model.get('Adresses');

var defaultAdresse = listeAdresses[0];

  

this.$el.html(this._template(defaultAdresse));

this.renderListAdresses(this.model);

this.delegateEvents();

return this;

},

renderListAdresses :function(data){

var listeAdresses = data.attributes.Adresses;

this.ChildViews.ListAdresses= new ListAdresses({model : data});

this.listenTo(this.ChildViews.ListAdresses, 'deleteOneAdress',this.DeleteOne);

  

this.$("#liste").append(this.ChildViews.ListAdresses.render().$el);

},

  

copyToClipboard : function (e){

var copyText = $(e.currentTarget).text();

const clipboard = navigator.clipboard;

if (clipboard !== undefined && clipboard !== "undefined") {

navigator.clipboard.writeText(copyText.trim()).then(this.successfully($(e.currentTarget)));

}

else

{

if (document.execCommand)

{

const el = document.createElement("input");

el.value = copyText;

document.body.append(el);

el.select();

el.setSelectionRange(0, value.length);

if (document.execCommand("copy"))

{

this.successfully();

}

el.remove();

}

}

},

  

successfully :function (el){

el.before('<div role="alert" aria-live="polite" style="" class="toastcopy"><div class="jq-toast-single jq-icon-success" style="text-align: left; /*! display: none; */"><span class="icon icon-check-circle"></span><span>'+translate("copy")+'</span></div></div>')

window.setTimeout(function(){

el.parent().find('.toastcopy').remove();

}, 2000);

}

});

return AdresseView;

});
```


#### listadresses.html

```html

  

<!--

******************************************

créer nouvelle childView marque client,

y déplacer ce contenu

******************************************

-->

  
  

<%

for(var i=1;i< liste.length; i++){

var adresse=liste[i];

var j = i +1;

%>

  

<div id="content" class="inline-params thin-border radius shadow">

<span class="inline-params__name">

<%=__("adresse")%> <%= j %> :

</span>

<label>

<span class="inline-params__nameLogoFooter shortcode">

<%= adresse.shortcode %>

</span>

</label> <br>

<span class="inline-params__name">

<%=__("nom")%> :

</span>

<label>

<span class="custom-input">

<input type="text" data-autosave="true" name="nom_<%=j%>" class="field-input neutral-input bold" value="<%= adresse.nom %>"/>

</span>

</label><br>

<span class="inline-params__name">

<%=__("adresse")%> :

</span>

<label>

<span class="custom-input">

<input type="text" data-autosave="true" name="adresse_<%=j%>" class="field-input neutral-input bold" value="<%= adresse.adresse %>"/>

</span>

</label><br>

<span class="inline-params__name">

<%=__("code_postal")%> :

</span>

<label>

<span class="custom-input">

<input type="text" data-autosave="true" name="cp_<%=j%>" class="field-input neutral-input bold" value="<%= adresse.cp %>"/>

</span>

</label><br>

<span class="inline-params__name">

<%=__("ville")%> :

</span>

<label>

<span class="custom-input">

<input type="text" data-autosave="true" name="ville_<%=j%>" class="field-input neutral-input bold" value="<%= adresse.ville %>"/>

</span>

</label><br>

<span class="inline-params__name">

<%=__("lien_plan")%> :

</span>

<label>

<span class="custom-input">

<input type="text" data-autosave="true" name="lienPlan_<%=j%>" class="field-input neutral-input bold" value="<%= adresse.lienPlan %>"/>

</span>

</label><br>

<span class="inline-params__name">

<%=__("telephone")%> :

</span>

<label>

<span class="custom-input">

<input type="text" data-autosave="true" name="telephone_<%=j%>" class="field-input neutral-input bold" value="<%= adresse.telephone %>"/>

</span>

</label>

<span id="deleteAdresse_<%=j%>"class="rigth-delete icon-bin"> </span>

</div>

  
  

<%

}

%>

  

<!--

******************

end new childView

******************

-->
```
#### adresses.html
```html

<div class="main-content__wrapper ">

<!--

******************************************

créer nouvelle childView marque client,

y déplacer ce contenu

******************************************

-->

<div class="ideo-title">

<h1>

<%=__("adresses")%> :

<span>

<%=__("set_adresses")%>

</span>

</h1>

</div>

  

<div id="content" class="inline-params thin-border radius shadow">

<span class="inline-params__name">

<%=__("adresse")%> 1 :

</span>

<label>

<span class="inline-params__nameLogoFooter shortcode">

<%= shortcode %>

</span>

</label> <br>

<span class="inline-params__name">

<%=__("nom")%> :

</span>

<label>

<span class="custom-input">

<input type="text" data-autosave="true" name="nom" class="field-input neutral-input bold" value="<%= nom %>"/>

</span>

</label><br>

<span class="inline-params__name">

<%=__("adresse")%> :

</span>

<label>

<span class="custom-input">

<input type="text" data-autosave="true" name="adresse" class="field-input neutral-input bold" value="<%= adresse %>"/>

</span>

</label><br>

<span class="inline-params__name">

<%=__("code_postal")%> :

</span>

<label>

<span class="custom-input">

<input type="text" data-autosave="true" name="cp" class="field-input neutral-input bold" value="<%= cp %>"/>

</span>

</label><br>

<span class="inline-params__name">

<%=__("ville")%> :

</span>

<label>

<span class="custom-input">

<input type="text" data-autosave="true" name="ville" class="field-input neutral-input bold" value="<%= ville %>"/>

</span>

</label><br>

<span class="inline-params__name">

<%=__("lien_plan")%> :

</span>

<label>

<span class="custom-input">

<input type="text" data-autosave="true" name="lienPlan" class="field-input neutral-input bold" value="<%= lienPlan %>"/>

</span>

</label><br>

<span class="inline-params__name">

<%=__("telephone")%> :

</span>

<label>

<span class="custom-input">

<input type="text" data-autosave="true" name="telephone" class="field-input neutral-input bold" value="<%= telephone %>"/>

</span>

</label>

</div>

  

<section id="liste"></section>

  

<div class="block-button medium align-center text-center">

<a class="button addAdresse">

<span class="txt"><span><%=__("ajouter_une_adresse")%></span></span>

</a>

</div>

<!--

******************

end new childView

******************

-->

  

</div>
```
dernier commit dans lib  : r5273 

```bash
svn diff -r 5273
```
liste fichiers impactés  : 


<h1>compareo reto avy eo </h1> (mitovy)

```shell
extension/ideo3/module/RechercheEnregistrees/src/RechercheEnregistrees/Service/RechercheEnregistreesApi.php et filesystem

```


### liste fichier impactés coté backoffice  : 

svg search
concretes/modules/catalogues02/controller/ConfigurationsController.class.php
concretes/modules/catalogues02/view/configurations/list.phtml
concretes/modules/catalogues02/langues/fr_FR.php
concretes/admin/integrations/src/js/app/catalog/i18n/en_AU.json  
concretes/admin/integrations/src/js/app/catalog/i18n/en_CA.json  
concretes/admin/integrations/src/js/app/catalog/i18n/en_FR.json  
concretes/admin/integrations/src/js/app/catalog/i18n/fr_AU.json  
concretes/admin/integrations/src/js/app/catalog/i18n/fr_CA.json  
concretes/admin/integrations/src/js/app/catalog/i18n/fr_FR.json
concretes/admin/integrations/src/js/app/configuration/ConfigurationView.js
concretes/admin/integrations/src/js/app/configuration/Recherche
concretes/admin/integrations/src/js/app/configuration/Recherche/Models
concretes/admin/integrations/src/js/app/configuration/Recherche/Models/Recherche.js
concretes/admin/integrations/src/js/app/configuration/Recherche/Views
concretes/admin/integrations/src/js/app/configuration/Recherche/Views/RechercheView.js
concretes/admin/integrations/src/js/app/configuration/Recherche/Views/RightPanel
concretes/admin/integrations/src/js/app/configuration/Recherche/Views/RightPanel/ConfigRechercheView.js
concretes/admin/integrations/src/js/js-list/configuration.json
concretes/admin/integrations/src/templates/configuration/recherche
concretes/admin/integrations/src/templates/configuration/recherche/recherche.mst

### liste des fichiers impactés FRONT 


concretes/modules/catalogues02/langues/en_AU.php
concretes/modules/catalogues02/langues/en_CA.php
concretes/modules/catalogues02/langues/en_FR.php
extension/ideo3/module/Catalogues/src/Catalogues/Language/fr_FR.php
extension/ideo3/module/CataloguesAuto/src/CataloguesAuto/Language/en_FR.php
extension/ideo3/module/CataloguesAuto/src/CataloguesAuto/Language/fr_FR.php extension/ideo3/module/CataloguesAuto/src/CataloguesAuto/Repository/ElementsCategoriesProduitsRepository.php
extension/ideo3/module/CataloguesAuto/src/CataloguesAuto/Service/Renderer/RechercheAvanceeMGRenderer.php
extension/ideo3/module/CataloguesAuto/src/CataloguesAuto/Service/Renderer/RechercheAvanceeRenderer.php
extension/ideo3/module/CataloguesAuto/src/CataloguesAuto/Service/TagHandlers/rechercheAvanceeMGShortCodeHandler.php
extension/ideo3/module/CataloguesAuto/src/CataloguesAuto/Service/TagHandlers/rechercheAvanceeShortCodeHandler.php
extension/ideo3/module/CataloguesAuto/view/catalogues/rechercheAvanceeMG.mustache
extension/ideo3/module/RechercheEnregistrees/src/RechercheEnregistrees/Service/RechercheEnregistreesApi.phpextension/ideo3/module/RechercheEnregistrees/src/RechercheEnregistrees/Service/TagHandlers/rechercheEnregistreesPopupShortCodeHandler.php
 extension/ideo3/module/RechercheEnregistrees/view/rechercheEnregistrees/rechercheEnregistreesMail.mustache

extension/ideo3/public/catalogues/api/produit.php




## voici comment on a procédé pour creer un param dans  B.O auto 

Ajout configuration dans

[http://localhost/Auto/est-autos.fr/public/catalogues/panel/index.php?action=configurations%3Aindex&module=catalogues02](http://localhost/Auto/est-autos.fr/public/catalogues/panel/index.php?action=configurations%3Aindex&module=catalogues02)


+ ajout html dans tamplate :

/home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769immo/#librairies/concretes/modules/catalogues02/view/configurations/list.phtml


+ Ajout module dans :

/home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769-immo/#librairies/concretes/admin/integrations/src/js/app/configuration/Recherche

ce module contient :
modele et views et rightpanel

+ ajout de view du nouveau module dans :

/home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769-immo/#librairies/extension/ideo3/public/catalogues/panel/css-js/js/app/configuration/ConfigurationView.js

+ ajout liste des js dans

/home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769-immo/#librairies/concretes/admin/integrations/src/js/js-list/configuration.json

+ creation du moustache du rightpanel dans

/home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769-immo/#librairies/concretes/admin/integrations/src/templates/configuration/recherche

**ce nouveau module est ajouté dans :** /home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769-immo/#librairies/extension/ideo3/public/catalogues/panel/css-js/js/app/configuration/ConfigurationView.js

ticket sur ajour ecran b.o pour configuration recherche haut, recherche gauche et recherche enregistrée
ajout des parametres dans config > configurer les champs

+recupération des valeurs dans renderer RAMG
+ajout des var dans moustache

le js se trouve dans handler pour auto et immo
  
var element = document.getElementById("rechercheWrap");

```php
if(motcleActif == "true"){
  element.classList.remove("hide");
}else{
  element.classList.add("hide");
}

```

pour afficher ou cacher le bouton recherche enregistrée :


ajouter cette ligne dans /home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769-immo/#librairies/extension/ideo3/public/catalogues/api/produit.php
  
$rechercheenregistreeActif = $configService->getValeur('RAMG_enregistree_actif')== "false" ? false : true;

et passer dans $listProduit

celui ci est retourné par produit.php à chaque recherche mg ou affichage


<span class="titre1"> Amélioration à faire </span> (23-03-2023)

* factoriser rechercheAvanceeMGShortCodeHandler.php
* trouves les codes superflus pour RechercheAvancéeMGRenderer


## css style pour recherche avancée menu gauche


```css 

/*--------------------------- Recherche avancée menu gauche----------------------------- */
    
    .advancedsearchMG {
		font-family: @secondaryFont;
		background-color: lighten(@darkColor, 15);
		padding:2rem;
		@media @mq-large-rule {
			margin-top: 9.7rem;
		}
		/*padding: 2rem 2.5rem 3rem;*/
		form {
		    column-count: 1;
			@media @mq-medium-rule {
				column-count: 1;
			}
			@media @mq-large-rule {
				column-count: 1;
			}
			label {
				display: inline-block;
				color: @lightColor;
			}
			input[type=button] {
				padding: 1rem 2rem;
				left: 25%;
				right: 25%;
				@media @mq-medium-rule {
					left: 42%;
					right: 42%;
				}
				@media @mq-large-rule {
					left: 45%;
					right: 45%;
				}
				&:hover {
					background-color: @tertiaryColor;
				}
			}
		}
	}
	
	.labelRecherche {

        font-size: 1.05rem;
        @media @mq-medium-rule {
			font-size: 1.1rem;
		}
		@media @mq-large-rule {
		    font-size: 1.2rem;
		}
        font-weight: 500;
        margin-bottom: 1rem;
    }
	
    .sliderRA{
    position: relative;
    //width: 95vmin;
    //background-color: #ffffff;
    //padding: 50px 40px 20px 40px;
    border-radius: 10px;
    margin-bottom: 35px;
    }
    .sliderRAContainer{
        position: relative;
        width: 100%;
        /*height: 100px;
        margin-top: 30px;*/
    }
    .sliderRAInput[type="range"]{
        -webkit-appearance: none;
        -moz-appearance: none;
        appearance: none;
        width: 100%;
        outline: none;
        position: absolute;
        margin: auto;
        top: 0;
        bottom: 0;
        background-color: transparent;
        pointer-events: none;
    }
    .sliderRATrack{
        width: 100%;
        height: 5px;
        position: absolute;
        margin: auto;
        top: 0;
        bottom: 0;
        border-radius: 5px;
        color: #465465;
        background: linear-gradient(to right, rgb(218, 218, 229) 0%, #465465 0%, #465465 100%, rgb(218, 218, 229) 100%);
    }
    .sliderRAInput[type="range"]::-webkit-slider-runnable-track{
        -webkit-appearance: none;
        height: 5px;
    }
    .sliderRAInput[type="range"]::-moz-range-track{
        -moz-appearance: none;
        height: 5px;
    }
    .sliderRAInput[type="range"]::-ms-track{
        appearance: none;
        height: 5px;
    }
    .sliderRAInput[type="range"]::-webkit-slider-thumb{
        -webkit-appearance: none;
        height: 1.7em;
        width: 1.7em;
        background-color: #fafafa;
        cursor: pointer;
        margin-top: -9px;
        pointer-events: auto;
        border-radius: 50%;
    }
    .sliderRAInput[type="range"]::-moz-range-thumb{
        -webkit-appearance: none;
        height: 1.7em;
        width: 1.7em;
        cursor: pointer;
        border-radius: 50%;
        /*background-color: #3264fe;*/
        pointer-events: auto;
        border:2px solid #ebeded;
    }
    .sliderRAInput[type="range"]::-ms-thumb{
        appearance: none;
        height: 1.7em;
        width: 1.7em;
        cursor: pointer;
        border-radius: 50%;
        /*background-color: #3264fe;*/
        pointer-events: auto;
        border:2px solid #ebeded;
    }
    .sliderRAInput[type="range"]:active::-webkit-slider-thumb{
        background-color: #ffffff;
        border: 3px solid #3264fe;
    }
    .sliderRAValues{
        /*background-color: #3264fe;*/
        width: 100%;
        position: relative;
        margin-right: 0%;
        padding: 10px 0;
        border-radius: 5px;
        /*text-align: center;*/
        /*font-weight: 500;*/
        font-size: 25px;
        color: #000000;
    }
    
    .sliderRAValues label{
        width:100%;
    }
    
    input#selPuissanceReelleMaxMG,
    input#selPuissanceReelleMinMG {
        display: inline-block;
        width: 100%;
    }
    
    #formRechercheAvanceeMG .optRAMG{
        width:100%;
    }
    
    #formRechercheAvanceeMG .optionRAMG{
        margin-bottom: 20px;
        background-color: @darkColor;
        padding: 1rem 1rem 0;
        transition: all .4s ease-in-out;
        label {
            margin-bottom: 1rem;
        }
        .optRAMG {
            position:relative;
            &:before{
                background: @lightColor;
                content: '';
                height: 1px;
                margin-left: 0;
                position: absolute;
                left: 95%;
                top: 50%;
                 .transform(rotate(90deg));
                .transition(all 0.3s ease-in-out);
                width: 10px;
            }
            &:after{
                background: @lightColor;
                content: '';
                height: 1px;
                margin-left: 0;
                position: absolute;
                left: 95%;
                top: 50%;
                width: 10px;
    
            }
        }
        &.active {
            background-color: @primaryColor;
            padding: 1rem;
            .optRAMG {
                position: relative;
                &:before{ .transform(rotate(0deg));}
            }
        }

        &:hover {
            background-color: @primaryColor;
           
        }
    }
    
    #backToSearch a {
        font-size: 0.8rem;
        /*@media @mq-medium-rule {
			font-size: 1rem;
		}
		@media @mq-large-rule {
		    font-size: 1.1rem;
		}*/
        line-height: 3;
        color: @lightColor;
        text-transform: uppercase;
        text-decoration: none;
        font-weight: 500;
        font-family: @secondaryFont;
    }
    
    #formRechercheAvanceeMG .tabRAMG{
        position: relative;
        left: 0;
        top: -47px;
    }
    
    #formRechercheAvanceeMG input.tabTypeOffre {
        background: @lightColor;
        border: 0;
        color: @darkColor;
    }
    
    
    
    #formRechercheAvanceeMG input.tabTypeOffre.active {
        background: @primaryColor;
        border: 0;
        color: @lightColor;
    }
    
    #formRechercheAvanceeMG label {
        color: #fff;
    }
    
    span.actual-price {
        font-family: @primaryFont !important;
    }
    
    /* custom checkbox */
    .MGcontent {
      display: block;
      position: relative;
      padding-left: 35px;
      padding-top: 4px;
      margin-left: 10px;
      margin-bottom: 12px;
      cursor: pointer;
      -webkit-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
      user-select: none;
    }
    
    /* Hide the browser's default checkbox */
    .MGcontent input {
      position: absolute;
      opacity: 0;
      cursor: pointer;
      height: 0;
      width: 0;
    }
    
    /* Create a custom checkbox */
    .checkmark {
      position: absolute;
      top: 0;
      left: 0;
      height: 25px;
      width: 25px;
      background-color: #eee;
    }
    
    /* On mouse-over, add a grey background color */
    .MGcontent:hover input ~ .checkmark {
      background-color: #ccc;
    }
    
    /* When the checkbox is checked, add a blue background */
    .MGcontent input:checked ~ .checkmark {
      background-color: #2196F3;
    }
    
    /* Create the checkmark/indicator (hidden when not checked) */
    .checkmark:after {
      content: "";
      position: absolute;
      display: none;
    }
    
    /* Show the checkmark when checked */
    .MGcontent input:checked ~ .checkmark:after {
      display: block;
    }
    
    /* Style the checkmark/indicator */
    .MGcontent .checkmark:after {
      left: 9px;
      top: 5px;
      width: 5px;
      height: 10px;
      border: solid white;
      border-width: 0 3px 3px 0;
      -webkit-transform: rotate(45deg);
      -ms-transform: rotate(45deg);
      transform: rotate(45deg);
    }
        .containerMinMax{
        display: flex;
    }
    .containerMinMax-item{
        display:flex; 
        flex-direction: row; 
        align-items :baseline;
        flex:1;
        
    }
    .containerMinMax-item input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
    /* display: none; <- Crashes Chrome on hover */
        -webkit-appearance: none;
        margin: 0; /* <-- Apparently some margin are still there even though it's hidden */
    }

    .containerMinMax-item input[type=number] {
        -moz-appearance:textfield; /* Firefox */
        text-align: center;
        border-radius: 5px;
    }
    .containerMinMax-item label{
        margin:  10px;
    }
    
    /*------------- FIN Recherche avancée menu gauche-------------------- */    

```



## pour recherche haut 

```css 
 /*------------- Recherche avancée menu haut-------------------- */ 
aside.aside01 {
        
            z-index: 2;
        @media @mq-large-rule {
        	margin-top: -9rem;
        }
    	.block-Advancedsearch {
    	    font-family: @secondaryFont;
    		background: @primaryColor;
    		background-color: lighten(@darkColor, 15);
    		padding: 2rem 2.5rem 3rem;
     		form {
        			@media @mq-medium-rule {
        				column-count: 2;
        			}
        			@media @mq-large-rule {
        				column-count: 3;
        			}
        			label {
        				display: inline-block;
        				color: @lightColor;
        			}
        			input[type=button] {
        				padding: 1rem 2rem;
        				left: 25%;
        				right: 25%;
        				position  : absolute;
        				@media @mq-medium-rule {
        					left: 42%;
        					right: 42%;
        				}
        				@media @mq-large-rule {
        					left: 45%;
        					right: 45%;
        				}
        				&:hover {
        					background-color: @tertiaryColor;
        				}
        			}
        		}
    	}
    }
/**------------- FIN Recherche avancée menu haut-------------------- */ 
```



## effacement prix max dans backoffice  : 

```html
<label>{{translations.prixmax}} :</label>
<input type="number" min=0 name="RAMG_max_prix" value={{maxprix.valeur}}>
```


## list of fichier a commiter  : 


/mnt/_cssframework/js/icom3/mst/products-auto.mst (pour bouton activer alerte)
/var/www/ambiances/AMBIANCE_1KJTQGFHV0_Automotive-*Concept/template/less/template.less (avec les css dessus)c


```php
public function insertLogPasserelle($message)
{
	$str = '';
	if(!empty($message))
	{
		$str .= $message . "\n";
	}
	if(!empty($str))
	{
		$pathLog = $this->getImportdestDirPasserelle() . $this->traceLog;
		$f = fopen($pathLog, "a");
		if(!$f) return;
		fwrite($f, $str . "\n");
		fclose($f);
	}
}

```

## table pour save config dans bdd 'est-auto.fr'

http://localhost/phpmyadmin/sql.php?server=1&db=CLICKCONTA6QCC&table=IC302_configurations&pos=0&token=884b334e59402ba1ed659659737aaa2a

## style recherche avanccée pour estauto

```css

   /*---------------------------------------- Recherche avancée menu gauche---------------------------------------- */
    
    .advancedsearchMG {
		font-family: @secondaryFont;
		background-color: lighten(@darkColor, 15);
		padding:2rem;
		@media @mq-large-rule {
			margin-top: 9.7rem;
		}
		/*padding: 2rem 2.5rem 3rem;*/
		form {
		    column-count: 1;
			@media @mq-medium-rule {
				column-count: 1;
			}
			@media @mq-large-rule {
				column-count: 1;
			}
			label {
				display: inline-block;
				color: @lightColor;
			}
			input[type=button] {
				padding: 1rem 2rem;
				left: 25%;
				right: 25%;
				@media @mq-medium-rule {
					left: 42%;
					right: 42%;
				}
				@media @mq-large-rule {
					left: 45%;
					right: 45%;
				}
				&:hover {
					background-color: @primaryColor;
				}
			}
		}
	}
	
	.labelRecherche {

        font-size: 1.05rem;
        @media @mq-medium-rule {
			font-size: 1.1rem;
		}
		@media @mq-large-rule {
		    font-size: 1.2rem;
		}
        font-weight: 500;
        margin-bottom: 1rem;
    }
	
    .sliderRA{
    position: relative;
    //width: 95vmin;
    //background-color: #ffffff;
    //padding: 50px 40px 20px 40px;
    border-radius: 10px;
    margin-bottom: 35px;
    }
    .sliderRAContainer{
        position: relative;
        width: 100%;
        /*height: 100px;
        margin-top: 30px;*/
    }
    .sliderRAInput[type="range"]{
        -webkit-appearance: none;
        -moz-appearance: none;
        appearance: none;
        width: 100%;
        outline: none;
        position: absolute;
        margin: auto;
        top: 0;
        bottom: 0;
        background-color: transparent;
        pointer-events: none;
    }
    .sliderRATrack{
        width: 100%;
        height: 5px;
        position: absolute;
        margin: auto;
        top: 0;
        bottom: 0;
        border-radius: 5px;
        color: #465465;
        background: linear-gradient(to right, rgb(218, 218, 229) 0%, #465465 0%, #465465 100%, rgb(218, 218, 229) 100%);
    }
    .sliderRAInput[type="range"]::-webkit-slider-runnable-track{
        -webkit-appearance: none;
        height: 5px;
    }
    .sliderRAInput[type="range"]::-moz-range-track{
        -moz-appearance: none;
        height: 5px;
    }
    .sliderRAInput[type="range"]::-ms-track{
        appearance: none;
        height: 5px;
    }
    .sliderRAInput[type="range"]::-webkit-slider-thumb{
        -webkit-appearance: none;
        height: 1.7em;
        width: 1.7em;
        background-color: #fafafa;
        cursor: pointer;
        margin-top: -9px;
        pointer-events: auto;
        border-radius: 50%;
    }
    .sliderRAInput[type="range"]::-moz-range-thumb{
        -webkit-appearance: none;
        height: 1.7em;
        width: 1.7em;
        cursor: pointer;
        border-radius: 50%;
        /*background-color: #3264fe;*/
        pointer-events: auto;
        border:2px solid #ebeded;
    }
    .sliderRAInput[type="range"]::-ms-thumb{
        appearance: none;
        height: 1.7em;
        width: 1.7em;
        cursor: pointer;
        border-radius: 50%;
        /*background-color: #3264fe;*/
        pointer-events: auto;
        border:2px solid #ebeded;
    }
    .sliderRAInput[type="range"]:active::-webkit-slider-thumb{
        background-color: #ffffff;
        border: 3px solid #3264fe;
    }
    .sliderRAValues{
        /*background-color: #3264fe;*/
        width: 100%;
        position: relative;
        margin-right: 0%;
        padding: 10px 0;
        border-radius: 5px;
        /*text-align: center;*/
        /*font-weight: 500;*/
        font-size: 25px;
        color: #000000;
    }
    
    .sliderRAValues label{
        width:100%;
    }
    
    input#selPuissanceReelleMaxMG,
    input#selPuissanceReelleMinMG {
        display: inline-block;
        width: 100%;
    }
    
    #formRechercheAvanceeMG .optRAMG{
        width:100%;
    }
    
    #formRechercheAvanceeMG .optionRAMG{
        margin-bottom: 20px;
        background-color: @darkColor;
        padding: 1rem 1rem 0;
        transition: all .4s ease-in-out;
        label {
            margin-bottom: 1rem;
        }
        .optRAMG {
            position:relative;
            &:before{
                background: @lightColor;
                content: '';
                height: 1px;
                margin-left: 0;
                position: absolute;
                left: 95%;
                top: 50%;
                 .transform(rotate(90deg));
                .transition(all 0.3s ease-in-out);
                width: 10px;
            }
            &:after{
                background: @lightColor;
                content: '';
                height: 1px;
                margin-left: 0;
                position: absolute;
                left: 95%;
                top: 50%;
                width: 10px;
    
            }
        }
        &.active {
            background-color: @primaryColor;
            padding: 1rem;
            .optRAMG {
                position: relative;
                &:before{ .transform(rotate(0deg));}
            }
        }

        &:hover {
            background-color: @primaryColor;
           
        }
    }
    
    #backToSearch a {
        font-size: 0.8rem;
        /*@media @mq-medium-rule {
			font-size: 1rem;
		}
		@media @mq-large-rule {
		    font-size: 1.1rem;
		}*/
        line-height: 3;
        color: @lightColor;
        text-transform: uppercase;
        text-decoration: none;
        font-weight: 500;
        font-family: @secondaryFont;
    }
    
    #formRechercheAvanceeMG .tabRAMG{
        position: relative;
        left: 0;
        top: -47px;
    }
    
    #formRechercheAvanceeMG input.tabTypeOffre {
        background: @lightColor;
        border: 0;
        color: @darkColor;
    }
    
    
    
    #formRechercheAvanceeMG input.tabTypeOffre.active {
        background: @primaryColor;
        border: 0;
        color: @lightColor;
    }
    
    #formRechercheAvanceeMG label {
        color: #fff;
    }
    
    span.actual-price {
        font-family: @primaryFont !important;
    }
    
    /* custom checkbox */
    .MGcontent {
      display: block;
      position: relative;
      padding-left: 35px;
      padding-top: 4px;
      margin-left: 10px;
      margin-bottom: 12px;
      cursor: pointer;
      -webkit-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
      user-select: none;
    }
    
    /* Hide the browser's default checkbox */
    .MGcontent input {
      position: absolute;
      opacity: 0;
      cursor: pointer;
      height: 0;
      width: 0;
    }
    
    /* Create a custom checkbox */
    .checkmark {
      position: absolute;
      top: 0;
      left: 0;
      height: 25px;
      width: 25px;
      background-color: #eee;
    }
    
    /* On mouse-over, add a grey background color */
    .MGcontent:hover input ~ .checkmark {
      background-color: #ccc;
    }
    
    /* When the checkbox is checked, add a blue background */
    .MGcontent input:checked ~ .checkmark {
      background-color: #2196F3;
    }
    
    /* Create the checkmark/indicator (hidden when not checked) */
    .checkmark:after {
      content: "";
      position: absolute;
      display: none;
    }
    
    /* Show the checkmark when checked */
    .MGcontent input:checked ~ .checkmark:after {
      display: block;
    }
    
    /* Style the checkmark/indicator */
    .MGcontent .checkmark:after {
      left: 9px;
      top: 5px;
      width: 5px;
      height: 10px;
      border: solid white;
      border-width: 0 3px 3px 0;
      -webkit-transform: rotate(45deg);
      -ms-transform: rotate(45deg);
      transform: rotate(45deg);
    }
        .containerMinMax{
        display: flex;
    }
    .containerMinMax-item{
        display:flex; 
        flex-direction: row; 
        align-items :baseline;
        flex:1;
        
    }
    .containerMinMax-item input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
    /* display: none; <- Crashes Chrome on hover */
        -webkit-appearance: none;
        margin: 0; /* <-- Apparently some margin are still there even though it's hidden */
    }

    .containerMinMax-item input[type=number] {
        -moz-appearance:textfield; /* Firefox */
        text-align: center;
        border-radius: 5px;
    }
    .containerMinMax-item label{
        margin:  10px;
    }
    
    /*---------------------------------------- FIN Recherche avancée menu gauche---------------------------------------- */  
```


## comment est ce que template less 
dans b.o pourrait être a jour après modification fichier dans ideo3-auto
efa natao  : jerena reseau refefa miclick am template.less, jerena hoe iza controller miketrika anzay action zay 
tajona  : hita oe iza controller ary aona anovana anle comportement ao 


admin/const/api/name/template

```shell

sudo chmod -R 777 customization
sudo chown -R www-data:www-data customization
```



## css haut et gauche 

```css 
// /*------------- Recherche avancée menu haut cssframework-------------------- */

// aside.aside01 {

// z-index: 2;

// @media @mq-large-rule {

// margin-top: -9rem;

// }

// .block-Advancedsearch {

// font-family: @secondaryFont;

// background: @primaryColor;

// background-color: lighten(@darkColor, 15);

// padding: 2rem 2.5rem 3rem;

// form {

// @media @mq-medium-rule {

// column-count: 2;

// }

// @media @mq-large-rule {

// column-count: 3;

// }

// label {

// display: inline-block;

// color: @lightColor;

// }

// input[type=button] {

// padding: 1rem 2rem;

// left: 25%;

// right: 25%;

// position : absolute;

// @media @mq-medium-rule {

// left: 42%;

// right: 42%;

// }

// @media @mq-large-rule {

// left: 45%;

// right: 45%;

// }

// &:hover {

// background-color: @tertiaryColor;

// }

// }

// }

// }

// }

// /**------------- FIN Recherche avancée menu haut-------------------- */

  

// /*--------------------------- Recherche avancée menu gauche----------------------------- */

// .advancedsearchMG {

// font-family: @secondaryFont;

// background-color: lighten(@darkColor, 15);

// padding:2rem;

// @media @mq-large-rule {

// margin-top: 9.7rem;

// }

// /*padding: 2rem 2.5rem 3rem;*/

// form {

// column-count: 1;

// @media @mq-medium-rule {

// column-count: 1;

// }

// @media @mq-large-rule {

// column-count: 1;

// }

// label {

// display: inline-block;

// color: @lightColor;

// }

// input[type=button] {

// padding: 1rem 2rem;

// left: 25%;

// right: 25%;

// @media @mq-medium-rule {

// left: 42%;

// right: 42%;

// }

// @media @mq-large-rule {

// left: 45%;

// right: 45%;

// }

// &:hover {

// background-color: @tertiaryColor;

// }

// }

// }

// }

  

// .labelRecherche {

  

// font-size: 1.05rem;

// @media @mq-medium-rule {

// font-size: 1.1rem;

// }

// @media @mq-large-rule {

// font-size: 1.2rem;

// }

// font-weight: 500;

// margin-bottom: 1rem;

// }

  

// .sliderRA{

// position: relative;

// //width: 95vmin;

// //background-color: #ffffff;

// //padding: 50px 40px 20px 40px;

// border-radius: 10px;

// margin-bottom: 35px;

// }

// .sliderRAContainer{

// position: relative;

// width: 100%;

// /*height: 100px;

// margin-top: 30px;*/

// }

// .sliderRAInput[type="range"]{

// -webkit-appearance: none;

// -moz-appearance: none;

// appearance: none;

// width: 100%;

// outline: none;

// position: absolute;

// margin: auto;

// top: 0;

// bottom: 0;

// background-color: transparent;

// pointer-events: none;

// }

// .sliderRATrack{

// width: 100%;

// height: 5px;

// position: absolute;

// margin: auto;

// top: 0;

// bottom: 0;

// border-radius: 5px;

// color: #465465;

// background: linear-gradient(to right, rgb(218, 218, 229) 0%, #465465 0%, #465465 100%, rgb(218, 218, 229) 100%);

// }

// .sliderRAInput[type="range"]::-webkit-slider-runnable-track{

// -webkit-appearance: none;

// height: 5px;

// }

// .sliderRAInput[type="range"]::-moz-range-track{

// -moz-appearance: none;

// height: 5px;

// }

// .sliderRAInput[type="range"]::-ms-track{

// appearance: none;

// height: 5px;

// }

// .sliderRAInput[type="range"]::-webkit-slider-thumb{

// -webkit-appearance: none;

// height: 1.7em;

// width: 1.7em;

// background-color: #fafafa;

// cursor: pointer;

// margin-top: -9px;

// pointer-events: auto;

// border-radius: 50%;

// }

// .sliderRAInput[type="range"]::-moz-range-thumb{

// -webkit-appearance: none;

// height: 1.7em;

// width: 1.7em;

// cursor: pointer;

// border-radius: 50%;

// /*background-color: #3264fe;*/

// pointer-events: auto;

// border:2px solid #ebeded;

// }

// .sliderRAInput[type="range"]::-ms-thumb{

// appearance: none;

// height: 1.7em;

// width: 1.7em;

// cursor: pointer;

// border-radius: 50%;

// /*background-color: #3264fe;*/

// pointer-events: auto;

// border:2px solid #ebeded;

// }

// .sliderRAInput[type="range"]:active::-webkit-slider-thumb{

// background-color: #ffffff;

// border: 3px solid #3264fe;

// }

// .sliderRAValues{

// /*background-color: #3264fe;*/

// width: 100%;

// position: relative;

// margin-right: 0%;

// padding: 10px 0;

// border-radius: 5px;

// /*text-align: center;*/

// /*font-weight: 500;*/

// font-size: 25px;

// color: #000000;

// }

  

// .sliderRAValues label{

// width:100%;

// }

  

// input#selPuissanceReelleMaxMG,

// input#selPuissanceReelleMinMG {

// display: inline-block;

// width: 100%;

// }

  

// #formRechercheAvanceeMG .optRAMG{

// width:100%;

// }

  

// #formRechercheAvanceeMG .optionRAMG{

// margin-bottom: 20px;

// background-color: @darkColor;

// padding: 1rem 1rem 0;

// transition: all .4s ease-in-out;

// label {

// margin-bottom: 1rem;

// }

// .optRAMG {

// position:relative;

// &:before{

// background: @lightColor;

// content: '';

// height: 1px;

// margin-left: 0;

// position: absolute;

// left: 95%;

// top: 50%;

// .transform(rotate(90deg));

// .transition(all 0.3s ease-in-out);

// width: 10px;

// }

// &:after{

// background: @lightColor;

// content: '';

// height: 1px;

// margin-left: 0;

// position: absolute;

// left: 95%;

// top: 50%;

// width: 10px;

  

// }

// }

// &.active {

// background-color: @primaryColor;

// padding: 1rem;

// .optRAMG {

// position: relative;

// &:before{ .transform(rotate(0deg));}

// }

// }

  

// &:hover {

// background-color: @primaryColor;

// }

// }

  

// #backToSearch a {

// font-size: 0.8rem;

// /*@media @mq-medium-rule {

// font-size: 1rem;

// }

// @media @mq-large-rule {

// font-size: 1.1rem;

// }*/

// line-height: 3;

// color: @lightColor;

// text-transform: uppercase;

// text-decoration: none;

// font-weight: 500;

// font-family: @secondaryFont;

// }

  

// #formRechercheAvanceeMG .tabRAMG{

// position: relative;

// left: 0;

// top: -47px;

// }

  

// #formRechercheAvanceeMG input.tabTypeOffre {

// background: @lightColor;

// border: 0;

// color: @darkColor;

// }

  
  
  

// #formRechercheAvanceeMG input.tabTypeOffre.active {

// background: @primaryColor;

// border: 0;

// color: @lightColor;

// }

  

// #formRechercheAvanceeMG label {

// color: #fff;

// }

  

// span.actual-price {

// font-family: @primaryFont !important;

// }

  

// /* custom checkbox */

// .MGcontent {

// display: block;

// position: relative;

// padding-left: 35px;

// padding-top: 4px;

// margin-left: 10px;

// margin-bottom: 12px;

// cursor: pointer;

// -webkit-user-select: none;

// -moz-user-select: none;

// -ms-user-select: none;

// user-select: none;

// }

  

// /* Hide the browser's default checkbox */

// .MGcontent input {

// position: absolute;

// opacity: 0;

// cursor: pointer;

// height: 0;

// width: 0;

// }

  

// /* Create a custom checkbox */

// .checkmark {

// position: absolute;

// top: 0;

// left: 0;

// height: 25px;

// width: 25px;

// background-color: #eee;

// }

  

// /* On mouse-over, add a grey background color */

// .MGcontent:hover input ~ .checkmark {

// background-color: #ccc;

// }

  

// /* When the checkbox is checked, add a blue background */

// .MGcontent input:checked ~ .checkmark {

// background-color: #2196F3;

// }

  

// /* Create the checkmark/indicator (hidden when not checked) */

// .checkmark:after {

// content: "";

// position: absolute;

// display: none;

// }

  

// /* Show the checkmark when checked */

// .MGcontent input:checked ~ .checkmark:after {

// display: block;

// }

  

// /* Style the checkmark/indicator */

// .MGcontent .checkmark:after {

// left: 9px;

// top: 5px;

// width: 5px;

// height: 10px;

// border: solid white;

// border-width: 0 3px 3px 0;

// -webkit-transform: rotate(45deg);

// -ms-transform: rotate(45deg);

// transform: rotate(45deg);

// }

// .containerMinMax{

// display: flex;

// }

// .containerMinMax-item{

// display:flex;

// flex-direction: row;

// align-items :baseline;

// flex:1;

// }

// .containerMinMax-item input::-webkit-outer-spin-button,

// input::-webkit-inner-spin-button {

// /* display: none; <- Crashes Chrome on hover */

// -webkit-appearance: none;

// margin: 0; /* <-- Apparently some margin are still there even though it's hidden */

// }

  

// .containerMinMax-item input[type=number] {

// -moz-appearance:textfield; /* Firefox */

// text-align: center;

// border-radius: 5px;

// }

// .containerMinMax-item label{

// margin: 10px;

// }

  

// /*------------- FIN Recherche avancée menu gauche-------------------- */
```


ajouter une div et class text-align center pour le bouton reinitialiser




<span class="remarque">Remarque</span>

## test en ligne après maj lib auto 

* fonctionnement B.O  - OK 
* front comportement  - Ok
* reste à tester affichage bouton "activer alerte" - attente maj cssframework



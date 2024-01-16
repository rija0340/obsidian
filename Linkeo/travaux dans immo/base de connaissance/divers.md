### base de données  : 

* images se trouvent dans la table __IC301_images_images__
* association produit avec image se trouve dans table  : __IC301_produits_images__

### flow passerelle 

* import.php est appelé par l'url du passerelle  (public/catalogues/api/import.php)
* passerelle utilisé est en fonction de param "file-product" dans url 
* après on utilise des methodes en fonction de file-product value, ces méthodes sont dans __catalogueController__
*  dans le contolleur on utilise une classe propre au type de passerelle 
* dans cette classe, il y a la correspondance ainsi que des overrides des methodes d'importabstractController si c'est nécessaire 
	* correspondance  : entre données xml et celui de notre bdd
```php
  <?php

public function importUbiflowFtpAuto($host, $user, $pwd)
{
    ini_set("memory_limit", "512M");
    $this->_load(
        "modules/" .
            getInfoCatalogue("module") .
            "/classes/ImportsUbiflow.class.php",
        PTR()
    );
    $import = new ImportsUbiflow();
    if ($import->isFtpValid($host, $user, $pwd)) {
        $datas = $import->extractDatas();
    }
    if (isset($datas)) {
        //return the name of the file converted into zip
        return $datas;
    } else {
        $aReturn = "Fichier invalide";
        //delete the file if invalide
        $import->cleanDirectoryImportUbiflow();
        header("Content-Type: application/json");
        echo json_encode($aReturn);
        exit();
    }
}

?>

```

dans le code ci-dessous  : 

* on check la connexion avec un serveur ftp, 
	* cela implique deux choses : connexion et telechargement du xml  

#### <span class="titre3">extract data methode
</span> 

* on loop over the xml et creer un array contenant les données produits -> $dataList
* telechargement des images ( dans methode setCorrespondance )
* création de csv depuis l'array contenant données produits -> $dataList
* <span class="text-danger"> creation de zip contenant csv,xml, images dans sauvegardeNomPasserelle</span>
* result contient ref des nouveaux produits (ceci est pour la recherche enregistrée)
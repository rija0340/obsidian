---
tags  : auto_work, CLICKCONTA6NVX
url : http://jira.linkeo.com/browse/IDEO-6637
date : 2023-02-03
---

ouvrir le site test [[sites local#auto]]

lien pour lien pour lib auto 
```shell 
cd /home/rrakotoarinelina/programming/Linkeo/libraries2/branches/immo-auto/#librairies
```

ceci a été fait en standardisation , voici la liste des fichiers impactés : 

* immo-auto/#librairies/concretes/modules/cataloguesAuto/classes/ImportsAutocargest.class.php
* immo-auto/#librairies/extension/ideo3/public/catalogues/api/import.php
* immo-auto/#librairies/modules/cataloguesAuto/ImportsPasserelleAbstract.class.php

1) dans le premier fichier : création de ce fichier pour y ajouter la correspondance, entre notre base de données et les données en xml du presta 
2) ajout du get des données du url à executer lors du lancement importation 
3) ajout d'une methode pour checker connexion serveur FTP, (protocol utilisé FTPS),
	 *  check connexion 
	 * telecharge le zip par un curl (seulement curl car ftps utilisé )
	 * extract le zip et recuperation du xml dedans ( et puis la suite est déjà existante)



### commentaire à faire dans ticket  : 

*travail fait* 

* liste des balises dans le xml du presta qu'on a utilisé  : 

reference
marque
modele
version
carrosserie
energie
kilometrage
garantie
prix
vendu
couleur
couleur_int
puissance_fiscale
puissance_din
cylindree
mise_en_circulation
nbr_vitesses
nbr_portes
nbr_places
CO2
equipements
grp_equipements
photos
* liste des balises dans le xml du presta qu'on a pas utilisé : 

adresse
code_postal
ville
email
tel
misenavant
dateachat
vuvp
prix_marchand
prix_catalogue
tva_recuperable

* liste des propriétés qu'on a trouvé des correspondances 

'produit_reference'
'produit_nom'
'images'
'elementsCategorie_nom'
'produit_marque'
'produit_actif'
'produit_descriptif'
'produit_caracteristique'
'produit_options'
'produit_prix'
'produit_carburant'
'produit_date_circulation'
'produit_kilometrage'
'produit_puissance_reelle'
'produit_cylindree'
'produit_puissance_fiscale'
'produit_co2'
'produit_type_transmission'
'produit_nombre_de_rapports'
'produit_type_carosserie'
'produit_portes'
'produit_places'

* liste des propriétés qu'on a pas pu trouvé de correspondance dans le xml du presta : 

'produit_collection'
'produit_status'
'produit_resume'
'fichier_fichier'
'produit_type_vehicule'
'produit_type_offre'
'produit_annee' 
'produit_prix_promo'
'produit_date_garantie'
'produit_gps'
'produit_climatisation'
'produit_fermeture_centralise'
'produit_regulateur_vitesse'
'produit_radard_recul'
'produit_bluetooth'
'produit_longueur'
'produit_largeur'
'produit_hauteur'
'produit_volume_coffre'
'produit_masse_vide'
'produit_vitesse_max'
'produit_capacite_nominale_coffre'
'produit_consommation_urbaine'
'produit_consommation_ext_urbaine'
'produit_consommation_mixte'
'produit_periode_production'
'produit_commercialisation'
'produit_type_moteur'
'produit_nbre_cylindres'

*le zip doit se trouver dans un dossier "datas" dans le serveur FTP.*

---------------lien import passerelle en ligne  : ---------------------
le key est déjà correct 

```url
https://www.garage-betton.fr/catalogues/api/import.php?key=3c6b39eb50e99bdc993036b9a7d5de92c37458cc&file-product=autocargest&user=CLICKCONTA6NVX&host=client.linkeo.com&pwd=cP6tE8jW7eN7
```

--------------lien local-----------
pour est auto 

http://127.0.0.1/Auto/est-autos.fr/public/catalogues/api/import.php?key=6cac992fc045a1f02cd448a9d15d2e693efaf2fc&file-product=autocargest&user=CLICKCONTA6NVX&host=client.linkeo.com&pwd=cP6tE8jW7eN7
pour muro cars


http://127.0.0.1/Auto/murocars.fr_60328/public/catalogues/api/import.php?key=f79dd5d529c8c6a45e996d45df7b732bdf5b1031&file-product=autocargest&user=CLICKCONTA6NVX&host=client.linkeo.com&pwd=cP6tE8jW7eN7


pour le site proprietaire du passerelle 

```url
http://127.0.0.1/Auto/garage-betton.fr_60956/public/catalogues/api/import.php?key=3c6b39eb50e99bdc993036b9a7d5de92c37458cc&file-product=autocargest&user=CLICKCONTA6NVX&host=client.linkeo.com&pwd=cP6tE8jW7eN7 

```


curl pour download file from ftp server  : 
curl --ftp-ssl -u CLICKCONTA6NVX:cP6tE8jW7eN7 ftp://ftp-auto.linkeo.com:21/autocargest.zip -o autocargest.zip



curl --ftp-ssl -u CLICKCONTA6NVX:cP6tE8jW7eN7 ftp://client.linkeo.com:21/betton.xml -o betton.xml


## modificaiton farany eo amle mi diferencier anle zip sy xml sy ny tohiny


commentaire atao ndray  : 

*essai en cours sur fichier presta et correction quelques changements correspondances*

* on a besoin de savoir la signification de cette balise ainsi que les valeur possible qu'elle peut contenir : <vuvp>vp</vuvp>
* valeur possible de cette balise aussi : <carrosserie>Combiné</carrosserie>

## modification d'extension et contenu xml venant du presa
il parle de zip dans la documentaion alors qu'il a envoyé un xml dans le serveur 

il a modififé l'exemple de xml dans la documentation , ajouter et remove quelques balises.

## contact client
user : CLICKCONTA6NVX  
pwd : cP6tE8jW7eN7  
host : client.linkeo.com  
Port : 21  
Protocole: FTP

# commentaire 
est ce que tu peux m'aider sur ces points : concernant le passerelle il ya ces balises 
<carrosserie>Combiné</carrosserie> quelles sont les valeurs possibles 
<vuvp>vp</vuvp> à quoi correspond cette balise ainis que les valeurs possibles et leur signification 
<misenavant>0</misenavant>

dans le xml on n'a pas année 

<span class="text-danger" style="font-size : 25px">voir le dernier commentaire de ce ticket pour l'utilisation de Curl </span> http://jira.linkeo.com/browse/IDEO-6232

```curl 
$destDir = $this->getImportdestDirUbiflow();
$local_file = "ubiflow.zip";

$ch = curl_init();
$fh   = fopen($destDir . $local_file, 'w');
curl_setopt($ch, CURLOPT_URL, "ftp://".$ftp_server."/ag890034.zip");
curl_setopt($ch, CURLOPT_USERPWD, $ftp_user_name.":".$ftp_user_pass);
curl_setopt($ch, CURLOPT_PORT, 21);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, FALSE);
curl_setopt($ch, CURLOPT_FTP_SSL,TRUE );
curl_setopt($ch, CURLOPT_VERBOSE, TRUE);
curl_setopt($ch, CURLOPT_FILE, $fh); 

//pasv
curl_setopt($ch, CURLOPT_FTP_USE_EPRT, true);

//curl_setopt($ch, CURLOPT_DIRLISTONLY, TRUE);
$result = curl_exec($ch);

fclose($fh);

curl_close($ch);

```

comment voir si un passerelle a été lancé
* zip dans sauvegardeNomPasserelle
* log dans import/import.log

## 28-04-2023

type energie dans xml  : 

Essence sans plomb
Diesel 
Essence 
ES
GO
Electrique

 + grp equipement misy encodage tsy mamely
 + cylindré n'est pas correct car valeur max permis est 99.99 -> type champ float(4,2) on utilise 4 digit dont 2 utilisé après virgule


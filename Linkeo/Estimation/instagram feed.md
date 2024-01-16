
http://jira.linkeo.com/browse/IDEO-6587

documentation que moi meme j'ai crée pour resumer ce qu'on doit faire pour mettre en place un instagram feed au sein d'un site web : 

premier lien  : https://developers.facebook.com/docs/instagram-basic-display-api/getting-started

###  <span class="titre1">Etape 1</span> 

* creation de compte developpeur facebook   : https://developers.facebook.com/apps
* creation app facebook ( instagram )   https://developers.facebook.com/docs/instagram-basic-display-api/getting-started (suivre le tutoriel)
* dans https://developers.facebook.com/apps, on a la liste des apps 
* dans https://developers.facebook.com/apps/656622146125988/instagram-basic-display/basic-display/, #basic_display ^45f4f2
	* id app instagram 
	* cle secrete instagram 
	* url de redirection (à renseigner)
	* liste des user instagram ( ce sont les users qu'on veut recuperer les feeds )

### Etape 2 : ajout d'utilisateur test dans l'app crée

après ajout, une invitation a été envoyé à l'utilisateur du compte insta, il faut qu'il confirme pour pouvoir continuer.

Ouvrez une nouvelle session de navigation web, accédez à [www.instagram.com](https://www.instagram.com/), puis connectez-vous au compte Instagram que vous venez d’inviter. Accédez à **(Icône de profil)** > **Modifier le profil** > **Applications et sites web** > **Invitations de testeur**, puis acceptez l’invitation.

### Etape 3 :  Authentifier l’utilisateur 

en ouvrant ce lien dans un navigateur, on authentifie un compte insta et obtient un code dans l'url de redirection 

id app instagram  : dans basic display [[#^45f4f2]]

```shell
https://api.instagram.com/oauth/authorize?client_id={id app instagram}&redirect_uri={url redirection}&scope=user_profile,user_media&response_type=code
```

reponse authentification de l'utilisateur test  :  le code dans l'url de redirection est à copier sans #_ (reponse po)

### Etape 4 : echanger le code contre un token

j'ai lancé ca dans un terminale pour le test

correctd verion chactgpt (echange code -> token) (code notahiana)

```
curl -X POST -F "client_id={id app insta}" -F "client_secret={key secret app insta}" -F "grant_type=authorization_code" -F "redirect_uri={url redirection}" -F "code={code}" "https://api.instagram.com/oauth/access_token"
```

En cas de réussite, l’API renvoie un objet encodé en JSON contenant un <span class="text-danger">token d’accès de courte durée pour utilisateur Instagram, valide pendant une heure</span>  et votre ID d’utilisateur test :

```
{ "access_token": "IGQVJ...", "user_id": 17841405793187218 }
```

### Etape 5 : obtenir un token longue durée 

utiliser le token de courte durée, client secrete ( key secret app instagram)

```curl
curl -i -X GET "https://graph.instagram.com/access_token?grant_type=ig_exchange_token&client_secret=0c5c1d6c1de665bfa0e65b645ff7bdc0access_token=IGQVJXcTBzX183TWdpQV9VWF90bFg1cjlzcWF0Sjl0VU82Y3FaNEN0Y3JIMFJlSklpN3lqdV92bVZAMMUdZAR09JRE1fQlh3d3NPWGlxWVhuZAHRVMmRtbXJ0YVdrZAzQ1LVk1aVdJbzU3Q2U5a2g3ajV6R2dPWTU1YURubzlv"
```
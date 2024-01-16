ter


il faut noter qu'il faut stopper mysql et apache avant de pouvoir demarrer container IDEO3.2 : 

[[stopper ou demarrer apache et mysql]]

commande pour accéder dans le dossier ideo3.2 et permettand de lancer le container 
#open_folder

```shell
cd /home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env

docker compose up -d 

xdg-open http://localhost:8585/public/

xdg-open http://localhost:8585/public/admin?debug=true

xdg-open http://localhost:8080

cd /home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies/
subl .

```
à noter que l'attribut -d a pour rôle de cacher log dans terminal

<span class="text-danger">chemin pour aller dans lib </span> 

```shell
cd /home/rrakotoarinelina/programming/Linkeo/libraries/IDEO3.2/env/src/ideo3/dev/#librairies
```

### Mettre à jour le build integration (le container doit être démarré) ###
```shell
docker exec -w /mnt/_phplib/#librairies3/public/integration apache-php-node grunt prod 
```

<link rel="preload" href="/css/print.min.css?v=1676995592" as="style" onload="this.onload=null;this.rel='stylesheet';this.media='print'">


## liste des fichiers impactés : 

M       public/integration/src/js/JEditor/ParamsPanel/Models/Params.js
M       public/integration/src/js/JEditor/ParamsPanel/Templates/ListSocialNetwork.html
M       public/integration/src/js/JEditor/ParamsPanel/Templates/SocialNetwork.html
M       public/integration/src/js/JEditor/ParamsPanel/Views/SocialNetworks.js
M       public/integration/src/js/JEditor/ParamsPanel/nls/fr-ca/i18n.js
M       public/integration/src/js/JEditor/ParamsPanel/nls/fr-fr/i18n.js
M       public/integration/src/js/JEditor/ParamsPanel/nls/i18n.js


<span class="remarque">remarque</span> : à la fin de la création de tous ces liens symboliques il faut exécuter 

```shell

sudo chmod -R 777 garage_breuil
sudo chown -R www-data:www-data garage_breuil

```
## dans www

```shell
sudo rm -r common_config
sudo ln -s /mnt/_phplib/#librairies3/common_config/ "common_config"

sudo rm -r includes
sudo ln -s config/ "includes"
```
## dans www/icom3

<span class="remarque">remarque</span> : il faut changer nom lib en fonction lib à utiliser (libsIcom3 / libsAuto/ libsImmo)

```shell
sudo rm -r common_config
ln -s /mnt/_phplib/#libsIcom3/extension/ideo3/common_config/ "common_config"
```

## dans www/icom3/includes : 

<span class="remarque">remarque</span> : il faut changer nom lib en fonction lib à utiliser

```shell
sudo rm -r app.config.php
ln -s /mnt/_phplib/#libsIcom3/concretes/includes/app.config.php "app.config.php"
```
 

## dans public

<span class="remarque">remarque</span> : il faut changer nom lib en fonction lib à utiliser ainsi que ambiance

Veuillez remplacer l'ambiance

```shell
sudo rm -r admin
sudo ln -s /mnt/_phplib/#librairies3/admin/ "admin"

sudo rm AMBIANCE_FEE1AKUZN5_My-Store
sudo ln -s /var/www/ambiances/AMBIANCE_FOYEWDPXGR_bon-Sens-Immo/ "AMBIANCE_FOYEWDPXGR_bon-Sens-Immo"

sudo rm -r catalogues
ln -s /mnt/_phplib/#libsIcom3/extension/ideo3/public/catalogues/ "catalogues"

sudo rm -r errorHandler
sudo ln -s /mnt/_phplib/#librairies3/public/errorHandler/ "errorHandler"

sudo rm -r formulaire01
sudo ln -s /mnt/_phplib/#librairies3/public/formulaire01/ "formulaire01"

sudo rm -r integration
sudo ln -s /mnt/_phplib/#librairies3/public/integration/ "integration"

sudo rm -r planAcces01
sudo ln -s /mnt/_phplib/#librairies3/public/planAcces01/ "planAcces01"

sudo rm -r videoLinkeo01
sudo ln -s /mnt/_phplib/#librairies3/public/videoLinkeo01/ "videoLinkeo01"

sudo rm -r wcb01
sudo ln -s /mnt/_phplib/#librairies3/public/wcb01/ "wcb01"

```

## dans ambiance 

```shell

sudo ln -s /mnt/_cssframework/less/ "less"
sudo ln -s /mnt/_cssframework/js/ "js"
sudo ln -s /mnt/_cssframework/svg/ "svg"

```
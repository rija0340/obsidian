/## dans www
```shell
sudo ln -s /mnt/_phplib/#librairies3/common_config/ "common_config"
sudo ln -s config/ "includes"
```

## dans public

Veuillez remplacer l'ambiance

```shell
sudo rm -r admin
sudo ln -s /mnt/_phplib/#librairies3/admin/ "admin"

sudo rm AMBIANCE_FEE1AKUZN5_My-Store
sudo ln -s /var/www/ambiances/AMBIANCE_FBNWQMW54V_bambooBay-grid/ "AMBIANCE_FBNWQMW54V_bambooBay-grid/"

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

```$ cd ../

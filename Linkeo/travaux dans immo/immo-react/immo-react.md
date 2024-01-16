
<span class="remarque">Remarque</span> si tu veux travailler avec react et docker , utilise le format de ce dossier , Dockerfile , docker-compose.yml


commande docker pour lancer le projet 
build aussi
```shell
docker run -d -p 3000:3000 -v /app/node_modules -v $(pwd):/app --name react-app react-image
```

```shell
docker build -t react-image -f Dockerfile .
```

```bash
docker run -d -p 3000:3000 --name react-app react-image
```

template de listing produit dans :

```bash 
/home/rrakotoarinelina/programming/Linkeo/libraries/Immo/#librairies/concretes/admin/integrations/src/templates/listing_product
```

header du template 
```shell
/home/rrakotoarinelina/programming/Linkeo/libraries/Immo/#librairies/concretes/admin/header.phtml
```

chemin pour layout de base

```path
/home/rrakotoarinelina/programming/Linkeo/libraries/Immo/#librairies/concretes/admin/layout.phtml
```

après le menu contenant le menu catalogue, paramétré et langue , on a ce ces options 
c'est ce fichier qui contient la structure du page listing, du titre ( liste des produits )

une table contenant liste des produits avec tbody vide 

```shell
/home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769-immo/#librairies/concretes/modules/catalogues02/view/catalogue/list.phtml
```

les elements de la table est formé par 

```shell
/home/rrakotoarinelina/programming/Linkeo/libraries2/branches/dev4769-immo/#sources/www/public/catalogues/panel/css-js/templates/listing_product/listing_product.mst

```

## Explicaiton Dockerfile

- telechargement de node js en ligne si pas de cache
- definition d'un work dir dans l'image (docker est linux , c est comme un systeme exploi)
- copy du package.json dans workdir pour etre utilisé par npm install
- npm install des dependances dans package.json et les directive npm install


## explication de docker compose yml 


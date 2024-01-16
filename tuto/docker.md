commande pour démarrer docker utilisant un fichier yml 

	docker compose up -d

commande pour arrêter un container 

```powershell
docker compose down 
```

liste docker images 

```shell
docker images 
```   

liste containers docker en cours d'utilisation 

```shell
docker ps 
```

commande pour suppression

 * supprimer un container 
 ```shell
 docker rm id_container
```

 * supprimer une image (possiblité de forcer) 
 ```shell
 docker rmi id_container
```

run a container 

```bash
docker run -d -p 3000:3000 --name react_app_name react_image_name
```


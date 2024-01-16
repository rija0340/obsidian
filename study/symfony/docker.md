
- chemin dans dev_symfony/docker_backend
- suivre ce tuto pour
https://yoandev.co/un-environnement-de-d%C3%A9veloppement-symfony-5-avec-docker-et-docker-compose/

![[Pasted image 20231013155047.png]]

exécuter une commande dans un container pour installer un projet symfony 5


```
docker exec www_docker_symfony composer create-project symfony/skeleton:"5.4.*" project
```

le nom de projet docker project ici est le meme que dans vhost
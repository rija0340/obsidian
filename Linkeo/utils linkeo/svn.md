* voir les modification dans svn  : 
```shell
svn st 
```

* ajouter un fichier à SVN 

```svn 
svn add chemin_fichier
```
* voir les commit effectué depuis un dossier, c'est à dire qu'il est possible de ne pas voir des commits qui on été effectué depuis autre emplacement même pour un même projet 

```svn 
svn log -l 5 
```
N.B : "__-l 5__" veut dire ici qu'on veut seulement voir les 5 derniers 

* commande pour voir les fichiers concernés pas un commit 
```svn 
svn log  -v -r numero_revision_sans_r
```

parcourir les fichiers concernés par un commit et faire cette commande pour voir les modifications faites

```svn
svn diff nom_fichier
```

commiter plusieurs fichiers avec un message 

```svn 
svn ci -m "IDEO-6546 Passerelle auto-gestion" concretes/modules/cataloguesAuto/classes/ImportsAutogestion.class.php extension/ideo3/public/catalogues/api/import.php
```

regarder les modifications dans un fichiers (historique total d'un fichier)

```
svn log --diff nom_fichier
```

regarder les modificaitons dans un fichiers concernée par un commit specific 

```shell
svn diff -c <revision number> <filename>
```

revert command 

```bash
svn update
svn merge -r num_revision_actuel:num_revision_à_retourner .
svn commit -m "Rolled back to num_revision_à_retourner"
```
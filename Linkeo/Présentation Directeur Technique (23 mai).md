
passerelles Auto  : 

- http://jira.linkeo.com/browse/IDEO-6546
- http://jira.linkeo.com/browse/IDEO-6637

## amélioration auto
### admin 

http://jira.linkeo.com/browse/IDEO-6605 

```text
Créer un écran depuis le backoffice d'AUTO pour permettre de configurer le mode d'affichage des recherches AUTO. On n'aura qu'un seul écran pou la recherche haut, gauche et enregistrée

**RECHERCHE HAUT**

-   Permettre d'activer/désactiver la recherche par mot clé.

**RECHERCHE GAUCHE**

-   Mettre les configruration dans paramètres/général en bas de réseaux sociaux, créer un nouvel onglet nommé configuration recherches
-   Voici la liste des champs qui peuvent être affichées/cachées:
    -   recherche par mot clé

-   Voici la liste des champs dont le maximum peut-être configuré depuis le BO:
    -   kilometrage
    -   année
    -   prix
    
	-   Voici la liste des champs dont le minimum peut-être configuré depuis le BO:
    -   année
    -   prix

**RECHERCHE ENREGISTRÉE**

Permettre d'activer/désactiver la recherche enregistrée depuis le BO

Est-ce qu'il est possible d'ajouter/supprimer des champs a afficher dans la recherche depuis le BO?


```

### recherche haut 
http://jira.linkeo.com/browse/IDEO-6573

### recherche enregistrée

```text
remplacement des sliders dans recherche gache par des input pour que les champs utilisés dans recherche haut et gauche sont les memes
```

----------------------------------------------------------------------------------

## amélioration immo 

### admin 

http://jira.linkeo.com/browse/IDEO-6604

### recherche haut

http://jira.linkeo.com/browse/IDEO-6594
-   remplacement inputs pour prix du recherche haut par double slider mais difficile à avoir des petits intervalles comme
-   on a laissé les inputs pour recherche haut mais on a remplacé le slider prix du recherche gauche par des inputs.

http://jira.linkeo.com/browse/IDEO-6593
Actuellement, il est impossible de spécifier manuellement une ville pour la recherche haut IMMO car nous récupérons la liste des villes directement depuis la base de données, hors si l'utilisateur oriente sa recherche sur une ville qui n'est pas présente, il ne pourra pas poursuivre sa recherche.

http://jira.linkeo.com/browse/IDEO-6572
Actuellement, l'internaute ne peux pas insérer un code postal, il ne peut que choisir un code postal déjà existant dans la base de données. Cela limite grandement la recherche de l'internaute mais nuit aussi au fonctionnement de la recherche enregistrée.

http://jira.linkeo.com/browse/IDEO-6512

### recherche enregistrée
http://jira.linkeo.com/browse/IDEO-6567

### autre
http://jira.linkeo.com/browse/IDEO-6472


documentation pour recherche enregistrée

http://10.22.4.20/redmine/projects/icomx_php/wiki/Recherche_enregistr%C3%A9e_Auto


## Speech
bonjour, je m'appelle Rija, développeur PHP, je travaille moins d'un an maintenant
j'ai surtout travaillé sur l'amélioration de ui/ux (experience utilisateur ) pour les catalogues immo et auto 

### <span class="titre1">lib AUTO</span>

j'ai un peu améliorer des attributs de recherches, pour que le recherche haut et gauche soient plus cohérent. et surtout pour ne pas limiter les internautes aux données qui sont dans la base de données. En changeant des champs en champs libre

J'ai aussi travaillé avec Kursley et continué ce qu'il a commencé sur la recherche enregistrée.

On a ajouté un ecran dans le backoffice pour permettre au webmaster de personnaliser les champs à afficher sur la recherche haut et gauche et puis activer ou pas l'affichage de certains boutons.


#### recherches

pour ne pas limiter le client, po
ur etre plus cohérent

#### recherche enregistrée 

si le client a la possiblité d'entrer des données qui ne sont pas dans la base comme critères de recherche, il peut arriver qu'ils n'y pas de résultats donc à ce moment là, la recherche enregistrée peut être utile pour permettre d'enregistrée ces critères de recherche et être notifiés si après des produits correspondent à ces critères. 

la notification se fait par email et peut etre activé par des opérations dans la base de données ou bien par des nouveaux produits importés par une passerelle.

le client a la possibilité de desactiver les alertes (suppression critères de recherche)  ou de se desabonner (suppression compte )

#### configuration dans la backoffice 

pour Auto, on peut cacher des champs ou setter des valeurs par défaut pour certains champs. Si ces champs libre sont vides alors les données de la base de données seront affichées

<span class="titre1">lib IMMO </span>


#### recherche haut 

pour plus de liberté, on a changé ville en champ libre avec suggestion, le code postal en champ libre 
et on a supprimé la requete envoyer pour n'avoir que le nombre de produit a chaque changement de champ, ceci a été fait pour optimiser.


#### recheche enregistrée 

même fonctionnement que pour Auto, 

#### configuration B.O

même philosophie que pour Auto avec des champs différentes. 


## passerelle Auto 


<span class="remarque" >remarque</span>
remarque  : 

ajouter un ecran  : 
je travaille actuellement sur des whishlist , mais continue de faire devspe, passerelle ,

modifier interface utilisateur pour plus facile d'utilisation, ( fa tsy hoe j'ai juste remplacé )



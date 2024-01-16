---
date: 2022-10-04
url: http://jira.linkeo.com/browse/SPE-1759
---


site exemple : 

[https://www.fps-thermique.net/](https://www.fps-thermique.net/)
[https://www.morin-serge.com/](https://www.morin-serge.com/)

DID exemple  : 
10.99.0.23/_production3/m/morin-serge.com_ID303/www/public/

Formule à utiliser  : 

![[Pasted image 20231004142534.png]]

formules : 
D = Ubat  * surface * hauteur maison * Detla T
Ubat est en fonction de type de maison 
surface à renseigner
hauteur à renseigner
Delta T est toujour 29
unité de D  : Kw

Les etapes : 

Etape 1 : choix de type de maison (0.5j)
Etape 2 : renseignement de surface et hauteur (0.5j) 
Etape 3 : affichage de summary pour les étapes (0.5j)
si + envoi de mail -> (0.5j)
navigation system (0.5j)

Estimation total  : 2.5j

contenu mail  :  summary des choix et prix total 

On a besoin de plus de précision sur l'utilisation du formule dans l'exemple pour une maison de 150m2 de 1990, D = 0,9 * 150 * 2,5 * 29
- est-ce que G ici est égale à Ubat ? si oui pourquoi on n'a pas utilisé 0.95 ? sinon comment on a obtenu la valeur de G ?
- est-ce que 2.5 ici représente l'hauteur de la maison ?
- comment va t-on choisir le type de maison ?
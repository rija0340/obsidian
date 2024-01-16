---
date: 2023-11-03
intervenant: Luke
---

## Définition  : 
- methode de test 
- bout de code soratana hahafanana mitest fonction 
- écrit par dev en général 

## objectif 
- validation de fonctionnalité 

## principe 

- executer code application à tester 

## importance 
- faclite maintenance code 
- garantir qualité code 
- reduction bugs

rehefa manao anle CI/CD dia miasa io. 

regression  :  zavatra efa nandhea dia niverina tsy nandeha ndray 

N.B : samihafa ilay teste unitaire sy ny test fonctionnel 
@test unitaire dia ny fonction iray dia test unitaire iray 

# php unit 

## définition

- open source fanaovana test unitaire 
- référence fanaovana test emin'ny php 
- manana library utils
- permet l'implémentation des tests de régression 

## installation 
utilisation de composer require phpunit/phpunit 
## strucuture des test phpunit 

misy convention manokana atao amin'ny test uniatire anakiray 
(miankina amin)

les choses qui ne doivent pas figuré dans les tests : 
	- if, switch , boucle , for

## assertions :
ensemble de méthod omen le lib le izy 

## doublure de test : 

phpunit permet de crée des objets simulés pour  : 

- isoler les tests de certains dépendances
- tsy mila mampiasa dépendance eo anatinle test unitaire fa mila manao mock 
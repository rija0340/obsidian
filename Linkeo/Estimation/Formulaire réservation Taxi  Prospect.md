---
url: http://jira.linkeo.com/browse/SPE-1758
date: 2023-10-03
site exemple à reproduire: https://izeocab-vtc-lyon.com/booking/
url site exemple: https://www.acces-lyon-taxi.fr/reservation.php
url site ex did: http://10.99.0.23/_production3/a/autocarlyontransfert.com_ID301/www/public/reservation.php
---


Déscription dans le ticket devspe : 

Un prospect cherche a avoir un formulaire de réservation spécifique selon le site exemple : [https://izeocab-vtc-lyon.com/booking/![](http://jira.linkeo.com/images/icons/linkext7.gif)](https://izeocab-vtc-lyon.com/booking/)
Merci de voir ce qu'on avait deja fait pour un client ici : [http://jira.linkeo.com/browse/IDEO-5520![](http://jira.linkeo.com/images/icons/linkext7.gif)](http://jira.linkeo.com/browse/IDEO-5520)
On a besoin d'une estimation complete avec ce qu'on aura besoin du client en amont  
Merci

## demande du client  : 

Il faudrait pourvoir mettre 
- la date,
- l'heure,
- le lieu de prise en charge
- le lieu de dépose 
- la distance total
- le temps
- choix du véhicule.

## simulation sur site exemple  : 

dans le site exemple, on a un système qui permet à l'internaute de choisir les lieux à l'aide de google maps. 
Google maps va calculer automatiquement la distance et le temps entre ces deux lieux. 
REMARQUE :  ce service est payant 

la simulation ne marche pas sur le site exemple. 
message d'erreur  : 

```
BillingNotEnabledMapError
```

possible cause du problème : 

```url 
https://stackoverflow.com/questions/58268679/enable-billing-on-the-google-cloud-project
```

## documentatio sur API Maps JavaScript

https://developers.google.com/maps/documentation/javascript?hl=fr

ce service nous permet d'avoir le system de pick location et calcul de distance et time en fonction de location 

documentation sur pricing  : 
```url 
https://developers.google.com/maps/documentation/javascript/usage-and-billing?hl=fr#new-payg
```

## Liste des tâches :
- construction du formulaire ( copier ce qui a été fait dans le site exemple )
	- mise en place date et heure 
	- mise en place lieu de prise en charge (  complétion par google map  )
	- mise en place lien de dépose (compétions par google map )
	- auto calcul de distance et temps par google map api
	- choix de véhicule 
		- on ne sait pas encore si besoin d'être dans nouvelle page ou même pages (ux)
		- 



Remarque : 
- on ne peut pas demander au client de nous fournir mail/mdp et numéro carte 
- on a besoin d'activer les projets pour pouvoir les utiliser
- l'activation a besoin d'un numéro de carte visa de paiement même si on a un crédit offert par google pour un essai gratuit. Ceci est pour vérifier qu'on n'est pas un robot.

## inspiration fred 

- création du widget choix de lieu dynamique via google map (x jours)
- Implémentation formulaire

- etape 1
- etape 2
- etape 3
- etape 4

- enregistrement bdd d la résa dans la table des contacts
- envoi email après la validation (client + admin)
- paiement stripe enregistrer le paiement
## ## Rappel des éléments du développement

Requête : formulaire de réservation de voiture VTC
site exemple Linkeo (ce qu'on a déjà fait similaire à la demande)   :  autocarlyontransfert.com/reservation.php
site exemple client  : https://izeocab-vtc-lyon.com/booking/
## demande du client  : 

Il faudrait pourvoir mettre 
- la date,
- l'heure,
- le lieu de prise en charge
- le lieu de dépose 
- la distance total
- le temps
- choix du véhicule.

## résumé fonctionnement

![[Pasted image 20231004105753.png]]
# Lés étapes dans le formulaire
### Etape 1 :
- intégration de formulaire date et heure (0.5j)
- intégration de choix de lieu de prise en charge et lieu de dépose (intégration api google maps ) (2j)
	- on va suivre l'exemple sur le site exemple du client mais pas celui de Linkeo -> seulement champs avec autocomplétion par google 
- intégration de calcul de distance et de temps (intégration api google maps) (2j)
## Etape 2 : 
- intégration d'une fenêtre de choix de véhicule (on ne sait pas encore si choix de véhicule impact le prix ) (1.5j -> affichage liste  simple )
remarque  :  estimation peut changer en fonction demande client  pour le style d'affichage des véhicules 
## Etape 3 : 
- intégration de summary du booking et formulaire de contact  (1j) (si affichage information simple)
- intégration de paiement par stripe (1j) ( redirection vers page stripe )
## navigation 
- gestion de navigation (1j)
## Lors du submit et réponse 
- envoi du mail au client et au internaute (1.5j)
	- envoi de mail seulement si le paiement stripe accepté 
- traitement retour stripe et enregistrement dans bdd (1.5j)
- rediriger le client vers une page de remerciement
## contenu  mail  : 
- référence paiement et montant 
- résumé résérvation, 
- pas de pièce jointe 
- même contenu mail pour client et internaute 
## Estimation : 
12 jours
## Nb :
- Le client doit avoir un compte Google Maps et nous fournir la clé API.
- Le client doit nous fournir tous les tarifs et les formules de calcul qui seront intégrées.
- Le client devra avoir un compte Stripe et nous en fournir les accès durant l'étape de développement.
- Le formulaire ne prend pas en compte la gestion de la disponibilité du parc véhicule
- La partie styling avancée de l'intérface, si nécessaire, seront fait par les webs
- Si le client veut voir les réservations -> dans onglets messages et mail 
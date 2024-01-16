---
date: 2022-12-11
code bouton: IDP00034738100
url: http://10.99.0.23/_production3/a/aix-treme-cross.com_ID303/www/public/
---

lien de documentation  : 
https://developer.paypal.com/docs/checkout/standard/upgrade-integration/


Après étude du site, j'ai vu que l'intégration des payements se font par ce moyen 
https://developer.paypal.com/api/nvp-soap/paypal-payments-standard/integration-guide/formbasics/

```html
<FORM action="https://www.paypal.com/cgi-bin/webscr" method="post">
```

url de redirection pour le mise à jour dans le mail 

```url 
https://developer.paypal.com/docs/checkout/standard/upgrade-integration/?utm_source=paypal&utm_medium=email&utm&_ga=2.84532058.293171511.1702283647-2080590797.1702282104
```

compte sandbox  : 

```
paaaaypaaaal-seller@hotmail.com/ paaaaypaaaal-seller  
paaaaypaaaal-buyer@hotmail.com / paaaaypaaaal-buyer
```

credentials for seller : ( picekd from the sandbox site )
https://www.sandbox.paypal.com/commercesetup/APICredentials
```
client id : AYZKooUoJoDSlyCd0sBCbLdKrbIQxwoDq94BjOfYNQAjx6bxBScMEoexai6o7xxf6lAXCd7GRadf9B3w
client secret : EHfkQ-rSJ_IHoZz1QKQnk2uaUdfC5dWmdkLyx3SYOVpHUY8SkSG-mj3vJiMGGd_QZe17Aij_TzrnDpTn
```
## comporehension du code front  :

```html
<!DOCTYPE html>
<html>
   <head>
      <meta name="viewport" content="width=device-width, initial-scale=1">
   </head>
   <body>
      <!-- Replace "test" with your own sandbox Business account app client ID -->
      <script src="https://www.paypal.com/sdk/js?client-id=test&currency=USD"></script>
      <!-- Set up a container element for the button -->
      <div id="paypal-button-container"></div>
      <script>
         paypal.Buttons({
           createOrder() {
             return fetch("/my-server/create-paypal-order", {
               method: "POST",
               headers: {
                 "Content-Type": "application/json",
               },
               body: JSON.stringify({
                 cart: [
                   {
                     sku: "YOUR_PRODUCT_STOCK_KEEPING_UNIT",
                     quantity: "YOUR_PRODUCT_QUANTITY",
                   },
                 ]
               })
             })
             .then((response) => response.json())
             .then((order) => order.id);
           }
         }).render('#paypal-button-container');
      </script>
   </body>
</html>
```


The code you provided sets up a simple PayPal button and utilizes the PayPal JavaScript SDK to create an order when the button is clicked. Let's break down how this works:

1. **Include PayPal SDK:**
    - The script tag includes the PayPal JavaScript SDK, specifying the client ID and currency.
```html
<script src="https://www.paypal.com/sdk/js?client-id=test&currency=USD"></script>
```

2. **Button Container:**
- The `<div>` element with the ID `paypal-button-container` serves as the container for the PayPal button.
<div id="paypal-button-container"></div>
<div id="paypal-button-container"></div>
<div id="paypal-button-container"></div>
<div id="paypal-button-container"></div>
<div id="paypal-button-container"></div>

```html
<div id="paypal-button-container"></div>
```
**Button Initialization:**

- The `paypal.Buttons()` function is called to initialize the PayPal button. It has a `createOrder` function that makes a `fetch` request to `/my-server/create-paypal-order` when the button is clicked.

```js
paypal.Buttons({
  createOrder() {
    return fetch("/my-server/create-paypal-order", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        cart: [
          {
            sku: "YOUR_PRODUCT_STOCK_KEEPING_UNIT",
            quantity: "YOUR_PRODUCT_QUANTITY",
          },
        ],
      }),
    })
    .then((response) => response.json())
    .then((order) => order.id);
  },
}).render('#paypal-button-container');

```

## comprehension  : 

-  creation order  : au click du bouton, on va créer un order, on passe envoi en post la liste des items à acheter, 
il faut les mettre dans purchase_units dans la fonction createOrder coté serveur
	- un fenetra apparai demandant au byuer de se logger et de confirmer le paiement 
- Capture payment when approved : on passe maintenant à la fonction onApprove (dans le front) lorsque le byer a approuvé le paiement 
- appel ajax dans la fonction approuve et finalisation du paiement

## Travaux à faire pour mise en prod de mise à jour paypal 
- rehefa azo ireo client_id sy client_secret avy amin'ny client dia 
	- mandeha ao amin'ny filesystem > public > api > global.php dia soloina anle prod le valeur ao 
	- soloina prod ian koa ilay url sandbox ao (endpoint prod : `https://api-m.paypal.com`)
- miditra ao amle page dupliqué (Tarifs / Horaires / Dates(1)) dia alaina atao copie collé contenu an'ireo item ao (7 items ) dia ecrasena ireo ao amin'ilay page tena izy.(Tarifs / Horaires / Dates(1))
- test en prod tsy haiko na azo atao
- ao amin'y page (Tarifs / Horaires / Dates(1)) misy js front anle payement paypal
- ao amin'ny filesystem > public > api misy ireo code server 
- ao amin'ny global misy anle script sdkjavascript
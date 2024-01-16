## Travaux à faire pour mise en prod de mise à jour paypal 
- rehefa azo ireo client_id sy client_secret avy amin'ny client dia 
	- mandeha ao amin'ny filesystem > public > api > global.php dia soloina anle prod le valeur ao 
	- soloina prod ian koa ilay url sandbox ao (endpoint prod : `https://api-m.paypal.com`)
- miditra ao amle page dupliqué (Tarifs / Horaires / Dates(1)) dia alaina atao copie collé contenu an'ireo item ao (7 items ) dia ecrasena ireo ao amin'ilay page tena izy.(Tarifs / Horaires / Dates(1))
- test en prod tsy haiko na azo atao
- ao amin'y page (Tarifs / Horaires / Dates(1)) misy js front anle payement paypal
- ao amin'ny filesystem > public > api misy ireo code server 
- ao amin'ny global misy anle script sdkjavascript
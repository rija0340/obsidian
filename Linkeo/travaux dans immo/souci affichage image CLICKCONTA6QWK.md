---
tags  : immo_work
url : http://jira.linkeo.com/browse/IDEO-6676
date : 2023-03-17

---

#conseil #toromarika #methode #debugage

jerena avy any ambony, 
* miditra avy aizay ny donnée (BO ? Passerelle)
* aiza no manomboka tsy mety 
* inona no tsy mapety azy 

lien passerelle en ligne  : 

```link

://www.agence-alexandre.com/catalogues/api/import.php?key=19a0185faf1031fd7f863420fbf6d14fc2eb6ccd&file-product=ubiflow&host=ftp-immo.linkeo.com&user=CLICKCONTA6QWK&pwd=tM4vL2sC8vA6dR6e
```

lien passerelle local  : 

```link

http://localhost/immo/agence_alexandre/public/catalogues/api/import.php?key=19a0185faf1031fd7f863420fbf6d14fc2eb6ccd&file-product=ubiflow&host=ftp-immo.linkeo.com&user=CLICKCONTA6QWK&pwd=tM4vL2sC8vA6dR6e

```

<span class="remarque">Solution</span> : remplacement de file_get_content par un cron car la fonction marche localement mais pas en ligne, on n'a pas pu avoir les photos que par cron.
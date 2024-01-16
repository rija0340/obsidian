---
tags : ideo3_work, CLICKCONTA61ZE
url : http://jira.linkeo.com/browse/IDEO-6689
date : 2023-03-31
---


```html
<div class="formDevisContainer block-button small align-left text-left block-text blk-text">
   <form class="formDevis">
      <p>
      <div style="width:100%">
         <span style="width:50%">Chaise blanche en résine + housse Bouton<br/><strong><em>4 € TTC L'unité</em></strong></span><span style="width:50%" class="qty"><label>Quantité</label><input name="16010|Chaise blanche en résine + housse Bouton|4" value="" type="text" class="quantite" style="width:50px;"></span>
      </div>
      <div style="width:100%">
         <span style="width:50%">Chaise blanche en résine + housse Alliance<br/><strong><em>4 € TTC L'unité</em></strong></span><span style="width:50%" class="qty"><label>Quantité</label><input name="16011|Chaise blanche en résine + housse Alliance|4" value="" type="text" class="quantite" style="width:50px;"></span>
      </div>
      <div style="width:100%">
         <span style="width:50%">Chaise blanche en résine + housse Noeud<br/><strong><em>4 € TTC L'unité</em></strong></span><span style="width:50%" class="qty"><label>Quantité</label><input name="16012|Chaise blanche en résine + housse Noeud|4" value="" type="text" class="quantite" style="width:50px;"></span>
      </div>
      </p><a class="button buttonDevis"><span class="txt">Ajouter au devis</span>
      </a>
   </form>
</div>
```

<span class="remarque" >mail du owner site : locvaisselle19@gmail.com</span>


* test fait dans rawvalidation.php (commenter envoi donnée vers logiciel client);


mande admin, le ray tsy mandeha ndray 


information alefa 

num ticket :http://jira.linkeo.com/browse/IDEO-6689
test natao  :

mail internaute : rija.rakotoarinelina@linkeo.com
mail admin: rija.rakotoarinelina@linkeo.com
resultat  : reception des deux mails mais dans indésirables (plusieurs test)

après changement de mail 
mail internaute  : gmail 
mail admin  : linkeo
resultat  : mail bien recu par deux boite mail et pas dans span 

après changement de mail 
mail internaute  : gmail 
mail admin  : gmail
resultat : client recoit mail dans boite reception, admin recoit mail dans spam

mail internaute : linkeo
mail admin : gmail
resultat : internaute recoit mail dans spam, admin recoit mail dans spam


test à faire dans DID :  commenter code dans /var/www/imbuilder/_production3/l/locvaisselle19.com_ID301/www/Customize/Service/rawvalidation.php pour ne pas envoyer à logiciel du client

remplace mail destinatair dans page demander devis et dans le formulaire


test ce 20-04-2023

CLICKCONTA61ZE
url : http://jira.linkeo.com/browse/IDEO-6689

mail admin : linkeo -> reception dans spam 
mail internaute  : gmail -> recu dans boite de reception 

mail admin : gmail -> reception dans spam 
mail internaute  : linkeo -> reception dans boite de reception 

mail admin : linkeo -> reception dans spam
main internaute  : linkeo ->reception dans boite reception

mail admin : linkeo -> reception dans spam 
main internaute  : linkeo ->reception dans boite reception

mail admin : gmail -> reception dans spam
main internaute  : yahoo ->reception dans boite reception
 
mail admin : yahoo ->  reception dans spam
main internaute  : yahoo -> reception dans spam

mail admin : gmail ->  reception dans spam
main internaute  : yahoo -> reception dans spam 

mail admin : linkeo -> reception dans spam 
main internaute  : yahoo -> reception dans spam

mail admin : gmail -> reception dans spam 
main internaute  : gmail -> reception dans spam

mail admin : yahoo -> reception dans boite reception
main internaute  : yahoo -> reception dans spam

mail admin : gmail -> reception dans spam 
main internaute  : gmail -> reception dans spam

## test 26-04-2023

admin  : linkeo -> recu dans boite reception (6:45)
internaute  : gmail -> pas encore recu 

admin : gmail -> boite reception (6:51)
internaute :  linkeo -> boite reception  (6:51)

admin : linkeo -> boite de reception (6:57)
internaute  : gmail -> boite de reception (6:57)

admin : linkeo -> boite de reception (6:59)
internaute  : yahoo -> boite de reception (6:59)

admin  : linkeo -> boite de reception (7:03)
internaute  : linkeo >  boite de reception (7:03)

admin : gmail -> boite de reception (07:08)
internaute : gmail -> boite de reception(07:08)

admin : yahoo -> boite de reception (7:13)
internaute  : gmail -> boite de reception (7:12)

admin : yahoo -> boite de reception (07:17)
internaute : yahoo -> boite de reception (07:17)
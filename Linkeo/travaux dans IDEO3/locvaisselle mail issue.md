---
date: 2023-11-29
url: http://jira.linkeo.com/browse/IDEO-6823
url site exemple: https://www.loc-vaisselle19.com/
shorcode: CLICKCONTA61ZE
---

mail  : location19@laposte.net

<h1 class="remarque" > N'oublie pas de changer mail dans le backoffice  </h1>

## test sur DID 

test dans page nous contacter.php ( deux mail utilisés : [[contact_email]] , location19@laposte.net )

- mail internaute : rakotoarinelinarija@gmail.com  -  no recu 
- mail admin : rija.rakotoarinelina@linkeo.com - recu dans span (avec latence ) 


test dans demander-devis.php

- mail internaute : rakotoarinelinarija@gmail.com - non recu 
- mail admin : rija.rakotoarinelina@linkeo.com - non recu 


- mail internaute :  rija.rakotoarinelina@linkeol.com - non recu 
- mail admin : rakotoarinelinarija@gmail.com - non recu 


- mail internaute : mail linkeo   - recu inbox 
- mail admin  : mail linkeo - recu span 

- main internaute : linkeo@sharklasers.com -recu  (https://www.guerrillamail.com/inbox)
- mail admin  : rija.rakotoarinelina@linkeo.com - non recu 

- mail interaue  : linkeo - recu 
- mail admin  : https://www.guerrillamail.com/inbox - recu
- mail admin 2 : linkeo  - recu dans span 

## test sur HID 


test sur page demander un devis 

- mail internaute : gmail -  recu 
- main admin  : linkeo - recu 

- mail internaute : linkeo - recu 
- mail admin  : gmail  - recu

- mail internaute  : gmail - recu 
- mail admin : linkeo - recu 
- mail admin2 : https://www.guerrillamail.com/inbox - recu 

- mail internaute  : ce8a3b65681e42@crankymonkey.info (https://internxt.com/temporary-email) -  recu 
- mail admin : xaseses748@cumzle.com (https://temp-mail.org/) - recu 
- mail admin2 : linkeo@guerillamail.net - recu 


test sur page nous contacter 

- mail admin : linkeo - recu 
- mail admin  : gmail - recu 
- mail admin : https://www.guerrillamail.com/inbox - recu 


linkeo@guerillamail.net
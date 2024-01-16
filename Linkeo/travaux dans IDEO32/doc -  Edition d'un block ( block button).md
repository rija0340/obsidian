## options d'un block (exemple block button)
Lors d'une edition d'un block button, en clickant sur le bouton edit (icon crayon) du block comme sur l'image 
![[Pasted image 20231110101428.png]]
on a des options qui apparaissent dans le rightpanel , pour le block bouton et bien d'autres blocks, on a trois sortes d'options   :
- bouton
- style
- avancé

![[Pasted image 20231110101756.png]]

Les modèles, views et template de ces options se trouvent dans le dossier:
#librairies/public/integration/src/js/JEditor/PagePanel/Contents/Blocks/ButtonBlock/



![[Pasted image 20231110102131.png]]

## rendu du block sur le pageview
pageview est  ceci  : 
ici on affiche la partie contenu de la page dans la pageview

![[Pasted image 20231110102816.png]]
le template qu'on utilise pour le rendu du block dans le pageview est le fichier buttonBlock.html.

## mise à jour de l'affichage block button dans pageview 

si on regarde dans le fichier  : buttonBlockvView.js, on a ces deur render function  : 

- render 
- renderOptions


### render()

cette fonction est responsable de render la le block button au moment ou l'on charge ce block dans la pageview.
En résumé  : ceci donne à la page html les attributs du modèle.

### renderOptions()
Ceci a pour fonction de rendre les modifications sur l’aperçu du bouton dans la pageview au moment de la modification sur les styles du boutons dans le rightpanel. Donc par cette fonction on peut avoir une aperçu en tant réel de la modification voulu. 
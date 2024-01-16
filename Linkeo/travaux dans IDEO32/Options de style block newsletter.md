---
date: 2023-10-13
url: https://trello.com/c/cyM3QbjD/371-options-de-style-block-newsletter
---
Il faut remarquer qu'il y d'autres types de blocks qui utilisent ces options : 
- row (sections)
- colonnes
- block texte
- block formulaire

On a examiné attentivement comment l'option a été implémenté pour block texte et formulaire et refait le même logique pour newsletter 

les fichiers impacté  : 
```
public/integration/src/js/JEditor/PagePanel/Contents/Blocks/NewsletterBlock/Views/NewsletterBlockView.js
public/integration/src/js/JEditor/PagePanel/Contents/Blocks/NewsletterBlock/NewsletterBlock.js
```
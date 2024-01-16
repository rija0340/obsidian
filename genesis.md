# Override formulaire AUTO

On reprend les mêmes principe pour overrider un formulaire en IDEO3 car Auto utilise module formulaire01 d'IDEO3.

Il faut commencer par vérifier dans le filesystem si on enregistre déjà un namespace 'Customize' dans l'un des deux fichiers  :

 * dans le dossier www/ModuleLoader.class.php 
 * ou dans www/icom3/ModuleLoader.class.php. 


Cette enregistrement se fait par l'ajout de cette ligne de code dans la function registerModulesByNamespace()

~~$loader->registerNamespace('Customize', realpath(__DIR__.'/Customize/'));~~

Si durant la vérification cette ligne est déjà présente dans l'un des fichiers mentionnés précédemment, il faut placer le dossier contenant les fichiers pour override dans le dossier Customize, le dossier Customize même niveau que le fichier contenant la ligne de code d'enregistrement.

Bien assurer que les namespaces dans les fichiers d'override sont correctes

Le premier site Auto dont un formulaire a été overridé est  : GARAGE DAVID BETTON SAS | CLICKCONTA6NVX
url du site  : http://validation.garage-betton.fr/conversion-lethanol.php


```html
<form method="POST">
  <label>
    <input type="checkbox" name="naturels">
    100% Naturels
  </label><br>

  <label>
    <input type="checkbox" name="fer">
    Un fer à lisser tous les matins
  </label><br>

  <label>
    <input type="checkbox" name="assouplissement">
    Juste un assouplissement
  </label><br>

  <label>
    <input type="checkbox" name="defrise">
    Défrisé
  </label><br>

  <label>
    <input type="checkbox" name="loks">
    Loks
  </label><br>

  <label>
    <input type="checkbox" name="no-cheveux">
    Je n'ai pas de cheveux
  </label><br>

  <button type="submit">Submit</button>
</form>

```
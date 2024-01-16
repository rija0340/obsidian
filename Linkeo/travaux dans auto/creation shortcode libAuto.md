---
date : 2023-07-27
---

liste des choses à faire  : 

- création de handler et renderer  (extension/ideo3/module/CataloguesAuto/Service)
- création de view (extension/ideo3/module/CataloguesAuto/view)
- décraltion du nouveau shortcode dans (extension/ideo3/module/CataloguesAuto/config/module.config.php)
- déclaration des sevice ici extension/ideo3/module/CataloguesAuto/Module.php
- dans handler  : retourn le service return '<?php echo $serviceManager -> get(\'recherchepieces.render\') -> render() ; ?>';
- ajouter methode pour remplace le php echo dans ce fichier (extension/ideo3/vendor/CoreMoteurDeRendu/src/CoreMoteurDeRendu/Service/PageContentFormatterService.php)
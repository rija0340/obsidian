
---
tags : ideo3_work, CLICKCONTA6KJ5
url : http://jira.linkeo.com/browse/IDEO-6645
date : 2023-02-17
---
* exportation de la base de données dans did après sync down 
* exécution requête dans la base locale pour récupérer les images qu'on besoins
* exportation résultats en csv
* utilisation de ce csv et les images dans public/ressoureces/images du filesyteme avec un petit programme en php pour copier les images voulu dans un autre dossier 

[[sites local#php (testCode)]]

```sql
SELECT id, mimeType, fileUrl 
FROM `ID302_resources` 
WHERE mimeType IN ('image/png', 'image/jpeg') 
  AND createdAt < '2021-01-01' 
  AND (modifiedAt IS NULL OR modifiedAt < '2021-01-01')
ORDER BY `ID302_resources`.`modifiedAt` DESC

```
![[CLICKCONTA6KJ5(1).sql]]
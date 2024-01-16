
---
tags : ideo3_work, CLICKCONTA6KJ5
url : http://jira.linkeo.com/browse/IDEO-6654
date : 2023-02-24
---
opération précédente  : [[recuperation images CLICKCONTA6KJ5]]

suppression des images avant 2021

```sql

DELETE FROM `ID302_resources` 
WHERE mimeType IN ('image/png', 'image/jpeg') 
  AND createdAt < '2021-01-01' 
  AND (modifiedAt IS NULL OR modifiedAt < '2021-01-01')

```

images restant uploadé sur DID, reste à supprimer dans base (simuleo anato local aloh ), et suncy up peut etre ( à confirmer)

liste image sur le site  :
ff5dabdef4ad.png - logo

### structure page 
zone > section > column > block


### link builder 

http://10.99.0.21/index.php?noApproxFilter_typeProduit=Site&approxFilter_codeBouton=CLICKCONTA6KJ5&approxFilter_initiatedBy=&approxFilter_ndd=&noApproxFilter_siteType_nom=Type+de+site&noApproxFilter_prodcore_nom=Maurice&action=listing&approxFilter_searchYear=Toutes+les+ann%C3%A9es&approxFilter_searchMonth=Tous+les+mois&noApproxFilter_ambiance=Tous

![[ID302_block 1.sql]]

creation d'un petit programme qui check les images selon un query 
et output un csv contenant  : 
* liste des images dans ressources 
* liste des images respectant le query (ici avant 2021)
* liste des images non utilisées 

on a dans un dossier toutes les images du site 
puis on a un csv content listes images qui doivent être sur le site ,"images_copier_DID" : 

<span class="text-danger">important : </span> on a utilisé liste comparaison dans base  + recupére depuis css (dans backoffice ->template.less) 


https://www.ecole-pauletvirginie.com/eleve-unique-accompagne-parcours-reussite.php
ces images ne sont ni dans block ni dans css

/ressources/images/b665aac1eb94.jpg

/ressources/images/e628211a1595.jpg

/ressources/images/3fad4079eef5.jpg


INSERT INTO `ID302_resources` (`id`, `title`, `desc`, `fileUrl`, `mimeType`, `ext`, `thumb`, `name`, `createdAt`, `modifiedAt`, `orginalFile`, `useCount`, `parentCollection`, `order`) VALUES
(961, '[]', '{"options":{"desc":[],"focus":{"x":null,"y":null}}}', '/ressources/images/b665aac1eb94.jpg', 'image/jpeg', 'jpg', 'thumb/thumb_b665aac1eb94.jpg', 'b665aac1eb94.jpg', '2020-12-11 07:29:00', '2020-12-11 07:29:00', 'image 2 final', NULL, NULL, NULL);


INSERT INTO `ID302_resources` (`id`, `title`, `desc`, `fileUrl`, `mimeType`, `ext`, `thumb`, `name`, `createdAt`, `modifiedAt`, `orginalFile`, `useCount`, `parentCollection`, `order`) VALUES
(959, '[]', '{"options":{"desc":[],"focus":{"x":null,"y":null}}}', '/ressources/images/e628211a1595.jpg', 'image/jpeg', 'jpg', 'thumb/thumb_e628211a1595.jpg', 'e628211a1595.jpg', '2020-12-11 07:29:00', '2020-12-11 07:29:00', 'image 1 final', NULL, NULL, NULL);


INSERT INTO `ID302_resources` (`id`, `title`, `desc`, `fileUrl`, `mimeType`, `ext`, `thumb`, `name`, `createdAt`, `modifiedAt`, `orginalFile`, `useCount`, `parentCollection`, `order`) VALUES
(960, '[]', '{"options":{"desc":[],"focus":{"x":null,"y":null}}}', '/ressources/images/3fad4079eef5.jpg', 'image/jpeg', 'jpg', 'thumb/thumb_3fad4079eef5.jpg', '3fad4079eef5.jpg', '2020-12-11 07:29:00', '2020-12-11 07:29:00', 'image 3 final', NULL, NULL, NULL);

### requete suppresion images

requête pour effacer les images non utilisé dans la base de données  : 

```sql

DELETE FROM `ID302_resources` WHERE fileUrl IN (

'/ressources/images/e7e29e87d7ce.jpg',

'/ressources/images/7bb0d5728f2d.jpeg',

'/ressources/images/8d07168109a0.jpg',

'/ressources/images/b5e21e280933.jpeg',

'/ressources/images/501180e0bbb8.jpg',

'/ressources/images/551fcf11940f.jpeg',

'/ressources/images/88894dede505.jpg',

'/ressources/images/4761ce64f6b1.jpg',

'/ressources/images/867ed53b3678.jpg',

'/ressources/images/fb33671288f6.jpg',

'/ressources/images/dcd4b37294fe.jpg',

'/ressources/images/4d5dc05094f3.jpg',

'/ressources/images/ac77e813977d.jpg',

'/ressources/images/7a89c7ef58b6.jpeg',

'/ressources/images/1d96839af1b8.jpeg',

'/ressources/images/c6d92bea9ef5.jpeg',

'/ressources/images/644469401783.jpg',

'/ressources/images/64bc39c42077.jpg',

'/ressources/images/db32017d0d79.jpg',

'/ressources/images/6f9d95283c84.jpg',

'/ressources/images/1d7c0e8c4bf0.jpeg',

'/ressources/images/78c92987cbf5.jpg',

'/ressources/images/bdc23dcbb671.JPG',

'/ressources/images/0cef94a045df.jpg',

'/ressources/images/bf80683e1097.jpg',

'/ressources/images/c54bb9186e25.jpg',

'/ressources/images/6dcf44d425f9.jpg',

'/ressources/images/536185b615fc.jpg',

'/ressources/images/f0c9d3bdebf7.jpg',

'/ressources/images/35faafb56ac3.jpg',

'/ressources/images/1831aa5c0d74.jpg',

'/ressources/images/36a8cac67adf.jpg',

'/ressources/images/3a81a15ad6dd.jpg',

'/ressources/images/912429be0980.jpg',

'/ressources/images/426a046b6aa0.jpg',

'/ressources/images/be529f47c62f.jpg',

'/ressources/images/9cfa4d1afc22.jpg',

'/ressources/images/528cbe0ac423.jpg',

'/ressources/images/6174e44e1478.jpg',

'/ressources/images/a9d3109281ef.jpg',

'/ressources/images/65ec39944950.jpg',

'/ressources/images/03bfd3dc742e.jpg',

'/ressources/images/5da49543cada.jpg',

'/ressources/images/92cbab7828dd.jpg',

'/ressources/images/774227f79466.jpg',

'/ressources/images/23b1981b56e8.jpg',

'/ressources/images/c799b8740d9a.jpg',

'/ressources/images/847d69c370f9.jpg',

'/ressources/images/e9088e530825.jpg',

'/ressources/images/41057618bb2b.jpg',

'/ressources/images/b3a459897b44.jpg',

'/ressources/images/ffb14ca27c61.jpg',

'/ressources/images/15ad2e725a0f.jpg',

'/ressources/images/e4b325db2cdf.jpg',

'/ressources/images/a0f3b86212f8.jpg',

'/ressources/images/9daa86a6f779.jpg',

'/ressources/images/bad2ec7b7a72.jpg',

'/ressources/images/f47049cb4f93.jpg',

'/ressources/images/064bcc265841.jpg',

'/ressources/images/1084d045aa5d.jpg',

'/ressources/images/b2d3e6341e40.jpg',

'/ressources/images/9a23b8fa1c11.jpg',

'/ressources/images/e52a1beb18fb.jpg',

'/ressources/images/cde932afaa94.jpg',

'/ressources/images/643f0f4ec541.jpg',

'/ressources/images/591fa172fa49.jpg',

'/ressources/images/0f9d0dd4d715.jpg',

'/ressources/images/e83a6e008a51.jpg',

'/ressources/images/3fea2d5f08f5.jpg',

'/ressources/images/8bad17eaed90.jpg',

'/ressources/images/7d853206c2c6.jpg',

'/ressources/images/54f4a99493ee.jpg',

'/ressources/images/fdaa58ca8fd7.jpg',

'/ressources/images/5ac5e5bdda50.jpg',

'/ressources/images/4fb08bb44528.jpg',

'/ressources/images/d712192f1d65.jpg',

'/ressources/images/49d156e1d7e7.JPG',

'/ressources/images/879d5a4eb1bf.JPG',

'/ressources/images/8aecf1e3d583.JPG',

'/ressources/images/e178dfad26fd.JPG',

'/ressources/images/1966053a8fbd.JPG',

'/ressources/images/29388fc46d89.jpg',

'/ressources/images/f812e9e810d9.JPG',

'/ressources/images/e52611eeff92.jpg',

'/ressources/images/2d4b374120dc.jpg',

'/ressources/images/2efb8e73fb18.jpg',

'/ressources/images/ee50a73e4e15.jpg',

'/ressources/images/f34020f8c225.JPG',

'/ressources/images/6a2014cea78d.JPG',

'/ressources/images/3e35004096fe.jpg',

'/ressources/images/c3d089bff38e.jpg',

'/ressources/images/ac1ae2512028.jpg',

'/ressources/images/52806fc30bdd.jpg',

'/ressources/images/bdaabafcab7d.jpg',

'/ressources/images/1ad8ff29c54c.jpg',

'/ressources/images/a588eff7d8e6.jpg',

'/ressources/images/80bc016da7e4.jpg',

'/ressources/images/5d257e1545d2.jpg',

'/ressources/images/812db2fab2d9.jpg',

'/ressources/images/c0fb3b8a6e91.jpg',

'/ressources/images/9dd51d863107.JPG',

'/ressources/images/a50fb64530fc.JPG',

'/ressources/images/7e52c85f1ca1.JPG',

'/ressources/images/d8514b4c6497.JPG',

'/ressources/images/00a082e784f6.JPG',

'/ressources/images/1d1fde5bf2bc.JPG',

'/ressources/images/7b27f9b23b61.JPG',

'/ressources/images/26f19a04441a.JPG',

'/ressources/images/d7ed89e1e568.JPG',

'/ressources/images/168093918843.JPG',

'/ressources/images/0a2e7feca962.JPG',

'/ressources/images/52a8e98bda77.JPG',

'/ressources/images/94f47fc2486e.JPG',

'/ressources/images/8c1b81698a4d.JPG',

'/ressources/images/cada3bb0c690.JPG',

'/ressources/images/d391124d1606.JPG',

'/ressources/images/7fb6be165a6d.JPG',

'/ressources/images/675dfa44b962.JPG',

'/ressources/images/b752fc1cb74f.JPG',

'/ressources/images/f5af1105f604.JPG',

'/ressources/images/42ae1c991624.JPG',

'/ressources/images/8dd78e950a4b.JPG',

'/ressources/images/8c99dbfb0096.JPG',

'/ressources/images/a2d96ab8b734.JPG',

'/ressources/images/fc55ca959e29.JPG',

'/ressources/images/33e99df3742d.JPG',

'/ressources/images/c624b35d9e62.JPG',

'/ressources/images/1a1fc4655a18.JPG',

'/ressources/images/063b3693bf90.JPG',

'/ressources/images/3ad0b4ad125e.JPG',

'/ressources/images/fafed374e4b4.JPG',

'/ressources/images/8d83c7cb4851.JPG',

'/ressources/images/eda4d9e0e7ee.JPG',

'/ressources/images/6ecb725b4b81.JPG',

'/ressources/images/57f72af68e71.JPG',

'/ressources/images/3ed02052e2af.JPG',

'/ressources/images/68d944fdc759.JPG',

'/ressources/images/096bb146832b.JPG',

'/ressources/images/37a96f76214f.JPG',

'/ressources/images/b52947afd31b.JPG',

'/ressources/images/41e5982b4b21.JPG',

'/ressources/images/bd8e6fde94ce.JPG',

'/ressources/images/25faff9059c1.JPG',

'/ressources/images/732f854e29b3.JPG',

'/ressources/images/7e3f04b570c4.JPG',

'/ressources/images/134c6b17c153.JPG',

'/ressources/images/409375cd6a00.JPG',

'/ressources/images/edb8a48009d4.JPG',

'/ressources/images/39ada892e336.JPG',

'/ressources/images/bb58f0e5994a.JPG',

'/ressources/images/3ffd02a689b0.JPG',

'/ressources/images/74792606b0f1.JPG',

'/ressources/images/d1581865bf36.JPG',

'/ressources/images/c068495fbbf8.JPG',

'/ressources/images/553ed0b05d6f.JPG',

'/ressources/images/cc245e9151e6.JPG',

'/ressources/images/fcc12e0e19d5.JPG',

'/ressources/images/6344bd26dd68.JPG',

'/ressources/images/d2c1692840f3.JPG',

'/ressources/images/d614c90f9ff8.JPG',

'/ressources/images/1eb67ad59e48.JPG',

'/ressources/images/a6b4acfafba5.JPG',

'/ressources/images/6ab11ea04bbc.JPG',

'/ressources/images/c1b67d72d909.JPG',

'/ressources/images/8154beebc352.JPG',

'/ressources/images/de5c97223b91.JPG',

'/ressources/images/ddd232818d96.JPG',

'/ressources/images/dff8de79efff.JPG',

'/ressources/images/0ca5aa80c282.JPG',

'/ressources/images/566cc17ad8ab.JPG',

'/ressources/images/2ba41cfeb2b1.JPG',

'/ressources/images/88d0659ff830.JPG',

'/ressources/images/5cf3244cafc3.JPG',

'/ressources/images/2e08e263abb0.JPG',

'/ressources/images/8586073ca190.JPG',

'/ressources/images/14f9f195afb3.JPG',

'/ressources/images/d9481922453f.JPG',

'/ressources/images/82194b2320b6.jpg',

'/ressources/images/2900100b30d5.jpg',

'/ressources/images/c282618ac4b1.JPG',

'/ressources/images/eba8ba29b3b0.JPG',

'/ressources/images/3b36e2d95b13.jpg',

'/ressources/images/ada7befcc832.JPG',

'/ressources/images/e157eb002b58.JPG',

'/ressources/images/a39a435d8d91.JPG',

'/ressources/images/6d57bb0fd404.jpg',

'/ressources/images/9f576b9d5dc0.JPG',

'/ressources/images/1d25fdfccf6a.JPG',

'/ressources/images/5c84d4e3b54d.JPG',

'/ressources/images/94453148abd4.JPG',

'/ressources/images/18f4e61cec98.JPG',

'/ressources/images/5e46b7c64ce2.JPG',

'/ressources/images/474cc3038974.JPG',

'/ressources/images/800b1ab7abc2.JPG',

'/ressources/images/f341728a8a1e.JPG',

'/ressources/images/98bfb6afa377.JPG',

'/ressources/images/d2c41e879079.JPG',

'/ressources/images/b4cc5dafe484.JPG',

'/ressources/images/fd994bad4ec3.JPG',

'/ressources/images/79f50692c1fb.JPG',

'/ressources/images/686032112c4f.JPG',

'/ressources/images/028b33828277.JPG',

'/ressources/images/7a7d568b0496.JPG',

'/ressources/images/72ecc8fab1da.JPG',

'/ressources/images/9551ebef25ee.JPG',

'/ressources/images/b5db05d5daa4.JPG',

'/ressources/images/120f1c1d3a95.JPG',

'/ressources/images/6d3a6c6441ac.JPG',

'/ressources/images/48787014107a.JPG',

'/ressources/images/d7249576f44f.JPG',

'/ressources/images/91c84bf5fec4.JPG',

'/ressources/images/0f7b160c7789.JPG',

'/ressources/images/0c097104f122.JPG',

'/ressources/images/a69df3925a7d.JPG',

'/ressources/images/9d984d894137.JPG',

'/ressources/images/4b4d2ea8f97c.JPG',

'/ressources/images/b26aa6e041cc.JPG',

'/ressources/images/808ae973c95f.JPG',

'/ressources/images/b2d3ca7bc194.JPG',

'/ressources/images/82c1ed2aeafd.JPG',

'/ressources/images/677cc350f19d.JPG',

'/ressources/images/3760834d2629.JPG',

'/ressources/images/c90c2356e55a.JPG',

'/ressources/images/c7c8530dc306.JPG',

'/ressources/images/52d642a8fadd.JPG',

'/ressources/images/6ca39f443cbb.JPG',

'/ressources/images/704f4edee4fb.jpg',

'/ressources/images/0da65dd11c8d.jpg',

'/ressources/images/36041bed195b.jpg',

'/ressources/images/5abe97477a73.jpg',

'/ressources/images/aee048f64f37.jpg',

'/ressources/images/22cfcec1ed3b.jpg',

'/ressources/images/f83ea526a592.jpg',

'/ressources/images/8246c90db60a.jpg',

'/ressources/images/03d8a6bb54fd.jpg',

'/ressources/images/97eea83ed97e.jpg',

'/ressources/images/5a066c5c05a9.jpg',

'/ressources/images/9f374f0cf621.jpg',

'/ressources/images/5f87b6828b86.jpg',

'/ressources/images/a208713d8fea.jpg',

'/ressources/images/2b0880506aca.jpg',

'/ressources/images/48cfc321a15b.jpg',

'/ressources/images/31bc76c2bdb3.jpg',

'/ressources/images/f8139a0c6b70.jpg',

'/ressources/images/2639117b0eb6.jpg',

'/ressources/images/cbc195e27397.jpg',

'/ressources/images/3a4f75da90d3.jpg',

'/ressources/images/21698efe29f7.JPG',

'/ressources/images/e65b0f8fe7a7.jpg',

'/ressources/images/e37052641cdd.JPG',

'/ressources/images/e45cf53fa070.JPG',

'/ressources/images/5b72347b7aa4.JPG',

'/ressources/images/836bd2e1bcca.JPG',

'/ressources/images/a680da7f5bb0.JPG',

'/ressources/images/2cb307da00ac.JPG',

'/ressources/images/b62476ae134b.jpg',

'/ressources/images/599740ca156f.jpg',

'/ressources/images/0547fa1490e8.JPG',

'/ressources/images/8b146bc9d2f0.JPG',

'/ressources/images/6d3acd735604.JPG',

'/ressources/images/c15912aa759d.JPG',

'/ressources/images/e2e0f8e7afaf.JPG',

'/ressources/images/234cfad8e95a.JPG',

'/ressources/images/807d139022d7.JPG',

'/ressources/images/1f82b81f96c6.JPG',

'/ressources/images/12642a47e49b.JPG',

'/ressources/images/e9e556a4367b.jpg',

'/ressources/images/c609b1f1d21b.jpg',

'/ressources/images/1e8d8b18f7d0.jpg',

'/ressources/images/9f34728ea1cc.jpg',

'/ressources/images/c662b953e25e.jpg',

'/ressources/images/d5422cdf927c.jpeg',

'/ressources/images/3c1b26d5a235.jpg',

'/ressources/images/09154e45ca55.jpeg',

'/ressources/images/ec84e7eb96a4.jpg',

'/ressources/images/6cefffbfd54f.jpg',

'/ressources/images/fb44e1211df7.jpg',

'/ressources/images/df6485b53132.jpg',

'/ressources/images/c3d030c453a5.jpg',

'/ressources/images/8a681a0a2547.jpg',

'/ressources/images/451f4c669ca5.JPG',

'/ressources/images/a1b1bd878662.jpeg',

'/ressources/images/c45aae558143.jpeg',

'/ressources/images/64f464ac08d4.JPG',

'/ressources/images/69c0745b07c7.JPG',

'/ressources/images/4d62f8ea6233.jpeg',

'/ressources/images/f9f1f4397c7e.jpeg',

'/ressources/images/4b560c56ec51.jpeg',

'/ressources/images/911cc87c04f1.jpeg',

'/ressources/images/42475db513d5.jpeg',

'/ressources/images/15b6960abb01.jpeg',

'/ressources/images/e7869456b44b.jpeg',

'/ressources/images/92e70b135044.jpeg',

'/ressources/images/13ef42e24895.jpg',

'/ressources/images/c9d0a700b86c.JPG',

'/ressources/images/37542053cd7d.png',

'/ressources/images/71476a5a77e6.jpg',

'/ressources/images/36941e0bfafc.JPG',

'/ressources/images/1cab065ca782.jpg',

'/ressources/images/da1e8111c523.jpg',

'/ressources/images/e2d61984aeee.jpeg',

'/ressources/images/e9e76ad9b396.JPG',

'/ressources/images/b87a882563f1.jpg',

'/ressources/images/10ee84848abb.JPG',

'/ressources/images/476b4b8f935b.jpg',

'/ressources/images/c3c5a3e87bda.JPG',

'/ressources/images/72a943522875.jpg',

'/ressources/images/934e12b1d8e4.jpg',

'/ressources/images/0d1bb6bb0247.jpeg',

'/ressources/images/68050fb7e8b4.jpeg',

'/ressources/images/8e0281ae2fb1.JPG',

'/ressources/images/9781e687f5d1.JPG',

'/ressources/images/3cdcd3222aae.JPG',

'/ressources/images/6e0a83d0367d.jpg',

'/ressources/images/28bea173a373.jpg',

'/ressources/images/e016b7103d6e.jpg',

'/ressources/images/e88aba9ed2f4.jpg',

'/ressources/images/9486562e65dc.jpg',

'/ressources/images/5924dd1c2d3e.JPG',

'/ressources/images/8ed82b8ae070.png',

'/ressources/images/a7293b518312.jpg',

'/ressources/images/5dfe9c4292ca.jpg',

'/ressources/images/9af1cb32954f.png',

'/ressources/images/b221587b7f01.png',

'/ressources/images/2919b2d94baf.jpg',

'/ressources/images/fd1c1f18bff6.JPG',

'/ressources/images/6640f777d757.jpg',

'/ressources/images/9e6a51d91437.png',

'/ressources/images/d12a447b87f6.jpg',

'/ressources/images/8a84a9f5460e.jpeg',

'/ressources/images/7f51e37d29e0.jpg',

'/ressources/images/f3a28c52387e.png',

'/ressources/images/ab8c3eeb9580.JPG',

'/ressources/images/6e6521fb45dc.jpg',

'/ressources/images/5b8b142ef77e.jpg',

'/ressources/images/6df38c63fa44.jpg',

'/ressources/images/9935f1b05a13.jpeg',

'/ressources/images/acac9d9674be.png',

'/ressources/images/0a964997851c.png',

'/ressources/images/8d15c5b0bca0.JPG',

'/ressources/images/fa67210ffb6f.JPG',

'/ressources/images/6b6098db76bc.jpg',

'/ressources/images/0f3f9a1c3fd7.jpg',

'/ressources/images/f0537a53aeb3.jpg',

'/ressources/images/2f50e442a268.jpeg',

'/ressources/images/11ca4fe0b1bf.JPG',

'/ressources/images/cb56b67de9c2.JPG',

'/ressources/images/6941381ec722.JPG',

'/ressources/images/a44e4c7a23f4.jpg',

'/ressources/images/35282b48fc21.jpg',

'/ressources/images/57bade9dcde9.jpg',

'/ressources/images/88a9fdadc7dc.jpg',

'/ressources/images/7c1eddd7665a.jpg',

'/ressources/images/be666303acb8.jpeg',

'/ressources/images/3c814728d0fa.jpg',

'/ressources/images/5e249b7c33f1.JPG',

'/ressources/images/9930cc5a6c5d.JPG',

'/ressources/images/8aaef66bb49d.jpg',

'/ressources/images/965921c5c39d.jpg',

'/ressources/images/5e6d81ee64f8.jpg',

'/ressources/images/87dfb6c4850a.jpg',

'/ressources/images/e1f7a9612385.jpg',

'/ressources/images/e89b06a8932c.jpg',

'/ressources/images/9fc481051fa9.jpg',

'/ressources/images/075dab4a8d49.jpg',

'/ressources/images/eddd365f51cf.jpg',

'/ressources/images/2c846805c282.jpg',

'/ressources/images/778aa76139f6.jpg',

'/ressources/images/e7f067d78e01.jpg',

'/ressources/images/1d29e8433745.jpg',

'/ressources/images/baa5739c63ad.jpg',

'/ressources/images/845482cdbac2.jpg',

'/ressources/images/c769a7ec118b.jpg',

'/ressources/images/65ee759ec070.jpg',

'/ressources/images/12e090145875.jpg',

'/ressources/images/d222fc20fa2a.jpg',

'/ressources/images/aed59cd93cad.jpg',

'/ressources/images/a23868315571.jpg',

'/ressources/images/44beec09951a.jpg',

'/ressources/images/467358d910d3.jpg',

'/ressources/images/33206fcc43f5.jpg',

'/ressources/images/e2c402397772.jpg',

'/ressources/images/cab3442ecf43.jpg',

'/ressources/images/3c15b90248c5.jpg',

'/ressources/images/f4e03ea372eb.jpg',

'/ressources/images/19bf56da5569.jpg',

'/ressources/images/1e3ca394d33e.jpg',

'/ressources/images/90d4964bc947.jpg',

'/ressources/images/d701ba9d4868.jpg',

'/ressources/images/e7c20c395651.jpg',

'/ressources/images/7da8b9ea31cb.jpg',

'/ressources/images/b60c0e036917.jpg',

'/ressources/images/4b8f5572a82c.jpg',

'/ressources/images/673cd6e9178a.jpg',

'/ressources/images/859c9af9c8fe.jpg',

'/ressources/images/db0d07e50bc8.jpg',

'/ressources/images/3cda15282f8f.jpg',

'/ressources/images/c25bfaca273a.jpg',

'/ressources/images/f75856024799.jpg',

'/ressources/images/eab800e0e588.jpg',

'/ressources/images/5c44fd258c8e.jpg',

'/ressources/images/bb2fa29db97f.jpg',

'/ressources/images/a3df3299a792.jpg',

'/ressources/images/6b11bc27d19e.jpg',

'/ressources/images/215b2ba43e68.jpg',

'/ressources/images/734cae0e24df.jpg',

'/ressources/images/e4cfe215e900.jpg',

'/ressources/images/3137de200750.jpg',

'/ressources/images/558b2359ef5f.jpg',

'/ressources/images/2c1e6bc06af2.jpg',

'/ressources/images/cf70fd1d8795.jpg',

'/ressources/images/2610b64ee96b.jpg',

'/ressources/images/c0af0c60562a.jpg',

'/ressources/images/f4d39518385b.jpg',

'/ressources/images/9edf31cd318c.jpg',

'/ressources/images/d9c5280d51ed.jpg',

'/ressources/images/6b7d7a337ccf.jpg',

'/ressources/images/a312befa7c4c.jpg',

'/ressources/images/5bfaa6ca8340.jpg',

'/ressources/images/75ffd58369bf.jpg',

'/ressources/images/bfc7b0bc8a32.jpg',

'/ressources/images/8e5cb7b3e35d.jpg',

'/ressources/images/5628fdcd16b1.jpg',

'/ressources/images/f6760aa3b554.jpg',

'/ressources/images/9dc593bfe589.jpg',

'/ressources/images/628893d56de8.jpg',

'/ressources/images/691297e4a197.jpg',

'/ressources/images/df77640598ba.jpg',

'/ressources/images/8cb4679d78b4.jpg',

'/ressources/images/0e170d8f51c0.jpg',

'/ressources/images/bf547da4c39e.jpg',

'/ressources/images/4e077b86fdc7.jpg',

'/ressources/images/a3a7c9fe96df.jpg',

'/ressources/images/ddf6c997ad87.jpg',

'/ressources/images/60b1f2079d4c.jpg',

'/ressources/images/b54625471d5d.jpg',

'/ressources/images/891953c18939.jpg',

'/ressources/images/b9859d945dbb.jpg',

'/ressources/images/6087edb46a6b.jpg',

'/ressources/images/9e5d9fb7b8c0.jpg',

'/ressources/images/726cb50e71a2.jpg',

'/ressources/images/792edf23b38d.jpg',

'/ressources/images/c0a79e8f8395.jpg',

'/ressources/images/c63e79dde97f.jpg',

'/ressources/images/06dc7c997fcd.jpg',

'/ressources/images/311507e8d977.jpg',

'/ressources/images/8fe20339eccb.jpg',

'/ressources/images/0ec80497dc7a.jpg',

'/ressources/images/f217f24b02e5.jpg',

'/ressources/images/d76fd683c3d7.jpg',

'/ressources/images/e41ec13ac4fd.jpg',

'/ressources/images/596c48cba49e.jpg',

'/ressources/images/6cd8812a1712.jpg',

'/ressources/images/7ae95cadca31.jpg',

'/ressources/images/47b5f8244eee.jpg',

'/ressources/images/1339c71b105c.jpg',

'/ressources/images/56a7c44d44a0.jpg',

'/ressources/images/5a54cdba20f7.jpg',

'/ressources/images/daf98e617a42.jpg',

'/ressources/images/25e2d407fe17.jpg',

'/ressources/images/f6a2e2470b50.jpg',

'/ressources/images/8c5080b7a0da.jpg',

'/ressources/images/248bb84f30c8.jpg',

'/ressources/images/0e95a0bcd603.jpg',

'/ressources/images/cf1410a5b93d.jpg',

'/ressources/images/4e3d082af952.jpg',

'/ressources/images/9651de1209ee.jpg',

'/ressources/images/f2a781ebec1e.jpg',

'/ressources/images/0e9708def52f.jpg',

'/ressources/images/1a8b4e05d8f4.jpg',

'/ressources/images/169844b79c1b.jpg',

'/ressources/images/aabb5f548ad6.jpg',

'/ressources/images/d7e25024108b.jpg',

'/ressources/images/6776adaccb63.jpg',

'/ressources/images/230c3d1ca9a8.jpg',

'/ressources/images/0d13bbaa09ce.jpg',

'/ressources/images/02dd45787b27.jpg',

'/ressources/images/908b432d0fd4.jpg',

'/ressources/images/c94af73daf31.jpg',

'/ressources/images/13523a149877.jpg',

'/ressources/images/acd6bb9160fd.jpg',

'/ressources/images/ffa65333337a.JPG',

'/ressources/images/7feeed8fab5f.jpg',

'/ressources/images/e73197314627.jpg',

'/ressources/images/dbb0563b2317.jpg',

'/ressources/images/1b6a8e2c6fc5.jpg',

'/ressources/images/4fa655d3e3cd.jpg',

'/ressources/images/89b0d58dae7f.jpg',

'/ressources/images/52f85780655d.jpg',

'/ressources/images/6678d6d2b9da.JPG',

'/ressources/images/fb68e6175749.jpg',

'/ressources/images/957b13c142ad.jpg',

'/ressources/images/20028b906a66.jpg',

'/ressources/images/ba3770b15158.JPG',

'/ressources/images/6ee37c9f2f17.jpg',

'/ressources/images/c930c0fbe902.jpg',

'/ressources/images/5eb10d631b89.jpg',

'/ressources/images/5536f013fbfb.jpg',

'/ressources/images/282bcb129bd2.JPG',

'/ressources/images/81c9479ab5b1.JPG',

'/ressources/images/06c075014962.jpg',

'/ressources/images/645edf9e1353.jpg',

'/ressources/images/36bc3c7f163c.jpg',

'/ressources/images/bfab48a3302f.jpg',

'/ressources/images/72a3a797056e.jpg',

'/ressources/images/46d194ec352f.jpg',

'/ressources/images/968650ba2e22.jpg',

'/ressources/images/fbff05332399.jpg',

'/ressources/images/bb406e5cd10a.jpg',

'/ressources/images/4ded3a9baf11.jpg',

'/ressources/images/088929bc5eba.jpg',

'/ressources/images/312712f2d144.jpg',

'/ressources/images/ce794555ed03.jpg',

'/ressources/images/97e4bdc80193.jpg',

'/ressources/images/fb0941b18a52.jpg',

'/ressources/images/64f32b8f6ab5.jpg',

'/ressources/images/b382fe95b33d.jpg',

'/ressources/images/6aaae670ba42.jpg',

'/ressources/images/b90d8f89a27a.jpg',

'/ressources/images/73d82ee8a7de.jpg',

'/ressources/images/2f3083c082f1.jpg',

'/ressources/images/629495d40486.jpg',

'/ressources/images/8c321a6c85f8.jpg',

'/ressources/images/901379c008de.jpg',

'/ressources/images/98d076611e26.jpg',

'/ressources/images/afd7e8e5c00f.jpg',

'/ressources/images/8358433f0a8d.jpg',

'/ressources/images/1d39e213bd81.jpg',

'/ressources/images/8cb05d3368a6.jpg',

'/ressources/images/3843c406b43b.jpg',

'/ressources/images/a3561769eec9.jpg',

'/ressources/images/ed988e30d046.jpg',

'/ressources/images/13e8b9a946fd.jpg',

'/ressources/images/679c1a53c260.jpg',

'/ressources/images/bb6136cbb58d.jpg',

'/ressources/images/0fc7f05710ac.jpg',

'/ressources/images/c6120bdcfa96.jpg',

'/ressources/images/c535974b2eba.jpg',

'/ressources/images/92c69ea97605.jpg',

'/ressources/images/02b8af262c6c.jpg',

'/ressources/images/26317fa478a0.jpg',

'/ressources/images/2f7eded06d6a.jpg',

'/ressources/images/c62d65910cd4.jpg',

'/ressources/images/73f831bf2da6.jpg',

'/ressources/images/9010bc232ac5.jpg',

'/ressources/images/a25928283d46.jpg',

'/ressources/images/a806d47d7682.jpg',

'/ressources/images/78a865fedeae.jpg',

'/ressources/images/218f4bbd9ee3.jpg',

'/ressources/images/831870ff4afe.jpg',

'/ressources/images/22f17b22debb.jpg',

'/ressources/images/f29fffe1dcd4.jpg',

'/ressources/images/4ab41b58b6d8.jpg',

'/ressources/images/344ff960026a.jpg',

'/ressources/images/740450205f86.jpg',

'/ressources/images/ef6f275de0e8.jpg',

'/ressources/images/805446565509.jpg',

'/ressources/images/8da4d2d75d97.jpg',

'/ressources/images/eb6f759d9fae.jpeg',

'/ressources/images/63ddd5529d1e.jpg',

'/ressources/images/18dda398a22b.jpg',

'/ressources/images/0ddbbd41602f.jpg',

'/ressources/images/96f96f7fa6bf.jpg',

'/ressources/images/08ab2ab3b9fa.jpg',

'/ressources/images/795aa06de017.jpg',

'/ressources/images/b18b65ed65d0.jpg',

'/ressources/images/052a9f83d9c0.jpg',

'/ressources/images/b9c0a0d93ce9.jpg',

'/ressources/images/e55290de4947.jpg',

'/ressources/images/2d5223e38e12.jpg',

'/ressources/images/57e815b41b1a.jpg',

'/ressources/images/e0c8e1b2bce3.jpg',

'/ressources/images/1cf5c87e75cd.jpg',

'/ressources/images/5c53ce46e5f7.jpg',

'/ressources/images/c8d5c1b48345.jpg',

'/ressources/images/56271dcc2939.jpg',

'/ressources/images/c11a64d49ee1.jpg',

'/ressources/images/9eef12bf77c2.jpeg',

'/ressources/images/a1e065e568f7.jpg',

'/ressources/images/ad1c9ac534e8.jpg',

'/ressources/images/433833d8b703.jpg',

'/ressources/images/4735a811d836.jpg',

'/ressources/images/133172259b5f.jpg',

'/ressources/images/671c8d4bfc64.jpg',

'/ressources/images/8c519aa4cebf.jpg',

'/ressources/images/0d0ccb7c35ef.jpg',

'/ressources/images/fb65dae785f5.jpg',

'/ressources/images/cd8cb3f76e55.jpg',

'/ressources/images/3935db256cc0.jpg',

'/ressources/images/ed405b2aaa00.jpg',

'/ressources/images/186d3db01f7c.jpg',

'/ressources/images/823fde6383fe.jpg',

'/ressources/images/616aacf15d39.jpeg',

'/ressources/images/e2ad032500d3.jpg',

'/ressources/images/6165256a5546.jpg',

'/ressources/images/debf8a10d14b.jpg',

'/ressources/images/e0d3dfa36c7b.jpg',

'/ressources/images/de10eefb1431.jpg',

'/ressources/images/aeb643ce971c.jpg',

'/ressources/images/42df6f24a77c.jpg',

'/ressources/images/094148a0f4d9.jpg',

'/ressources/images/63e2f4c57688.jpg',

'/ressources/images/9fbf4bf0ff23.jpg',

'/ressources/images/4be58f8d7eda.jpg',

'/ressources/images/11fa2c100c69.jpg',

'/ressources/images/ed3c84dd326d.JPG',

'/ressources/images/2f81610fca43.jpg',

'/ressources/images/c3527de93ee4.jpg',

'/ressources/images/3b703e51d724.jpg',

'/ressources/images/3ff71e436464.JPG',

'/ressources/images/209ed83e0d3b.JPG',

'/ressources/images/a9416a6cdf98.jpg',

'/ressources/images/92d2ca1c12ab.jpg',

'/ressources/images/25023240a084.JPG',

'/ressources/images/ec63bf4b26f1.jpg',

'/ressources/images/28d3cec987c9.JPG',

'/ressources/images/9dc58d8933dd.JPEG',

'/ressources/images/91a3ce9e7a32.JPEG',

'/ressources/images/4b9208419101.JPEG',

'/ressources/images/3cb4b7a87b26.JPEG',

'/ressources/images/ddaf8195386f.JPG',

'/ressources/images/2f00afc78464.JPG',

'/ressources/images/e8184dc3eea2.JPG',

'/ressources/images/dc57029840ca.JPG',

'/ressources/images/08e8c1e3c13c.JPG',

'/ressources/images/3642222997d3.JPG',

'/ressources/images/0b4c57f987d1.JPG',

'/ressources/images/c6c8588cb607.JPEG',

'/ressources/images/218ef9837efd.JPEG',

'/ressources/images/15d81f0e4892.JPEG',

'/ressources/images/1173b6ba3784.JPEG',

'/ressources/images/fb10ee922e78.JPG',

'/ressources/images/65a65bbf13bb.png',

'/ressources/images/463aaff8c807.jpg',

'/ressources/images/c5c01fb39642.jpg',

'/ressources/images/2c79ef24b0b8.jpg',

'/ressources/images/decd2fc8c0f2.JPG',

'/ressources/images/2478a78ae462.JPG',

'/ressources/images/abe1a164a34a.png',

'/ressources/images/eb4523f3b95a.jpg',

'/ressources/images/487111993751.JPG',

'/ressources/images/7bf9e22c736e.JPG',

'/ressources/images/337cc6075deb.JPG',

'/ressources/images/e1ab1e562c66.JPG',

'/ressources/images/0545466aa05f.JPG',

'/ressources/images/35aad9a8d7bd.png',

'/ressources/images/92083aaa19de.jpeg',

'/ressources/images/c2033112fee5.JPG',

'/ressources/images/662ee0680e3e.JPG',

'/ressources/images/de4d0cc12e70.JPG',

'/ressources/images/5bc936a692a8.JPG',

'/ressources/images/928f6e82d122.JPG',

'/ressources/images/67fcb47c58b9.JPG',

'/ressources/images/397288a48545.JPG',

'/ressources/images/e1a912abc0a5.JPG',

'/ressources/images/bf41ecb4e2ee.JPG',

'/ressources/images/225e254b0bb7.JPG',

'/ressources/images/314b9bcbffb9.JPEG',

'/ressources/images/29555d87e7d9.JPG',

'/ressources/images/5ff344aa79d8.JPG',

'/ressources/images/d8c5a3de9efd.JPG',

'/ressources/images/42a463d6d435.JPG',

'/ressources/images/3b30980bbd1d.JPG',

'/ressources/images/5c5247f681de.JPG',

'/ressources/images/ca0758f8119b.JPG',

'/ressources/images/bded70e34537.JPG',

'/ressources/images/534c07675331.JPG',

'/ressources/images/b157935a86f6.JPG',

'/ressources/images/38012032bfde.JPG',

'/ressources/images/702ef15c05aa.JPG',

'/ressources/images/41b2e1b4fba7.JPG',

'/ressources/images/feb966ec35d8.JPG',

'/ressources/images/313badea5cf4.JPG',

'/ressources/images/2a1ee3796c02.JPG',

'/ressources/images/efe9bbf2d2c7.JPG',

'/ressources/images/657dcc378f87.JPG',

'/ressources/images/b7ed4d6dcc7c.JPG',

'/ressources/images/c8771dd745eb.JPG',

'/ressources/images/83b199a08a7e.JPG',

'/ressources/images/ee71ceb4932e.JPG',

'/ressources/images/c1117efbe665.JPEG',

'/ressources/images/fe0dde090005.JPG',

'/ressources/images/da897ed9e99d.JPG',

'/ressources/images/359a43527ca6.JPG',

'/ressources/images/69c0ee539aaa.JPG',

'/ressources/images/f3452fe93190.JPG',

'/ressources/images/9dca5f91fa9d.JPG',

'/ressources/images/a5db0e954c57.JPG',

'/ressources/images/8b0ac7d0490b.JPG',

'/ressources/images/25da65cce04b.JPG',

'/ressources/images/6383f3982977.JPG',

'/ressources/images/973b2e3dce3e.JPG',

'/ressources/images/9c2225ee71b2.JPG',

'/ressources/images/ddce3b785a08.JPG',

'/ressources/images/dd14ea36c129.JPEG',

'/ressources/images/11da203e2951.JPEG',

'/ressources/images/67d001273db1.jpg',

'/ressources/images/cf00eff7487d.JPG',

'/ressources/images/7b50e138fddf.JPG',

'/ressources/images/ef6770d8d2a1.JPG',

'/ressources/images/d282d84cf082.JPG',

'/ressources/images/452a605f5cc4.jpg',

'/ressources/images/5f322fa86a82.JPG',

'/ressources/images/0e29c287d750.jpg',

'/ressources/images/dbfc625030d4.jpg',

'/ressources/images/7d0e9a40db16.jpg',

'/ressources/images/6e690c9eb666.JPG',

'/ressources/images/8b43b90f24b3.jpg',

'/ressources/images/e0647eae1060.JPEG',

'/ressources/images/f71dfce95904.JPG',

'/ressources/images/f61a07cfe327.jpg',

'/ressources/images/30cebf14ec92.jpg',

'/ressources/images/4eb8aab8b477.JPG',

'/ressources/images/a9058c884b0f.JPG',

'/ressources/images/cab842fa506a.JPEG',

'/ressources/images/59e05e6c4bfb.JPG',

'/ressources/images/4b29cc8312a9.JPG',

'/ressources/images/6f165f53e52f.JPG',

'/ressources/images/191c4949f9de.JPG',

'/ressources/images/e7b5462a26e0.JPG',

'/ressources/images/f4272425429a.jpg',

'/ressources/images/a115bf5a5c83.JPG',

'/ressources/images/a11463fdbec4.JPG',

'/ressources/images/35ddcf103ba3.JPG',

'/ressources/images/8d9d995d721b.JPG',

'/ressources/images/eb51ad99acb5.JPG',

'/ressources/images/29231948eded.jpg',

'/ressources/images/e4d465e95f36.jpg',

'/ressources/images/e273c9393902.JPG',

'/ressources/images/9c265258b183.JPG',

'/ressources/images/dbdb186ff6a1.JPG',

'/ressources/images/1b0f47f20e45.JPG',

'/ressources/images/3ffef99a2b01.JPG',

'/ressources/images/25e68056bbee.jpg',

'/ressources/images/ef148f2ca1b7.JPG',

'/ressources/images/7aee6bf422fc.JPG',

'/ressources/images/4a7ccadb2f94.JPG',

'/ressources/images/2d1048103346.JPG',

'/ressources/images/2253141c6915.JPG',

'/ressources/images/bdc58ddc7314.JPG',

'/ressources/images/973be44ed720.JPG',

'/ressources/images/31fdde214c0c.JPEG',

'/ressources/images/8365cf3a732f.JPG',

'/ressources/images/d10180c07c79.JPG',

'/ressources/images/608128935cf8.JPG',

'/ressources/images/d901f1fa8b87.JPG',

'/ressources/images/c7bc6576ab83.JPG',

'/ressources/images/8100387d987a.JPG',

'/ressources/images/6ddbc6b4fef2.jpg',

'/ressources/images/94a5d4a520e2.JPG',

'/ressources/images/c6202c721ad1.JPG',

'/ressources/images/4223ae1934f0.JPG',

'/ressources/images/148bc9312db7.JPG',

'/ressources/images/2258775fa2e0.JPG',

'/ressources/images/b2c2608b09bc.JPG',

'/ressources/images/7fd39d6ec3e5.JPG',

'/ressources/images/ec45aa088552.JPG',

'/ressources/images/94a9088701c6.JPG',

'/ressources/images/2acff8fe8544.JPG',

'/ressources/images/4fafd687b183.JPG',

'/ressources/images/5f3d116bed0e.JPG',

'/ressources/images/0fd6741abff8.JPG',

'/ressources/images/7393b1241322.JPG',

'/ressources/images/04916dd3d91b.JPG',

'/ressources/images/3f8cee3d7f02.JPG',

'/ressources/images/9226bf77834f.JPG',

'/ressources/images/d4fffee51373.JPG',

'/ressources/images/5bdfe4cfdc24.JPG',

'/ressources/images/1de7f7a65636.JPG',

'/ressources/images/58791531dd44.JPG',

'/ressources/images/95bcd8f4b8e0.JPG',

'/ressources/images/e4c1bb9725c7.JPG',

'/ressources/images/d5332b4d921a.JPG',

'/ressources/images/abd4e0c3be9e.JPG',

'/ressources/images/cd59f60d31d8.JPG',

'/ressources/images/4bc6ca716930.JPG',

'/ressources/images/91bfad9a9e84.JPG',

'/ressources/images/3316f95c75a5.JPEG',

'/ressources/images/9d04f63ccc8c.JPG',

'/ressources/images/e1aee9e6964b.JPEG',

'/ressources/images/9f83dfed037b.JPEG',

'/ressources/images/bb8a2cd64c07.JPG',

'/ressources/images/78186324c9e2.JPG',

'/ressources/images/afb8983903ac.JPEG',

'/ressources/images/95c7a314aa0a.JPG',

'/ressources/images/69f9734e4098.JPG',

'/ressources/images/88d6da3d0747.JPG',

'/ressources/images/2ebb22f9711b.jpg',

'/ressources/images/be3a03245c99.JPEG',

'/ressources/images/d1abeab59410.jpg',

'/ressources/images/de1a3c8b1971.JPG',

'/ressources/images/df76d2004b9d.jpg',

'/ressources/images/dcb844158371.JPEG',

'/ressources/images/e245b7a822de.JPG',

'/ressources/images/23c23ca1f609.JPEG',

'/ressources/images/e97a82ff9dbb.JPG',

'/ressources/images/19f43abb59ac.jpg',

'/ressources/images/e32155aaf369.JPG',

'/ressources/images/3bd97b8f6168.JPEG',

'/ressources/images/a365104ee0ca.JPG',

'/ressources/images/b718540af86e.JPG',

'/ressources/images/7c8c87774b41.JPG',

'/ressources/images/eda889d94035.jpg',

'/ressources/images/fefc16982c2a.jpg',

'/ressources/images/719797f13cbe.JPG',

'/ressources/images/14dba0defb86.jpg',

'/ressources/images/3dd3340b7c1c.jpg',

'/ressources/images/5e87fa4d4fac.JPG',

'/ressources/images/9bd78e389fbf.jpg',

'/ressources/images/08999aa4fc44.JPG',

'/ressources/images/7262f88beb63.jpg',

'/ressources/images/db6af3283863.JPG',

'/ressources/images/3b963e3e7a86.JPG',

'/ressources/images/74c4d35a38ba.JPG',

'/ressources/images/4e8871f474e7.JPG',

'/ressources/images/aae1d8e0ff23.JPEG',

'/ressources/images/7c7ecd0e450f.JPG',

'/ressources/images/59a86907230e.JPG',

'/ressources/images/9aeed3ba5271.JPG',

'/ressources/images/7a45eff3a864.JPG',

'/ressources/images/06496513ef35.JPG')

```



### statistique opération effectués

* nombre images avant 2021 :  890 images , obtenues à partir requête sql
* nombre images utilisés par site  : 	282 , obtenues par check table bloc, template.css, front (front -> slider dans une page spécifique)
* nombre de fichier à supprimer  : 821, obtenu (on a checké s'il y a des images utlisés dans les images avant 2021 et ceux là n'ont pas été supprimées)

### outils 
on a programmé por check database, checkfront, check css 
[[sites local#php (testCode)]]


## logique pour trouver images à supprimer

* recuperation liste images avant 2021 (requete bdd)
* recuperation liste images utilisés par site (requete dans table block , check css  )
* recuperation liste images avant 2021 et non utilisé
* suppression des images non utilisées et avant 2021 dans table ressources et dossier ressources 
* comparaison contenu site DID et HID (puisque suppression a été fait sur DID)
* 3 images manquaient sur site DID (ne sont ni dans table block ni dans css)
	* ces images ont été supprimées car on ne savait pas qu'elles sont utilisés qu'après compraisons sites

<span style="font-size : 20px">Problèmes</span> on n'a pas pu récupérer les collections qui sont utilisés dans bloc (a verifier)on a effacé accidentellement des images qui sont appelé dans collection

* récupération images dans table resources_collections_resources
*  recuperation images avant 2021 et utilisé dans bloc
* recuperation image utilisé dans css 

### donc on gros 
en prend toutes les images avant 2021 et on enlève celles qui sont utilisées dans 
* bloc
* css
* collections 

farany natao  : exporter ressource complet dia aveo maka anle id anle images tokon supprimena
efa ao list images a supprimer fa nom( dia supprimena anaty base ressources ary atao insert amle base did ilay izy)

---------------------
iza zan le ligne tsy tokon vofafa nefa lasa any dia averina 


total de 628 dans table ressources 


08-03-2023 (version final)

nombre de fichier(s) supprimé(s): 390  
nombre total images dans dossier sources :716  
nombre de ligne CSV: 390


### select or delete using this 

```sql
SELECT * FROM `ID302_resources` WHERE fileUrl IN (

'/ressources/images/e7e29e87d7ce.jpg',

'/ressources/images/7bb0d5728f2d.jpeg',

'/ressources/images/8d07168109a0.jpg',

'/ressources/images/b5e21e280933.jpeg',

'/ressources/images/501180e0bbb8.jpg',

'/ressources/images/551fcf11940f.jpeg',

'/ressources/images/88894dede505.jpg',

'/ressources/images/4761ce64f6b1.jpg',

'/ressources/images/fb33671288f6.jpg',

'/ressources/images/dcd4b37294fe.jpg',

'/ressources/images/db32017d0d79.jpg',

'/ressources/images/78c92987cbf5.jpg',

'/ressources/images/bdc23dcbb671.JPG',

'/ressources/images/0cef94a045df.jpg',

'/ressources/images/1831aa5c0d74.jpg',

'/ressources/images/9cfa4d1afc22.jpg',

'/ressources/images/a9d3109281ef.jpg',

'/ressources/images/03bfd3dc742e.jpg',

'/ressources/images/847d69c370f9.jpg',

'/ressources/images/41057618bb2b.jpg',

'/ressources/images/15ad2e725a0f.jpg',

'/ressources/images/e4b325db2cdf.jpg',

'/ressources/images/bad2ec7b7a72.jpg',

'/ressources/images/f47049cb4f93.jpg',

'/ressources/images/cde932afaa94.jpg',

'/ressources/images/591fa172fa49.jpg',

'/ressources/images/0f9d0dd4d715.jpg',

'/ressources/images/e83a6e008a51.jpg',

'/ressources/images/3fea2d5f08f5.jpg',

'/ressources/images/8bad17eaed90.jpg',

'/ressources/images/7d853206c2c6.jpg',

'/ressources/images/fdaa58ca8fd7.jpg',

'/ressources/images/5ac5e5bdda50.jpg',

'/ressources/images/4fb08bb44528.jpg',

'/ressources/images/f812e9e810d9.JPG',

'/ressources/images/ee50a73e4e15.jpg',

'/ressources/images/26f19a04441a.JPG',

'/ressources/images/d7ed89e1e568.JPG',

'/ressources/images/168093918843.JPG',

'/ressources/images/0a2e7feca962.JPG',

'/ressources/images/52a8e98bda77.JPG',

'/ressources/images/94f47fc2486e.JPG',

'/ressources/images/8c1b81698a4d.JPG',

'/ressources/images/cada3bb0c690.JPG',

'/ressources/images/d391124d1606.JPG',

'/ressources/images/7fb6be165a6d.JPG',

'/ressources/images/675dfa44b962.JPG',

'/ressources/images/b752fc1cb74f.JPG',

'/ressources/images/f5af1105f604.JPG',

'/ressources/images/42ae1c991624.JPG',

'/ressources/images/8dd78e950a4b.JPG',

'/ressources/images/8c99dbfb0096.JPG',

'/ressources/images/a2d96ab8b734.JPG',

'/ressources/images/fc55ca959e29.JPG',

'/ressources/images/33e99df3742d.JPG',

'/ressources/images/c624b35d9e62.JPG',

'/ressources/images/1a1fc4655a18.JPG',

'/ressources/images/063b3693bf90.JPG',

'/ressources/images/3ad0b4ad125e.JPG',

'/ressources/images/fafed374e4b4.JPG',

'/ressources/images/8d83c7cb4851.JPG',

'/ressources/images/eda4d9e0e7ee.JPG',

'/ressources/images/6ecb725b4b81.JPG',

'/ressources/images/57f72af68e71.JPG',

'/ressources/images/3ed02052e2af.JPG',

'/ressources/images/68d944fdc759.JPG',

'/ressources/images/096bb146832b.JPG',

'/ressources/images/37a96f76214f.JPG',

'/ressources/images/b52947afd31b.JPG',

'/ressources/images/41e5982b4b21.JPG',

'/ressources/images/bd8e6fde94ce.JPG',

'/ressources/images/25faff9059c1.JPG',

'/ressources/images/732f854e29b3.JPG',

'/ressources/images/7e3f04b570c4.JPG',

'/ressources/images/134c6b17c153.JPG',

'/ressources/images/409375cd6a00.JPG',

'/ressources/images/edb8a48009d4.JPG',

'/ressources/images/39ada892e336.JPG',

'/ressources/images/bb58f0e5994a.JPG',

'/ressources/images/3ffd02a689b0.JPG',

'/ressources/images/74792606b0f1.JPG',

'/ressources/images/d1581865bf36.JPG',

'/ressources/images/c068495fbbf8.JPG',

'/ressources/images/553ed0b05d6f.JPG',

'/ressources/images/cc245e9151e6.JPG',

'/ressources/images/fcc12e0e19d5.JPG',

'/ressources/images/6344bd26dd68.JPG',

'/ressources/images/d2c1692840f3.JPG',

'/ressources/images/d614c90f9ff8.JPG',

'/ressources/images/1eb67ad59e48.JPG',

'/ressources/images/a6b4acfafba5.JPG',

'/ressources/images/6ab11ea04bbc.JPG',

'/ressources/images/c1b67d72d909.JPG',

'/ressources/images/8154beebc352.JPG',

'/ressources/images/de5c97223b91.JPG',

'/ressources/images/ddd232818d96.JPG',

'/ressources/images/566cc17ad8ab.JPG',

'/ressources/images/2ba41cfeb2b1.JPG',

'/ressources/images/88d0659ff830.JPG',

'/ressources/images/5cf3244cafc3.JPG',

'/ressources/images/2e08e263abb0.JPG',

'/ressources/images/c282618ac4b1.JPG',

'/ressources/images/eba8ba29b3b0.JPG',

'/ressources/images/9f576b9d5dc0.JPG',

'/ressources/images/94453148abd4.JPG',

'/ressources/images/c9d0a700b86c.JPG',

'/ressources/images/37542053cd7d.png',

'/ressources/images/71476a5a77e6.jpg',

'/ressources/images/36941e0bfafc.JPG',

'/ressources/images/e2d61984aeee.jpeg',

'/ressources/images/8ed82b8ae070.png',

'/ressources/images/a7293b518312.jpg',

'/ressources/images/5dfe9c4292ca.jpg',

'/ressources/images/9af1cb32954f.png',

'/ressources/images/b221587b7f01.png',

'/ressources/images/6640f777d757.jpg',

'/ressources/images/9e6a51d91437.png',

'/ressources/images/7f51e37d29e0.jpg',

'/ressources/images/f3a28c52387e.png',

'/ressources/images/ab8c3eeb9580.JPG',

'/ressources/images/6e6521fb45dc.jpg',

'/ressources/images/5b8b142ef77e.jpg',

'/ressources/images/6df38c63fa44.jpg',

'/ressources/images/9935f1b05a13.jpeg',

'/ressources/images/acac9d9674be.png',

'/ressources/images/0a964997851c.png',

'/ressources/images/5c44fd258c8e.jpg',

'/ressources/images/a3df3299a792.jpg',

'/ressources/images/78a865fedeae.jpg',

'/ressources/images/218f4bbd9ee3.jpg',

'/ressources/images/831870ff4afe.jpg',

'/ressources/images/22f17b22debb.jpg',

'/ressources/images/f29fffe1dcd4.jpg',

'/ressources/images/4ab41b58b6d8.jpg',

'/ressources/images/344ff960026a.jpg',

'/ressources/images/740450205f86.jpg',

'/ressources/images/ef6f275de0e8.jpg',

'/ressources/images/805446565509.jpg',

'/ressources/images/8da4d2d75d97.jpg',

'/ressources/images/eb6f759d9fae.jpeg',

'/ressources/images/63ddd5529d1e.jpg',

'/ressources/images/18dda398a22b.jpg',

'/ressources/images/0ddbbd41602f.jpg',

'/ressources/images/96f96f7fa6bf.jpg',

'/ressources/images/08ab2ab3b9fa.jpg',

'/ressources/images/795aa06de017.jpg',

'/ressources/images/b18b65ed65d0.jpg',

'/ressources/images/052a9f83d9c0.jpg',

'/ressources/images/b9c0a0d93ce9.jpg',

'/ressources/images/e55290de4947.jpg',

'/ressources/images/2d5223e38e12.jpg',

'/ressources/images/57e815b41b1a.jpg',

'/ressources/images/e0c8e1b2bce3.jpg',

'/ressources/images/1cf5c87e75cd.jpg',

'/ressources/images/5c53ce46e5f7.jpg',

'/ressources/images/c8d5c1b48345.jpg',

'/ressources/images/56271dcc2939.jpg',

'/ressources/images/c11a64d49ee1.jpg',

'/ressources/images/9eef12bf77c2.jpeg',

'/ressources/images/a1e065e568f7.jpg',

'/ressources/images/ad1c9ac534e8.jpg',

'/ressources/images/433833d8b703.jpg',

'/ressources/images/4735a811d836.jpg',

'/ressources/images/133172259b5f.jpg',

'/ressources/images/671c8d4bfc64.jpg',

'/ressources/images/8c519aa4cebf.jpg',

'/ressources/images/0d0ccb7c35ef.jpg',

'/ressources/images/fb65dae785f5.jpg',

'/ressources/images/cd8cb3f76e55.jpg',

'/ressources/images/3935db256cc0.jpg',

'/ressources/images/ed405b2aaa00.jpg',

'/ressources/images/186d3db01f7c.jpg',

'/ressources/images/823fde6383fe.jpg',

'/ressources/images/616aacf15d39.jpeg',

'/ressources/images/e2ad032500d3.jpg',

'/ressources/images/6165256a5546.jpg',

'/ressources/images/debf8a10d14b.jpg',

'/ressources/images/e0d3dfa36c7b.jpg',

'/ressources/images/de10eefb1431.jpg',

'/ressources/images/aeb643ce971c.jpg',

'/ressources/images/42df6f24a77c.jpg',

'/ressources/images/094148a0f4d9.jpg',

'/ressources/images/63e2f4c57688.jpg',

'/ressources/images/9fbf4bf0ff23.jpg',

'/ressources/images/4be58f8d7eda.jpg',

'/ressources/images/11fa2c100c69.jpg',

'/ressources/images/ed3c84dd326d.JPG',

'/ressources/images/2f81610fca43.jpg',

'/ressources/images/c3527de93ee4.jpg',

'/ressources/images/3ff71e436464.JPG',

'/ressources/images/a9416a6cdf98.jpg',

'/ressources/images/92d2ca1c12ab.jpg',

'/ressources/images/25023240a084.JPG',

'/ressources/images/28d3cec987c9.JPG',

'/ressources/images/9dc58d8933dd.JPEG',

'/ressources/images/91a3ce9e7a32.JPEG',

'/ressources/images/4b9208419101.JPEG',

'/ressources/images/3cb4b7a87b26.JPEG',

'/ressources/images/ddaf8195386f.JPG',

'/ressources/images/2f00afc78464.JPG',

'/ressources/images/e8184dc3eea2.JPG',

'/ressources/images/dc57029840ca.JPG',

'/ressources/images/08e8c1e3c13c.JPG',

'/ressources/images/3642222997d3.JPG',

'/ressources/images/0b4c57f987d1.JPG',

'/ressources/images/c6c8588cb607.JPEG',

'/ressources/images/218ef9837efd.JPEG',

'/ressources/images/15d81f0e4892.JPEG',

'/ressources/images/1173b6ba3784.JPEG',

'/ressources/images/fb10ee922e78.JPG',

'/ressources/images/463aaff8c807.jpg',

'/ressources/images/c5c01fb39642.jpg',

'/ressources/images/2c79ef24b0b8.jpg',

'/ressources/images/decd2fc8c0f2.JPG',

'/ressources/images/2478a78ae462.JPG',

'/ressources/images/abe1a164a34a.png',

'/ressources/images/eb4523f3b95a.jpg',

'/ressources/images/487111993751.JPG',

'/ressources/images/7bf9e22c736e.JPG',

'/ressources/images/337cc6075deb.JPG',

'/ressources/images/e1ab1e562c66.JPG',

'/ressources/images/0545466aa05f.JPG',

'/ressources/images/92083aaa19de.jpeg',

'/ressources/images/c2033112fee5.JPG',

'/ressources/images/662ee0680e3e.JPG',

'/ressources/images/de4d0cc12e70.JPG',

'/ressources/images/5bc936a692a8.JPG',

'/ressources/images/928f6e82d122.JPG',

'/ressources/images/67fcb47c58b9.JPG',

'/ressources/images/397288a48545.JPG',

'/ressources/images/e1a912abc0a5.JPG',

'/ressources/images/bf41ecb4e2ee.JPG',

'/ressources/images/225e254b0bb7.JPG',

'/ressources/images/314b9bcbffb9.JPEG',

'/ressources/images/29555d87e7d9.JPG',

'/ressources/images/5ff344aa79d8.JPG',

'/ressources/images/d8c5a3de9efd.JPG',

'/ressources/images/42a463d6d435.JPG',

'/ressources/images/3b30980bbd1d.JPG',

'/ressources/images/5c5247f681de.JPG',

'/ressources/images/ca0758f8119b.JPG',

'/ressources/images/bded70e34537.JPG',

'/ressources/images/534c07675331.JPG',

'/ressources/images/b157935a86f6.JPG',

'/ressources/images/38012032bfde.JPG',

'/ressources/images/702ef15c05aa.JPG',

'/ressources/images/41b2e1b4fba7.JPG',

'/ressources/images/feb966ec35d8.JPG',

'/ressources/images/313badea5cf4.JPG',

'/ressources/images/2a1ee3796c02.JPG',

'/ressources/images/efe9bbf2d2c7.JPG',

'/ressources/images/657dcc378f87.JPG',

'/ressources/images/b7ed4d6dcc7c.JPG',

'/ressources/images/c8771dd745eb.JPG',

'/ressources/images/83b199a08a7e.JPG',

'/ressources/images/ee71ceb4932e.JPG',

'/ressources/images/c1117efbe665.JPEG',

'/ressources/images/fe0dde090005.JPG',

'/ressources/images/da897ed9e99d.JPG',

'/ressources/images/359a43527ca6.JPG',

'/ressources/images/69c0ee539aaa.JPG',

'/ressources/images/f3452fe93190.JPG',

'/ressources/images/9dca5f91fa9d.JPG',

'/ressources/images/a5db0e954c57.JPG',

'/ressources/images/8b0ac7d0490b.JPG',

'/ressources/images/25da65cce04b.JPG',

'/ressources/images/6383f3982977.JPG',

'/ressources/images/973b2e3dce3e.JPG',

'/ressources/images/9c2225ee71b2.JPG',

'/ressources/images/dd14ea36c129.JPEG',

'/ressources/images/11da203e2951.JPEG',

'/ressources/images/67d001273db1.jpg',

'/ressources/images/cf00eff7487d.JPG',

'/ressources/images/7b50e138fddf.JPG',

'/ressources/images/ef6770d8d2a1.JPG',

'/ressources/images/d282d84cf082.JPG',

'/ressources/images/452a605f5cc4.jpg',

'/ressources/images/5f322fa86a82.JPG',

'/ressources/images/6e690c9eb666.JPG',

'/ressources/images/8b43b90f24b3.jpg',

'/ressources/images/e0647eae1060.JPEG',

'/ressources/images/f71dfce95904.JPG',

'/ressources/images/f61a07cfe327.jpg',

'/ressources/images/30cebf14ec92.jpg',

'/ressources/images/4eb8aab8b477.JPG',

'/ressources/images/a9058c884b0f.JPG',

'/ressources/images/cab842fa506a.JPEG',

'/ressources/images/59e05e6c4bfb.JPG',

'/ressources/images/4b29cc8312a9.JPG',

'/ressources/images/6f165f53e52f.JPG',

'/ressources/images/191c4949f9de.JPG',

'/ressources/images/e7b5462a26e0.JPG',

'/ressources/images/f4272425429a.jpg',

'/ressources/images/a115bf5a5c83.JPG',

'/ressources/images/a11463fdbec4.JPG',

'/ressources/images/35ddcf103ba3.JPG',

'/ressources/images/8d9d995d721b.JPG',

'/ressources/images/eb51ad99acb5.JPG',

'/ressources/images/29231948eded.jpg',

'/ressources/images/e273c9393902.JPG',

'/ressources/images/9c265258b183.JPG',

'/ressources/images/dbdb186ff6a1.JPG',

'/ressources/images/1b0f47f20e45.JPG',

'/ressources/images/3ffef99a2b01.JPG',

'/ressources/images/25e68056bbee.jpg',

'/ressources/images/ef148f2ca1b7.JPG',

'/ressources/images/7aee6bf422fc.JPG',

'/ressources/images/4a7ccadb2f94.JPG',

'/ressources/images/2d1048103346.JPG',

'/ressources/images/2253141c6915.JPG',

'/ressources/images/bdc58ddc7314.JPG',

'/ressources/images/973be44ed720.JPG',

'/ressources/images/31fdde214c0c.JPEG',

'/ressources/images/8365cf3a732f.JPG',

'/ressources/images/d10180c07c79.JPG',

'/ressources/images/608128935cf8.JPG',

'/ressources/images/d901f1fa8b87.JPG',

'/ressources/images/c7bc6576ab83.JPG',

'/ressources/images/8100387d987a.JPG',

'/ressources/images/6ddbc6b4fef2.jpg',

'/ressources/images/94a5d4a520e2.JPG',

'/ressources/images/c6202c721ad1.JPG',

'/ressources/images/4223ae1934f0.JPG',

'/ressources/images/148bc9312db7.JPG',

'/ressources/images/2258775fa2e0.JPG',

'/ressources/images/b2c2608b09bc.JPG',

'/ressources/images/7fd39d6ec3e5.JPG',

'/ressources/images/ec45aa088552.JPG',

'/ressources/images/94a9088701c6.JPG',

'/ressources/images/2acff8fe8544.JPG',

'/ressources/images/4fafd687b183.JPG',

'/ressources/images/5f3d116bed0e.JPG',

'/ressources/images/0fd6741abff8.JPG',

'/ressources/images/7393b1241322.JPG',

'/ressources/images/04916dd3d91b.JPG',

'/ressources/images/3f8cee3d7f02.JPG',

'/ressources/images/9226bf77834f.JPG',

'/ressources/images/d4fffee51373.JPG',

'/ressources/images/5bdfe4cfdc24.JPG',

'/ressources/images/1de7f7a65636.JPG',

'/ressources/images/58791531dd44.JPG',

'/ressources/images/95bcd8f4b8e0.JPG',

'/ressources/images/e4c1bb9725c7.JPG',

'/ressources/images/d5332b4d921a.JPG',

'/ressources/images/abd4e0c3be9e.JPG',

'/ressources/images/cd59f60d31d8.JPG',

'/ressources/images/4bc6ca716930.JPG',

'/ressources/images/91bfad9a9e84.JPG',

'/ressources/images/3316f95c75a5.JPEG',

'/ressources/images/9d04f63ccc8c.JPG',

'/ressources/images/e1aee9e6964b.JPEG',

'/ressources/images/9f83dfed037b.JPEG',

'/ressources/images/bb8a2cd64c07.JPG',

'/ressources/images/78186324c9e2.JPG',

'/ressources/images/afb8983903ac.JPEG',

'/ressources/images/95c7a314aa0a.JPG',

'/ressources/images/69f9734e4098.JPG',

'/ressources/images/88d6da3d0747.JPG',

'/ressources/images/2ebb22f9711b.jpg',

'/ressources/images/be3a03245c99.JPEG',

'/ressources/images/d1abeab59410.jpg',

'/ressources/images/de1a3c8b1971.JPG',

'/ressources/images/dcb844158371.JPEG',

'/ressources/images/e245b7a822de.JPG',

'/ressources/images/23c23ca1f609.JPEG',

'/ressources/images/e97a82ff9dbb.JPG',

'/ressources/images/e32155aaf369.JPG',

'/ressources/images/3bd97b8f6168.JPEG',

'/ressources/images/a365104ee0ca.JPG',

'/ressources/images/b718540af86e.JPG',

'/ressources/images/7c8c87774b41.JPG',

'/ressources/images/eda889d94035.jpg',

'/ressources/images/fefc16982c2a.jpg',

'/ressources/images/719797f13cbe.JPG',

'/ressources/images/14dba0defb86.jpg',

'/ressources/images/3dd3340b7c1c.jpg',

'/ressources/images/5e87fa4d4fac.JPG',

'/ressources/images/9bd78e389fbf.jpg',

'/ressources/images/08999aa4fc44.JPG',

'/ressources/images/7262f88beb63.jpg',

'/ressources/images/db6af3283863.JPG',

'/ressources/images/3b963e3e7a86.JPG',

'/ressources/images/74c4d35a38ba.JPG',

'/ressources/images/4e8871f474e7.JPG',

'/ressources/images/aae1d8e0ff23.JPEG',

'/ressources/images/7c7ecd0e450f.JPG',

'/ressources/images/59a86907230e.JPG',

'/ressources/images/9aeed3ba5271.JPG',

'/ressources/images/7a45eff3a864.JPG',

'/ressources/images/06496513ef35.JPG');
```
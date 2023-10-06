---
title: "La sauvegarde des données de travail - principes"
date: 2023-10-06T11:00:20+02:00
draft: false
authors: ["Alexandre"]
---

L'une de mes plus grandes peurs, sans doute partagée par beaucoup, est de perdre l'intégralité de mon travail de thèse. Pour cette raison, il me semble essentiel de mettre en place des stratégies de sauvegarde efficaces de mon travail.

Avec le développement des clouds, on a souvent l'impression que nos données sont protégées, tout le temps, partout. Qu'une fois notre smartphone ou ordinateur éteint, "le cloud" est là pour délester toute la mémoire de son fardeau. En réalité, les risques de pertes de données sont nombreux : vols, pertes, casses, corruption du matériel (le *hardware*) pour les causes physiques, mais aussi les défaillances *software* qui, sans être particulièrement fréquentes, peuvent être dévastatrices. Qui n'a jamais paniqué devant le fameux [blue screen of death](https://en.wikipedia.org/wiki/Blue_screen_of_death) ? 

Bien gérer ses données demande patience et méthode. Ce que je vais présenter est une stratégie parmi d'autres. Elle est animée par deux volontés personnelles : 

1. **un recours faible à un service tiers** : il existe un certain nombre de services dédiés à la sauvegarde des données – serveurs clouds propriétaires (Google Drive, OneDrive, iCloud, pCloud etc.). Dans un souci de conservation et de protection de mes données, je préfère m'en éloigner. Cela permet notamment d'éviter qu'une perte d'accès à ces services me fassent perdre, aussi, à mes données.
2. **un faible coût en temps et en argent** : 
   1. je ne veux pas avoir à faire un copier-coller tous les soirs pour sauvegarder mon travail. Je trouve cela particulièrement ennuyant et pas forcément plus sécurisé (une perte de la clef USB sur laquelle tout est enregistré, et c'est fini) ;
   2. de même, le recours à des services tiers implique souvent un coût pouvant devenir important. Les abonnements clouds peuvent être chers.

Dans ce billet, je présenterai les différents principes qui me semblent importants dans la gestion de ses données de travail. Le système que je mets en œuvre sera présenté dans un billet prochain.

Les trois principes en question sont : la redondance, le *versioning* et la synchronisation.

## Redondance

En ingénierie, il est souvent recommandé d'assurer la [redondance](https://fr.wikipedia.org/wiki/Redondance_(ing%C3%A9nierie)) des composants d'un outil, engin ou toute autre machine fabriquée par la main humaine dont la sécurité est critique. Il s'agit avant tout de garantir la fiabilité d'un système même en cas de défaillance matérielle grave. 

En informatique, on utilise aussi cette notion pour désigner, entre autres, la duplication (en deux ou plusieurs copies) de données dont la sauvegarde est essentielle. L'idée se comprend relativement bien : n'avoir qu'une seule copie d'un fichier expose ce dernier à sa perte totale et définitive en cas de défaillance *hardware* ou *software*. 

En général, la première idée qui nous vient lorsqu'on s'interroge sur la manière dont on peut protéger ses données est la copie sur un support externe. L'opération est généralement très simple : brancher un périphérique externe (USB, disque dur) ; copier les fichiers à protéger et les coller sur le périphérique ; débrancher le périphérique.

Cela suffit dans certains cas, par exemple lorsque les fichiers n'ont pas vocation à être modifiés fréquemment. En revanche, dès lors que les fichiers sont nombreux, ont plusieurs versions différentes et sont ouverts tous les jours, ce mode de fonctionnement pose plusieurs problèmes.

D'abord, la gestion des versions est particulièrement mauvaise. Quand on fait un copier-coller, le système d'exploitation ne fait *que* copier et coller, en écrasant toutes versions antérieures d'un fichier. Par ailleurs, les fichiers présents dans la copie qui ne nous sont plus utiles demeurent, et prennent de l'espace. 

Ensuite, l'opération qui, pour être efficace, doit être répétée régulièrement, implique une certaine discipline et un moment dédié à cela dans la journée. Pour peu que le nombre de fichiers soit important, cela peut parfois revenir à passer une dizaine de minutes à faire quelque chose de relativement peu intéressant.

Enfin, la dépendance matérielle au périphérique externe peut-être contraignante. Une clef USB perdue ou un HDD corrompu après un choc sont autant de risques de perte de données.

## *Versioning*

Qui ne s'est jamais retrouvé avec un dossier rempli de `Document.docx`, `Document_final.docx`, `Document_corrigé_final.docx`, `Document_final_corrigé_final.docx`, etc. ? 

La question de la gestion des versions est très importante pour les programmeurs (on en voit une expression dans le développement des v1, v1.1, v1.2.3, etc.), mais elle l'est aussi pour toute personne ayant à produire des documents à l'aide d'un ordinateur. Heureusement aujourd'hui, la plupart des outils de traitement de textes permettent une gestion des versions, mais celle-ci est souvent peu intuitive, et s'articule assez mal avec la question de la sauvegarde des données.

Aussi, l'un des principes fondamentaux d'une bonne gestion des données est le *[versioning](https://en.wikipedia.org/wiki/Software_versioning)*, c'est-à-dire la pratique consistant à garder un historique des différentes modifications qu'un fichier a subies. Cet historique n'a pas forcément besoin d'être complet ou conservé sur un temps très long – tout dépend de ce qu'on fait. Néanmoins, il me semble essentiel d'intégrer une certaine pratique de conservation de cet historique afin de s'assurer contre la suppression d'éléments importants dans une nouvelle copie d'un fichier.

Cette pratique peut concerner un fichier en particulier (différentes versions d'un fichier `markdown` par exemple) comme d'un dossier ou d'une sauvegarde complète. Nous verrons plus tard ce que cela implique et comment constituer une sauvegarde automatique qui garde en mémoire la suppression et l'ajout de fichiers, par exemple.

## Synchronisation

Le dernier principe est celui de la *synchronisation*. Il répond à la problématique du temps et de la discipline qu'implique la gestion de ses données. La synchronisation automatique permet de ne pas avoir à penser à sa sauvegarde en laissant un programme gérer à notre place le processus. 

Nous sommes beaucoup à être familiers avec ce processus de synchronisation. Lors de la configuration d'un nouveau smartphone, par exemple, les services d'Apple ou de Google demandent quasi-systématiquement si l'on souhaite synchroniser nos photos avec les services clouds. On synchronise aussi nos mails, nos messages, etc. 

Ces modes de synchronisation mettent en général en action deux acteurs : le client (votre smartphone) et le serveur (d'Apple, de Google, ou autres). Aussi, les données synchronisées sont stockées sur des ordinateurs parfois à l'autre bout du monde. 

Il est possible de mettre en œuvre des mécanismes de synchronisation qui conservent les données sur des appareils personnels. Certains de ces mécanismes peuvent être très coûteux (tant sur le plan matériel que sur le coût en électricité) ; d'autres le sont moins et font usage d'outils que vous avez déjà à la maison.

De manière générale, et peu importe la méthode employée, il me paraît important de mettre en œuvre une forme de synchronisation limitant ainsi l'action de l'utilisateur une fois le système mis en place.

## Conclusion

Dans le prochain billet, je présenterai le système que je mets en place pour garantir une sauvegarde effective de mes données de travail, en suivant ces différents principes et enseignements. Si votre curiosité est piquée et que vous êtes impatients, vous pouvez d'ores et déjà vous renseigner sur un merveilleux programme utilitaire, *open-source* et *intégralement gratuit* : [Syncthing](https://syncthing.net/).

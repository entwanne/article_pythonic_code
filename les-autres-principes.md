La programmation Python repose sur d'autres principes généraux, qui sont les principes **KISS**, **DRY** et **YAGNI**.

# *Keep it simple, stupid* (*KISS*)

Ce premier principe se rapproche clairement du *Simple is better than complex*.
Le code doit toujours rester le plus simple possible, afin de rester lisible pour les autres contributeurs.

Cela s'illustre par la syntaxe même du langage, qui comprend peu de constructions différentes, mais doit aussi se retrouver dans le code produit.
Les fonctions, par exemple, doivent être dédiées à une unique fonctionnalité, de même pour les classes et leurs méthodes.
En parlant de classes, il est inutile de créer des classes trop vite, là où les types primitifs du langage pourraient répondre au besoin.

Le principe s'exprime aussi par le fait de ne pas créer de hiérarchie de classes trop complexe, et même d'ailleurs de ne pas user d'héritage quand cela n'est pas nécessaire (penser au *duck-typing*).
De même, Python dispose d'outils puissants (décorateurs, générateurs, métaclasses), qui doivent être utilisées judicieusement, quand ils ne nuisent pas à la simplicité.

# *Don't repeat yourself* (*DRY*)

Cette seconde règle a pour but d'éviter la redondance. Le code dupliqué est plus difficile à maintenir, car chaque modification doit être répercutée sur toutes les occurrences du code.

La répétition peut se comprendre à petite échelle : par exemple une même ligne répétée à deux endroits du code. Au-delà, une factorisation est nécessaire, afin de dédier une fonction à ce comportement.

# *You ain't gonna need it* (*YAGNI*)

Ce dernier principe est plus une ligne de conduite pour le processus de développement.
Il est inutile de développer maintenant une fonctionnalité qui ne servira peut-être jamais. Il est préférable de s'attaquer d'abord à ce qui est actuellement nécessaire.

Développer une fonctionnalité trop tôt présente de plus d'autres problèmes :

* Inutilisée, elle restera inconnue des autres développeurs ;
* Si elle vient à être utilisée, elle ne le sera peut-être pas dans les termes actuellement définis ;
* La fonctionnalité devra être continuellement testée tout le long du développement du projet, et potentiellement déboguée ;
* Enfin, elle pourrait entrer en conflit avec d'autres fonctionnalités requises.

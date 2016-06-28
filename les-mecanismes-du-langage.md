On reconnaît généralement un bon code Python à l'utilisation des mécanismes qui lui sont propres.

Je pense en priorité au protocole d'itération, mis en œuvre par la boucle `for`.

En Python, la boucle `for` doit toujours être privilégiée pour itérer sur un ensemble d'éléments. Si vous recourrez à une boucle `while` pour itérer, c'est probablement que vous avez un problème de conception ou méconnaissez les fonctions qui pourraient vous être utiles.
Cet ensemble d'éléments ne prend pas toujours la forme d'une liste, il peut s'agir d'un dictionnaire, d'un fichier, d'un intervalle de nombres (`range`).

Et ceci est valable pour toutes les variables qui devraient prendre des valeurs successives à chaque itération.
Ainsi, on s'orientera vers `zip` pour itérer sur plusieurs éléments à la fois, vers `enumerate` pour itérer en gardant trace de l'index dans la liste, ou encore vers des constructions plus complexes du module `itertools` que nous verrons plus loin.

Outre la boucle `for`, le protocole d'itération est aussi représenté par les listes en intension (`[x**2 for x in range(10)]`), qui doivent être utilisées dès que possible, tant qu'elles ne nuisent pas à la lisibilité bien sûr.

On retrouve aussi les générateurs (et les générateurs en intension), à utiliser quand il n'est pas nécessaire d'avoir une représentation complète de l'ensemble en mémoire.
Par exemple, si la liste en intension précédente a pour but de calculer la somme des éléments (`sum([x**2 for x in range(10)])`), on lui préférera la version utilisant un générateur, évitant des opérations inutiles : `sum(x**2 for x in range(10))`.

Les mécanismes du langage regroupent aussi les décorateurs, à utiliser à bon escient.
On reconnaît un code idiomatique à l'utilisation des décorateurs de la bibliothèque standard (`staticmethod`, `classmethod`, `property`).
La définition de ses propres décorateurs ne doit en revanche avoir lieu que si elle permet un gain net en lisibilité.

Enfin, je voudrais aborder les gestionnaires de contexte (`with`), et notamment l'ouverture de fichiers, qui doit toujours passer par l'utilisation d'un bloc `with`.
Ce bloc permet en effet d'automatiser des opérations de libération des ressources, et ce en tous les cas (déroulement normal ou erreur).

Un code pythonique se doit d'exploiter au mieux les modules de la bibliothèque standard.
Il convient alors de les connaître dans les grandes lignes, pour être en mesure de les utiliser quand le besoin se fait sentir.

Cela commence par la bonne utilisation des *builtins*[^builtins]. Savoir comment elles s'utilisent, connaître leurs paramètres (notamment le paramètre `key` des fonctions `min`, `max` et `sorted`).

Les types *builtins* sont aussi à regarder, afin d'en connaître les principales méthodes. Les exemples les plus flagrants concernent les chaînes de caractères. La concaténation y est une fonctionnalité coûteuse, et donc à déconseiller.
On lui préférera les méthodes `str.format` (concaténer et formater différentes chaînes) et `str.join` (unir un ensemble de chaînes).

Le module `collections`[^collections] est aussi très important. il comporte des structures de données essentielles au langage (`defaultdict`, `OrderedDict`, `namedtuple`, `Counter`).

Viennent ensuite les autres modules, tels que `itertools`[^itertools], `functools`[^functools] ou `operator`[^operator]. Ces modules regroupent divers utilitaires sympathiques, qui simplifient grandement le code.
En faire bon usage permet de se conformer aux standards du langage.

Enfin, suivant le domaine d'application du projet, entrent en compte les modules dédiés : `re`, `math`, `random`, `urllib`, `datetime`, `struct`, etc., et leurs propres bonnes pratiques, souvent détaillées dans la documentation.

La référence complète de la bibliothèque standard peut être trouvée ici : [https://docs.python.org/3/library/index.html]().

[^builtins]: [https://docs.python.org/3/library/functions.html]()
[^collections]: [https://docs.python.org/3/library/collections.html]()
[^itertools]: [https://docs.python.org/3/library/itertools.html]()
[^functools]: [https://docs.python.org/3/library/functools.html]()
[^operator]: [https://docs.python.org/3/library/operator.html]()

Un code pythonique se doit d'exploiter au mieux les modules de la bibliothèque standard.
Il convient alors de les connaître dans les grandes lignes, pour être en mesure de les utiliser quand le besoin se fait sentir.

# *Built-in*

Cela commence par la bonne utilisation des [fonctions *built-in*](https://docs.python.org/3/library/functions.html).
Savoir comment elles s'utilisent, connaître leurs paramètres (notamment le paramètre `key` des fonctions `min`, `max` et `sorted`).

Les [types *built-in*](https://docs.python.org/3/library/stdtypes.html) sont aussi à regarder, afin d'en connaître les principales méthodes.
Je pense par exemple à la méthode `format` des chaînes de caractères qui permet facilement de composer plusieurs valeurs en une chaîne.

```python
print('{} + {} = {}'.format(2, 3, 2 + 3))
```

Je voudrais aussi aborder les méthodes `get` et `setdefault` des dictionnaires, qui permettent de gérer facilement les éléments manquants.

```python
>>> database = {'foo': 123}
>>> database.get('bar')
>>> database.get('bar', 0)
0
>>> database.setdefault('letters', []).append('a')
>>> database.setdefault('letters', []).append('b')
>>> database
{'foo': 123, 'letters': ['a', 'b']}
```

Ou encore le constructeur des conteneurs standards (`list`, `tuple`, `dict`, `set`), qui accepte un autre itérable en paramètre.

```python
>>> names = ['Guido', 'Tim', 'Barry', 'Nick']
>>> ages = [38, 15, 52, 33]
>>> list(enumerate(names))
[(0, 'Guido'), (1, 'Tim'), (2, 'Barry'), (3, 'Nick')]
>>> dict(zip(names, ages))
{'Tim': 15, 'Barry': 52, 'Guido': 38, 'Nick': 33}
```

Nous retrouvons enfin les [exceptions *built-in*](https://docs.python.org/3/library/exceptions.html) et leur hiérarchie.

On distinguera par exemple les `TypeError` pour relever une erreur due au type d'une variable, et les `ValueError` quand la valeur est du bon type mais ne correspond pas à ce qui est attendu.
On notera aussi `IndexError` et `KeyError`, respectivement pour un index ou une clef non trouvée dans un conteneur.

# Autres modules

Le module [`collections`](https://docs.python.org/3/library/collections.html) comporte d'autres structures de données essentielles au langage : `OrderedDict`, `namedtuple`, `Counter`, ou encore `defaultdict` qui sera préférable à une utilisation systématique de `setdefault`.
Des développeurs débutants auront le réflexe de recréer ces classes, alors qu'elles sont à portée de main.

```python
>>> from collections import Counter
>>> names = ['Guido', 'Tim', 'Barry', 'Tim', 'Nick', 'Nick', 'Tim']
>>> count = Counter(names)
>>> count
Counter({'Tim': 3, 'Nick': 2, 'Guido': 1, 'Barry': 1})
>>> count['Nick']
2
>>> count['Robert']
0
```

Viennent ensuite les autres modules, tels que [`itertools`](https://docs.python.org/3/library/itertools.html), [`functools`](https://docs.python.org/3/library/functools.html) ou [`operator`](https://docs.python.org/3/library/operator.html).
Ces modules regroupent divers utilitaires sympathiques, qui simplifient grandement le code.
En faire bon usage permet de se conformer aux standards du langage.

```python
>>> from itertools import product
>>> for x, y in product(range(10), range(5)):
...     print('{} + {} = {}'.format(x, y, x + y))
...
0 + 0 = 0
0 + 1 = 1
...
9 + 3 = 12
9 + 4 = 13
```

```python
>>> import functools, operator
>>> add_3 = functools.partial(operator.add, 3)
>>> add_3(5)
8
```

Enfin, suivant le domaine d'application du projet, entrent en compte les modules dédiés : `re`, `math`, `random`, `urllib`, `datetime`, `struct`, etc., et leurs propres bonnes pratiques, souvent détaillées dans la documentation.

La référence complète de la bibliothèque standard peut être [trouvée ici](https://docs.python.org/3/library/index.html).

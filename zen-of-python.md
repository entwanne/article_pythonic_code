Tout commence par la fameuse [PEP20](https://www.python.org/dev/peps/pep-0020/), *The Zen of Python*, écrite par Tim Peters, et qui exprime les valeurs du langage.

Celle-ci énonce les règles suivant un poème. On peut la retrouver *via* l'instruction `import this` dans un interpréteur Python.

# Beautiful is better than ugly.

_Le beau est préférable au laid._

Le point de départ. Un bon code Python se doit d'être beau, c'est à dire agréable à regarder.
Nous reviendrons par la suite sur les règles de style, qui définissent plus précisément en quoi consiste un beau code.

Cela se voit en Python par l'utilisation de mots plutôt que de symboles pour certains opérateurs (`and`, `or`, `not`, `in`), qui rendent les expressions plus proches du langage naturel.

```python
if number > 0 and number not in invalid_numbers:
    ...
```

# Explicit is better than implicit.

_L'explicite est préférable à l'implicite_.

Un développeur doit pouvoir lire un code Python sans se demander sans cesse ce que fait telle ou telle ligne.
Utiliser des noms et des constructions explicites permet de limiter ce genre de problèmes.

Par exemple, en programmation objet, lors d'un héritage et de la surcharge de la méthode d'initialisation (`__init__`), il convient d'appeler explicitement la méthode de la classe parente.
Cela ne sera jamais fait automatiquement dans le dos du développeur, afin d'avoir la main sur le comportement voulu.

```python
class User:
    def __init__(self, name):
        self.name = name

class SecureUser(User):
    def __init__(self, name, password):
        super().__init__(name)
        self.password = password
```

# Simple is better than complex.

_Le simple est préférable au complexe._

Certaines structures du langage vont s'avérer plus complexes que d'autres.
L'application d'un décorateur est une instruction complexe, par les mécanismes qu'elle met en œuvre :
patron de conception décorateur, fonctions passées implicitement en paramètre.

# Complex is better than complicated.

_Le complexe est préférable au compliqué._

Il convient déjà de bien faire la différence entre les deux termes.

« compliqué » se rapporte à l'utilisation. Un code compliqué est difficile à relire et à maintenir.
Un code complexe utilise des mécanismes avancés, mais il peut être simple à appréhender.
Pour reprendre l'exemple précédent, l'application d'un décorateur n'est pas compliquée.

# Flat is better than nested.

_Le plat est préférable à l'imbriqué._

Quand on lit un code, il est facile de perdre le fil et d'oublier à quel endroit on se trouve.
D'autant plus si de nombreux niveaux d'imbrications se succèdent.

Pour palier à ce problème, on préférera produire du code plat chaque fois que cela est possible, et ainsi éviter les imbrications inutile.
Dans le cadre d'une fonction, on choisira par exemple de retourner directement quand des préconditions ne sont pas validées, plutôt que de placer le contenu de notre fonction dans plusieurs sous-niveaux de conditions.

```python
def print_items(obj):
    if not hasattr(obj, 'items'):
        return
    for item in obj.items:
        print(item)
```

# Sparse is better than dense.

_L'aéré est préférable au dense._

Un code compréhensible est un code aéré. La syntaxe même du langage se base sur l'indentation pour séparer les blocs logiques.
L'aération du code y est donc une valeur très importante.

# Readability counts.

_La lisibilité compte._

Vous, et les autres développeurs du projet, passerez probablement plus de temps à lire votre code qu'à l'écrire.
Le code se doit donc d'être lisible facilement, pour ne pas faire perdre de temps à tous.

La lisibilité passera par de nombreux points évoqués par les autres directives, mais aussi par un choix judicieux des noms de fonctions et variables par exemple.

# Special cases aren't special enough to break the rules.

_Les cas spéciaux ne le sont pas assez pour briser les règles._

Ce principe est celui de la cohérence. Les mêmes règles s'appliquent pour tous, ce n'est pas parce qu'un bout de code semble sortir du lot qu'il y déroge.
Même un code imbriqué doit rester lisible, par exemple.

# Although practicality beats purity.

_Bien que la praticité prévale sur la pureté._

Et cette règle, qui nuance la précédente, représente le bon sens.
Il peut devenir nécessaire d'outrepasser les règles pour des raisons pratiques, telles que des questions de performances.
Cela doit dans tous les cas rester anecdotique.

# Errors should never pass silently.

_Les erreurs ne devraient jamais se produire silencieusement._

Quand une erreur se produit c'est qu'il y a un problème, quel qu'il soit.
Ce problème ne doit jamais être masqué au développeur.

```python
>>> def division(a, b):
...     return a / b
...
>>> division(1, 0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 2, in division
ZeroDivisionError: division by zero
```

# Unless explicitly silenced.

_À moins d'être explicitement tues._

Le développeur peut ensuite choisir d'ignorer une erreur en particulier, car celle-ci est attendue dans ce cas précis.
Mais il le fera de façon explicite, avec un bloc `try`/`except` par exemple.

```python
def division(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        return 0
```

# In the face of ambiguity, refuse the temptation to guess.

_En cas d'ambiguïté, résister à la tentation de deviner._

Deviner implique un choix, choix qui ne sera pas forcément clair pour tous les développeurs.
S'il n'est pas clair, c'est qu'il n'est pas explicite.

Par exemple, dans le cas d'une addition entre de valeurs de types `str` et `int`, il y a ambiguïté entre le fait de choisir de convertir les deux opérandes en nombres ou en chaînes de caractères.
Aucune conversion implicite ne sera effectuée, il faudra convertir manuellement les deux opérandes en types compatibles.

```python
>>> a = '5'
>>> a + 1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: Can't convert 'int' object to str implicitly
>>> int(a) + 1
6
>>> a + str(1)
'51'
```

# There should be one -- and preferably only one -- obvious way to do it.

_Il devrait y avoir une -- et de préférence une seule -- manière évidente de le faire._

Python prône le fait qu'il existe toujours une manière optimale de procéder, et donc que toutes ne se valent pas.
Celle-ci est préférable car évidente.

Nous y reviendrons plus loin avec les mécanismes du langage, mais la manière évidente d'itérer sur des nombres est par exemple d'utiliser une boucle `for`.

```python
for i in range(100):
    print(apply_func(i))
```

# Although that way may not be obvious at first unless you're Dutch.

_Bien que cette manière ne vous semble pas évidente au premier abord, à moins que vous ne soyez néerlandais._

Cependant, l'évidence n'est pas innée. Elle vient avec la pratique, et est entre autres dictée par cette *PEP*.
La manière évidente est la manière la plus idiomatique.

Cette règle se termine par une note humoristique sur Guido van Rossum, néerlandais, le créateur de Python.

# Now is better than never.

_Maintenant est préférable à jamais._

La procrastination est l'ennemie du développeur Python.
Si vous avez besoin d'une fonctionnalité manquante, implémentez-la, ne codez pas de rustines temporaires pour y revenir « plus tard ».

# Although never is often better than *right* now.

_Bien que jamais soit souvent préférable à tout de suite._

Assurez-vous cependant que cette fonctionnalité soit vraiment nécessaire.
Dans le cas contraire, il peut être préférable de ne pas perdre trop de temps dessus pour le moment.

Ce point sera détaillé par la suite quand nous aborderons le principe *YAGNI*.

# If the implementation is hard to explain, it's a bad idea.

_Si l'implémentation est difficile à expliquer, c'est une mauvaise idée._

Une implémentation difficile à expliquer est compliquée, elle produira du code compliqué.
On préférera donc l'éviter au profit d'une implémentation plus simple, plus facile à expliquer.

# If the implementation is easy to explain, it may be a good idea.

_Si l'implémentation est facile à expliquer, il peut s'agir d'une bonne idée._

Pour autant, être facile à expliquer n'en fait pas une bonne implémentation.
C'est une bonne chose, mais ce n'est pas un critère suffisant.

Il est facile d'expliquer comment concaténer plusieurs chaînes de caractères : on itère sur notre ensemble de chaînes, et on les concatène chacune à une chaîne finale à l'aide de l'opérateur `+`.
Pourtant, celle solution est à proscrire, dû à l'inefficacité de l'opérateur de concaténation, et à la présence d'une méthode `join` bien plus lisible.

```python
>>> tags = ['<html>', '<body>', '<p>', 'text', '</p>', '</body>', '</html>']
>>> ''.join(tags)
'<html><body><p>text</p></body></html>'
```

# Namespaces are one honking great idea -- let's do more of those!

_Les espaces de noms sont une sacrée bonne idée -- utilisons-les plus souvent !_

Les espaces de noms sont créés à l'aide des paquets, modules et objets, ils permettent de diviser les classes et fonctions en ensembles logiques.
Ils évitent aussi les conflits de noms, un même nom pouvant être utilisé pour des valeurs différentes dans des espaces différents.
On aimera alors en user pour bien classifier nos objets.

```python
import math, cmath

print(math.exp(0))
print(cmath.exp(0))
```

# Fin ?

Tim Peters avait initialement annoncé que son *Zen of Python* contiendrait 20 directives.
Si vous y avez prêté attention, on en compte plutôt 19. Où est passée cette fameuse 20ème règle ?

Certains évoquent qu'elle pourrait être implicite, une simple ligne vide. Une ligne vide qui rappellerait l'aération.

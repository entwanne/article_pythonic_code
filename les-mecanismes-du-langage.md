On reconnaît généralement un bon code Python à l'utilisation des mécanismes qui lui sont propres.

# *Unpacking*

Un premier point à aborder est celui de l'*unpacking* (ou déconstruction), une technique qui permet l'assignation de plusieurs variables en une seule instruction.

Vous l'avez probablement déjà rencontré comme exemple pour échanger les valeurs de deux variables.

```python
>>> a = 5
>>> b = 2
>>> a, b = b, a
>>> print(a, b)
2 5
```

Ce qui se passe en interne lors de la 3ème ligne est la création d'un *tuple* `(b, a)`, qui est ensuite déconstruit et son contenu stocké dans les variables `a` et `b`.

Mais l'*unpacking* ne se limite pas à cela, et permet aussi de déconstruire des structures imbriquées (*tuples*, listes, chaînes de caractères, dictionnaires).

```python
>>> l = [0, (1, 2, {3: 'foo', 4: 'bar'}), 5]
>>> a, (b, c, (d, e)), f = l
>>> print(a, b, c, d, e, f)
0 1 2 3 4 5
>>> x, y, z = 'bar'
>>> print(x, y, z)
b a r
```

L'*unpacking* est une manière élégante de séparer les éléments d'une liste, il est donc courant de l'employer en Python.

Nous n'aborderons pas ici les constructions plus complexes de l'*unpacking*, rendue possible grâce à l'opérateur *splat*, comme [décrit ici](https://zestedesavoir.com/articles/175/sortie-de-python-3-5/#2-principales-nouveautes).

# Conditions

Toute valeur en Python peut s'évaluer sous forme d'un booléen, il n'est donc pas nécessaire de la convertir préalablement.
Les valeurs `None`, `0` et le conteneurs vides (`''`, `()`, `[]`, `set()`, etc.) s'évaluent à `False`.
Les autres nombres, les conteneurs non vides, et plus généralement toute valeur qui n'est pas explicitement fausse s'évaluent à `True`.

Ainsi, pour tester si une chaîne `s` n'est pas vide, il suffit de faire une condition sur `s`. On ne convertira jamais la valeur en booléen pour la comparer à `True` ou `False`.

```python
if s:
    print("s n'est pas vide")
```

L'usage de ternaires est aussi à privilégier quand on souhaite évaluer des expressions conditionnelles courtes.

```python
name = user.name if user is not None else 'anonymous'
```

On notera l'utilisation de l'opérateur `is` pour la comparaison avec `None`. Ce dernier étant une constante unique, `is` permet d'en assurer la singularité.

# Boucle `for`

Un mécanisme important du langage est le protocole d'itération, mis en œuvre par la boucle `for`.

En Python, la boucle `for` doit toujours être privilégiée pour itérer sur un ensemble d'éléments. Si vous recourrez à une boucle `while` pour itérer, c'est probablement que vous avez un problème de conception ou méconnaissez les fonctions qui pourraient vous être utiles.
Cet ensemble d'éléments ne prend pas toujours la forme d'une liste, il peut s'agir d'un dictionnaire, d'un fichier, d'un intervalle de nombres (`range`).

Et ceci est valable pour toutes les variables qui devraient prendre des valeurs successives à chaque itération.
Ainsi, on s'orientera vers `zip` pour itérer sur plusieurs éléments à la fois, vers `enumerate` pour itérer en gardant trace de l'index dans la liste, ou encore vers des constructions plus complexes du module `itertools` que nous verrons plus loin.

```python
names = ['Guido', 'Tim', 'Barry', 'Nick']
ages = [38, 15, 52, 33]

for i, (name, age) in enumerate(zip(names, ages)):
    print(i, name, age)
```

Nous retrouvons dans cette construction l'*unpacking* abordé plus haut, qui peut donc s'utiliser aussi pour les boucles `for`.

# Listes en intension

Outre la boucle `for`, le protocole d'itération est aussi représenté par les listes en intension, qui doivent être utilisées dès que possible, tant qu'elles ne nuisent pas à la lisibilité bien sûr.

Pour construire la liste des carrés des nombres de 0 à 9, on utilisera par exemple le code suivant, plutôt qu'une boucle multi-lignes et un remplissage de liste manuel.

```python
squares = [i**2 for i in range(10)]
```

On retrouve la même construction pour les dictionnaires en intension.

```python
squares = {i: i**2 for i in range(10)}
```

# Générateurs

Un autre mécanisme est celui des générateurs (et des générateurs en intension), à utiliser quand il n'est pas nécessaire d'avoir une représentation complète d'un ensemble en mémoire.
Si notre liste `squares` a simplement pour but de calculer la somme des éléments (`sum(squares)`), nous lui préférerons la version utilisant un générateur, évitant ainsi le stockage inutile de la liste.

```python
sum_squares = sum(x**2 for x in range(10))
```

# Exceptions

La gestion d'erreurs est réalisée en Python à l'aide d'un mécanisme d'exceptions, mais les exceptions ne se limitent pas à cela.
Le protocole d'itération décrit plus haut s'appuie par exemple sur une exception `StopIteration` levée en fin de boucle.

Vos traitements défectueux doivent toujours remonter une exception adaptée au problème, et décrivant au mieux sa raison.
Les types d'exceptions sont généralement hiérarchisés de façon à représenter le problème à différents niveaux d'abstractions.

Si vous êtes par exemple amené à développer une bibliothèque, il est courant que toutes ses exceptions héritent d'une même base permettant facilement d'attraper toutes les erreurs de la bibliothèque.
Dans le cas d'un champ manquant lors de l'analyse du fichier de configuration d'un composant de votre bibliothèque `mylib`, vous pourriez avoir une exception de type `mylib.FieldMissingError` héritant de `mylib.ParseError` et elle même de `mylib.Error`.

De l'autre côté, il est conseillé d'attraper judicieusement les exceptions.
Si vous souhaitez traiter un tel problème de champ manquant, vous attraperez l'exception `mylib.FieldMissingError` plutôt que `mylib.Error` qui serait ici trop générale.

# Décorateurs

Les décorateurs, utilisés à bon escient, sont aussi une particularité du langage.
On reconnaît un code idiomatique à l'utilisation des décorateurs de la bibliothèque standard (`staticmethod`, `classmethod`, `property`).

```python
class Circle:
    def __init__(self, cx, cy, radius):
        self.cx, self.cy = cx, cy
        self.radius = radius

    @classmethod
    def from_diameter(cls, ax, ay, bx, by):
        cx, cy = (ax + bx) / 2, (ay + by) / 2
        radius = ((ax - bx)**2 + (ay - by)**2)**0.5 / 2
        return cls(cx, cy, radius)

    @property
    def area(self):
        return math.pi * self.radius**2
```

La définition de ses propres décorateurs ne doit en revanche avoir lieu que si elle permet un gain net en lisibilité par rapport aux autres solutions envisagées.

# Gestionnaires de contextes

Enfin, je voudrais aborder les gestionnaires de contexte (`with`), et notamment l'ouverture de fichiers, qui doit toujours passer par l'utilisation d'un bloc `with`.
Ce bloc permet en effet d'automatiser des opérations de libération des ressources, et ce en tous les cas (déroulement normal ou erreur).

```python
with open('hello.txt', 'w') as hello_file:
    print('Hello World!', file=hello_file)
```

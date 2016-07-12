Les règles de style permettent d'assurer une certaine lisibilité d'un code, elles sont un socle commun à tous les projets Python.
Ces règles sont énoncées par la [PEP8](https://www.python.org/dev/peps/pep-0008/).

Le premier principe à respecter est la cohérence. Il se peut que vous ayez affaire à une bibliothèque ne respectant pas la PEP8.
Dans ce cas, adaptez-vous au style de cette bibliothèque. La concordance avec les règles de style générales passe en second plan.

Aussi, la lisibilité prévaut sur tout le reste. Si, dans votre cas précis, une règle nuit à la compréhension d'une ligne, ne l'appliquez pas. *Practicability beats purity*.

Je ne vais pas détailler ici l'ensemble des directives, je vous laisse consulter la PEP pour cela.
Retenez qu'elle concerne l'indentation et l'aération, les imports, les commentaires, les conventions de nommage, et d'autres recommandations plus générales.

Les commentaires sont très importants pour la compréhension du code.
Ils expliquent comment fonctionne le code et pourquoi il est implémenté de telle manière.
Ils sont complétés par les *docstrings*, des chaînes de caractères en en-tête des modules, classes et fonctions qui permettent de les documenter (d'expliquer comment s'utilise le code).
Les *docstrings* d'un objet Python sont accessibles *via* la fonction `help` appelée sur cet objet.
On y retrouvera d'autres informations telles que les annotations (spécifications des types des paramètres et du type de retour des fonctions).

```python
>>> def addition(a : int, b : int) -> int:
...     "Return the sum of numbers `a` and `b`."
...     return a + b
...
>>> help(addition)
```

Sachez aussi que des outils sont à votre disposition pour analyser le style de votre code et son respect des conventions.
Ils sont divers et variés, mais les deux plus connus sont probablement `pylint` et `flake8`.

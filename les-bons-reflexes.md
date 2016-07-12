En premier lieu, il faut bien sûr se relire en faisant attention aux divers principes et règles énoncés.
Voire se faire relire par un tiers lorsque cela est possible.

Vous l'aurez compris, un autre réflexe sera de s'imprégner de la bibliothèque standard, et de s'assurer pour chaque fonctionnalité que l'on s'apprête à implémenter que celle-ci n'y existe pas déjà.

La fonction `help` permet aussi d'obtenir plus d'informations sur un module, un type, une fonction, ou même un mécanisme du langage.
Elle offre ainsi un accès rapide à la documentation directement depuis votre interpréteur interactif.
Utilisée sans paramètre, `help` propose aussi une aide interactive.

```python
>>> import itertools
>>> help(itertools)
>>> help(str)
>>> help(max)
>>> help('for')
>>> help()
```

Il conviendra aussi de connaître les bibliothèques tierces, dans une moindre mesure, afin de savoir trouver une bibliothèque répondant à un besoin précis.
Il n'est pas nécessaire de toutes les connaître sur le bout des doigts, ni de sortir une usine à gaz pour une petite fonctionnalité, mais simplement de ne pas réinventer la roue.

Les paquets Python sont généralement publiés sur le [PyPI](https://pypi.python.org/pypi), ce qui en fait un répertoire de choix pour trouver une bibliothèque.

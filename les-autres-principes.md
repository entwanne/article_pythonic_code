La programmation Python repose sur d'autres principes généraux, décrits dans cette section.

# Keep it simple, stupid (*KISS*)

_Garde ça simple, stupide_

Ce premier principe se rapproche clairement du *Simple is better than complex*.
Le code doit toujours rester le plus simple possible, afin de rester lisible pour les autres contributeurs.

Cela s'illustre par la syntaxe même du langage, qui comprend peu de constructions différentes, mais doit aussi se retrouver dans le code produit.
Les fonctions, par exemple, doivent être dédiées à une unique fonctionnalité, de même pour les classes et leurs méthodes.

En parlant de classes, il est inutile de créer de nouvelles classes trop vite, là où les types primitifs du langage pourraient répondre au besoin.
Par exemple, pour un objet qui ne contiendrait que des données, associées à aucune méthode, un dictionnaire fait très bien l'affaire.

```python
user = {'username': 'guido', 'realname': 'Guido van Rossum', 'password': '12345'}
```

Le principe s'exprime aussi par le fait de ne pas créer de hiérarchie de classes trop complexe, et même d'ailleurs de ne pas user d'héritage quand ce n'est pas nécessaire (penser au *duck-typing*).
De même, Python dispose d'outils puissants (décorateurs, générateurs, métaclasses), qui doivent être utilisés judicieusement, quand ils ne nuisent pas à la simplicité.

# Don't repeat yourself (*DRY*)

_Ne te répète pas_

Cette seconde règle a pour but d'éviter la redondance. Le code dupliqué est plus difficile à maintenir, car chaque modification doit être répercutée sur toutes les occurrences du code.

La répétition peut se comprendre à petite échelle : par exemple une même ligne répétée à deux endroits du code. Au-delà, une factorisation est nécessaire, afin de dédier une fonction à ce comportement.

```python
import sys
import random

def errlog(template, *args):
    print(template.format(*args), file=sys.stderr)

secret = random.randint(0, 100)
guess = int(input('Entrez un nombre entre 0 et 100: '))

if guess < secret:
    errlog('Nombre {} trop petit', guess)
elif guess > secret:
    errlog('Nombre {} trop grand', guess)
...
```

Notre fonction `errlog` permet ici de factoriser le formatage et l'affichage de messages d'erreur.

# You ain't gonna need it (*YAGNI*)

_Tu n'en auras pas besoin_

Ce principe est plus une ligne de conduite pour le processus de développement.
Il est inutile de développer maintenant une fonctionnalité qui ne servira peut-être jamais. Il est préférable de s'attaquer d'abord à ce qui est actuellement nécessaire.

Développer une fonctionnalité trop tôt présente de plus d'autres problèmes :

* Inutilisée, elle restera inconnue des autres développeurs ;
* Si elle vient à être utilisée, elle ne le sera peut-être pas dans les termes actuellement définis ;
* La fonctionnalité devra être continuellement testée tout le long du développement du projet, et potentiellement déboguée ;
* Enfin, elle pourrait entrer en conflit avec d'autres fonctionnalités requises.

# We're all consenting adults here

_Nous sommes ici entre adultes consentants_

Ou plus clairement, les développeurs sont conscients et responsables de leurs actes.
Cela s'illustre par la manière de protéger des attributs en Python, en les préfixant par un `_`.

En soi, rien n'empêche d'accéder depuis l'extérieur à un tel attribut.
Mais le préfixe signale au développeur qu'il accède à un état interne, que sa modification pourrait compromettre le comportement normal de l'objet, et qu'il le fait donc en connaissance de cause.

```python
class MyObject:
    def __init__(self):
        self._internal = 'internal state'

obj = MyObject()
print(obj._internal)
```

En parlant d'attributs, on préférera toujours en Python un accès direct aux attributs plutôt que des méthodes *getter*/*setter*.
Quitte à passer par des propriétés s'il est nécessaire que la récupération ou la modification de l'attribut soit dynamique.

# *Easier to ask forgiveness than permission* (*EAFP*)

_Il est plus facile de demander pardon que la permission_

Python fait partie des langages qui considèrent qu'il est plus simple d'essayer puis de gérer les erreurs, que de demander la permission en amont.

Pour gérer l'ouverture d'un fichier, par exemple, on préférera faire appel à `open`, et traiter les différentes exceptions qui pourraient se produire (fichier inexistant, droits insuffisants, etc.), plutôt que de tester une à une ces différentes conditions.

```python
try:
    with open('filename', 'r') as f:
        handle_file(f)
except FileNotFoundError as e:
    errlog('Fichier {!r} non trouvé', e.filename)
except PermissionError as e:
    errlog('Fichier {!r} non lisible', e.filename)
```

Cette manière de procéder a aussi l'avantage d'être plus sûre en Python. En effet, dans le cas où l'on testerait d'abord l'existence du fichier, rien ne nous garantit qu'il serait toujours présent au moment de l'ouverture proprement dite (il peut être supprimé par un autre programme entretemps).

Ce principe s'oppose au *LBYL* (*Look before you leap*, *Regarde avant d'essayer*), préconisé par d'autres langages comme le C.

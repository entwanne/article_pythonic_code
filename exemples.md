Pour terminer, je voudrais présenter quelques exemples de mauvais code, et leur équivalent pythonique.

# Boucle de construction d'une liste

## Pas bien

```python
squares = []
i = 0
while i < 10:
    squares.append(i**2)
    i += 1
```

## Bien

```python
squares = [i**2 for i in range(10)]
```

# Itérations numérotées et formatage de chaînes

## Pas bien

```python
names = ['John', 'Peter', 'Jack']

i = 0
for name in names:
    print('names[' + str(i) + '] = ' + name)
    i += 1
```

## Bien

```python
names = ['John', 'Peter', 'Jack']

for i, name in enumerate(names):
    print('names[{}] = {}'.format(i, name))
```

# Construction d'un dictionnaire à partir de deux listes

## Pas bien

```python
names = ['John', 'Peter', 'Jack']
ages = [38, 15, 52]

names_ages = {}
for i, name in enumerate(names):
    names_ages[name] = ages[i]
```

## Bien

```python
names = ['John', 'Peter', 'Jack']
ages = [38, 15, 52]

names_ages = dict(zip(names, ages))
```

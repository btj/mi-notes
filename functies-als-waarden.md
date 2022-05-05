# Functies als waarden

Beschouw de volgende functie die het kleinste element van een niet-lege lijst teruggeeft:

```python
def min(values):
    result = values[0]
    for x in values:
        if x < result:
            result = x
    return result
```

Deze functie werkt goed voor eenvoudige gegevens:
```python
assert min([30, 10, 20]) == 10
assert min(['C', 'A', 'B']) == 'A'
```
Kunnen we deze functie echter veralgemenen zodat we haar ook kunnen toepassen op complexe gegevens met toepassings-specifieke noties van "kleiner dan"? Beschouw bijvoorbeeld de volgende lijst van studenten met hun voornaam, hun geboortedatum, en hun behaalde credits:
```python
studenten = [
  ('Elke', (2005, 6, 24), 90),
  ('Arne', (2004, 8, 1), 60),
  ('Jan', (2005, 7, 15), 30)
]
```
Kunnen we een versie maken van de `min`-functie die we kunnen gebruiken om bijvoorbeeld de student met de alfabetisch "kleinste" naam (Arne), de jongste student (Arne), de student met de vroegste verjaardag (Elke), of de student met het kleinste aantal credits (Jan) te vinden?

Ja, dat kunnen we, door als extra argument aan `min` een *functie* door te geven die voor een gegeven element van de lijst de vergelijkingssleutel teruggeeft:

```python
def min(values, key_func):
    result = values[0]
    for x in values:
        if key_func(x) < key_func(result):
            result = x
    return result

def student_naam(s): return s[0]
def student_geboortedatum(s): return s[1]
def student_verjaardag(s): return s[1][1:]
def student_credits(s): return s[2]

assert min(studenten, student_naam)[0] == 'Arne'
assert min(studenten, student_geboortedatum)[0] == 'Arne'
assert min(studenten, student_verjaardag)[0] == 'Elke'
assert min(studenten, student_credits)[0] == 'Jan'
```
Deze veralgemeende `min`-functie vergelijkt niet de elementen zelf, maar hun vergelijkingssleutels. De `min`-functie vraagt de vergelijkingssleutel van een gegeven element op door de meegegeven sleutelfunctie op te roepen met het element als argument.

Deze `min`-functie is een voorbeeld van een *hogere-orde-functie*, een functie die een functie als argument neemt of als resultaat teruggeeft.

Functies in Python zijn dus gewoon waarden, net zoals getallen, strings, tuples, de Booleaanse waarden `True` en `False`, enz. ook waarden zijn. Net zoals andere waarden kan je functies in Python doorgeven als argumenten aan functies, teruggeven als resultaat van functies, toekennen aan variabelen, en opslaan in collectie-objecten zoals lijsten, tuples, sets of dictionaries.

Hier is nog een voorbeeld:
```python
def plus(x, y): return x + y
def minus(x, y): return x - y
def maal(x, y): return x * y
def gedeeld_door(x, y): return x / y

operaties = {
  '+': plus,
  '-': minus,
  '*': maal,
  '/': gedeeld_door
}

def reken_uit(waarde1, operatie, waarde2):
    return operaties[operatie](waarde1, waarde2)

assert reken_uit(10, '+', 20) == 30
assert reken_uit(10, '*', 20) == 200
assert reken_uit(10, '-', 20) == -10
assert reken_uit(10, '/', 20) == 0.5
```

### Oefeningen

- Schrijf een functie `map_pair` zodat de volgende test cases slagen:
  ```python
  def plus1(x): return x + 1
  def maal2(x): return x * 2

  assert map_pair(plus1, (3, 5)) == (4, 6)
  assert map_pair(plus1, (7, 3)) == (8, 4)
  assert map_pair(maal2, (3, 5)) == (6, 10)
  assert map_pair(maal2, (7, 3)) == (14, 6)
  ```
- Schrijf een functie `herhaal` zodat de volgende test cases slagen:
  ```python
  def plus1(x): return x + 1
  def vet(x): return '*' + x + '*'

  assert herhaal(3, plus1, 10) == 13
  assert herhaal(2, vet, 'echt') == '**echt**'
  ```
  Merk op dat `herhaal(0, plus1, 10) == 10`, `herhaal(1, plus1, 10) == plus1(10)`, `herhaal(2, plus1, 10) == plus1(plus1(10))`, enzovoort.
- Schrijf een functie `map` zodat de volgende test cases slagen:
  ```python
  def plus1(x): return x + 1
  def str_upper(x): return x.upper()

  assert map(plus1, [10, 20, 30]) == [11, 21, 31]
  assert map(str_upper, ['foo', 'bar']) == ['FOO', 'BAR']
  ```
  Merk op dat de `map`-functie eigenlijk overbodig is: je kan de voorbeelden beknopter schrijven met *list comprehensions* als volgt:
  ```python
  assert [x + 1 for x in [10, 20, 30]] == [11, 21, 31]
  assert [x.upper() for x in ['foo', 'bar']] == ['FOO', 'BAR']
  ```
- Schrijf een functie `filter` zodat de volgende test cases slagen:
  ```python
  def is_kleiner_dan_nul(x): return x < 0
  def begint_met_M(x): return x.startswith('M')

  assert filter(is_kleiner_dan_nul, [10, -20, 30, -40]) == [-20, -40]
  assert filter(begint_met_M, ['Adam', 'Bert', 'Mark', 'Jan', 'Mia']) == ['Mark', 'Mia']
  ```
  Merk op dat de `filter`-functie eigenlijk overbodig is: je kan de voorbeelden beknopter schrijven met list comprehensions als volgt:
  ```python
  assert [x for x in [10, -20, 30, -40] if x < 0] == [-20, -40]
  assert [x for x in ['Adam', 'Bart', 'Mark', 'Jan', 'Mia'] if x.startswith('M')] == ['Mark', 'Mia']
  ```
- Schrijf een functie `reduce` zodat de volgende test cases slagen:
  ```python
  def plus(x, y): return x + y
  def maal(x, y): return x * y

  assert reduce(plus, [10, 20, 30, 40]) == 100
  assert reduce(maal, [10, 20, 30, 40]) == 240000
  assert reduce(min, [10, 20, 30, 40]) == 10
  assert reduce(max, [10, 20, 30, 40]) == 40
  ```
  Merk op dat `reduce(plus, [10, 20, 30, 40]) == plus(plus(plus(10, 20), 30), 40)`.

## Lambda-uitdrukkingen

Als je een functie enkel definieert om haar op één plaats als waarde te gebruiken, en het functielichaam bestaat enkel uit een `return`-opdracht, dan kan je dit beknopter schrijven door een *lambda-uitdrukking* te gebruiken. We kunnen bijvoorbeeld de definities van de functies `student_naam`, `student_verjaardag`, `plus`, `min`, `maal`, en `gedeeld_door` in de voorbeelden hierboven elimineren door een lambda-uitdrukking te schrijven op de plaats waar we deze functies gebruiken als waarde:

```python
assert min(studenten, lambda s: s[0]) == 'Arne'
assert min(studenten, lambda s: s[1][1:]) == 'Elke'

operaties = {
  '+': lambda x, y: x + y,
  '-': lambda x, y: x - y,
  '*': lambda x, y: x * y,
  '/': lambda x, y: x / y
}
```

De uitdrukking `lambda x, y: x + y` stelt de functie voor die twee argumenten neemt en hun som teruggeeft als resultaat.

- Schrijf alle bovenstaande test cases voor `map_pair`, `herhaal`, `map`, `filter`, en `reduce` met behulp van lambda-uitdrukkingen, zodat je de functies `plus1`, `maal2`, `vet`, enzovoort niet meer hoeft te definiëren.

## Geneste functies

We kunnen functies definiëren in het lichaam van andere functies. Beschouw bijvoorbeeld de functie `min_by_element` hieronder, die het kleinste element teruggeeft van de gegeven lijst van tuples, waarbij als vergelijkingssleutel het `k`de element van elke tuple gebruikt wordt:
```python
def min_by_element(values, k):
    def kth(value): return value[k]
    return min(values, kth)

assert min_by_element(studenten, 0) == 'Arne'
assert min_by_element(studenten, 1) == 'Arne'
assert min_by_element(studenten, 2) == 'Jan'
```
We noemen de functie `kth` een *geneste functie*; haar definitie is genest binnen die van `min_by_element`. Merk op dat een geneste functie gebruik kan maken van de lokale variabelen van de omsluitende functie (zoals de parameter `k` in het voorbeeld).

We kunnen deze functie ook korter schrijven met een lambda-uitdrukking:
```python
def min_by_element(values, k):
    return min(values, lambda s: s[k])
```

## Functies die functies teruggeven

We kunnen hetzelfde effect ook als volgt bereiken:
```python
def kth_func(k):
    return lambda value: value[k]

assert min(studenten, kth_func(0)) == 'Arne'
assert min(studenten, kth_func(1)) == 'Arne'
assert min(studenten, kth_func(2)) == 'Jan'
```
De functie `kth_func` geeft, gegeven een getal `k`, een functie terug die van een gegeven tuple het `k`-de element teruggeeft.

### Oefeningen

- Schrijf een functie `above` zodat de volgende test cases slagen:
  ```python
  assert list(filter(above(10), [5, 7, 10, 12, 15])) == [12, 15]
  assert list(filter(above('M'), ['Adam', 'Bert', 'Mark', 'Peter', 'Zidan'])) == ['Mark', 'Peter', 'Zidan']
  ```
  (We passen `list` toe op het resultaat van `filter` omdat de ingebouwde `filter`-functie van Python een *iterator* teruggeeft. Dit is geen lijst maar je kan een iterator wel converteren naar een lijst.)
  (Merk op dat `<` in Python ook werkt op strings: voor strings `x` en `y` geeft `x < y` terug of `x` voor `y` komt in het alfabet. Voor woorden van meerdere tekens past Python de lexicografische volgorde toe.)
- Schrijf een functie `prefix` zodat de volgende test cases slagen:
  ```python
  assert list(map(prefix('_'), ['aap', 'koe', 'slang'])) == ['_aap', '_koe', '_slang']
  assert list(map(prefix('rare '), ['aap', 'koe', 'slang'])) == ['rare aap', 'rare koe', 'rare slang']
  ```
  (We passen `list` toe op het resultaat van `map` omdat de ingebouwde `map`-functie van Python een *iterator* teruggeeft. Dit is geen lijst maar je kan een iterator wel converteren naar een lijst.)

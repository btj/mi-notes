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

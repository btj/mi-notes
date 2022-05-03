# Recursieve datastructuren

## Uitdrukkingen

Eén manier om de wiskundige uitdrukking (10 + 5) * 3 voor te stellen in Python is als volgt:
```python
uitdrukking = ('*', ('+', 10, 5), 3)
```

- Schrijf een functie die nagaat of een waarde een geldige uitdrukking is. Een geldige uitdrukking is ofwel een `int`, ofwel een tuple met drie elementen, waarvan het eerste een string is met als inhoud `+`, `-`, `*`, of `/`, en het tweede en derde een geldige uitdrukking is. Gebruik `type(x) == tuple` of `type(x) == int` of `type(x) == str` om na te gaan of een waarde `x` een tuple, een `int`, of een string is. Je moet dus een functie `is_geldige_uitdrukking` schrijven zodat `is_geldige_uitdrukking(x)` `True` teruggeeft als `x` een geldige uitdrukking is, en `False` als `x` geen geldige uitdrukking is.
- Schrijf een functie die een gegeven uitdrukking uitrekent. Voor het voorbeeld moet dit dus 45 teruggeven. Om een bewerking uit te voeren: kijk eerst of het een `+` is; zo niet, kijk of het een `-` is; zo niet, kijk of het een `*` is, enz.
- Stel dat een uitdrukking ook variabelenamen kan bevatten. Bv.: `('*', ('+', 'x', 'y'), 'z')`. Schrijf een functie die, gegeven een dict die variabelenamen afbeeldt op hun waarde, een gegeven uitdrukking uitrekent. Gegeven de dict `{'x': 10, 'y': 5, 'z': 3}` moet dit voor de voorbeelduitdrukking dus 45 teruggeven.
- Schrijf een functie die een uitdrukking met variabelen neemt en een dict die variabelenamen afbeeldt op uitdrukkingen. De functie moet de uitdrukking teruggeven die je krijgt als je de variabelenamen vervangt door de overeenkomstige uidrukkingen. Bv. `('+', 'x', 'x')` met dict `{'x': ('-', 'y', 'y')}` moet `('+', ('-', 'y', 'y'), ('-', 'y', 'y'))` teruggeven.

## Bestanden en mappen

Een *item* op je computer is ofwel een bestand ofwel een map. Een map kan bestanden bevatten, maar ook mappen.
Stel bijvoorbeeld dat de map Documenten drie items bevat: het bestand `hello.py`, het bestand `boodschappen.txt`, en de map `Vakken`. Die map bevat zelf de twee mappen `Analyse 1` en `MI`. De map `Analyse 1` bevat de twee bestanden `voorbeeldexamen.txt` en `Cursustekst.txt`. De map `MI` bevat het bestand `notities.txt`. We kunnen dit in Python voorstellen als volgt:
```python
item = ('Documenten', [
  ('hello.py', 'print("Hello world!")'),
  ('boodschappen.txt', 'melk, boter, brood'),
  ('Vakken', [
     ('Analyse 1', [
        ('voorbeeldexamen.txt', 'Wat is de afgeleide van x^2 in x?'),
        ('Cursustekst.txt', 'De afgeleide van x^2 is 2x. De afgeleide van x is 1.')
      ]),
     ('MI', [
        ('notities.txt', 'Functioneel programmeren is tof!')
      ])
   ])
])
```

- Schrijf een functie die nagaat of een waarde een geldig item is. Een geldig item is een tuple van lengte 2, met als eerste element een string en als tweede element ofwel een string ofwel een lijst van geldige items. Gebruik `type(x) == tuple` of `type(x) == str` of `type(x) == list` om na te gaan of `x` een tuple, een string, of een lijst is. Je moet dus een functie `is_geldig_item` schrijven zodat `is_geldig_item(x)` `True` teruggeeft als `x` een geldig item is, en `False` als `x` geen geldig item is.
- Schrijf een functie die het totale aantal bestanden in een item telt. Het item `Documenten` hierboven bevat bv. 5 bestanden.
- Schrijf een functie die de totale lengte van alle bestanden in een item teruggeeft (dus het totale aantal tekens in de inhouden van alle bestanden). Voor het voorbeeld moet dit 156 teruggeven.
- Schrijf een functie die een lijst teruggeeft met alle bestanden (naam en inhoud) in een gegeven item. Voor Documenten zijn dat er dus vijf. De functie moet dus een lijst van tuples teruggeven. (Merk op: `lijst.append(andereLijst)` voegt `andereLijst` toe als element aan `lijst`; je krijgt dan een lijst van lijsten. `lijst += andereLijst` daarentegen voegt de *elementen* van `andereLijst` toe aan `lijst`.)
- Schrijf een functie die een kopie van een item teruggeeft waarin alle item-namen geconverteerd zijn naar kleine letters. (Gebruik `x.lower()` om een kopie van de string `x` te krijgen geconverteerd naar kleine letters.)

## Stambomen

Stel dat Jan uit zijn huwelijk met Mia drie kinderen had: Piet, Elke, en Veerle. Piet is nooit getrouwd. Elke heeft uit haar huwelijk met David twee kinderen: Leen en Erik. Veerle heeft uit haar huwelijk met Karel geen kinderen, en uit een later huwelijk met Peter een kind: Laurens. Laurens heeft uit zijn huwelijk met Els twee kinderen: Stef en Mark.

Dit kunnen we als volgt voorstellen in Python:
```python
stamboom = (
  ('Jan', [
    ('Mia', [
       ('Piet', []),
       ('Elke', [
          ('David', [
             ('Leen', []),
             ('Erik', [])
           ])
        ]),
       ('Veerle', [
          ('Karel', []),
          ('Peter', [
             ('Laurens', [
                ('Els', [
                   ('Stef', []),
                   ('Mark', [])
                 ])
              ])
           ])
        ])
     ])
   ])
)
```

- Schrijf een functie die nagaat of een waarde een geldige stamboom is en een functie die nagaat of een waarde een geldig huwelijk is. Een geldige stamboom is een tuple van lengte 2, met als eerste element een string en als tweede element een lijst van geldige huwelijken. Een geldig huwelijk is een tuple met als eerste element een string en als tweede element een lijst van geldige stambomen. Gebruik `type(x) == str` of `type(x) == tuple` of `type(x) == list` om na te gaan of `x` een string is of een tuple of een lijst.

- Schrijf een functie die nagaat hoeveel afstammelingen een persoon met een gegeven stamboom heeft. Jan heeft bijvoorbeeld 8 afstammelingen: Piet, Elke, Leen, Erik, Veerle, Laurens, Stef, en Mark.
- Schrijf een functie die een set teruggeeft met de afstammelingen van een persoon met een gegeven stamboom.
- Schrijf een functie die de diepte van een gegeven stamboom teruggeeft. De diepte van de stamboom van Jan is 3 want hij heeft achterkleinkinderen maar geen achter-achterkleinkinderen.
- Schrijf een functie de een set teruggeeft met de afstammelingen van een persoon met een gegeven stamboom die een gegeven aantal generaties jonger zijn. Bijvoorbeeld: Stef en Mark zijn drie generaties jonger dan Jan.

## Zoekbomen

Eén mogelijke manier om een vertaalwoordenboek voor te stellen in Python is als volgt:
```python
woordenboek = (
  ('marriage', 'huwelijk',
     ('ghost', 'geest',
        ('dad', 'pa',
           (),
           ()),
        ('kid', 'kind',
           (),
           ())),
     ('sad', 'treurig',
        ('paw', 'poot',
           ('old', 'oud',
              (),
              ()),
           ()),
        ('world', 'wereld',
           (),
           ())))
)
```
Dit is een voorbeeld van een *binaire zoekboom*: het woordenboek is een tuple met vier elementen: een Engels woord, de Nederlandse vertaling, een deelwoordenboek met woorden die voorafgaan aan het Engelse woord in het alfabet, en een deelwoordenboek met woorden die volgen op het Engelse woord in het alfabet. Een leeg (deel)woordenboek wordt voorgesteld door een leeg tuple.

- Schrijf een functie die nagaat of een gegeven waarde een geldig woordenboek is waarvan de Engelse woorden tussen twee gegeven woorden W1 en W2 liggen in het alfabet. Dit is het geval als het een leeg tuple is, of een tuple met vier elementen: een string W die tussen W1 en W2 ligt, een string, een geldig woordenboek waarvan de woorden tussen W1 en W liggen, en een geldig woordenboek waarvan de woorden tussen W en W2 liggen.
- Schrijf een functie die nagaat of een gegeven waarde een geldig woordenboek is. Dit is het geval als het een geldig woordenboek is waarvan de Engelse woorden tussen `''` en `'zzzz'` liggen. (Alle woorden liggen immers tussen die twee woorden.)
- Schrijf een functie die gegeven zo'n woordenboek de Nederlandse vertaling teruggeeft voor een gegeven Engels woord, of `None` als het gegeven woord niet in het woordenboek voorkomt.
- Schrijf een functie die een woordenboek in deze vorm omzet naar een dict. (Merk op: je kan twee dicts `x` en `y` samenvoegen met `x | y`.)
- Schrijf een functie die, gegeven een woordenboek, een nieuw woordenboek teruggeeft waaraan een gegeven Engels woord met een gegeven vertaling op de juiste plaats toegevoegd werd. Dus: als je `dad` met vertaling `pa` toevoegt aan `('marriage', 'huwelijk', (), ())`, krijg je `('marriage', 'huwelijk', ('dad', 'pa', (), ()), ())` en als je `world` met vertaling `wereld` toevoegt aan `('marriage', 'huwelijk', (), ())` krijg je `('marriage', 'huwelijk', (), ('world', 'wereld', (), ()))`.
- Schrijf een functie die, gegeven een woordenboek Engels-Nederlands in deze vorm, het overeenkomstige woordenboek Nederlands-Engels teruggeeft. (Een binaire zoekboom heet *gebalanceerd* als voor elke deelboom geldt dat haar linkerkant ongeveer even diep is als haar rechterkant. Voor deze oefening is het niet nodig dat de zoekboom die je teruggeeft gebalanceerd is.)

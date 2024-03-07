# Functies: Extra oefeningen

Schrijf voor elke functie een "testsuite" in de vorm van een aantal `assert`-opdrachten.

## Meest nabije punt

Voor deze oefening mag je het `**`-bewerkingsteken van Python niet gebruiken. Je mag ook geen bibliotheken gebruiken, dus ook `math` niet.

1. Definieer een functie `kwadraat` die het kwadraat van een gegeven getal teruggeeft.
2. Definieer een functie `vierkantswortel` die een benadering van de vierkantswortel
   van het gegeven getal X teruggeeft. Het verschil tussen het kwadraat van het resultaat
   en het gegeven getal mag niet groter zijn dan één duizendste van het gegeven getal. Gebruik Newton's methode: neem als eerste benadering B0 voor de vierkantswortel het getal B0 = 1. Gegeven een benadering Bold voor de vierkantswortel kan je een betere benadering Bnew krijgen met de formule Bnew = (Bold + X/Bold) / 2. Herhaal dit tot je de gewenste nauwkeurigheid bereikt hebt.
3. Definieer, gebruik makend van `kwadraat` en `vierkantswortel`, een functie `afstand` die de Euclidische afstand tussen twee punten in het vlak teruggeeft, elk gegeven als een tuple met als elementen de X- en Y-coördinaat van het punt.
4. Definieer, gebruik makend van `afstand`, een functie `meest_nabij` die gegeven een punt P en een lijst L van punten, de index teruggeeft van het element van L dat het dichtst bij P ligt. Elk punt wordt gegeven als een tuple met als elementen de X- en Y-coördinaat van het punt.
5. Definieer, gebruik makend van `meest_nabij`, een functie `gulzig_pad` die, gegeven een lijst L van punten, een nieuwe lijst teruggeeft met dezelfde punten als L maar in de volgorde waarin iemand de punten zou doorlopen die, vertrekkend van het punt op index 0, telkens het meest nabije nog niet bezochte punt zou bezoeken.

## Afstammingsbomen

Stel dat oma Marianne drie kinderen heeft: Anita, Karin, en Bart. Anita heeft één kind: Lewis. Karin heeft twee kinderen: Laurens en Hannah. Bart heeft geen kinderen. Deze gegevens kan je voorstellen als een string, als volgt: `"(Marianne(Anita(Lewis))(Karin(Laurens)(Hannah))(Bart))"`, maar ook als een structuur bestaande uit tuples en strings, als volgt: `("Marianne", (("Anita", (("Lewis", ()))), ("Karin", (("Laurens", ()), ("Hannah", ()))), ("Bart", ())))`.

Meer algemeen bestaat een tekstuele voorstelling van een afstammingsboom uit `(`, gevolgd door een naam, gevolgd door de afstammingsbomen van de kinderen, gevolgd door `)`. De voorstelling van een afstammingsboom als een tuple is een tuple met twee elementen: een naam en een tuple met de afstammingsbomen van de kinderen.

1. Definieer een functie `lees_naam` die, gegeven een string en een positie in die string waar een naam staat, de naam teruggeeft. Preciezer uitgedrukt: geef een zo lang mogelijk stuk van die string terug dat begint op die positie en dat geen haakjes bevat.
2. Definieer, gebruik makend van functie `lees_naam`, een functie `ontleed_hulp` die, gegeven een string en een positie in die string waar een tekstuele afstammingsboom staat, een tuple teruggeeft met als eerste element de tuple-voorstelling van die afstammingsboom en als tweede element de lengte van de tekstuele voorstelling.
3. Definieer een functie `ontleed` die, gegeven een tekstuele voorstelling van een afstammingsboom, een tuple-voorstelling van die boom teruggeeft.
4. Definieer een functie `tel` die, gegeven een tuple-voorstelling van een afstammingsboom, het totale aantal personen in die boom telt.
5. Definieer een functie `tel_tekst` die, gegeven een tekstuele voorstelling van een afstammingsboom, het totale aantal personen in die boom telt.
6. Definieer een functie `diepte` die, gegeven een tuple-voorstelling van een afstammingsboom, de diepte van die boom teruggeeft. De diepte van een boom voor een persoon zonder kinderen is 1. De diepte van een boom voor een persoon met kinderen is één plus het maximum van de dieptes van de bomen voor de kinderen.
7. Definieer een functie `verzamel_namen` die, gegeven een tuple-voorstelling van een afstammingsboom en een lijst, de namen van de personen in de afstammingsboom toevoegt aan de lijst. Deze functie geeft niets terug.

Bijvoorbeeld:

```python
assert lees_naam("aaa(bbb)(ccc)dd", 4) == "bbb" # Op index 4 in "aaa(bbb)(ccc)dd" staat de naam "bbb"
assert lees_naam("a(b)cc", 4) == "cc" # Op index 4 in "a(b)cc" staat de naam "cc"

assert ontleed_hulp("aaa(bbb)ccc", 3) == (("bbb", ()), 5) # Op index 3 in "aaa(bbb)ccc" begint de afstammingsboom "(bbb)" die 5 tekens lang is.
assert ontleed_hulp("aa(b(c)(d))e", 4) == (("c", ()), 3) # Op index 4 in "aa(b(c)(d))e" begint de afstammingsboom "(c)" die 3 tekens lang is.
assert ontleed_hulp("aa(b(c)(d))(f)", 2) == (("b", (("c", ()), ("d", ()))), 9) # Op index 3 in "aa(b(c)(d))(f)" begint de afstammingsboom "(b(c)(d))" die 9 tekens lang is.

assert ontleed("(b(c)(d))") == ("b", (("c", ()), ("d", ())))

assert tel(("Marianne", (("Anita", (("Lewis", ()))), ("Karin", (("Laurens", ()), ("Hannah", ()))), ("Bart", ())))) == 7
assert tel_tekst("(a(b(c(d(e)(f))(g))(h))(i))") == 9

assert diepte(("Marianne", (("Anita", (("Lewis", ()))), ("Karin", (("Laurens", ()), ("Hannah", ()))), ("Bart", ())))) == 3

mijnLijst = []
verzamel_namen(("Marianne", (("Anita", (("Lewis", ()))), ("Karin", (("Laurens", ()), ("Hannah", ()))), ("Bart", ()))), mijnLijst)
assert mijnLijst = ["Marianne", "Anita", "Lewis", "Karin", "Laurens", "Hannah", "Bart"]
```

Tip: gebruik recursie!

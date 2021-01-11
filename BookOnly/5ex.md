
## Oefeningen

### Ziekenhuis

#### Deel 1 
Maak een basisklasse ``Patient`` die een programma kan gebruiken om de doktersrekening te berekenen.

Een patiënt heeft:
* een naam
* het aantal uur dat hij in het ziekenhuis heeft gelegen

Een ``virtual`` methode ``BerekenKost`` zal de totaalkost berekenen. Deze bestaat uit 50euro+  20euro per uur dat de patiënt in het ziekenhuis lag.

Maak een methode ``ToonInfo`` die steeds de naam van de patiënt toont gevolgd door het aantal uur en z'n kosten.

#### Deel 2
Maak een specialisatieklasse ``VerzekerdePatient``. Deze klasse heeft alles dat een gewone ``Patient`` heeft, echter de berekening van de kosten zal steeds gevolgd worden door een 10% reductie.

Toon de werking aan van deze klasse.

### HiddenBookmark

Voeg een ``HiddenBookmark`` klasse toe aan je bestaande Bookmark Manager applicatie van vorige hoofdstuk.

De ``HiddenBookmark`` is een ``Bookmark`` klasse die de ``ShowSite`` methode override door VOOR en NA dat de site op het scherm werd getoond er de tekst `**********INCOGNITO MODE************`  getoond wordt

Test wat er gebeurt als je al je bookmarks vervangt door ``HiddenBookmarks``.

### Pong Advanced

Kan je het ``Pong`` spel uitwerken uit dit boek, waarbij er echter verschillende soorten ``Balletje`` klassen zijn die allemaal van ``Balletje`` overerven? Maak de methoden ``Update`` en ``TekenOpScherm`` virtueel zodat je allerlei verschillende balletjes kunt verzinnen (grotere, andere kleur, ander soort update (denk maar aan teleportatie, versnellen en vertragen, etc.))

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

 De ``HiddenBookmark`` is een ``Bookmark`` klasse die de browser in Incognito-modus zal opstarten bij het openen van de bookmark. Dit kan je bewerkstelligen door ``-incognito`` achter ``chrome.exe`` te plaatsen. Maak de ``OpenSite`` methode ``virtual``  in ``BookMark`` om vervolgens via ``override`` in ``HiddenBookmark`` dit op te lossen.

 Test wat er gebeurt als je al je bookmarks vervangt door ``HiddenBookmarks``.

Afhankelijk van de browser die je wilt aanroepen moet je de incognito parameter iets anders doorgeven:
**Let op de spatie na "-private ", deze moet er staan anders plak je je url aan de parameter:**

```java
Process.Start("iexplore.exe", "-private " + url);
Process.Start("chrome.exe", "-incognito " + url);
Process.Start("firefox.exe", "-private-window " + url);
Process.Start("iexplore.exe", "-private " + url);
```


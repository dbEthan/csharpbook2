## Oefeningen

### Carbon Footprint

Maak 4 klassen:
* ``Huis``
* ``Fabriek``
* ``Auto``
* ``Plant``

We maken een programma'tje om de fictieve ecologische voetafdruk van bepaalde objecten te berekenen

Maak een interface ``ICarbonFootPrint`` die 
* 1 methode ``BerekenFootprint`` heeft die een int teruggeeft en geen parameters nodig heeft
* 1 methode ``VerlaagFootprint`` die niets teruggeeft en geen parameters nodig heeft

Breidt de volgende klassen met de interface uit:
* De carbon footprint van een ``huis`` is gebaseerd op het volume van het huis in kubieke meter maal 10.
* De carbon footprint van een ``fabriek`` is gebaseerd op het aantal werknemers maal 100. 
* De carbon footprint van een ``auto`` is gebaseerd op het merk

Het verlagen van de footprint in iedere klasse verzin je zelf (door bijvoorbeeld bij het huis de factor 10 met 1 te verlagen).

Zorg ervoor dat van iedere klasse de footprint kan bevraagd worden (maak/verzin dus de nodige properties per klasse om dit te bereken). De klasse plant moet je niet aanpassen.

Plaats van iedere klasse 2 objecten  in een gemeenschappelijke lijst en zorg ervoor dat:
* de footprint van alle objecten getoond wordt (planten worden overgeslagen)
* de gemiddelde footprint van alle objecten (ook planten worden meegeteld) berekend
* toont welk object de hoogte footprint heeft
* van alle objecten de footprint kan verlaagt worden
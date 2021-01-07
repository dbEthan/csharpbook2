## Oefeningen

### Meetlat

Maak een klasse ``Meetlat``. Via een write-only property BeginLengte kan de gebruiker de lengte van een voorwerp instellen (in meter). Via een reeks read-only properties (die transformeren) kan de gebruiker deze lengte in verschillende eenheden uitlezen namelijk:

* ``LengteInM``
* ``LengteInCm``
* ``LengteInKm``
* ``LengteInVoet`` (1m= 3.2808ft)

{blurb, class: warning}
**Opgelet het ``readonly`` keyword heb je niét nodig om readonly properties te maken. Zoek op hoe je dit wel doet.**
{/blurb}


Voorbeeld gebruik van klasse:

```java
Meetlat mijnLat = new Meetlat();
mijnLat.BeginLengte = 2;
Console.WriteLine($"{mijnLat.LengteInM} meter is {mijnLat.LengteInVoet} voet.");
```
## Oefeningen

### Meetlat

Maak een klasse ``Meetlat``. Via een write-only property ``BeginLengte`` kan de gebruiker de lengte van een voorwerp instellen (in meter). Via een reeks read-only properties (die transformeren) kan de gebruiker deze lengte in verschillende eenheden uitlezen namelijk:

* ``LengteInM``
* ``LengteInCm``
* ``LengteInKm``
* ``LengteInVoet`` (1m= 3.2808ft)

Voorbeeld gebruik van klasse:

```java
Meetlat mijnLat = new Meetlat();
mijnLat.BeginLengte = 2;
Console.WriteLine($"{mijnLat.LengteInM} meter is {mijnLat.LengteInVoet} voet.");
```

### Bankmanager 2

Breidt de bankmanager oefening uit het vorige hoofdstuk uit met volgende functionaliteiten:
* Voorzie Exception Handling op alle plaatsen waar potentiële problemen kunnen opdoeken.
* Voorzie in je programma een methode ``SimuleerOverdracht``. Je kan aan deze methode 2 ``Rekening`` objecten meegeven. Vervolgens zal de methode 5x een willekeurig bedrag van de ene naar de andere rekening sturen, hierbij wisselen de rekeningen om de beurt wie verzender en wie ontvanger is. Wanneer de methode klaar is wordt er niets teruggestuurd.
* Maak een methode ``CreeerTienerRekening`` in je programma. Deze methode geeft een nieuwe rekening terug waar de balans reeds op 50 staat. De methode aanvaardt 1 parameter: de naam van de klant, dat vervolgens in het nieuwe object wordt ingesteld. 

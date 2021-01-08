## Oefeningen


{blurb, class: tip}
We sluiten ieder hoofdstuk af met een  selectie oefeningen. In de mate van het mogelijk zijn ze gerangschikt van eenvoudig tot iets pittiger. Bekijk zeker [timdams.com/ziescherp](https://timdams.com/ziescherp) waar je een gigantiche hoeveelheid extra oefeningen zal terugvinden..
{/blurb}

### RapportModule

Ontwerp een klasse ``Resultaat`` die je zal tonen wat je graad is gegeven een bepaald behaald percentage. Het enige dat je aan een ``Resultaat``-object moet kunnen geven is het behaalde percentage dat wordt bijgehouden via een auto-property. Via een methode PrintGraad kan de behaalde graad weergegeven worden, gebaseerd op dit percentage. Dit zijn de mogelijkheden:

* Minder dan 50%: niet geslaagd.
* Tussen 50% en 68% (68 incl.): voldoende.
* Tussen 68% en 75% (75 incl.): onderscheiding.
* Tussen 75% en 85% (85 incl.): grote onderscheiding.
* Meer dan 85%: grootste onderscheiding.


Test je klasse door enkele objecten in je ``main`` en te onderzoeken of deze de juiste graden op het scherm printen. Bijvoorbeeld:

```java
Resultaat mijnpunten = new Resultaat();
mijnpunten.Percentage = 65;
mijnpunten.PrintGraad();
```

### Nummers

Maak een klasse ``Nummers``. Deze klasse bevat 2 getallen (type ``int``) die via een autoproperty kunnen aangepast worden. Er zijn 4 methoden:

* ``Som``: geeft de som van beide getallen terug.
* ``Verschil``: geeft het verschil van beide getallen terug.
* ``Product``: geeft het product van beide getallen terug.
* ``Quotient``: geeft de deling van het eerste door het tweede getal terug; toon een foutboodschap op het scherm indien er een deling door nul zal gebeuren.

Toon in je ``main`` aan dat je code werkt.

Volgende code zou bijvoorbeeld onderstaande output moeten geven:

```java
Nummers paar1 = new Nummers();
paar1.Getal1 = 12;
paar1.Getal2 = 34;

Console.WriteLine("Paar:" + paar1.Getal1 + ", " + paar1.Getal2);
Console.WriteLine("Som = " + paar1.Som());
Console.WriteLine("Verschil = " + paar1.Verschil());
Console.WriteLine("Product = " + paar1.Product());
Console.WriteLine("Quotient = " + paar1.Quotient());
```

Output:

{line-numbers:false}
```text
Paar: 12, 34
Som = 46
Verschil = -22
Product = 408
Quotient = 0,352941176470588
```

### Bibliotheek

Boeken in een bibliotheek mogen maximum 14 dagen uitgeleend worden. Schrijf een console-applicatie om de volgende gegevens te tonen door middel van een klasse ``BibBoek``:
* de naam van de ontlener, die werd ingelezen (autoproperty).
* de datum van vandaag (autoproperty met private set).
* de datum dat het boek ten laatste terug moet ingeleverd worden (readonly property).

### BankManager

Ontwerp een klasse ``Rekening`` die minstens instantievariabelen ``naamKlant``, ``balans`` en ``rekeningnummer`` bevat. Voorzie 3 methoden:

1. ``HaalGeldAf``: bepaalt bedrag (als parameter) wordt van de ``balans`` verwijderd.
2. ``StortGeld``: bepaalt bedrag (als parameter) wordt op de rekening gezet en aan ``balans`` toegevoegd.
3. ``ToonBalans``: het totale bedrag op de rekening wordt getoond, alsook de naam van de klant en het rekeningnummer.

Pas de ``HaalGeldAf`` methode aan zodat als returntype het bedrag (``int``) wordt teruggegeven. Indien het gevraagde bedrag meer dan de ``balans`` is dan geef je al het geld terug dat nog op de rekening staat en toon je in de console dat niet al het geld kon worden gegeven.

Maak 2 instanties van het type ``Rekening`` aan en toon aan dat je geld van de ene Rekening aan de andere kunt geven, als volgt:

```java
BankRekening rekening1 = new BankRekening();
BankRekening rekening2 = new BankRekening();
```

Voeg aan de ``Rekening``-klasse een instantievariabele vanvan het type ``RekeningState`` toe, dat een enumeratie bevat. De Rekening kan in volgende states zijn ``Geldig``, ``Geblokkeerd``). 

Maak een bijhorende publieke Methode waarmee je de Rekening van state kunt veranderen. Deze methode (noem ze ``ChangeState``) vereist geen parameters. Telkens je ze aanroept wordt de staat omgewisseld. Als dus het object momenteel op ``Geldig`` stond, dan wordt ze nu ``Geblokkeerd`` en omgekeerd.

Indien een persoon geld van of naar een Geblokkeerde rekening wil sturen dan zal er een error op het scherm verschijnen.

Test je klasse.

1. Nieuwe klant aanmaken (max 10) 
2. Status van bestaande klant tonen 
3. Geld op een bepaald Rekening zetten 
4. Geld van een bepaald Rekening afhalen
5. Geld tussen 2 Rekeningen overschrijven

Voorzie extra functionaliteit naar keuze.
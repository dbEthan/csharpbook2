## Oefeningen


{blurb, class: tip}
We sluiten ieder hoofdstuk af met een  selectie oefeningen. In de mate van het mogelijk zijn ze gerangschikt van eenvoudig tot iets pittiger. Bekijk zeker [timdams.com/ziescherp](https://timdams.com/ziescherp) waar je een gigantiche hoeveelheid extra oefeningen zal terugvinden..
{/blurb}

### RapportModule

Ontwerp een klasse ``Resultaat`` die je zal tonen wat je graad is gegeven een bepaald behaald percentage. Het enige dat je aan een ``Resultaat``-object moet kunnen geven is het behaalde percentage. Enkel het totaal behaalde % wordt bijgehouden via een auto-property. Via een methode PrintGraad kan de behaalde graad weergegeven worden. Dit zijn de mogelijkheden:

* < 50: niet geslaagd;
* tussen 50 en 68: voldoende;
* tussen 68 en 75: onderscheiding;
* tussen 75 en 85: grote onderscheiding;
* \> 85: grootste onderscheiding.


Test je klasse door enkele objecten in je main aan te maken en de verschillende properties waarden te geven en methoden aan te roepen.
Deze code zou moeten werken:

```java
Resultaat mijnpunten= new Resultaat();
mijnpunten.Percentage=65;
mijnpunten.PrintGraad();
```

### Nummers

Maak een klasse ``Nummers``. Deze klasse bevat 2 getallen (type int) die via een autoproperty kunnen aangepast worden. Er zijn 4 methoden:

* ``Som``: geeft de som van beide getallen terug
* ``Verschil``: geeft het verschil van beide getallen terug
* ``Product``: geeft het product van beide getallen terug
* ``Quotient``: geeft de deling van beide getallen terug. Toon "Error" indien je zou moeten delen door 0.

Toon in je main aan dat je code werkt.

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
* de naam van de ontlener, die werd ingelezen (autoproperty)
* de datum van vandaag (autoproperty met private set)
* de datum, dat het boek ten laatste terug moet ingeleverd worden (readonly property)

### BankManager

Ontwerp een klasse Account die minstens een ``naamveld``, ``balans`` en ``rekeningnummer`` bevat. Voorzie 3 methoden:

1. ``WithdrawFunds``: bepaalt bedrag wordt van de ``balans`` verwijderd
2. ``PayInFunds``: bepaalt bedrag (als parameter) wordt op de rekening gezet en aan ``balans`` toegevoegd
3. ``GetBalance``: het totale bedrag op de rekening wordt teruggegeven, m.a.w. ``balans`` wordt teruggegeven

Pas de ``WithdrawFunds`` methode aan zodat als returntype het bedrag (int) wordt teruggegeven. Indien het gevraagde bedrag meer dan de balans is dan geef je al het geld terug dat nog op de rekening staat en toon je in de console dat niet al het geld kon worden gegeven.

Maak 2 instanties van het type ``Account`` aan en toon aan dat je geld van de ene account aan de andere kunt geven, als volgt:

```java
BankAccount rekening1=new BankAccount();
BankAccount rekening2=new BankAccount();
```

Voeg aan de ``Account``-klasse een private field toe zijnde van het type ``accountState`` dat een enumeratie bevat. De account kan in volgende states zijn "Geldig", "Geblokkeerd"). 
Maak een bijhorende publieke Methode  waarmee je de account van state kunt veranderen. Deze methode (noem ze ChangeState) vereist één parameter van het type ``accountState`` natuurlijk.

Indien een persoon geld van of naar een Geblokkeerde rekening wil sturen dan zal er een error op het scherm verschijnen.

Test je klasse.

1. Nieuwe klant aanmaken (max 10) 
2. Status van bestaande klant tonen 
3. Geld op een bepaald account zetten 
4. Geld van een bepaald account afhalen
5. Geld tussen 2 accounts overschrijven

Voorzie extra functionaliteit naar keuze.
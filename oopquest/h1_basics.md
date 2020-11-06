
## OopQuest Fase 1

<!---
1. Basis klassen monster, schat en helden met nodige properties
2. Random monster generator
3. Constructor om helden in te stellen + static kaartgenerator
4. Lijst van monsters, dictionary van schatten
5. overerving van monsters en kamers
6. exception handling voor user input
7. abstracte gameelement klasse
8. held+inventaris , kaart+monster+held
9. spelmanager
10. klaarmaken voor de toekomst ?--->


<!---NOBOOKSTART--->
{% hint style='warning' %}
<!---NOBOOKEND--->
<!---{aside}--->
<!--- {float:right, width:50%} --->
![](../assets/oopquesttitel.png)

Doorheen dit boek zullen we aan het einde van ieder hoofdstuk een stuk werken aan **OopQuest** een vereenvoudigde versie van HeroQuest, een spel dat ik vroeger erg graag speelde. Voor de gamers die dit boek lezen (vermoedelijk 90% van de lezers dus): we zullen een *turn-based rogue-like topdown dungeon crawler* maken, maar met een hoek af.
<!---{/aside}--->
<!---NOBOOKSTART--->
{% endhint %}
<!---NOBOOKEND--->



De opzet van OopQuest is als volgt:
* de kiest uit 1 van 4 helden
* de speler bewegen hun held rond op een random gegenereerde kaart
* de speler bestrijdt monsters en worden sterker naarmate er meer monsters gedood worden
* de speler kan schatten verzamelen en moet proberen zo lang mogelijk te overleven
* wanneer de speler sterft begint het spel opnieuw, maar worden er enkele eigenschappen vanuit het 'vorige leven' doorgegeven


### Laten we de zoektocht beginnen

OopQuest zou niets zijn zonder nodige basis-klassen. We duiden daarom in de originele opzet alle zelfstandige naamwoorden (*substantieven*) aan, deze zijn potentiele kandidaten om in klassen te gieten:

* de **speler** kiest uit 1 van 4 **helden**
* de speler beweegt de held rond op een random gegenereerde **kaart**
* de speler bestrijdt **monsters** en worden sterker naarmate er meer monsters gedood worden
* de speler kan **schatten** verzamelen en moet proberen zo lang mogelijk te overleven
* wanneer de speler sterft begint het **spel** opnieuw, maar worden er enkele eigenschappen vanuit het 'vorige leven' doorgegeven

Voorlopig gaan zullen we van ieder zelfstandig naamwoord het enkelvoud nemen (schatten wordt dus schat).
We krijgen volgende klassen:

```java
class Speler {}
class Held {}
class Kaart {}
class Monster {}
class Schat {}
class Spel {}
```

### Held klasse

We gaan nog niet alle klassen volledig uitwerken. De ``Held`` klasse gaan we als eerste aanpakken. Een ``Held`` wordt gedefinieerd door volgende eigenschappen:
* Naam (bv Crusher McCrusher)
* Type (bv Paladijn, Barbaar, etc)
* Gezondheidspercentage (0 is dood, 100 is kerngezond)
* Sterkte bij de start (een positief getal)

Laten we dit in een klasse gieten met de nodige autoproperties:

```java
class Held
{
    public string Naam { get; set; }
    public HeldTypes HeldType { get; set; }
    public int Gezondheid { get; set; }
    public int Sterkte { get; set; }
}
```

Uiteraard definiëren we ook HeldType:
```java
enum HeldTypes { Barbaar, Tovenaar, Paladijn, Boogschutter}
```

We herbekijken de klasse nog eens en kijken welke properties beter omgezet worden naar full properties. Zeker ``Gezondheid`` en ``Sterkte`` komen hiervoor in aanmerking. We veranderen deze naar:

```csharp
private int gezondheid;
public int Gezondheid
{
    get { return gezondheid; }
    set { 
        if(value>=0 && value<=100)
            gezondheid = value; 
    }   
}

private int sterkte;
public int Sterkte
{
    get { return sterkte; }
    set {
        if(value>=0)
            sterkte = value; 
    }
}
```

Voorts is het handig om een ``Info`` methode te hebben op een held om snel z'n stats naar het scherm te sturen:

```java
public void ToonInfo()
{
    Console.WriteLine($"Held:{Naam} , {HeldType}");
    Console.WriteLine($"Gezondheid={Gezondheid}%, Sterkte={Sterkte}");
}
```
### Held klasse testen

We zullen eens testen of deze Held-klasse al werkt. We schrijven in de ``main``:

```java
Held MijnEersteHeld = new Held();
MijnEersteHeld.Naam = "Egon De Verschrikkelijke";
MijnEersteHeld.HeldType = HeldTypes.Barbaar;
MijnEersteHeld.Gezondheid = 100;
MijnEersteHeld.Sterkte = 5;

MijnEersteHeld.ToonInfo();
```
Er verschijnt, zoals gehoopt dan op het scherm:

```text
Held:Egon De Verschrikkelijke , Barbaar
Gezondheid=100%, Sterkte=5
```

Voorts merken we dat volgende lijn de sterkte niét zal aanpassen omdat deze geen positief getal is:
```java
MijnEersteHeld.Sterkte = -9;
```
## Objecten en methoden

### Objecten als actuele parameters

Klassen zijn "gewoon" nieuwe datatypes. Alle regels die we dus al kenden in verband met het doorgeven van variabelen als parameters in een methoden blijven gelden.
Het enige verschil is dat we objecten **by reference** meegeven aan een methode. Aanpassingen aan het object in de methode zal dus betekenen dat je het originele object aanpast dat aan de methode werd meegegeven. Hier moet je dus zeker rekening mee houden.

Een voorbeeld. Stel dat we volgende klasse hebben waarin we metingen willen opslaan, alsook wie de meting heeft gedaan:

```java
class Meting
{
    public int Temperatuur { get; set; }
    public string OpgemetenDoor { get; set; }
}
```

In ons hoofdprogramma schrijven we een methode ``ToonMetingInKleur`` die ons toelaat om deze meting op het scherm te tonen in een bepaalde kleur. Het gebruik en de methode zelf zouden er zo kunnen uitzien:

```java
static void Main(string[] args)
{
    Meting m1 = new Meting();
    m1.Temperatuur = 26; 
    m1.OpgemetenDoor = "Elon Musk";
    Meting m2 = new Meting();
    m2.Temperatuur = 34; 
    m2.OpgemetenDoor = "Dennis Rodman";

    ToonMetingInKleur(m1, ConsoleColor.Red);
    ToonMetingInKleur(m2, ConsoleColor.Gray);
}

static void ToonMetingInKleur (Meting inMeting, ConsoleColor kleur)
{
    Console.ForegroundColor = kleur;
    Console.WriteLine($"{inMeting.Temperatuur}°C gemeten door: {inMeting.OpgemetenDoor}");
    Console.ResetColor();
}
```

### Objecten in methoden aanpassen

Je kan dus ook methoden schrijven die meegegeven objecten aanpassen daar we deze **by reference** doorsturen. Een voorbeeld:

```java
static void ToonMetingEnVerhoog(Meting inMeting)
{
    ToonMetingInKleur(inMeting, ConsoleColor.Green);

    inMeting.Temperatuur++;
}
```

Als we deze methode als volgt aanroepen:
```java
Meting m1 = new Meting();
m1.Temperatuur = 26; m1.OpgemetenDoor = "Elon Musk";
ToonMetingEnVerhoog(m1);
Console.WriteLine(m1.Temperatuur);
```

Dan zullen we zien dat de temperatuur in ``m1`` effectief met 1 werd verhoogd.

Dit gedrag zouden we NIET zien bij volgende methode daar ``int`` **by value** wordt doorgegeven:

```java
static void VerhoogGetal(int inMeting)
{
    inMeting++;
}
```

### Objecten als resultaat

Weer hetzelfde verhaal: ook klassen mogen het resultaat van een methoden zijn.

```java
static Meting GenereerRandomMeting()
{
    Meting result = new Meting();
    Random r = new Random();
    result.Temperatuur = r.Next(-100, 200);
    result.OpgemetenDoor = "Onbekend";

    return result;
}
```

Deze methode kan je dan als volgt gebruiken:

```java
Meting m3 = GenereerRandomMeting();
```
<!---NOBOOKSTART--->
### Kennisclip
![](../assets/infoclip.png)
* [Objecten als parameter of returnwaarde](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=8dbbc3f8-56ed-4657-82a7-ab7400e422bc) (opname uit hoorcollege 4/3/20)
<!---NOBOOKEND--->
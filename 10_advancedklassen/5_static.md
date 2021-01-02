## Static

Je hebt het keyword ``static`` al een paar keer zien staan in de methodesignaturen in het vorige boek. En dit boek werd er dan weer nadrukkelijk verteld géén ``static`` voor methoden te plaatsen. Wat is het nu?

Bij klassen en objecten duidt ``static`` aan dat een methode of variabele "gedeeld" wordt over alle objecten van die klasse. Wanneer je het keyword ergens voor plaatst (voor een methode, variabele, property, etc) dan kan je dit element aanroepen **zonder dat je een instantie van die klasse nodig hebt**

``static`` kan op verschillende plaatsen in een klasse gebruikt worden:

1. Bij *variabelen* om een gedeelde variabele aan te maken, over de objecten heen. We spreken dan niet meer over een instantievariabele maar over een *static field*.
2. Bij *methoden* om zogenaamde methoden-bibliotheken of hulpmethoden aan te maken (denk maar aan ``DateTime.IsLeap()``) en spreken dan over een *static method*.
3. Bij de klasse zelf om te voorkomen dat er objecten van de klasse aangemaakt kunnen worden (bijvoorbeeld de ``Console`` en ``Math`` klasse). Je raadt het nooit, maar dit noemt dan een *static class*.
4. Bij *properties*. We hebben al met 1 *static property* gewerkt namelijk de readonly property ``Now`` van de ``DateTime`` klasse (``DateTime.Now``).

{% hint style='tip' %}
Ook een constructor kan ``static`` gemaakt worden, maar dat gaan we in dit boek niet bespreken. Samengevat kan je een *static constructor* gebruiken indien je een soort *oer-constructor* wilt hebben die eenmalige wordt aangeroepen wanneer het allereerste object van een klasse wordt aangemaakt. Wanneer een tweede (of derde, etc.) instantie wordt aangemaakt zal de *static constructor* niet meer aangeroepen worden.
{% endhint %}


### static fields

Zonder het keyword ``static`` heeft ieder object z'n eigen instantievariabelen.  Aanpassingen binnen het object aan die variabelen heeft geen invloed op andere objecten van hetzelfde type. We tonen eerst de werking zoals we gewend zijn en vervolgens hoe ``static`` werkt.

#### Zonder static fields

Gegeven volgende klasse:

```java
class Mens
{
    private int leeftijd=1;
    public void Jarig()
    {
        leeftijd++;
    }

    public void ToonLeeftijd()
    {
        Console.WriteLine(leeftijd);
    }
}
```

Als we dit doen:

```java
Mens m1= new Mens();
Mens m2= new Mens();

m1.Jarig();
m1.Jarig();

m2.Jarig();

m1.ToonLeeftijd();
m2.ToonLeeftijd();
```

Dan zien we volgende uitvoer:

<!---{line-numbers:false}--->
```text
3
2
```

Ieder object houdt de stand van z'n eigen variabelen bij. Ze kunnen elkaars interne (zowel publieke als private) staat niet rechtstreeks veranderen.

#### En nu mét static fields

Laten we eens kijken wat er gebeurt indien we instantievariabele ``static`` maken. 

We maken de variabele ``private int leeftijd`` static als volgt: ``private static int leeftijd=1;``. We krijgen dan:

```java
class Mens
{
    private static int leeftijd=1;
    public void Jarig()
    {
        leeftijd++;
    }

    public void ToonLeeftijd()
    {
        Console.WriteLine(leeftijd);
    }
}
```

**We hebben nu gezegd dat ALLE objecten de variabele ``leeftijd`` *delen*. Er wordt van deze variabele dus maar een "instantie" in het geheugen gemaakt.**

Voeren we nu terug volgende code uit:

```java
Mens m1= new Mens();
Mens m2= new Mens();

m1.Jarig();
m1.Jarig();

m2.Jarig();

m1.ToonLeeftijd();
m2.ToonLeeftijd();
```

Dan wordt de uitvoer:

```
4
4
```

We zien dat de ``leeftijd`` dus niet meer per object individueel wordt bewaard, maar dat het één globale variabele als het ware is geworden.
``static`` laat je dus toe om informatie over de objecten heen te delen. 

{% hint style='warning' %}
Gebruik static niet te pas en te onpas: vaak druist het in tegen de concepten van OO en wordt het vooral misbruikt
{% endhint %}

Ga je dit static variabelen, ook wel static fields genoemd, vaak nodig hebben? Niet zo vaak. Het volgende concept wel.

### static methoden

Heb je er al bij stil gestaan waarom je dit kan doen:

```
Math.Pow(3,2);
```

Zonder dat we objecten moeten aanmaken in de trend van:

```java
Math myMath= new Math(); //dit mag niet!
myMath.Pow(3,2)
```

De reden dat je de ``Math``-bibliotheek kan aanroepen rechtsreeks **op de klasse** en niet op objecten van die klasse is omdat de methoden in die klasse als ``static`` gedefineerd staan.

{% hint style='tip' %}
De klasse is op de koop toe ook zelf ``static`` gemaakt. Zo kan er zeker geen twijfel bestaan: deze klasse kan niét in een object gegoten worden.

De klasse zal er dus zo ongeveer uitzien:

```java
static class Math
{
    public static double Pow(int getal, int macht)
    {
        //etc.
```
{% endhint %}

#### Voorbeeld van static methoden

Stel dat we enkele veelgebruikte methoden willen groeperen en deze gebruiken zonder telkens een object te moeten aanmaken dan doen we dit als volgt:

```java
static class EpicLibray
{
    static public void ToonInfo()
    {
        Console.WriteLine("Ik ben ik");
    }

    static public int TelOp(int a, int b)
    {
        return a+b;
    }
}
```

We kunnen deze methoden nu als volgt aanroepen:

```java
EpicLibrary.ToonInfo();

int opgeteld= EpicLibrary.TelOp(3,5);
```

Mooi toch.

#### Nog een voorbeeld

In het volgende voorbeeld gebruiken we een ``static`` variabele om bij te houden hoeveel objecten (via de constructor) er van de klasse reeds zijn aangemaakt:

```java
class Fiets
{
    private static int aantalFietsen = 0;
    public Fiets()
    {
        aantalFietsen++;
		Console.WriteLine($"Er zijn nu {aantalFietsen} gemaakt");
    }
	
	public static void VerminderFiets()
	{
		aantalFietsen--;
        Console.WriteLine($"STATIC: Er zijn {aantalFietsen} fietsen");
	}
}
```

Merk op dat we de methoden ``VerminderFiets`` enkel via de klasse kunnen aanroepen daar deze ``static`` werd gemaakt. We kunnen echter nog steeds instantie, ``Fiets``-objecten, aanmaken aangezien de klasse zelf niet ``static`` werd gemaakt.

Laten we de uitvoer van volgende code eens bekijken:
```java
Fiets Merckx = new Fiets();
Fiets Steels = new Fiets();
Fiets Evenepoel = new Fiets();
Fiets.VerminderFiets();
Fiets Aert = new Fiets();
Fiets.VerminderFiets();
```

Dit zal volgende uitvoer geven:

```text
Er zijn nu 1 gemaakt  
Er zijn nu 2 gemaakt
Er zijn nu 3 gemaakt
STATIC:Er zijn 2 fietsen
Er zijn nu 3 gemaakt
STATIC:Er zijn 2 fietsen
```

### Static vs non-static

Van zodra je een methode hebt die ``static`` is dan zal deze methode enkel andere ``static` methoden en variabelen kunnen aanspreken. Dat is logisch: een static methode heeft geen toegang tot de gewone niet-statische variabelen van een individueel object, want welk object zou hij dan moeten benaderen?

Volgende code zal dus een fout geven:

```java
class Mens
{
	private int gewicht=50;
	
	private static void VerminderGewicht()
	{
		gewicht--;
	}
```

De error die verschijnt **An object reference is required for the non-static field, method, or property 'Program.Fiets.gewicht'** zal bij de lijn ``gewicht--`` staan.


<!---NOBOOKSTART--->
{% hint style='warning' %}
<!---NOBOOKEND--->
<!---{aside}--->
<!--- {float:right, width:50%} --->
![](../assets/attention.png)

Een eenvoudige regel is te onthouden dat van zodra je in een ``static`` omgeving (meestal een methode of property) bent je niet meer naar de niet-static delen van je code zal geraken.


### Static en main

Dit verklaart ook waarom je bij console applicaties in Program.cs steeds alle methoden ``static`` moet maken. Een console-applicatie is als volgt beschreven wanneer je het aanmaakt:

```java
public class Program
{
		public static void Main()
		{

	    }
}
```

Zoals je ziet is de ``Main`` methode als ``static`` gedefinieerd. Willen we dus vanuit deze methode andere methoden aanroepen dan moeten deze als ``static`` aangeduid zijn.

Uiteraard kan je wel niet-static zaken gebruiken en daarom kan je dus gewone objecten etc. in je static methoden aanmaken.
<!---{/aside}--->
<!---NOBOOKSTART--->
{% endhint %}
<!---NOBOOKEND--->


### Een use-case met static

Beeld je in dat je (weer) een pong-variant moet maken waarbij meerdere balletjes over het scherm moeten botsen. Je wilt echter niet dat de balletjes zelf allemaal apart moeten weten wat de grenzen van het scherm zijn. Mogelijk wil je bijvoorbeeld dat je code ook werkt als het speelveld kleiner is dan het eigenlijke Console-scherm.

We gaan dit oplossen met een static property waarin we de grenzen voor alle balletjes bijhouden. Onze basis-klasse wordt dan al vast:

```java
class Balletje
{
    static public int Breedte { get; set; }
    static public int Hoogte { get; set; }

```

In ons hoofdprogramma (``Main``) kunnen we nu de grenzen voor alle balletjes vastleggen:

```java
Balletje.Hoogte = Console.WindowHeight;
Balletje.Breedte = Console.WindowWidth;
```

Maar even goed maken we de grenzen voor alle balletjes gebaseerd op zelf gekozen waarden:

```java
Balletje.Hoogte = 20;
Balletje.Breedte = 10;

```

De interne werking van de balletjes hoeft dus geen rekening meer te houden met de grenzen van het scherm. We passen de ``Update``-methode aan rekening houdend met deze nieuwe kennis:

```java

public void Update()
{
    if (BalX + VX >= Balletje.Breedte || BalX + VX < 0)
    {
        VX = -VX;
    }


    BalX = BalX + VX;

    if (BalY + VY >= Balletje.Hoogte || BalY + VY < 0)
    {
        VY = -VY;
    }

    BalY = BalY + VY;
}

}
```

En nu kunnen we vlot balletjes laten rondbewegen op bijvoorbeeld een klein deeltje maar van het scherm:

```java
static void Main(string[] args)
{
    Console.CursorVisible = false; //handig dit hoor
    Balletje.Hoogte = 15;
    Balletje.Breedte = 15;

    Balletje m1 = new Balletje(1,1,1,1);
    Balletje m2 = new Balletje(2,2,-2,1);
    
    while (true)
    {
        m1.Update();
        m1.TekenOpScherm();

        m2.Update();
        m2.TekenOpScherm();
  
        System.Threading.Thread.Sleep(50);
        Console.Clear();
    }
}
```

<!---NOBOOKSTART--->
# Kennisclip
![](../assets/infoclip.png)
* [static keyword](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=04805e97-94e8-4593-b30c-ab750089ffa6)
<!---NOBOOKEND--->
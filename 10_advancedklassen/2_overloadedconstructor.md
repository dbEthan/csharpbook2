## Overloaded constructors

Soms wil je parameters aan een object meegeven bij de creatie ervan. We willen bijvoorbeeld de leeftijd meegeven die het object moet hebben bij het aanmaken.

Met andere woorden, stel dat we dit willen schrijven:

```java
Student jos= new Student(19);
```

Als we dit met voorgaande klasse uitvoeren , die enkel een default constructor heeft, zal de code een fout geven. C# vindt geen constructor die een ``int`` als actuele parameter aanvaardt.

Net zoals bij overloading van methoden kunnen we ook constructors overloaden. De code is verrassend gelijkaardig aan method overloading:

```java
class Student
{
    public Student(int startgeboorteJaar)
    {
        geboorteJaar = startgeboorteJaar
    }

    private int geboorteJaar;
}

```

Dat was eenvoudig, hé?

**Maar** denk eraan, je hebt een overloaded constructor geschreven en dus heeft C# gezegd *"ok, je schrijft zelf constructor, trek je plan. Maar de default zal je ook zal moeten schrijven!"*
Je kan nu enkel je objecten nog via de overloaded constructor aanmaken. Schrijf je ``new Student()`` dan zal je een error krijgen. Wil je die constructor, de default constructor, nog hebben dan zal je die dus ook moeten schrijven, bijvoorbeeld:


```java
class Student
{
    public Student(int startgeboorteJaar) //overloaded
    {
        geboorteJaar= startgeboorteJaar;
    }
    
    public Student() //default
    {
       geboorteJaar =  DateTime.Now.Year-18;
    }

    private int geboorteJaar;
}
```

<!---NOBOOKSTART--->
{% hint style='warning' %}
<!---NOBOOKEND--->
<!---{aside}--->
<!--- {float:right, width:50%} --->
![](../assets/attention.png)
Voorgaande wil ik nog eenmaal herhalen. Herinner je m'n voorbeeld van die aannemers die soms wel en soms niet opruimden? Laten we nog eens samenvatten hoe het zit met constructors in C#:
* Als je geen constructors schrijft krijg je een default constructor gratis. Die doet echter niets extra.
* Van zodra je één constructor zelf schrijft, default of overloaded, krijg je niets meer gratis én zal je dus zelf die constructors moeten bijschrijven die jouw code vereist.
<!---{/aside}--->
<!---NOBOOKSTART--->
{% endhint %}
<!---NOBOOKEND--->


### Meerdere overloaded constructors
Wil je meerdere overloaded constructors dan mag dat ook. Je wilt misschien een constructor die de leeftijd vraagt alsook een ``bool`` om mee te geven of het om een werkstudent gaat:

```java
class Student
{
    public Student(int startgeboorteJaar) //overloaded
    {
        geboorteJaar = startgeboorteJaar;
    }
    
    public Student(int startgeboorteJaar, bool werkstart) //overloaded
    {
        geboorteJaar= startgeboorteJaar;
        isWerkStudent= werkstart;
    }

    public Student() //default
    {
        geboorteJaar= DateTime.Now.Year-18;
    }

    private int geboorteJaar;
    private bool isWerkStudent;
}

```

{% hint style='tip' %}
Merk op dat je ook properties mag gebruiken in je constructor. Zo kan je ogenblikkelijk de typische controles in een ``set`` in gebruik nemen:

Beeld je in dat het schoolsysteem crasht wanneer een nieuwe student een geboortejaar heeft dat in de 19e eeuw ligt (<1900). Wanneer dit gebeurt moet het geboortejaar altijd gewoon op 1900 gezet worden, ongeacht het effectieve geboortejaar van de student. Via een ``set``-controle kunnen we dit doen én vervolgens passen we de constructor aan zodat deze via de property werkt én niet rechtstreeks met de instantievariabele:
```java
class Student
{
    public Student(int startgeboorteJaar) //overloaded
    {
        GeboorteJaar = startgeboorteJaar; //let op GeboorteJaar i.p.v. geboorteJaar
    }

    private int geboorteJaar;
    public int GeboorteJaar
    {
        get { return geboorteJaar; }
        set
        {
            if (value < 1900)
                geboorteJaar = 1900;
            else 
                geboorteJaar = value;
        }
    }
}
```

{% endhint %}

<!---NOBOOKSTART--->
{% hint style='tip' %}
<!---NOBOOKEND--->
<!---{aside}--->
<!--- {float:right, width:50%} --->
![](../assets/attention.png)
Maar welke constructors moet ik nu eigenlijk allemaal voorzien? 

Dit hangt natuurlijk af van de soort klasse dat je maakt. Een constructor is minimaal nodig om ervoor te zorgen dat alle variabele die essentieel zijn in je klasse een beginwaarde hebben.

Beeld je volgende klasse voor die een breuk voorstelt:

```java
class  Breuk
{
    private int noemer;
    private int teller;

    public void PrintAlsDouble()
    {
        Console.WriteLine((double)teller/noemer);
    }
}
```

De methode zal een onaarde "DivideByZeroException" opleveren als ik de methode zou aanroepen nog voor de ``noemer`` een waarde heeft gekregen:

```java
Breuk eenBreuk =new Breuk();
eenBreuk.PrintAlsDouble();
```

Via een constructor kunnen we dus dit soort bugs voorkomen. We beschermen ontwikkelaars hiermee dat ze jouw klasse foutief gebruiken. Door een overloaded constructor te schrijven die een noemer en teller vereist verplichten we de ontwikkelaar jouw klasse correct te gebruiken:

```java
class  Breuk
{
    private int noemer;
    private int teller;

    public Breuk(int tellerIn, int noemerIn)
    {
        teller=tellerIn;
        if(noemerIn == 0)
            noemer =1 ; //of werp Exception op. Zie verder in boek
        else
            noemer=noemerIn;
    }

    public void PrintAlsDouble()
    {
        Console.WriteLine((double)teller/noemer);
    }
}
```
Hierdoor kan ik geen ``Breuk`` objecten meer als volgt aanmaken:
```java
Breuk eenBreuk =new Breuk();
```

Maar ben ik verplicht deze als volgt aan te maken:
```java
Breuk eenBreuk =new Breuk(21,8);
```
<!---{/aside}--->
<!---NOBOOKSTART--->
{% endhint %}
<!---NOBOOKEND--->


<!---NOBOOKSTART--->
{% hint style='tip' %}
<!---NOBOOKEND--->
<!---{aside}--->
<!--- {float:right, width:50%} --->
![](../assets/care.png)
We zullen deze nieuwe informatie gebruiken om onze ``Pong``-klasse uit het eerste hoofdstuk te verbeteren door deze de nodige constructors te geven. Namelijk een default die een balletje aanmaakt dat naar rechtsonderbeweest, en één overloaded=

```java
class Balletje
{
    public Balletje()
    {
        BalX = 5;
        BalY = 5;
        VX = 1;
        VY = 1;
    }

    public Balletje(int startPosX, int startPosY, int startVX, int startVY)
    {
        BalX = startPosX;
        BalY = startPosY;
        VX= startVX;
        VY = startVY;
    }

    public int BalX { get; set; }
    public int BalY { get; set; }
    public int VX { get; set; }
    public int VY { get; set; }


    public void Update()
    {

        if (BalX + VX >= Console.WindowWidth || BalX + VX < 0)
        {
            VX = -VY;
        }


        BalX = BalX + VX;

        if (BalY + VY >= Console.WindowHeight || BalY + VY < 0)
        {
            VY = -VY;
        }

        BalY = BalY + VY;
    }

    public void TekenOpScherm()
    {
        Console.SetCursorPosition(BalX, BalY);
        Console.Write("O");      
    }
}
```

We kunnen nu op 2 manieren balletjes aanmaken:
```text
Balletje bal1 = new Balletje();
Balletje bal2 = new Balletje(10,8,-2,1);
```

<!---{/aside}--->
<!---NOBOOKSTART--->
{% endhint %}
<!---NOBOOKEND--->

<!---NOBOOKSTART--->
# Kennisclip
![](../assets/infoclip.png)

* [Overloaded constructors](https://ap.cloud.panopto.eu/Panopto/PgeboorteJaars/Viewer.aspx?id=24f83488-a058-4898-b34d-ab7a0097f165)
<!---NOBOOKEND--->

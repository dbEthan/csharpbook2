<!---{sample: true}--->
### De anatomie van een klasse

We zullen nu enkele basisconcepten van klassen en objecten toelichten aan de hand van praktische voorbeelden.

#### Object methoden

Stel dat we een klasse willen maken die ons toelaat om objecten te maken die verschillende mensen voorstellen. We willen aan iedere mens kunnen zeggen "Praat eens".

We maken een nieuwe klasse ``Mens`` en maken een plaatsen in de klasse een methode ``Praat``:

```java
class Mens
{
    public void Praat()
    {
        Console.WriteLine("Ik ben een mens!");
    }
}
```

We zien twee nieuwe aspecten:

* Het keyword **``static``** mag je **niet** voor een methode signatuur zetten (later ontdekken we wanneer dat soms wel moet) .
* Voor de methode plaatsen we ``public`` : dit is een *access modifier* die aangeeft dat de buitenwereld deze methode op het object kan aanroepen.

Je kan nu elders objecten aanmaken en ieder object z'n methode ``Praat`` aanroepen:

```java
Mens joske = new Mens();
Mens alfons = new Mens();

joske.Praat();
alfons.Praat();
```

Er zal 2x ``Ik ben een mens!`` op het scherm verschijnen. Waarbij telkens ieder object (``joske`` en ``alfons``) zelf verantwoordelijk was dat dit gebeurde.

#### Public en private access modifiers

De **access modifier** geeft aan hoe zichtbaar een bepaald deel van de klasse is. Wanneer je niet wilt dat "van buitenuit" een bepaalde methode kan aangeroepen worden, dan dien je deze als ``private`` in te stellen. Wil je dit net wel dat moet je er expliciet ``public`` voor zetten.

Test in de voorgaande klasse eens wat gebeurt wanneer je ``public`` vervangt door ``private``. Inderdaad, je zal de methode ``Praat`` niet meer op de objecten kunnen aanroepen.

{% hint style='tip' %}
Wanneer je geen access modifier voor een methode zet in C# dan zal deze als ``private`` beschouwd worden. Dit geldt voor alle zaken waar je access modifiers voor kan zetten: niets ervoor zetten wil zeggen ``private``.

Volgende twee methoden-signaturen zijn dus identiek:

```java
private void NiemandMagDitGebruiken()
{
    ...
}

void NiemandMagDitGebruiken()
{
    ...
}
```

**Het is een héél slechte gewoonte om géén access modifiers voor iedere methode te zetten. Maar er dus een gewoonte van dit steeds ogenblikkelijk te doen.**
{% endhint %}



Test volgende klasse eens, kan je de methode ``VertelGeheim`` vanuit de Main op ``joske`` aanroepen?

```java
class Mens
{
    public void Praat()
    {
        Console.WriteLine("Ik ben een mens!");
    }

    private void VertelGeheim()
    {
        Console.WriteLine("Ik ben verliefd op Anneke");
    }
}
```

<!---{pagebreak} --->


#### Reden van private

Waarom zou je bepaalde zaken ``private`` maken? 

De code binnenin een klasse kan overal aan binnen de klasse zelf. Stel dat je dus een erg complexe publieke methode hebt, en je wil deze opsplitsen in meerdere delen, dan ga je die andere delen ``private`` maken. Dit voorkomt dat programmeurs die je klasse later gebruiken, stukken code aanroepen die helemaal niet bedoeld zijn om rechtstreeks aan te roepen.

Volgende voorbeeld toont hoe je binnenin een klasse andere zaken van de klasse kunt aanroepen: we roepen in de methode ``Praat`` de methode ``VertelGeheim`` aan (die ``private`` is voor de buitenwereld, maar niet voor de code binnen de ``Praat``-methode).

```java
class Mens
{
    public void Praat()
    {
        Console.WriteLine("Ik ben een mens!");
        VertelGeheim();
    }

    private void VertelGeheim()
    {
        Console.WriteLine("Ik ben verliefd op Anneke");
    }
}
```

Als we nu elders een object laten praten als volgt:

```java
Mens rachid = new Mens();
rachid.Praat();
```

Dan zal de uitvoer worden:

{line-numbers:false}
```text
Ik ben een mens!
Ik ben verliefd op Anneke
```

{% hint style='tip' %}
Met behulp van de **dot-operator** (``.``) kunnen we aan alle informatie die ons object aanbiedt aan de buitenwereld. Ook dit zagen we reeds toen we een ``Random``-object hadden: we konden maar een handvol zaken aanroepen op zo'n object, waaronder de ``Next`` methode.
{% endhint %}


Het is natuurlijk een beetje vreemd dat nu al onze objecten zeggen dat ze verliefd zijn op Anneke. Dit is niet het smurfendorp met maar 1 meisje! Dit gaan we verderop oplossen. *Stay tuned!*


#### Instantievariabelen

Voorlopig doen alle objecten van het type ``Mens`` hetzelfde. Ze kunnen praten en zeggen hetzelfde. We weten echter dat objecten ook een interne staat hebben die per object individueel is (we zagen dit reeds toen we balletjes over het scherm lieten botsen: ieder balletje onthield z'n eigen richtingsvector en positie). Dit kunnen we dankzij **instantievariabelen** (ook wel **datavelden** of **datafields** genoemd) oplossen. Dit zullen variabelen zijn waarin zaken kunnen bewaard worden die verschillen per object.

Stel je voor dat we onze mensen een geboortejaar willen geven. Ieder object zal zelf in een instantievariabele bijhouden wanneer ze geboren zijn(het vertellen van geheimen zullen we verderop behandelen):

```java
class Mens
{
    private int geboorteJaar = 1970;  //instantievariabele

    public void Praat()
    {
        Console.WriteLine("Ik ben een mens! ");
        Console.WriteLine($"Ik ben geboren in {geboorteJaar}.");
    }
}
```

Enkele belangrijke concepten:
* De instantievariabele ``geboorteJaar`` zetten we private: we willen niet dat de buitenwereld het geboortejaar van een object kan aanpassen. Beeld je in dat dat in de echte wereld ook kon. Dan zou je naar je kameraad kunnen roepen "Hey Adil, jouw geboortejaar is nu 1799! Ha.". Waarop Adil vloekend verandert in een steenoud mannetje.
* We geven de variabele een beginwaarde ``1970``. Alle objecten zullen dus standaard in het jaar 1970 geboren zijn wanneer we deze met ``new`` aanmaken.
* We kunnen de inhoud van de instantievariabelen lezen (en veranderen) vanuit andere delen in de code. Zo gebruiken we ``geboorteJaar`` in de tweede lijn van de ``Praat`` methode. Als je die methode nu zou aanroepen dan zou het geboortejaar van het object dat je aanroept mee op het scherm verschijnen.

{% hint style='warning' %}
We moeten ook dringend enkele extra niet-officiële identifier regels in het leven roepen:
* Klassenamen en methoden in klassen beginnen altijd met een hoofdletter.
* Alles dat ``public`` is in een klasse begint ook met een hoofdletter.
* Alles dat ``private`` is begint met een kleine letter (of liggend streepje), tenzij het om eem methode gaat, die begint altijd met een hoofdletter.

Dit zijn geen officiële regels, maar afspraken die veel programmeurs onderling hebben gemaakt. Het maakt de code leesbaarder.
{% endhint %}

<!---NOBOOKSTART--->
{% hint style='tip' %}
<!---NOBOOKEND--->
<!---{aside}--->
<!--- {float:right, width:50%} --->
![](../assets/gotopolice.png)
Wat?! Ik ben hier niet voor jou? Omdat je geen ``goto`` hebt gebruikt?! Flink hoor. Maar daarvoor ben ik hier niet. Ik zag je wel denken: "Als ik nu die instantievariabele ook eens ``public`` maak."

Niet doen. Simpel! **Instantievariabele mogen NOOIT ``public`` gezet worden.** De C# standaard laat dit weliswaar toe, maar dit is één van de slechtste programmeerdingen die je kan doen. Wil je toch de interne staat van een object kunnen aanpassen dan gaan we dat via **properties** en **methoden** kunnen doen, wat we zo meteen gaan uitleggen. Zie dat ik hier niet te vaak tussenbeide moet komen. Dank!
<!---{/aside}--->
<!---NOBOOKSTART--->
{% endhint %}
<!---NOBOOKEND--->

Ok, we zullen maar luisteren naar meneer de agent. Stel nu dat we een verjongingsstraal hebben waarmee we het geboortejaar van de mensen steeds met 1 jaar kunnen verhogen (en ze dus een jaar jonger maken!)

```java
class Mens
{
    private int geboorteJaar = 1970;  
    public void Praat()
    {
        Console.WriteLine("Ik ben een mens! ");
        Console.WriteLine($"Ik ben geboren in {geboorteJaar}.");
    }
    public void StartVerjongingskuur()
    {
        Console.WriteLine("Jeuj. Ik word jonger!");
        geboorteJaar--;
        Praat();
    }
}
```
Zoals al gezegd: **Ieder object zal z'n eigen geboortejaar hebben.**

Die laatste opmerking is een kernconcept van OOP: ieder object heeft z'n eigen interne staat die kan aangepast worden individueel van de andere objecten van hetzelfde type. We zullen dit testen in volgende voorbeeld waarin we 2 objecten maken en enkel 1 ervan verjongen. Kijk wat er gebeurt:

```java
Mens elvis = new Mens();
Mens bono = new Mens();
elvis.StartVerjongingskuur();
elvis.Praat();
bono.Praat();
```

Als je deze code zou uitvoeren zal je zien dat het geboortejaar van Elvis verhoogd en niet die van Bono wanneer we ``StartVerjongingskuur`` aanroepen. Zoals het hoort!

<!---NOBOOKSTART--->
{% hint style='tip' %}
<!---NOBOOKEND--->
<!---{aside}--->
<!--- {float:right, width:50%} --->
![](../assets/care.png)
"Ja maar, nu pas je toch het geboortejaar van buitenuit aan via een methode, ook al gaf je aan dat dit niet de bedoeling was want dan zou je Adil ogenblikkelijk erg jong kunnen maken."

Correct. Maar dat was dus maar een voorbeeld. De hoofdreden dat we instantievariabelen niet zomaar ``public`` mogen maken is om te voorkomen dat de buitenwereld instantievariabelen waarden geeft die de werking van de klasse zouden stuk maken. Stel je voor dat je dit kon doen: ``adil.geboortejaar = -12000;``

Dit kan nefaste gevolgen hebben voor de klasse.

Daarom gaan we de toegang tot instantievariabelen als het ware controleren door deze enkel via properties en methoden toe te laten. We zouden dan bijvoorbeeld het volgende kunnen doen:

```csharp
class Mens
{
    private int geboorteJaar = 1970;

    public void VeranderGeboortejaar(int geboorteJaarIn)
    {
        if(geboorteJaarIn >= 0)
            geboorteJaar = geboorteJaarIn;
    }
```

Mooi he. Zo voorkomen we dus dat de buitenwereld illegale waarden aan een variabele kan geven. **Objecten zijn verantwoordelijk voor zichzelf** en moeten zichzelf dus ook beschermen zodat de buitenwereld niets met hen doet dat hun eigen werking om zeep helpt.

<!---{/aside}--->
<!---NOBOOKSTART--->
{% endhint %}
<!---NOBOOKEND--->

<!---{pagebreak} --->


#### Andere lieven

We kunnen nu het probleem oplossen dat al onze mensen verliefd zijn op Anneke. Volgende code toont dit:

```java
class Mens
{
    private string lief = "niemand";

    public VeranderLief(string nieuwLief)
    {
        lief = nieuwLief;
    }
    public void Praat()
    {
        Console.WriteLine("Ik ben een mens!");
        VertelGeheim();
    }

    private void VertelGeheim()
    {
        if( lief != "niemand")
            Console.WriteLine($"Ik ben verliefd op {lief}");
        else
            Console.WriteLine("Ik ben op niemand verliefd.");
    }
}
```

Nu kunnen we dus "Temptation Island - de OOP editie" beginnen:

```java
Mens deelnemer1 = new Mens();
Mens deelnemer2 = new Mens();
deelnemer1.Praat();
deelnemer2.Praat();

deelnemer2.VeranderLief("phoebe");
deelnemer1.Praat();
deelnemer2.Praat();

deelnemer1.VeranderLief("camilla");
deelnemer1.Praat();
deelnemer2.Praat();
```

<!---{sample: false}--->
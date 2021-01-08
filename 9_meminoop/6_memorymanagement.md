# Geheugenmanagement, uitzonderingen en namespaces

## Geheugenmanagement in C#

In het vorige boekdeel deden we reeds uit de doeken dat variabelen op 2 manieren in het geheugen kunnen leven:

* **Value types**: waren variabelen wiens waarde rechtstreeks op de geheugenplek stonden waar de variabele naar verwees. Dit gold voor alle bestaande, ingebakken datatypes zoals ``int``, ``bool``, ``char`` etc. alsook voor ``enum`` types.
* **Reference types**: deze variabelen bevatten als inhoud een geheugenadres naar een andere plek in het geheugen waarde effectieve waarde van deze variabele stond. We zagen dat dit voorlopig enkel bij arrays gebeurde

**Ook objecten zijn reference types.** Alhoewel het vorige boek liet uitschijnen dat vooral value type variabelen veelvuldig in programma's voorkwamen, zal je nu ontdekken dat reference types véél meer voorkomen, simpelweg omdat quasi alles in OOP **objecten** zijn (en dus ook arrays van objecten).

Om goed te begrijpen waarom reference types zo belangrijk zijn, zullen we nu eerst eens inzoomen op hoe het geheugen van een C# applicatie werkt. 

### Stack en heap

In het vorige boek toonden we hoe alle variabelen in één grote "wolk geheugen" zitten, ongeacht of ze nu value types of reference types zijn. Dat klopt niet helemaal. Eigenlijk zijn er **2 soorten geheugens** die een C# applicatie tot z'n beschikking heeft.

 Wanneer een C# applicatie wordt uitgevoerd krijgt het twee soorten geheugen toegewezen dat het 'naar hartelust' kan gebruiken, namelijk:

1. Het kleine, maar snelle **stack** geheugen.
2. Het grote, maar tragere **heap** geheugen.

Afhankelijk van het soort variabele wordt ofwel de stack, ofwel de heap gebruikt. **Het is uitermate belangrijk dat je weet in welk geheugen de variabele zal bewaard worden!** Je hebt hier geen controle over, maar het beïnvloed wel de manier waarop je code zal werken.

Volgende tabel vat samen welke type in welk geheugen wordt bewaard:

|         | Value types           | Reference types  |
| ------------- |-------------| -----|
|Inhoud van de variabele    | De eigenlijke data | Een referentie naar de eigenlijke data |
|Locatie      |  **Stack**      |   **Heap**  |
| Beginwaarde | ``0``,``0.0``, ``""``,``false``, etc.      |    ``null`` |
| Effect van de ``=`` operator | Kopieert de actuele waarde     |   Kopieert het adres naar de actuele waarde |

![Stack en heap](../assets/5_arrays/gc1.png)

### Waarom twee geheugens?

Waarom plaatsen we niet alles in de stack? De reden hiervoor is dat bij het compileren van je applicatie er reeds zal berekend worden hoeveel geheugen de stack zal nodig hebben. Wanneer je programma dus later wordt uitgevoerd weet het OS perfect hoeveel geheugen het minstens moet reserveren bij het besturingssysteem.

Er is echter een probleem: de compiler kan niet alles perfect berekenen of voorspellen. Een variabele van het type ``int`` is perfect geweten hoe groot die zal zijn (32 bit). Maar wat met een string die je aan de gebruiker vraagt? Of wat met een array waarvan we pas tijdens de uitvoer de lengte gaan berekenen gebaseerd op *runtime* informatie?

Het zou nutteloos (en zonde) zijn om reeds bij aanvang een bepaalde hoeveelheid stackgeheugen voor een array te reserveren als we niet weten hoe groot die zal worden. Beeld je in dat alle applicaties op je computer *voor alle zekerheid* een halve gigabyte aan geheugen zouden vragen: "just in case". Je computer zou enkele terrabyte aan geheugen nodig hebben. Het is dus veel realistischer om enkel het geheugen te reserveren waar de compiler 100% zeker van is dat deze zal nodig zijn.

De heap laat ons toe om geheugen op een wat minder gestructureerde manier in te palmen. Tijdens de uitvoer van het programma zal de heap als het ware dienst doen als een grote zandbak waar eender welke plek kan ingepalmd worden om zaken te bewaren (op voorwaarde dat die vrij is natuurlijk) De stack daarentegen is het kleine bankje naast de zandbak: handig, snel, en perfect geweten hoe groot.

### Value types in de stack

**Value** type variabelen worden in de stack bewaard. **De effectieve waarde van de variabele wordt in de stack bewaard.**
Dit zijn alle gekende, 'eenvoudige' datatypes die we totnogtoe gezien hebben, inclusief enums en structs:
* ``sbyte``, ``byte``
* ``short``, ``ushort``
* ``int``, ``uint``
* ``long``, ``ulong``
* ``char``
* ``float``, ``double``, ``decimal``
* ``bool``
* structs (niet besproken in dit boek)
* enums (zie het vorige boek)

### = operator bij value types

Wanneer we een value-type willen kopiëren gebruiken we de =-operator die de waarde van de rechtse operand zal uitlezen en zal kopiëren naar de linkse operand:

```java
int getal = 3;
int anderGetal = getal;
```

Vanaf nu zal ``anderGetal`` de waarde ``3`` hebben. Als we nu één van beide variabelen aanpassen dan zal dit **geen** effect hebben op de andere variabelen.

We zien hetzelfde effect wanneer we een methode maken die een parameter van het value type aanvaardt: we geven een kopie van de variabele mee:

```java
void VerhoogParameter(int a)
{
    a++;
    Console.WriteLine($"In methode {a}");
}

//Elders:
int getal = 5;
VerhoogParameter(getal);
Console.WriteLine($"Na methode {getal}");
```

De parameter ``a`` zal de waarde ``5`` gekopieerd krijgen. Maar wanneer we nu zaken aanpassen in ``a`` zal dit geen effect hebben op de waarde van ``getal``.

De output van bovenstaand programma zal zijn:
```
In methode 6
Na methode 5
```

### Reference types

**Reference** types worden in de heap bewaard. De *effectieve waarde* wordt in de heap bewaard, en in de stack zal enkel een **referentie** of **pointer** naar de data in de heap bewaard worden. Een referentie (of pointer) is niet meer dan het geheugenadres naar waar verwezen wordt (bv. ``0xA3B3163``)  Concreet zijn dit alle zaken die vaak redelijk groot zullen zijn of waarvan op voorhand niet kan voorspeld worden hoe groot ze *at runtime* zullen zijn, namelijk:
* objecten, interfaces en delegates (die laatste behandelen we niet in dit boek).
* arrays.

### = operator bij reference types
Wanneer we de = operator gebruiken bij een reference type dan kopiëren we de referentie naar de waarde van de rechtse operand, niet de waarde zelf.

#### Bij objecten

We zien dit gedrag bij alle reference types, zoals objecten:
```java
Student stud = new Student();
```

Wat gebeurt er hier?

1. ``new Student()``  : ``new`` roept de constructor van ``Student`` aan. Deze zal een constructor in de **heap** aanmaken en vervolgens de geheugenlocatie teruggeven.
2. Een variabele ``stud`` wordt in de **stack** aangemaakt.
3. De geheugenlocatie uit de eerste stap wordt vervolgens in ``stud`` opgeslagen in de stack.

Laten we eens inzoomen op voorgaande door de code even in 2 delen op te splitsen:

```java
Student stud;
stud = new Student();
```

Het geheugen na lijn 1 ziet er zo uit:

![](../assets/6_klassen/memzoom1.png)

Lijn 2 gaan we nog trager bekijken. Eerst zal het gedeelte rechts van de ``=``-operator uitgevoerd worden. Er wordt dus **in de heap** een nieuw ``Student``-object aangemaakt:

![](../assets/6_klassen/memzoom2.png)

Vervolgens wordt de toekenning toegepast en wordt het geheugenadres van het object in de variabele ``stud`` geplaatst:

![](../assets/6_klassen/memzoom3.png)

{% hint style='warning' %}
We gaan nogal licht over het ``new``-keyword. Maar zoals je merkt is dit een ongelooflijk belangrijk mechanisme in de wereld van de objecten. Het brengt letterlijk objecten tot leven (in de heap) en zal als resultaat laten weten op welke plek in het geheugen het object staat.
{% endhint %}

#### Bij arrays

Zoals we in het vorige boek hebben gezien zien we het zelfde gedrag bij arrays:

```java
int[] nummers = {4,5,10};
int[] andereNummers = nummers;
```

In dit voorbeeld zal ``andereNummers`` nu dus ook verwijzen naar de array in de heap waar de actuele waarden staan.

Als we dus volgende code uitvoeren dan ontdekken we dat beide variabele naar dezelfde array verwijzen:

```java
andereNummers[0] = 999;
Console.WriteLine(andereNummers[0]);
Console.WriteLine(nummers[0]);
```

We zullen dus als output krijgen:

```
999
999
```

Hetzelfde gedrag zien we bij objecten:

```java
Student a = new Student("Abba");
Student b = new Student("Queen");
a = b;
Console.WriteLine(a.Naam);
```

We zullen in dit geval dus ``Queen`` op het scherm zien omdat zowel ``b`` als ``a`` naar het zelfde object in de heap verwijzen. Het originele "abba"-object zijn we kwijt en zal verdwijnen (zie Garbage collector verderop).

{% hint style='warning' %}
De meeste klassen zullen met value type-properties en instantievariabelen werken in zich, toch worden ook samen met het gehele object in de heap bewaard en niet in de stack. Kortom **het hele object** ongeacht de vorm van z'n inhoud wordt in de heap bewaard.
{% endhint %}

### Methoden en reference parameters

Ook bij methoden geven we de dus de referentie naar de waarde mee. In de methode kunnen we dus zaken aanpassen van de parameter en dan passen we eigenlijk de originele variabele aan:
```java
void VerhoogEersteElementInArray(int[] a)
{
   a[0]++;
   Console.WriteLine($"In methode {a[0]}");
}

//Elders:
int[] getallen = {5,3,2};
VerhoogEersteElementInArray(getallen);
Console.WriteLine($"Na methode {getallen[0]}");
```

We krijgen als uitvoer:
```
In methode 6
Na methode 6
```

{% hint style='warning' %}
**Opgelet:** Wanneer we een methode hebben die een value type aanvaardt en we geven één element van de array mee dan geven we dus een kopie van de actuele waarde mee!
{% endhint %}

```java
void VerhoogParameter(int a)
{
    a++;
    Console.WriteLine($"In methode {a}");
}

//Elders:
int[] getallen = {5,3,2};
VerhoogParameter(getallen[0]); //<= VALUE TYPE!
Console.WriteLine($"Na methode {getallen[0]}");
```

De output bewijst dit:

```
In methode 6
Na methode 5
```

### De Garbage Collector 
Een essentiëel onderdeel van .NET is de zogenaamde GC, de **Garbage Collector**. Dit is een geautomatiseerd onderdeel van ieder C# programma dat ervoor zorgt dat we geen geheugen nodeloos gereserveerd houden.
De GC zal geregeld het geheugen doorlopen en kijken of er in de heap data staat waar geen referenties naar verwijzen. Indien er geen referenties naar wijzen zal dit stuk data verwijderd worden.

![Data in de heap waar geen referenties naar wijzen zullen ten gepaste tijde verwijderd worden](../assets/5_arrays/gc2.png)

In dit voorbeeld zien we dit in actie:

```java
int[] array1 = {1,2,3};
int[] array2 = {3,4,5};
array2 = array1;
```

Vanaf de laatste lijn zal er geen referentie meer naar ``{3,4,5}`` zijn in de heap, daar we deze hebben overschreven met een referentie naar ``{1,2,3}``. De GC zal dus deze data verwijderen.

Wil je dat niet dan zal je dus minstens 1 variabele moeten hebben die naar de data verwijst. Volgend voorbeeld toont dit:

```java
int[] array1 = {1,2,3};
int[] array2 = {3,4,5};
int[] bewaarArray = array2;
array2 = array;
```
De variabele ``bewaarArray`` houdt dus een referentie naar ``{3,4,5}`` bij en we kunnen dus later via deze variabele alsnog aan de originele data.

{% hint style='warning' %}
De GC werkt niet continue daar dit te veel overhead van je computer zou vereisen. De GC zal gewoon om de zoveel tijd alle gereserveerde geheugenplekken van de applicatie controleren en die delen verwijderen die niet meer nodig zijn.  
Je kan de GC manueel de opdracht geven om een opkuisbeurt te starten (``GC.Collect()``) maar dit is ten stelligste af te raden! De GC weet meestal beter dan ons wanneer er gekuist moet worden.
{% endhint %}

<!---NOBOOKSTART--->
# Meer weten?

Voor meer info, lees zeker volgende artikels:
* [Reference en value types](https://www.c-sharpcorner.com/uploadfile/prvn_131971/types-in-C-Sharp/)
* [Stack vs heap](https://www.c-sharpcorner.com/article/C-Sharp-heaping-vs-stacking-in-net-part-i/)

# Kennisclip
![](../assets/infoclip.png)
* [Stack vs heap](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=bf7ea9bc-7469-446b-b226-ab5e008085a8)
* [Stack Overflow Exception](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=640a52f0-9ea0-42fc-b1f6-ab7a0093eda6)
<!---NOBOOKEND--->

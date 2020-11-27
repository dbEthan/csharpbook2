# Gevorderde overervingsconcepten

C# houdt van objecten. De hele taal is letterlijk opgebouwd om maximaal het object georiënteerd programmeren te omarmen. Van zodra je een nieuw project aanmaakt kan je niet naast de ``class Program`` zien. Hoe meer je C# en de bestaande bibliotheken bekijkt, hoe duidelijker dit wordt. Alles is een klasse. Maar dan stel zich natuurlijk de vraag. "Staat er nog iets boven alle klassen die wij aan het maken zijn?" Is er een soort oer-klasse waar alle klassen van overerven? 
De vraag stellen is ze beantwoorden! Er is effectief een oer-klasse, de ``System.Object``-klasse, waar alles en iedereen in C# van moet overerven.



## System.Object 
**Alle** klassen C# zijn afstammelingen van de ``System.Object`` klasse. Zowel de bestaande, ingebouwde klassen zoals ``Random`` en ``Console`` alsook klassen die je zelf maakt. En ja, zelfs de bestaande valuetype datypes zoals ``int`` en ``bool`` zijn afstammelingen van ``System.Object`` (er zit wel nog één klasse tussen in hun geval, de ``ValueType`` klasse) 

![Enkele voorbeelden. Merk op dat er véél meer ingebouwde klassen in .NET zitten dan degene die we hier tonen.](../assets/7_overerving/systemroot.png)


Indien je een klasse schrijft zonder een expliciete parent dan zal deze steeds ``System.Object`` als rechtstreekse parent hebben. Ook afgeleide klassen stammen dus af uiteindelijk af van ``System.Object``. Concreet wil dit zeggen dat alle klassen ``System.Object``-klassen zijn en dus ook de bijhorende functionaliteit ervan hebben.

{% hint style='tip' %}
Indien je de ``System`` namespace in je project gebruikt door bovenaan ``using System;`` te schrijven dan moet je dus niet altijd ``System.Object`` schrijven maar mag je ook **``Object``** schrijven.
Maar om de klasse ``Object`` niet te verwarren met hel concept "object" zullen we hier steeds praten over ``System.object`` (en zo tonen we nogmaals aan waarom namespaces nuttig zijn: ze halen dubbelzinnigheden uit onze code).
{% endhint %}

### Impliciete overerving

Wanneer je dus een klasse ``Student`` aanmaakt als volgt:

```java
class Student
{

}
```

Dan gebeurt er een zogenaamde impliciete overerving van ``System.Object``. Er staat dus eigenlijk:

```java
class Student: System.Object
{

}
```
Je mag dat trouwens ook expliciet zelf schrijven, dat maakt niet uit. Maar van zodra je een klasse schrijft die nergens expliciet van overerft, dan zal deze dus automatisch van ``System.Object`` overerven.


### Hoe ziet System.Object er uit?
Wanneer je een lege klasse maakt dan zal je misschien al gezien hebben dat instanties van deze nieuwe klasse reeds 4 methoden ingebouwd hebben, dit zijn uiteraard de methoden die in de ``System.Object`` klasse staan gedefiniëerd:

|Methode| Beschrijving|
|-------| ------------|
|``Equals()``| Gebruikt om te ontdekken of twee instanties gelijk zijn. |
|``GetHashCode()``| Geeft een unieke code (*hash*) terug van het object; nuttig om o.a. te sorteren.|
|``GetType()``| Geeft het datatype (de klasse) van het object terug.|
|``ToString()``| Geeft een ``string`` terug die het object voorstelt.|

Deze methoden zijn redelijk nutteloos in het begin. Enkel door ze zelf te ``overriden`` zullen ze hun nut bewijzen. Uiteraard kan je de de methoden testen om te zien wat er gebeurt.


### GetType()
Stel dat je een klasse Student hebt gemaakt in je project. Je kan dan op een object van deze klasse de GetType() -methode aanroepen om te weten wat het type van dit object is:

```java
Student stud1= new Student();
Console.WriteLine(stud1.GetType());
```

Dit zal als uitvoer de namespace gevolgd door het type van het object op het scherm geven . Als je project bijvoorbeeld "StudentManager" heet (en je namespace dus vermoedelijk ook) dan zal er op het scherm verschijnen: ``StudentManager.Student``.

Wil je enkel het type zonder namespace dan is het nuttig te beseffen dat ``GetType()`` eigenlijk een object teruggeeft van het type ``Type`` met meerdere eigenschappen, waaronder ``Name``. Volgende code zal dus enkel ``Student`` op het scherm tonen:

```java
Student stud1= new Student();
Console.WriteLine(stud1.GetType().Name);
```

{% hint style='tip' %}
Je kan in de .NET documentatie altijd opzoeken waar een klasse van overerft. De ``Type`` klasse bijvoorbeeld erft, je raadt het nooit, finaal ook van ``System.Object`` over. Eerst erft ``Type`` over van de ``MemberInfo`` klasse, die op zijn beurt overerft van de oer-klasse. Bekijk dit zelf maar eens op [docs.microsoft.com/en-us/dotnet/api/system.type](https://docs.microsoft.com/en-us/dotnet/api/system.type):
![](../assets/7_overerving/typeclass.png)

{% endhint %}

### ToString()
Deze methode is de nuttigste waar je al direct leuke dingen mee kan doen die je programmeursleven, hopelijk, wat gaan vereenvoudigen. 

Wanneer je schrijft:
```java
Console.WriteLine(stud1);
```
Wordt er eigenlijk een impliciete aanroep naar ``ToString`` gedaan. Er staat dus eigenlijk altijd:
```java
Console.WriteLine(stud1.ToString());
```

Op het scherm verschijnt dan ``StudentManager.Student``. Waarom? Wel, de methode ToString() wordt in System.Object() ongeveer als volgt beschreven:
```java
public virtual string ToString()
{ 
    return GetType(); 
}
 ```

Merk twee zaken op:

 1. GetType wordt aangeroepen en die output krijg je dus terug.
 2. De methode is **virtual** gedefinieerd.

 **Alle 4 methoden in System.Object zijn ``virtual`` , en je kan deze dus ``override``'n!**

 Nu komen we tot het hart van deze methoden. Aangezien ze alle 4 ``virtual`` zijn, kunnen we de werking ervan dus naar onze hand zetten in onze eigen klassen. Aardig wat .NET bibliotheken rekenen er namelijk op dat je deze methoden op de juiste manier hebt aangepast, zodat ook jouw nieuwe klassen perfect kunnen samenwerken met deze bibliotheken. Een eerste voorbeeld hiervan toonden we net: de ``Console.WriteLine`` methode gebruikt van iedere parameter dat je er aan meegeeft de ``ToString``-methode om de parameter op het scherm als ``string`` te tonen.
 
 #### ToString() overriden
 Het zou natuurlijk fijner zijn dat de ``ToString()-``methode van onze student nuttigere info teruggeeft, zoals bijvoorbeeld de ``Voornaam`` die we als autoprop in de klassen hebben geplaatst, gevolgd door de ``Leeftijd`` (ook een autoprop). 
 
 We kunnen dat eenvoudig verkrijgen door gewoon ``ToString`` to overriden:
 ```java
 class Student
 {
   public int Leeftijd {get;set;}
   public string Voornaam {get;set;}
   
   public override string ToString()
   {
       return $"Student genaamd {Voornaam} (Leeftijd:{Leeftijd})";
   }
 }
 ```
 Wanneer je nu ``Console.WriteLine(stud1);`` (gelet dat hij een Voornaam en Leeftijd heeft) zou schrijven dan wordt je output: ``Student Tim Dams (Leeftijd:35)``.

 {% hint style='tip' %}
 Een extra handigheidje van ``ToString`` is dat deze methode wordt gebruikt tijdens het debuggen om je objecten samen te vatten in het watch-venster:

 ![](../assets/7_overerving/tostringdebug.png)
 {% endhint %}
 
 
 ### Equals()
 Ook deze methode kan je dus overriden om twee objecten met elkaar te vergelijken. Op het  einde van dit boek zal dieper in ``Equals`` ingaan worden om objecten te vergelijken, maar we tonen hier reeds een voorbeeld:

 ```java
if(stud1.Equals(stud2))
   //...
```

De ``Equals`` methode heeft  als signatuur: ``public virtual bool Equals(Object o)``
Twee objecten zijn gelijk voor .NET als aan volgende afspraken wordt voldaan:

* Het moet ``false`` teruggeven indien de parameter ``o`` ``null`` is
* Het moet ``true`` teruggeven indien je het object met zichzelf vergelijkt (bv ``stud1.Equals(stud1)``)
* Het mag enkel ``true`` teruggeven als volgende statements beide waar zijn:
```java
stud1.Equals(stud2);
stud2.Equals(stud1);
```
* Indien ``stud1.Equals(stud2)`` true teruggeeft en ``stud1.Equals(stud3)`` ook true is, dan moet ``stud2.Equals(stud3)`` ook true zijn.


#### Equals overriden
Het is echter aan de maker van de klasse om te beslissen wanneer 2 objecten van een zelfde type gelijk zijn. Het is dus niet zo dat iedere waarde van een instantievariabele bijvoorbeeld gelijk moet zijn opdat 2 objecten gelijk zijn. Alles hangt af van de wijze waarop de klasse dienst moet doen.

Stel dat we vinden dat een student gelijk is aan een andere student indien z'n Voornaam en Leeftijd dezelfde is, we kunnen dan de Equals-methode overriden als volgt:

```java
//In de Student class
public override bool Equals(Object o)
{
     
     if(GetType() != o.GetType()) 
         return false;
     else
     {
         Student temp= (Student)o; //Zie opmerking na code!
         if(Leeftijd== temp.Leeftijd && Voornaam== temp.Voornaam)
            return true;
     }
     return false;

}
```

{% hint style='tip' %}
De lijn ``Student temp = (Student)o;`` zal het ``object o`` casten naar een ``Student``. Doe je dit niet dan kan je niet aan de interne Student-variabelen van het ``object o``. Dit concept, **polymorfisme**, bespreken we verderop in het boek.
{% endhint %}


### GetHashcode
Indien je ``Equals`` override dan moet je eigenlijk ook ``GetHashCode`` overriden, daar er wordt verondersteld dat twee gelijke objecten ook dezelfde unieke hashcode teruggeven. Wil je dit dus implementeren dan zal je dus een (bestaand) algoritme moeten schrijven dat een uniek nummer genereert voor ieder niet-gelijke object. 
Algoritmes bespreken om zelf een hash te genereren ligt niet in de scope van dit boek. 



<!---NOBOOKSTART--->
{% hint style='tip' %}
<!---NOBOOKEND--->
<!---{aside}--->
<!--- {float:right, width:50%} --->
![](../assets/care.png)
# Ik ben nog niet helemaal mee
Niet getreurd, je bent niet de enige. Overerving,``System.Object``, ``Equals``,...het is allemaal een hoop nieuwe kennis om te verwerken. 
Hou vol, we zijn een hoop puzzelstukjes aan het opnemen die finaal zullen samenkomen om een gigantisch knappe OOPuzzel te maken (see what we did there?)

<!---{/aside}--->
<!---NOBOOKSTART--->
{% endhint %}
<!---NOBOOKEND--->


<!---NOBOOKSTART--->
# Kennisclip
![](../assets/infoclip.png)
* [System.Object en ToString](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=00cad992-7714-4051-a992-ab7d0093864b)
* [Equals - objecten vergelijken](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=c18b27c9-ad5a-444b-9695-ab7d00c2c3d9)
<!---NOBOOKEND--->
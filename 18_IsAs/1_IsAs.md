## Is en As
Dankzij polymorfisme kunnen we dus child en parent-objecten door elkaar gebruiken. De keywords ``is`` en ``as`` gaan ons helpen om door het bos van objecten het bos nog te zien. 

### Is keyword
Het ``is`` keyword is een operator die je kan gebruiken om te weten te komen of:
* Een object van een bepaalde datatype is
* Een object een bepaalde interface bevat (zie volgende hoofdstuk)

De ``is`` operator heeft twee operanten nodig en geeft een bool terug als resultaat. De linkse operator moet een variabele zijn, de rechtse een datatype. Bijvoorbeeld:

```java
if( mijnStudent is Student)
```

#### Is voorbeeld 1
Stel dat we volgende drie klassen hebben:
```java
class Voertuig {}

class Auto: Voertuig{}

class Persoon {}
```
Een Auto **is** een Voertuig.
Een Persoon **is géén** Voertuig.

Stel dat we enkele variabelen hebben als volgt:
```java
Auto myAuto= new Auto();
Persoon rambo= new Persoon();
```

We kunnen nu de objecten met ``is`` bevragen of ze van een bepaalde type zijn:
```java
if(myAuto is Voertuig)
{
    Console.WriteLine("The first object is a Voertuig");
}
if(rambo is Voertuig)
{
    Console.WriteLine("The second object is a Voertuig");
}
```

De uitvoer zal worden:``The first object is a Voertuig``.

Met polymorfisme wordt dit voorbeeld echter interessanter. Wat als we een hoop objecten in een lijst van voertuigen plaatsen en nu enkel met de auto's iets willen doen, dan kan dat:

```java
List<Voertuig> alleMiddelen = new List<Voertuig>();
alleMiddelen.Add(new Voertuig());
alleMiddelen.Add(new Auto());
alleMiddelen.Add(new Voertuig());
foreach (var middel in alleMiddelen)
{
    if(middel is Auto)
    {
        //Doe iets met middel
    }
}
```

### As keyword met voorbeeld
Wanneer we objecten van het ene naar het andere type willen omzetten dan doen we dit vaak met behulp van casting:
```java
Student fritz= new Student();
Mens jos = (Mens)fritz;
```

 Het probleem bij casting is dat dit niet altijd lukt. Indien de conversie niet mogelijk is zal een uitzondering gegenereerd worden en je programma zal  crashen als  je niet aan exception handling doet.

 Het ``as`` keyword lost dit op. Het keyword zegt aan de compiler **"probeer dit object te converteren. Als het niet lukt, zet het dan op ``null`` in plaats van een Exception te werpen."**
 
 De code van daarnet herschrijven we dan naar:

 ```java
Student fritz= new Student();
Mens jos =fritz as Mens;
```

Indien nu de casting niet lukt (omdat ``Student`` misschien geen childklasse van ``Mens`` blijkt te zijn) dan zal ``jos`` de waarde ``null`` hebben gekregen.

We kunnen dan vervolgens bijvoorbeeld schrijven:
 ```java
Student fritz= new Student();
Mens jos =fritz as Mens;
if(jos!=null)
{
    //Doe Mens-zaken   
}
```

<!---NOBOOKSTART--->
{% hint style='warning' %}
<!---NOBOOKEND--->
<!---{aside}--->
<!--- {float:right, width:50%} --->
![](../assets/Autoe.png)

De ``is`` en ``as`` keywords laten toe om meer dynamische code te schrijven. Mogelijk weet je niet op voorhand wat voor datatype je code zal moeten verwerken en wordt polymorfisme je oplossing. Maar dan? Dan komen ``is`` en ``as`` to the rescue!

Je , dank zij polymorfisme, gevuld lijst van objecten van allerhande typen wordt nu beheersbaarder. Je kan nu , met ``is`` een element bevragen of hij van een bepaald type is. Vervolgens kan je met ``as`` het element even 'omzetten' naar z'n effectieve type (en dus meer doen dan wat hij kan in de vermomming van z'n eigen basistype).

<!---{/aside}--->
<!---NOBOOKSTART--->
{% endhint %}
<!---NOBOOKEND--->

<!---NOBOOKSTART--->
# Kennisclip
![](../assets/infoclip.png)

* [Is en as keywords](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=aba3bca4-ed3a-4067-a611-ab7d00cc2178)
<!---NOBOOKEND--->
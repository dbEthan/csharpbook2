## Bestaande interfaces in .NET

De bestaande .NET klassen gebruiken vaak interfaces om bepaalde zaken uit te voeren. Zo heeft .NET tal van interfaces gedefiniëerd (bv. ``IEnumerable``, ``IDisposable``, ``IList``, ``IQueryable`` etc.) waar je zelfgemaakte klassen mogelijk aan moeten voldoen indien ze bepaalde bestaande methoden wensen te gebruiken. Een typisch voorbeeld is het gebruik van de ``Array.Sort`` methode. Hier wordt het echte nut van interfaces erg duidelijk: de ontwikkelaars van .NET kunnen niet voorspellen hoe andere ontwikkelaars hun bibliotheken gaan gebruiken. Via interfaces geven ze als het ware krijtlijnen en vanaf dan moeten de ontwikkelaars zelf maar bepalen hoe hun nieuwe klassen zullen samenwerken met die van .NET.


### Sorteren met Array.Sort en de IComparable interface

Een veelgebruikte .NET interface is de ``IComparable`` interface. Deze wordt gebruikt indien .NET bijvoorbeeld een array van objecten wil sorteren. Bij wijze van demonstratie zullen we tonen waarom deze interface erg nuttig kan zijn. 

#### Stap 1: Het probleem
Indien je een array van objecten hebt en je wenst deze te sorteren via ``Array.Sort`` dan dienen de objecten dus de ``IComparable`` interface te hebben. 

We willen een array van landen kunnen sorteren op grootte van oppervlakte.

Stel dat we de klasse ``Land`` hebben:
```java
class Land
{
    public string Naam {get;set;}
    public int Oppervlakte {get;set;}
    public int Inwoners {get;set;}
}
```
We plaatsen 3 landen in een array:
```java
Land[] eurolanden = new Land[3];
eurolanden[0] = new Land() {Naam = "België", Oppervlakte = 5, Inwoners = 2000};
eurolanden[1] = new Land() {Naam = "Frankrijk", Oppervlakte = 7, Inwoners = 2500};
eurolanden[2] = new Land() {Naam = "Nederland", Oppervlakte = 6, Inwoners = 1800};
```
Wanneer we nu zouden proberen de landen te sorteren:
```java
Array.Sort(eurolanden);
```
Dan treedt er een uitzondering op:``InvalidOperationException: Failed to compare two elements in the array``. Dit is erg logisch: .NET heeft geen flauw benul hoe objecten van het type ``Land`` moeten gesorteerd worden. Moet dit alfabetisch volgens de ``Naam`` property, of van groot naar klein op aantan ``Inwoners``. Enkel jij als ontwikkelaar weet momenteel hoe er gesorteerd moet worden. 

#### Stap 2: IComparable onderzoeken
We kunnen dit oplossen door de ``IComparable`` interface in de klasse ``Land`` te implementeren. We bekijken daarom eerst de documentatie van deze interface ([hier](https://msdn.microsoft.com/en-us/library/system.icomparable.aspx)).

De interface is beschreven als:

```java
interface IComparable
{
    int CompareTo(Object obj);
}
```

{% hint style='warning' %}
**OPGELET: Deze interface bestaat al in .NET en mag je dus niet opnieuw in code schrijven!**
{% endhint %}


Daarbij moet de methode een ``int`` teruggeven als volgt:

| Waarde        | Betekenis           |
|:------------- |:-------------|
| Getal kleiner dan 0      | Huidig object komt **voor** het ``obj`` dat als parameter werd meegegeven. |
|  0      | Huidig object komt op **dezelfde** positie als  ``obj``  werd meegegeven. |
| Getal groter dan 0      | Huidig object komt **na** het ``obj`` dat als parameter werd meegegeven. |

De ``Array.Sort`` methode zal werken tegen deze ``IComparable`` interface om juist te kunnen sorteren. Het verwacht dat de klasse in kwestie een ``int`` teruggeeft volgens de afspraken van de tabel hierboven. 

#### Stap 3: IComparable in Land implementeren

We zorgen er nu voor dat ``Land`` deze interface implementeert. Daarbij willen we dat *de landen volgens oppervlakte worden gesorteerd* :
```java
class Land: IComparable
{
    //....

    public int CompareTo(object obj)
    {
        Land temp =  obj as Land;
        if(temp != null)
        { 
            
            if(Oppervlakte > temp.Oppervlakte) 
                return 1;
            if(Oppervlakte < temp.Oppervlakte) 
                return -1;
            return 0;
        }
        else
            throw new ArgumentException("Object is not a Land"); 
    }
}
```

Nu zal de ``Sort`` werken:
```java
Array.Sort(eurolanden);
```
De ``Sort()``-methode kan nu ieder object bevragen via de ``CompareTo()``-methode en zo volgens een eigen sorteeralgoritme de landen in de juiste volgorde plaatsen. 

Stel dat vervolgens nog beter willen sorteren: *we willen dat landen met een gelijke oppervlakte, op hun aantal inwoners gesorteerd worden*:
```java
public int CompareTo(object obj)
{

    Land temp =  obj as Land;
    if(temp != null)
    { 
        if(Oppervlakte > temp.Oppervlakte) return 1;
        if(Oppervlakte < temp.Oppervlakte) return -1;
        if(this.Inwoners > temp.Inwoners) return 1;
        if(this.Inwoners < temp.Inwoners) return -1;
    }
    else
        throw new ArgumentException("Object is not a Land"); 
    
}
```

Ik laat jou de code schrijven wat er moet gebeuren indien het aantal inwoners én de oppervlakte dezelfde is. Misschien kan je dan sorteren volgens de ``Naam`` van het land

{% hint style='tip' %}
De bestaande datatypes in .NET hebben allemaal de ``IComparable`` interface ingebakken. Zo ook dus het ``int`` datatype, maar ook ``string`` laat het volgende toe:

```java
return this.Naam.CompareTo(temp.Naam);
```
{% endhint %}

<!---NOBOOKSTART--->
## Kennisclip
![](../assets/infoclip.png)
* [Interfaces in de praktijk](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=2ace92d8-27c8-4b3a-9a3d-abac014a15a9)
* [Interfaces en polymorfisme in de praktijk: Vloekende mensen](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=01040bf2-b14d-407f-b186-abad00b66540) 
* [Interfaces en polymorfisme in de praktijk: fuifsimulator (LESOPNAME 2017)](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=1827a908-a435-4d89-ae7a-aa4c00911c87)

<!---NOBOOKEND--->


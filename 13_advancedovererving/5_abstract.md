## Abstracte klassen

Aan de start van dit boek beschreven we volgende 2 duidelijke definities:
* Een **klasse** is een beschrijving en verzameling van dingen (objecten) met soortgelijke eigenschappen.
* Een individueel **object** is een **instantie** van een klasse.

Niemand die zich hier vragen bij stelde? Als ik in het echte leven zeg: "Geef mij eens de beschrijving van een meubel." Wat voor soort meubel zie je voor je bij het lezen van deze zin? Een tafel? Een kast? Een zetel? Een bed? 

En wat zie je voor je als ik vraag om een "geometrische figuur" in te beelden. Een cirkel? Een rechthoek? Een kubus? Een buckyball? Kortom, er zijn in het leven ook soms eerder abstracte verzamelingen dingen die niet op zich in objecten kunnen gegoten worden zonder meer informatie. Toch is het concept "geometrische figuur" een belangrijk concept: we weten dat alle geometrische figuren een gemeenschappelijke definitie hebben, namelijk (met dank aan Encyclo.nl) dat het *twee- of meerdimensionale grafische elementen zijn waarvan de vorm wiskundig te berkenen valt.* **En dus is er ook een bestaansreden voor een klasse ``GeometrischeFiguur``. Objecten van deze, abstracte, klasse maken daarentegen lijkt ons uit ten boze.**

Het is dit concept, **abstracte klasse** dat we in dit hoofdstuk uit te doeken gaan doen. Het laat ons toe klassen te definiëren die niet niet kunnen geïnstantieerd worden, maar die dus wel dienst kunnen doen als parentklasse voor andere klassen.


### Abstracte klassen in C#

Laten we voorgaande eens praktisch binnen C# bekijken. Soms maken we dus een parent-klasse waar op zich geen instanties van kunnen gemaakt worden: denk aan de parent-klasse ``Dier``. Subklassen van Dier kunnen ``Paard``, ``Wolf``, etc zijn. Van ``Paard`` en ``Wolf`` is het logisch dat je instanties kan maken (echte paardjes en wolfjes) maar van 'een dier'? Hoe zou dat er uit zien.

Met behulp van het keyword **``abstract``** kunnen we aangeven dat een klasse abstract is: **je kan overerven van deze klasse, maar je kan er geen instanties van aanmaken.**

We plaatsen ``abstract`` voor de klasse definitie om dit aan te duiden.

Een voorbeeld:
```java
abstract class Dier
{
    public int Name {get;set;}
}
```

We kunnen nu geen objecten meer van het type ``Dier`` aanmaken. Volgende code zal een foutboodschap geven: ``Dier hetDier = new Dier();``

Maar, we mogen dus wel klassen overerven van deze klasse en instanties van deze nieuwe klasse aanmaken:
```java
class Paard: Dier
{
    //...
}

class Wolf: Dier
{
    //..
}
```
En dan zal dit wel werken: ``Wolf wolfje = new Wolf();``

En als we polymorfisme gebruiken (wat we later zullen zien) dan mag dit ook: ``Dier paardje = new Paard();`` 

{% hint style='tip' %}
In het begin lijkt ``abstract`` een beperkende factor: je kan minder dan ervoor. Maar het heeft dus één heel duidelijke functie: je kan een parent-klasse maken waarin de gedeelde functionaliteit van je child-klassen in zit, zonder dat je deze parent-klasse op zich kunt gebruiken. 
{% endhint %}

### Abstracte methoden
Het is logisch dat we mogelijk ook bepaalde zaken in de abstracte klasse als ``abstract`` kunnen aanduiden. Beeld je in dat je een methode ``MaakGeluid`` hebt in je klasse ``Dier``. Wat voor een geluid maakt 'een dier'? We kunnen dus ook geen implementatie (code) geven in de abstracte parent klasse, maar willen wel zeker ervoor zorgen dat alle child-klassen van ``Dier`` geluid kunnen maken, op wat voor manier dan ook.

Via abstracte methoden geven we dit aan: we hoeven enkel de methode signature te geven, met ervoor ``abstract``:
```java
abstract class  Dier
{
   public abstract string MaakGeluid();
}
```

Door het keyword ``abstract`` **zijn child-klassen verplicht deze abstracte methoden te overriden!** 

{% hint style='tip' %}
Merk op dat er geen codeblock-accolades na de signature van abstracte methodes komt.
{% endhint %}


De Paard-klasse wordt dan:
```java
class Paard: Dier
{
  public bool HeeftTetanus {get;set;}

  public override string MaakGeluid()
  { 
      return "Hinnikhinnik";
  }
}
```
(en idem voor de wolf-klasse uiteraard)

Dit is dus niet hetzelfde als ``virtual`` waar een ``override`` MAG. Bij ``abstract`` MOET je ``override``. We komen dan ook bij het hart van het abstracte klasse concept: ze laten ons toe om, als het ware, klasen te maken waar nog gaten in zitten qua implementatie. Een soort klasse-template die de child-klassen nog verder moeten inkleuren.
![](../assets/7_overerving/abstracttemplate.png)

{% hint style='warning' %}
#### Abstracte methoden enkel in abstracte klassen
Van zodra een klasse een abstracte methode of property heeft dan ben je, logischerwijs, verplicht om de klasse ook abstract te maken. 

Het zou heel vreemd zijn om objecten in het leven te kunnen roepen die letterlijk stukken ontbrekende code hebben...
{% endhint %}

### Abstracte properties

Properties kunnen ``virtual`` gemaakt, en dus ook ``abstract``. Net zoals bij abstracte methoden, kunnen we met abstracte properties de overgeërfde klassen verplichten een eigen implementatie van de property te schrijven. Volgende voorbeeld toont hoe dit werkt:

```java
    abstract class Dier
    {
        abstract public int MaxLeeftijd { get;}
    }

    class Olifant : Dier
    {
        public override int MaxLeeftijd {
            get { 
                return 100; 
                }
        }
    }
```

Wanneer je een abstracte property maakt dien je ogenblikkelijk aan te geven of het om een readonly, writeonly, of property met get én set gaat:
* ``public abstract int Oppervlakte {get;}``
* ``public abstract int GeheimeCode {set;}``
* ``public abstract int Leeftijd {get;set}``

<!---NOBOOKSTART--->
# Kennisclip
![](../assets/infoclip.png)

* [Abstract klassen](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=a6f513b8-e299-4118-986d-ab7c00e47861)
* [Uitgewerkt voorbeeld Abstract en System.Object mbv Zoo-dieren](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=e0c0f796-de77-4930-bcb6-ab8d00ce0c24) (compilatie uit hoorcollege 18-19)
<!---NOBOOKEND--->
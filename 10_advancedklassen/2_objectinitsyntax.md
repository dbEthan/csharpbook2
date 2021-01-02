## Object initializer syntax

Het is niet altijd duidelijk hoeveel overloaded constructors je juist nodig hebt. Meestal beperken we het tot de default constructor en 1 of 2 heel veel gebruikte overloaded constructors. 

Dankzij **object initializer syntax** kan je ook parameters tijdens de aanmaak van objecten meegeven zonder dat je hiervoor een specifieke constructor voor moet schrijven.

**Object initializer syntax laat je toe om tijdens (eigenlijk direct er na) creatie van een object, properties beginwaarden te geven.**

{% hint style='warning' %}
Object initializer syntax is een eerste glimp in het feit waarom properties zo belangrijk zijn in C#. Je kan object initializer syntax enkel gebruiken om via properties je object extra beginwaarden te geven.
{% endhint %}

Stel dat we volgende klasse hebben waarin we enkele autoproperties gebruiken (merk op dat dit evengoed full properties mochten zijn). Voor object initializer syntax maakt dat niet uit, het ziet toch enkel maar het ``public`` gedeelte van de klasse):

```java
class Meting
{
    public double Temperatuur {get;set;}
    public string GemetenDoor {get;set;}
    public bool IsGeconfirmeerd {get;set;}
}
```


We kunnen deze properties beginwaarden geven via volgende initializer syntax:

```java
Meting meting = new Meting() { Temperatuur= 3.4, IsGeconfirmeerd=true};
```

Object initializer syntax bestaat er dus uit dat je een object aanmaakt met de **default constructor** en dat je dan tussen accolades een lijst van properties en hun beginwaarden kunt geven. Object initializer werkt enkel indien het object een default constructor heeft (je hoeft deze niet expliciet te maken indien je klasse geen andere constructors heeft zoals in een eerder hoofdstuk al besproken).

{% hint style='warning' %}
Bovenstaande code mag ook iets korter nog:

```java
Meting meting = new Meting { Temperatuur= 3.4, IsGeconfirmeerd=true};
```

Zie je het verschil? De ronde haakjes van de default constructor mag je dus achterwege laten.
{% endhint %}

De volgorde waarin je code wordt uitgevoerd is wel belangrijk. Je ziet het niet duidelijk, maar sowieso wordt eerst nu de  default constructor aangeroepen. Pas wanneer die klaar is zullen de properties de waarden krijgen die je meegeeft tussen de accolades. Als je dus zelf een default constructor in ``Meting`` had geschreven dan had eerst die code uitgevoerd zijn geweest. Voorgaande voorbeeld zal intern eigenlijk als volgt plaatsvinden:

```java
Meting meting = new Meting();
meting.Temperatuur = 3.4;
meting.IsGeconfirmeerd = true;
```

{% hint style='tip' %}
Je bent niet verplicht alle properties via deze syntax in te stellen, enkel de zaken die je wilt meegeven tijdens de objectcreatie.
{% endhint %}

<!---NOBOOKSTART--->
# Kennisclip
![](../assets/infoclip.png)

* [Object initializer syntax](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=8f1ceebc-9f02-4593-84da-ab7a0099bf99)
<!---NOBOOKEND--->
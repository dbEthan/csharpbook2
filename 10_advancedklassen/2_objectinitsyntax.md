## Object initializer syntax

Het is niet altijd duidelijk hoeveel overloaded constructor je juist nodig hebt. Meestal beperken we het tot de default constructor en 1 of 2 heel veel gebruikte overloaded constructors. 

Dankzij **object initializer syntax** kan je ook parameters aan variabelen meegeven zonder dat je hiervoor een specifieke constructor voor moet schrijven.



**Object initializer syntax laat je toe om tijdens (eigenlijk direct er na) creatie van een object, bepaalde properties beginwaarden te geven.**

{% hint style='warning' %}
Object intializer syntax is een eerste glimps in het feit waarom properties zo belangrijk zijn in C#. Je kan object initialezer syntax enkel gebruiken om via properties je object extra beginwaarden te geven.
{% endhint %}

Stel dat we volgende klasse hebben waarin we enkele autoproperties gebruiken (merk op dat dit evengoed full properties mochten zijn. Voor ojbect initializer syntax maakt dat niet uit, het ziet toch enkel maar het ``public`` gedeelte van de klasse):

```java
class TemperatuurMeting
{
    public double Temperatuur {get;set;}
    public string GemetenDoor {get;set;}
    public bool IsGeconfirmeerd {get;set;}
}
```


We kunnen deze properties beginwaarden geven via volgende initializer syntax:

```java
TemperatuurMeting eenMeting = new TemperatuurMeting() { Temperatuur= 3.4, IsGeconfirmeerd=true};
```

Object initializer syntax bestaat er dus uit dat je een object aanmaakt met de **default constructor** en dat je dan tussen accolades een lijst van properties en hun beginwaarden kunt geven.

{% hint style='warning' %}
Object intializer werkt enkel indien het object een default constructor heeft!

Bovenstaande code mag ook iets korter nog:

```java
TemperatuurMeting eenMeting = new TemperatuurMeting { Temperatuur= 3.4, IsGeconfirmeerd=true};
```

De ronde haakjes van de default constructor mag je dus achterwege laten.
{% endhint %}

De volgorde waarin je code wordt uitgevoerd is wel belangrijk. Je ziet het niet duidelijk, maar sowieso wordt eerst nu de  default constructor aangeroepen. Pas wanneer die klaar is zullen de properties de waarden krijgen die je meegeeft tussen de accolades. Als je dus zelf een default constructor in ``TemperatuurMeting`` had geschreven dan had eerst die code uitgevoerd zijn geweest. Voorgaande voorbeeld zal intern eigenlijk als volgt plaatsvinden:

```java
TemperatuurMeting eenMeting = new TemperatuurMeting();
eenMeting.Temperatuur = 3.4;
eenMeting.IsGeconfirmeerd = true;
```

{% hint style='tip' %}
Je bent niet verplicht alle properties via deze syntax in te stellen, enkel de zaken die je wilt meegeven tijdens de objectcreatie.
{% endhint %}

<!---NOBOOKSTART--->
# Kennisclip
![](../assets/infoclip.png)

* [Object initializer syntax](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=8f1ceebc-9f02-4593-84da-ab7a0099bf99)
<!---NOBOOKEND--->
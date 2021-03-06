<!---{sample: true}--->
## OOP in C#

We kunnen in C# geen objecten aanmaken voor we een klasse hebben gedefinieerd dat de algemene eigenschappen (properties én instantievariabelen) en gedrag (methoden) beschrijft van die objecten.


### Klasse maken

Een klasse heeft minimaal de volgende vorm:

```java
class ClassName
{

}
```

{% hint style='warning' %}
De naam die je een klasse geeft moet voldoen aan de identifier regels uit het eerste boek. Het is echter een goede gewoonte om **klassenamen altijd met een hoofdletter te laten beginnen**.
{% endhint %}


Volgende code beschrijft de klasse ``Auto`` in C#

```java
class Auto
{

}
```

Binnen het codeblock dat bij deze klasse hoort zullen we verderop dan de werking via properties en methoden beschrijven.

### Klassen in Visual Studio toevoegen

Je kan "eender waar" een klasse aanmaken in een project, maar het is een goede gewoonte om per klasse **een apart bestand** te gebruiken. Dit kan op 2 manieren.

Manier 1:
* In de Solution Explorer, rechterklik op je project.
* Kies "Add".
* Kies "Class..".
* Geef een goede naam voor je klasse.

Manier 2:
* Klik in de menubalk bovenaan op "Project".
* Kies "Add class..." .

![Manier 2 is de snelste](../assets/6_klassen/addclass.png)

### Objecten aanmaken

Je kan nu objecten aanmaken van de klasse die je hebt gedefinieerd. Dit kan op alle plaatsen in je code waar je in het verleden ook al variabelen kon declareren, bijvoorbeeld in een methode of je ``Main``-methode.

Je doet dit door eerst een variabele te definiëren en vervolgens een object te **instantiëren** met behulp van het ``new`` keyword. De variabele heeft als datatype ``Auto``:

```java
Auto mijnEersteAuto = new Auto();
Auto mijnAndereAuto = new Auto();
```

We hebben nu **twee objecten aangemaakt van het type Auto** die we verderop zouden kunnen gebruiken.

Let goed op dat je dus op de juiste plekken dit alles doet:

* Klassen maak je aan als aparte bestanden in je project.
* Objecten creëer je in je code op de plekken waar je deze nodig hebt, bijvoorbeeld in je ``Main`` methode bij een Console-applicatie.


### De  ``new`` operator

In het volgende hoofdstuk gaan we kijken wat er allemaal gebeurt in het geheugen wanneer we een object met ``new`` aanmaken. Het is echter nu al belangrijk te beseffen dat objecten niet kunnen gemaakt worden zonder ``new``. De ``new`` operator vereist dat je aangeeft van klasse je een object wilt aanmaken, gevolgd door ronde haakjes (bijvoorbeeld``new Student()``). We roepen hier een constructor aan (zie verder) die het object in het geheugen zal aanmaken. Vervolgens geeft ``new`` een adres terug waar het object zich bevindt. Het is dit adres dat we vervolgens kunnen bewaren in een variabele die links van de toekenningsoperator (``=``) staat. 

Test maar eens wat er gebeurt als je volgende code probeert te compileren:
```java
Auto mijnEersteAuto = new Auto();
Auto mijnAndereAuto;
Console.WriteLine(mijnEersteAuto);
Console.WriteLine(mijnAndereAuto);
```

Je zal een ``"Use of unassigned local variable`'mijnAndereAuto'`` foutboodschap krijgen. Inderaad, je hebt nog geen object aangemaakt met ``new`` en ``mijnAndereAuto`` is dus voorlopig een lege doos (het heeft de waarde ``null``).

{% hint style='tip' %}
Dit concept is dus fundamenteel verschillend van de klassieke *valuetypes* die we al kenden (``int``, ``double``, etc.). Daar zal volgende code wél werken:
```java
int balans;
Console.WriteLine(balans);
```
{% endhint %}

<!---{pagebreak} --->

### Klassen zijn gewoon nieuwe datatypes

In het vorige boek leerden we dat er allerlei datatypes bestaan. We maakten vervolgens variabelen aan van een bepaald datatype zodat deze variabele als inhoud enkel zaken kon bevatten van dat ene datatype. 

Zo leerden we toen volgende datatypes:
* **Valuetypes** zoals ``int``, ``char`` en ``bool``.
* Het **``enum``** keyword liet ons toe om een nieuw datatype te maken dat maar een eindig aantal mogelijke waarden (values) kon hebben. Intern bewaarden variabelen van zo'n enum-datatype hun waarde als een ``int``.
* **Arrays** waren het laatste soort datatypes. We ontdekten dat we arrays konden maken van eender welk datatype (valuetypes en enums) dat we tot dan kenden.

**Wel nu, klassen zijn niet meer dan een nieuw soort datatypes**. Kortom: telkens je een klasse aanmaakt, kunnen we in dat project variabelen en arrays aanmaken met dat datatype. We noemen variabelen die een klasse als datatype hebben **objecten**.

Het grote verschil dat deze objecten zullen hebben is dat ze dus vaak veel complexer zijn dan de eerdere datatypes die we kennen:
* Ze zullen meerdere "waarden" tegelijk kunnen bewaren (een ``int`` variabele kan maar één waarde tegelijkertijd in zich hebben).
* Ze zullen methoden hebben die we kunnen aanroepen om de variabele "voor ons te laten werken".

<!---NOBOOKSTART--->
{% hint style='tip' %}
<!---NOBOOKEND--->
<!---{aside}--->
<!--- {float:right, width:50%} --->
![](../assets/care.png)
Het blijft ingewikkeld hoor. Heel boeiend om de theorie van een speer te leren, maar ik denk dat ik toch beter een paar keer met een speer naar een mammoet werp om echt te voelen wat OOP is. 

Ik onthoud nu alvast **"klassen zijn gewoon een nieuwe vorm van complexere datatypes"** dan diegene die ik in het vorige boek heb geleerd? Ok?

**Correct. Er verandert dus niet veel. Enkel je variabelen worden krachtiger!**
<!---{/aside}--->
<!---NOBOOKSTART--->
{% endhint %}
<!---NOBOOKEND--->


<!---{sample: false}--->

<!---{pagebreak} --->




<!---NOBOOKSTART--->
# Kennisclip
![](../assets/infoclip.png)
* [Klassen en objecten in C#](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=6d91d9e1-9c8e-4b7a-a9a0-accd00b0ff32)
<!---NOBOOKEND--->
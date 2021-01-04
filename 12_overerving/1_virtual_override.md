## Virtual en Override
Het is fijn dat onze child-klasse alles kan dat onze parent-klasse doet. Maar soms is dat beperkend:
* Mogelijk wil je een bestaande methode van de parent-klasse uitbreiden/aanvullen met extra functionaliteit.
* Soms wil je gewoon de volledige implementatie van een methode of property herschrijven in je child-klasse.

**De keywords ``virtual`` en ``override`` gaan je hiermee kunnen helpen.**

### De werking van child-klassen aanpassen

Om te voorkomen dat child-klassen zomaar eender welke methode of property van de parent-klasse kunnen aanpassen gaan we de hulp van het ``virtual`` keyword inroepen. Standaard is het geen goede gewoonte om de bestaande werking van een klasse in de child-klasse aan te passen: beeld je in dat je een essentieel stuk code aanpast waardoor je hele klasse plots niet meer werkt!

Soms willen we echter kunnen aangeven dat de implementatie (code) van een property of methode in een parent-klasse door child-klassen mag aangepast worden. Dit geven we aan met het  **virtual** keyword. En we zeggen hiermee aan zij die willen overerven van deze klasse: *"de werking van deze methode of property (waar ``virtual`` voor staat) mag je in je child-klasse uitbreiden of aanpassen."*

Vervolgens dient de child-klasse het keyword ``override`` te gebruiken om expliciet aan te geven dat er een methode of property komt wiens werking die van de parent-klasse zal wijzigen.

{% hint style='warning' %}
Enkel indien een element met ``virtual`` werd aangeduid, kan je deze dus met ``override`` aanpassen. Uiteraard ben je niet verplicht om elke *virtueel* element ook effectief te *overriden*. **``virtual`` geeft enkel aan dat dit een mogelijkheid is, geen verplichting.**
{% endhint %}

### Een voorbeeld met vliegende objecten

Stel je voor dat je een applicatie hebt met 2 klassen, ``Vliegtuig`` en ``Raket``. Een raket is een vliegtuig, maar kan veel hoger vliegen dan een vliegtuig. Omdat we weten dat potentiële childklassen op een andere manier zullen willen vliegen, zullen we de methode ``Vlieg`` ``virtual`` zetten:

```java
class Vliegtuig
{
   public virtual void Vlieg()
   {
      Console.WriteLine("Het vliegtuig vliegt rustig door de wolken.");
   }
}

class Raket: Vliegtuig
{
}

```
{% hint style='tip' %}
Merk op dat we het keyword ``virtual`` mee opnemen in de methodesignatuur op lijn 3, en dat deze dus niets te maken heeft met het returntype en de zichtbaarheid van de methode.
{% endhint %}

Stel dat we 2 objecten aanmaken en laten vliegen:

```java
Vliegtuig f1 = new Vliegtuig();
Raket spaceX1 = new Raket();
f1.Vlieg();
spaceX1.Vlieg();
```

De uitvoer zal dan zijn:

```
Het vliegtuig vliegt rustig door de wolken.
Het vliegtuig vliegt rustig door de wolken.
```

{% hint style='warning' %}
Enkel ``public`` methoden (en properties) kan je ``virtual`` instellen!
{% endhint %}

Momenteel doet het ``virtual`` keyword niets. Het is enkel een signaal aan mede-programmeurs: *"hey, als je wilt mag je de werking van deze methode aanpassen als je van deze klasse overerft."*

Een raket is een vliegtuig, toch vliegt het anders. We willen dus de methode ``Vlieg`` anders uitvoeren voor een raket. Daar hebben we **override** voor nodig. Door override voor een methode in de child-klasse te plaatsen zeggen we "gebruik deze implementatie en niet die van de parent klasse."
**Je kan enkel overriden indien de respectievelijke methode of property in de parent-klasse als virtual werd aangeduid.**

```java
class Raket:Vliegtuig
{
   public override void Vlieg()
   {
      Console.WriteLine("De raket verdwijnt in de ruimte.");
   }     
}
```



De uitvoer van volgende code zal nu anders zijn:
```java
Vliegtuig f1 = new Vliegtuig();
Raket spaceX1 = new Raket();
f1.Vlieg();
spaceX1.Vlieg();
```
Uitvoer:
```
Het vliegtuig vliegt rustig door de wolken.
De raket verdwijnt in de ruimte.
```

{% hint style='warning' %}
Indien je iets ``override`` moet de signatuur van je methode (of property) uiteraard identiek zijn aan deze van de parent-klasse. Het enige verschil is dat je het keyword ``virtual`` vervangt door ``override``.
{% endhint %}





{% hint style='tip' %}
Ook properties kan je ``virtual`` instellen en ``override``'n. We gaan dit verderop tonen nadat we het ``base`` keyword uit de doeken hebben gedaan.
{% endhint %}


<!---NOBOOKSTART--->
# Kennisclip
![](../assets/infoclip.png)
* [Virtual en override](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=d549422d-eb27-4dd5-8154-ab7c00ba0728)
<!---NOBOOKEND--->
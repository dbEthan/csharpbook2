## Polymorfisme in de praktijk

Beeld je in dat je een klasse ``EersteMinister`` hebt met een methode "Regeer"
<!---[^stack]--->.


<!---NOBOOKSTART--->
(Dit voorbeeld is gebaseerd op een [StackOverflow](https://stackoverflow.com/questions/1031273 ) post).
<!---NOBOOKEND--->

De ``EersteMinister`` heeft toegang tot tal van ministers die hem kunnen helpen (inzake milieu, binnenlandse zake en economie). Zonder de voordelen van polymorfisme zou de klasse ``EersteMinister`` er zo kunnen uitzien (**slechte manier**!):

<!---[^stack]Dit voorbeeld is gebaseerd op een oplossing op StackOverflow: https://stackoverflow.com/questions/1031273 ).--->


```java
public class EersteMinister
{
    MinisterVanMilieu Jansens = new MinisterVanMilieu();
    MinisterBZ Ganzeweel = new MinisterBZ();
    MinisterVanEconomie VanCent = new MinisterVanEconomie();

    public void Regeer()
    {
        // ministers stappen binnen en zeggen wat er moet gebeuren

        // Jansens: Problematiek aangaande bos dat gekapt wordt
        Jansens.VerhoogBosSubsidies();
        Jansens.OpenOnderzoek();
        Jansens.ContacteerGreenpeace();

        // Ganzeweel advies omtrent rel aan grens met Nederland

        Ganzeweel.VervangAmbassadeur();
        Ganzeweel.RoepTroepenmachtTerug();
        Ganzeweel.VerhoogRisicoZoneAanGrens();

        // Van Cent geeft advies omtrent nakende beurscrash

        VanCent.InjecteerGeldInMarkt();
        VanCent.VerlaagWerkloosheidsPremie();
    }
}
```

De ``MinisterVanMilieu`` zou er zo kunnen uitzien:
```java
class MinisterVanMilieu
{
  public void VerhoogBosSubsidies()
  {
    //..
  }
  public void OpenOnderzoek()
  {
    //..
  }
  etc
}
```

De ``MinisterVanEconomie``-klasse heeft dan weer heel andere publieke methoden. En de ``MinisterBZ`` ook weer totaal andere.

Je merkt dat de ``EersteMinister`` (of de programmeur van deze klasse) aardig wat specifieke kennis moet hebben van de vele verschillende departementen van het land. Bovenstaande code is dus zeer slecht en vloekt een beetje tegen het abstractie-principe van OOP: onze klasse moeten veel te veel weten van andere klassen, wat niet altijd gewenst is. Telkens er zaken binnen een specifieke ministerklasse wijzigen moet dit ook in de ``EersteMinister`` aangepast worden. 

**Dankzij polymorfisme en overerving kunnen we dit alles veel mooier oplossen:**

**Ten eerste:** We verplichten alle ministers dat ze overerven van de abstracte klasse ``Minister`` die maar 1 abstracte methode heeft ``Adviseer``:

```java
abstract class Minister
{
  abstract public void Adviseer();
}

class MinisterVanMilieu:Minister
{
  public override void Adviseer()
  {
       VerhoogBosSubsidies();
       OpenOnderzoek();
       ContacteerGreenpeace();
  }
  private void VerhoogBosSubsidies(){ ... }
  private void OpenOnderzoek(){ ... }
  private void ContacteerGreenpeace(){ ... }
  }
}

class MinisterBZ:Minister
{
  //...
}
class MinisterVanEconomie:Minister
{
  //...
}
```

**Ten tweede:**  Het leven van de EersteMinister wordt plots véél makkelijker. Hij kan gewoon de ``Adviseer`` methode aanroepen van iedere minister:

```java
public class EersteMinister
{
    Minister Jansens = new MinisterVanMilieu();
    Minister Ganzeweel = new MinisterBZ();
    Minister VanCent= new MinisterVanEconomie();
    
    public void Regeer()
    {

        Jansens.Adviseer(); 
        Ganzeweel.Adviseer(); 
        VanCent.Adviseer();
    }
}
```

**En ten derde:** En we kunnen hem nog helpen door met een array of ``List<Minister>`` te werken zodat hij ook niet steeds de "namen" van z'n ministers moet kennen:

```java
public class EersteMinister
{
   List<Minister> alleMinisters = new List<Minister>();
    public EersteMinister()
    {
        alleMinisters.Add(new MinisterVanMilieu());
        alleMinisters.Add(new MinisterBZ());
        alleMinisters.Add(new MinisterVanEconomie());
    }

    public void Regeer()
    {  
        foreach (Minister minister in alleMinisters)
        {
            minister.Adviseer();
        }
    }
}
```

En wie zei dat het regeren moeilijk was?!

{% hint style='tip' %}
Merk op dat dit voorbeeld ook goed gebruik maakt van **compositie**.
{% endhint %}


<!---NOBOOKSTART--->
{% hint style='tip' %}
## Nog voorbeelden van polymorfisme nodig?

Volgende tekst heeft een leuke insteek om polymorfisme uit te leggen... aan de hand van...wait for it... Zeemeerminnen! :) [Lezen maar!](http://www.techoschool.com/Technology/Dotnet/Csharp-for-Beginners_Csharp-Polymorphism)

Volgende voorbeeld is iets praktischer: [Arena with a mage in C# .NET (inheritance and polymorphism)](https://www.ict.social/csharp/oop/arena-with-mage-in-csharp-net-inheritance-and-polymorphism)
{% endhint %}

<!---NOBOOKEND--->

<!---NOBOOKSTART--->
# Kennisclip
![](../assets/infoclip.png)

* [Polymorfisme in de praktijk](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=06305096-bee1-466a-9b70-aba700860b64)
<!---NOBOOKEND--->
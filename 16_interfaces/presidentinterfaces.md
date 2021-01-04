##  Interfaces in de praktijk

In het hoofdstuk Polymorfisme bespraken we een voorbeeld van een klasse ``EersteMinister`` die enkele ``Minister``-klassen gebruikte om hem of haar te helpen.

Een nadeel van die voorgaande aanpak is dat al onze Ministers maar 1 "job" kunnen hebben: ze erven allemaal over van ``Minister`` en kunnen nergens anders van overerven (geen *multiple inheritance* is toegestaan in C#). Je wordt uiteraard niet geboren als Minister, en het zou dus handig zijn dat ook andere mensen Minister kunnen worden, zonder dat ze hun expertise moeten wegdoen. 

Via interfaces kunnen we dit oplossen. Een ``Minister`` gaan we dan eerder als een "bij-job" beschouwen en niet de hoofdreden van een klasse.

We definiëren daarom eerst een nieuwe interface ``IMinister``:
```java
interface IMinister
{
    void Adviseer();
}
```

Vanaf nu kan eender *wie* die deze interface implementeert de ``EersteMinister`` advies geven. Hoera! En daarnaast kan die klasse echter ook nog tal van andere zaken doen. Beeld je bijvoorbeeld een CEO van een bedrijf in die ook minister bij de EersteMinister wilt zijn. De bestaande klasse is bijvoorbeeld:

```java
class MicrosoftCEO: CEO
{
    public void MaakJaarlijkseOmzet()
    { 
       Console.WriteLine("Geld!!!");       
    }
    public void OntslaDepartement()
     { 
       Console.WriteLine("You're all fired!");       
    }
}
```
Nu we de interface ``IMinister`` hebben kunnen we deze klasse aanvullen met deze interface zonder dat de bestaande werken van de klasse moet aangepast worden:
```java
class MicrosoftCEO: CEO, IMinister
{
     
    public void Adviseer()
    { 
        Console.WriteLine("Vrijhandel is essentieel!");
    }
    
    public void MaakJaarlijkseOmzet()
    { 
       Console.WriteLine("Geld!!!");       
    }
    public void OntslaDepartement()
     { 
       Console.WriteLine("You're all fired!");       
    }
}
```
De CEO kan dus z'n bestaande job blijven uitoefenen maar ook als Minister optreden. 

Ook de ``EersteMinister`` moet aangepast worden om nu met een lijst van ``IMinister`` ipv ``Minister`` te werken. Dankzij, wederom, polymorfisme is dat erg eenvoudig! 

```java
public class MisterEersteMinister
{
    public void Regeer()
    {
    
        List<IMinister> alleMinisters = new List<IMinister>();
        alleMinisters.Add(new MicrosoftCEO);
        
        foreach (IMinister minister in alleMinisters)
        {
            minister.Adviseer();
        }
    }
}
```

De eerder beschreven ``MinisterVanMilieu``,``MinisterBZ`` en ``MinisterVanEconomie`` dienen ook niet meer van de abstracte klasse ``Minister``(deze zou je kunnen verwijderen) over te erven en kunnen gewoon de interface implementeren. Enkel lijn 1 moet hierbij aangepast worden:

```java
class MinisterVanMilieu:IMinister
{
    public void Adviseer()
    {
        increaseTroopNumbers();
        improveSecurity();
        payContractors();
    }

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
```

<!---NOBOOKSTART--->
# Kennisclip
![](../assets/infoclip.png)

* [Interfaces in de praktijk met EersteMinisteren, deel 2](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=1df92edd-ba85-42f4-bdd0-abac0149cc10)
<!---NOBOOKEND--->

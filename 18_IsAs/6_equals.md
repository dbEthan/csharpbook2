## Is, as en polymorfisme: een krachtige bende

Dankzij polymorfisme hebben we nu met de ``is`` en ``as`` keywords handige hulpmiddelen om meer "generieke" methoden te schrijven. Herinner je je nog de ``Equals`` methode die we schreven om 2 studenten te vergelijken toen we leerden dat alle klassen van ``System.Object`` overerfden? Laten we deze code er nog eens bijnemen en verbeteren:

```java
//In de Student class
public override bool Equals(Object o)
{  
    Student temp = (Student)o; 
    return (GeboorteJaar == temp.GeboorteJaar && Voornaam == temp.Voornaam)
}
```

De eerste lijn waarin we casten ``o`` casten naar een student kan natuurlijk mislukken. Het is dan ook veiliger om eerst te controleren of we wel mogen casten, voor we het effectief doen. Hierdoor schrijven we een minder foutgevoelige methode:

```java
//In de Student class
public override bool Equals(Object o)
{  
    if(o is Student)
    { 
        Student temp = o as Student; 
        return (GeboorteJaar == temp.GeboorteJaar && Voornaam == temp.Voornaam)
    }
    return false;
}
```

Of we kunnen ook het volgende doen:
```java
//In de Student class
public override bool Equals(Object o)
{  
    Student temp = o as Student; 
    if(o != null)
    { 
        return (GeboorteJaar == temp.GeboorteJaar && Voornaam == temp.Voornaam)
    }
    return false;
}
```
Beide zijn geldige oplossingen.


<!---NOBOOKSTART--->
{% hint style='warning' %}
<!---NOBOOKEND--->
<!---{aside}--->
<!--- {float:right, width:50%} --->
![](../assets/care.png)

Let's be honest. Als je aan dit punt en geen flauw benul hebt waarom je in godsnaam je hier iets van moet aantrekken, wel dan wordt het dringend tijd om dit boek van voor naar achter, links naar rechts en onder tot boven terug door te nemen én vervolgens te gaan fietsen...ik bedoel programmeren.
<!---{/aside}--->
<!---NOBOOKSTART--->
{% endhint %}
<!---NOBOOKEND--->

<!---NOBOOKSTART--->
# Kennisclip
![](../assets/infoclip.png)

* [Samenvatting objecten vergelijken met equals: polymorfisme in actie](https://ap.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=b705422d-db2d-420a-bcda-aba700fd9336)
<!---NOBOOKEND--->
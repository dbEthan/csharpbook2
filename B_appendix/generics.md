## Generics

### Generieke methoden
Vaak schrijf je methoden die hetzelfde doen, maar waarvan enkel het type van de parameters en/of het returntype verschilt. Stel dat je een methode hebt die de elementen in een array onder elkaar toont. Je wil dit werkende hebben voor arays van het type ``int``, ``string``, etc. Zonder generics moeten we dan per type een methode moeten schrijven:

```java
public static void ToonArray(int[] array)
{
    foreach (var i in array)
    {
        Console.WriteLine(i);
    }
}
 
public static void ToonArray(string[] array)
{
    foreach (var i in array)
    {
        Console.WriteLine(i);
    }
}
```
Dankzij generics kunnen we nu het deel dat **generiek** moet zijn aanduiden (in dit geval met ``T``) en onze methode eenmalig definiëren. We gebruiken hierbij de ``< >`` aanduiding die aan de compiler verteld "dit stuk is een generiek type``:

```java
public static void ToonArray<T>(T[] array)
{
    foreach (T item in array)
    {
        Console.WriteLine(item);
    }
}
```

### Generic types
We kunnen niet alleen generieke methoden schrijven, maar ook eigen klassen definieren die generiek zijn. In het volgende codevoorbeeld is te zien hoe een eigen generic class in C# gedefinieerd en gebruikt kan worden. Merk het gebruik van de aanduiding ``T`` , deze geeft  weer aan dat hier een type (zoals ``int``, ``double``, ``Student``,etc.) zal worden ingevuld tijdens het compileren.

{% hint style='tip' %}
## ``<T>``
De typeparameter T wordt pas voor de specifieke instantie van de generieke klass of type ingevuld bij het compileren. Hierdoor kan de compiler per instantie controleren of alle parameters en variabelen die in samenhang met het generieke type gebruikt worden wel kloppen.

De afspraak is om .NET een ``T`` te gebruiken indien het type nog dient bepaald te worden (dit is niet verplicht).
{% endhint %}


We wensen een klasse te maken die de locatie in X,Y,Z richting kan bewaren. We willen echter zowel ``float``, ``double`` als ``int`` gebruiken om deze X,Y,Z coördinaten in bij te houden:


```java
class Location<T>
{
    public T X;
    public T Y;
    public T Z;
}
```
We kunnen deze klasse nu als volgt gebruiken:

```java
Location<int> plaats;
plaats.X = 34;
plaats.Y = 22;
plaats.Z = 56;

Location<double> plaats2;
plaats2.X = 34.5;
plaats2.Y = 22.2;
plaats2.Z = 56.7;

Location<string> plaats3;
plaats3.X = "naast de kerk";
plaats3.X = "links van de bakker";
plaats3.Z = "onder het hotel";
```


### Een complexere generieke klassen
Voorgaan voorbeeld is natuurlijk maar de tip van de ijsberg. We kunnen bijvoorbeeld volgende klasse maken die we kunnen gebruiken met eender welk type om de meetwaarde van een meting in op te slaan/ Merk op hoe we op verschillende plaatsen in de klasse ``T`` gebruiken:

```java
public class Meting<T>
{
    private T waarde;

    public Meting(T waardein)
    {
        waarde = waardein;
    }

    public T Waarde 
    { 
        get { return waarde; } 
        set { waarde = value ;}  
    }
}
```
Een voorbeeldgebruik van dit nieuwe type kan zijn:

```java
Meting<int> m1 = new Meting<int>(44);
Console.WriteLine(m1.Waarde);

Meting<string> m2 = new Meting<string>("slechte meting");
Console.WriteLine(m2.Waarde);
```


### Meerdere types in generics
Zoals reeds eerder vermeld is de ``T`` aanduiding enkel maar een afspraak. Je kan echter zoveel ``T``-parameters meegeven als je wenst. Stel dat je bijvoorbeeld een klasse wenst te maken waarbij 2 verschillende types kunnen gebruikt worden. De klassedefinitie zou er dan als volgt uit zien:

```csharp
class DataBewaarder<Type1, Type2>
{
    private Type1 waarde1;
    private Type2 waarde2;

    public DataBewaarder(Type1 w1, Type2 w2)
    {
        waarde1 = w1;
        waarde2 = w2;
    }
    public string ToonInfo()
    {
        return $"Waarde1: {waarde1}.\nWaarde2: {waarde2}";
    }
}
```
Een object aanmaken zal nu als volgt gaan:

```csharp
DataBewaarder<int, string> d1 = new DataBewaarder<int, string>(4, "Ok");
```



### Constraints
We willen vaak voorkomen dat bepaalde types wel of niet gebruikt kunnen worden in je zelfgemaakte generieke klasse. Stel bijvoorbeeld dat je een klasse schrijft waarbij je de ``CompareTo()`` methode wenst te gebruiken. Dit gaat enkel indien het type in kwestie de ``IComparable`` interface implementeert. We kunnen als **constraint** (*beperking*) dan opgeven dat de volgende klasse enkel kan gebruikt worden door klassen die ook effectief die interface implementeren (en dus de ``CompareTo()``-methoden hebben). We doen dit in de klasse-definitie met het nieuwe ``where`` keyword. We zeggen dus letterlijk (*"waar T overerft van IComparable"*):

```csharp
public class Wijziging<T> where T : IComparable
{
    public T vorigewaarde;
    public T huidigewaarde;
    public Wijziging(T vorig, T huidig)
    {
        vorigewaarde = vorig;
        huidigewaarde = huidig;
    }
 
    public bool IsGestegen()
    {
        if (huidigewaarde.CompareTo(vorigewaarde) > 0)
            return true;
        else return false;
    }
}
```

Volgende gebruik van deze klasse zou dan ``True`` op het scherm tonen:

```csharp
Wijziging<double> w = new Wijziging<double>(3.4, 3.65);
Console.WriteLine(w.IsGestegen());
```

### Mogelijke constraints
Verschillende zaken kunnen als constraint optreden. Naast de verplichting dat een bepaalde interface moet worden geïmplementeerd kunnen ook volgende constraints gelden (bekijk de online documentatie voor meer informatie hierover):
* Enkel value types.
* Enkel klassen.
* Moet default constructor hebben.
* Moet overerven van een bepaalde klasse.
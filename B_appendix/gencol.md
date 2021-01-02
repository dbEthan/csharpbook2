## Queue en Stack collectie

In het boek bespraken we de ``List``-collectie al. Dit was niet meer dan een geavanceerde array. Elementen worden achteraan toegevoegd en via de index kan je bijhouden waar welk element juist staat. Er zijn echter nog enkele andere generieke collectie-klassen in C# die je mogelijk wel handig zult vinden. We bespreken daarom hier kort de ``Queue`` en ``Stack`` ` collectie-klassen. 


### ``Queue<>`` collectie
Een queue, uitgesproken als "kjioe" stelt een "first in, first out"-lijst (FIFO) voor. Een ``Queue`` stelt dus de rijen voor die we in het echte leven ook hebben wanneer we bijvoorbeeld aanschuiven aan een ticketverkoop of in de supermarkt. Met deze klasse kunnen we zo’n rij simuleren en ervoor zorgen dat steeds het eerste/oudste element in de rij als eerste wordt behandeld. Nieuwe elementen worden achteraan de rij toegevoegd.

We gebruiken 2 methoden om met een ``Queue``-lijst te werken:

* ``Enqueue(T item)``: Voeg een item achteraan de lijst toe.
* ``Dequeue()``: geeft een referentie naar het eerste element in de queue terug en verwijdert dit element vervolgens uit de lijst.

Voorbeeld:

```csharp
Queue<string> theQueue =  new Queue<string>();
theQueue.Enqueue("I arrived here first!");
theQueue.Enqueue("I arrived second.");
theQueue.Enqueue("I'm last");
 
Console.WriteLine(theQueue.Dequeue());
Console.WriteLine(theQueue.Dequeue());
```

Dit zal op het scherm tonen:
```
I arrived here first!
I arrived here second.
```

{% hint style='tip' %}
Een andere interessante methode is de **Peek()** methode: hiermee kunnen we kijken in de queue wat het eerste element is, zonder het te verwijderen.
{% endhint %}

### ``Stack<>`` collectie
Daar waar een queue "first in,first out" is, is een stack "last in,first out" (LIFO). Met andere woorden het recentst toegevoegde element zal steeds vooraan staan en als eerste verwerkt worden. Je kan dit vergelijken met een stapel papieren waar je steeds bovenop een nieuw papier legt.

We gebruiken volgende 2 methoden om met een ``Stack`` te werken:

* ``Push(T item)``: plaats een nieuw element bovenop de stapel.
* ``Pop()``: geeft het bovenste element in de stack terug en verwijdert vervolgens dit element van de stack.

Voorbeeld:

```csharp
Stack<string> theStack =  new Stack<string>();
theStack.Push("I arrived here first!");
theStack.Push("I arrived second.");
theStack.Push("I'm last");
 
Console.WriteLine(theStack.Pop());
Console.WriteLine(theStack.Pop());
```
Dit zal dus het volgende resultaat geven:
```
I'm last
I arrived second.
``` 

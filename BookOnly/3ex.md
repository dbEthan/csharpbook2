
## Oefeningen

### Meetlat constructor

Vul de ``Meetlat`` klasse uit het vorige hoofdstuk aan met een constructor. De constructor laat toe om de lengte in meter als parameter mee te geven. De ``LengteInMeter`` write-only property vervang je door een instantievariabele ``double lengteInMeter``.

``lengteInMeter`` stel je nu in via de parameter die je in de constructor meekrijgt.

### Digitale kluis

Maak een klasse ``DigitaleKluis`` die we gaan gebruiken om een kluis voor te stellen.

De klasse heeft volgende elementen:

* Een fullproperty ``Code`` met private set. De get van deze property zal altijd -666 teruggeven, tenzij ``CanShowcode`` op ``true`` staat, in dit geval zal de effectieve code worden terug gegeven die in het private field staat. 
* De effectieve toegang tot de kluis wordt bewaard in de achterliggende instantievariabele die bij deze full property hoort. 
* Een constructor die als parameter een geheel getal toelaat. Dit getal zal worden toegewezen aan ``Code``.
* Een full property ``CanShowCode`` die kan ingesteld worden op ``true`` or ``false``, om aan te geven of de code van buitenuit kan gezien worden.
* Een methode ``CodeLevel`` dat een ``int`` teruggeeft. Deze methode zal het level van de code teruggeven. Het level is eenvoudigweg de code gedeeld door 1000 als geheel getal (dus indien de code 500 is zal 0 worden teruggegeven, indien de code 2000 is wordt 2 teruggegeven, etc. ).
* Een methode ``TryCode`` die een geheel getal als parameter aanvaardt. De methode geeft een ``true`` terug indien de code correct was, anders ``false``. Deze methode kan gebruikt worden om extern een code te testen , indien deze overeenkomt met de bewaarde code dan zal gemeld worden dat de code geldig is en wordt ook getoond hoeveel keer de gebruiker geprobeerd heeft. Indien de gebruiker -666 meegaf dan meldt de methode dat de gebruiker een *cheater* is . Indien de gebruiker een foute code meegaf dan meldt de methode dat dit een foute code was en wordt het aantal pogingen met 1 verhoogd.  
* Een private variabele ``aantalpogingen`` om bij te houden hoe vaak de gebruiker geprobeerd heeft de code te vinden.
* Een ``static`` methode waar je een kluis-object aan kan geven. De methode zal alle mogelijke codes brute forcen (met een loop) door telkens de ``TryCode`` methode van de meegegeven kluis aan te roepen, tot dat de juiste code wordt gevonden. Wanneer de code werd gevonden zal het aantal pogingen terug gegeven.


Maak enkele Digitale Kluis objecten aan in je ``main`` en test of je bovenstaande klasse correct is geïmplementeerd.

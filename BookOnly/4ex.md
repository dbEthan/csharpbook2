## Oefeningen

### Prijzen met foreach

Maak een array die tot 20 prijzen (``double``) kan bewaren. Vraag aan de gebruiker om 20 prijzen in te voeren en bewaar deze in de array. Doorloop vervolgens m.b.v. een ``foreach``-lus de volledige array en toon enkel de elementen op het scherm wiens prijs hoger of gelijk is aan €5.00. Toon op het einde van het programma het gemiddelde van alle prijzen (dus inclusief de lagere prijzen).

### Speelkaarten

Maak een klasse ``Speelkaart`` die je kan gebruiken om een klassieke speelkaart met getal en "kleur" voor te stellen. 

* Een kaart heeft 2 eigenschappen, een getal van 1 tot en met 13 (boer=11, koningin= 12, heer= 13).
* Een soort, de zogenaamde suite. Deze stel je voor via een enumtype en kan als waarden Schoppen, Harten, Klaveren of Ruiten zijn.


Schrijf nu 2 loops die de 52 kaarten van een standaard pak in een ``List<SpeelKaart>`` lijst plaatst.

Maak een applicatie die telkens een willekeurige kaart uit de *stapel* trekt en deze aan de gebruiker toont. De kaart wordt na het tonen ook uit de lijst verwijderd. Door met een willekeurig getal te werken hoef je dus je deck niet te schudden.

### Bookmark Manager

Maak een "bookmark manager". Deze tool zal in de console aan de gebruiker 5 favoriete sites vragen: ``naam`` en ``url``. Vervolgens zal de tool alle sites in een lijst tonen met een nummer ervoor. De gebruiker kan dan de nummer intypen en de tool zal automatisch de site in een vereenvoudigde versie op het scherm tonen. 

Je opdracht:

1. Maak een array of ``List`` waarin je 5 bookmark objecten kan plaatsen. 
2. Vul de applicatie aan zodat de gebruiker een bestaand bookmark kan verwijderen en een bestaand bookmark kan aanpassen.
3. De gebruiker kan een bookmark selecteren (door de index ervan in te geven) en vervolgens zal deze site getoond worden op het scherm.

Hierna volgen enkele zaken die je zal nodig hebben.

<!---{pagebreak} --->

```java
class BookMark
{
    public BookMark(string naamIn, urlIn)
    {
        Naam = naamIn;
        URL = urlIn;
    }

    public string Naam { get; set; }
    public string URL { get; set; }
    public string DownloadSite()
    {
        var wc = new WebClient();
        string result = wc.DownloadString(URL);
        return GetPlainTextFromHtml(result);
    }
    
    private string GetPlainTextFromHtml(string html)
    {
        string htmlTagPattern = "<.*?>";
        string reg = "(\\<script(.+?)\\</script\\>)|(\\<style(.+?)\\</style\\>)";
        var regCss = 
            new Regex(reg, RegexOptions.Singleline|RegexOptions.IgnoreCase);
        html = regCss.Replace(html, string.Empty);
        html = Regex.Replace(html, htmlTagPattern, string.Empty);
        html = Regex.Replace(html, @"^\s+$[\r\n]*", "", RegexOptions.Multiline);
        html = html.Replace("&nbsp;", " ");
        return html;
    }
}
```

[De ``GetPlanTextFromHtml()`` methode komt van volgende post.](https://www.mercator.eu/mercator/std/info_aruba/reporting-hoe-gegevens-afdrukken-met-html-tags.html))


Voorbeeld van hoe de ``Bookmark`` klasse zal werken:

```java
BookMark u = new BookMark("Google", "https://www.google.be" );
Console.WriteLine(u.DownloadSite());
```

Kan je je eigen "console browser" maken?
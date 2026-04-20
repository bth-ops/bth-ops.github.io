---
title: "Uppgift: Databasen World (kmom01)" 
description: "Uppgift att använda en databas och ställa frågor mot den."
revision:
    "2026-01-09": "(A) Första versionen."
sidebar:
    order: 0010
---

Denna uppgift görs som en del av kmom01.

<!--
TODO

* 
-->



## Förutsättning

Du har tillgång till ditt kursrepo.

Du behöver ha jobbat igenom "Övning med databasen World och SELECT".



## Krav - Allmänt

Utför följande krav.

1. Spara all din kod i filen `kmom/01/world1/task.sql`, tillsammans med kommentarer ovanför varje uppgift så att det blir enkelt att se vilken uppgift som är löst. 



## Krav - Besvara frågor

Skapa SQL-kod för att besvara följande frågor. När man kör din SQL-kod skall man se svaret på respektive fråga.

1. Visa alla länder som ligger i Norden (Region) och sortera dem i stigande ordning efter befolkning. Visa ländernas namn, region och befolkning. Sortera tabellen i stigande ordning efter befolkning.

1. Hitta alla länder som ligger i Europa och har en befolkning större än 10 miljoner. Visa ländernas namn, kontinent och befolkning. Sortera tabellen i sjunkande ordning efter befolkning.

1. Hitta alla länder som har "United" i sitt namn. Visa ländernas namn och region. Sortera tabellen i stigande ordning efter namn. Ledtråd är att använda operatorn LIKE.

1. Visa de 5 länder som har den minsta landytan (SurfaceArea). Visa ländernas namn och landyta. Sortera tabellen i stigande ordning efter landyta.

1. Lista alla länder som blev självständiga (IndepYear) någon gång mellan år 1980 och 1990. Visa ländernas namn och år för självständighet. Sortera tabellen i stigande ordning efter år för självständighet.



## Krav - Skapa rapporter

Skapa SQL-kod för att generera följande rapporter. Din SQL-kod skall generera **exakt samma rapport** som finns i utskriften nedan.

1. Slå ihop tabellerna country och city för att visa alla länder i norden och deras huvudstäder. Visa regionen, landets namn och huvudstadens namn samt hur många som bor i huvudstaden. Sortera tabellen och byt ut rubrikerna i resultatet för att göra dem mer beskrivande.

```txt
+------------------+------------------------+------------------------+-----------------+
| Region           | Land                   | Huvudstad              | Antal invånare  |
+------------------+------------------------+------------------------+-----------------+
| Nordic Countries | Finland                | Helsinki [Helsingfors] |          555474 |
| Nordic Countries | Denmark                | København              |          495699 |
| Nordic Countries | Svalbard and Jan Mayen | Longyearbyen           |            1438 |
| Nordic Countries | Norway                 | Oslo                   |          508726 |
| Nordic Countries | Iceland                | Reykjavík              |          109184 |
| Nordic Countries | Sweden                 | Stockholm              |          750348 |
| Nordic Countries | Faroe Islands          | Tórshavn               |           14542 |
+------------------+------------------------+------------------------+-----------------+
7 rows in set (0,001 sec)
```

__ÖVERKURS UTMANING__ Klarar du även av att skapa följande variant på rapporten? Du ser vad som är skillnaden under "Antal invånare"? 

Du får tre ledtrådar, om du vill. Manualen är din vän. Om du klarar det med enbart hjälp av manualen så är det bonuspoäng. Använd din Ai-kompis som en allra sista utväg.

<details><summary>Ledtråd 1</summary>

* FORMAT

</details>

<details><summary>Ledtråd 2</summary>

* sv_SE

</details>

<details><summary>Ledtråd 3</summary>

* LPAD

</details>

```txt
+------------------+------------------------+------------------------+-----------------+
| Region           | Land                   | Huvudstad              | Antal invånare  |
+------------------+------------------------+------------------------+-----------------+
| Nordic Countries | Finland                | Helsinki [Helsingfors] |         555 474 |
| Nordic Countries | Denmark                | København              |         495 699 |
| Nordic Countries | Svalbard and Jan Mayen | Longyearbyen           |           1 438 |
| Nordic Countries | Norway                 | Oslo                   |         508 726 |
| Nordic Countries | Iceland                | Reykjavík              |         109 184 |
| Nordic Countries | Sweden                 | Stockholm              |         750 348 |
| Nordic Countries | Faroe Islands          | Tórshavn               |          14 542 |
+------------------+------------------------+------------------------+-----------------+
```



## Avslutningsvis

Det var en start på SELECT och att jobba med databaser.



<!--
Visa rapport i terminalklienten.

Visa rapport i workbench (eller motsvarande)

Joina två tabeller
Språk
Länder med högst lägst population, area
Länder i Europa, Norden, Continent, Region
LifeExpectancy
Vilka länder har kungadömen?
Vilka länder har inget independently Year?

-->

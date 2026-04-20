---
title: "Uppgift: JOIN (kmom02)" 
description: "Uppgift att använda en databas och ställa frågor mot den."
revision:
    "2026-01-26": "(B) Uppdaterade utskrifter av förväntat resultat."
    "2026-01-25": "(A) Första versionen."
sidebar:
    order: 0020
---

Denna uppgift görs som en del av kmom02.



## Förutsättning

Du har tillgång till ditt kursrepo.

Du behöver ha jobbat igenom övningarna "Övning databasen World: JOIN och rapporter" och "Övning databasen World: Aggregerande funktioner och vyer".



## Krav - Allmänt

Utför följande krav.

1. Spara all din kod i filen `kmom/02/world2/task.sql`, tillsammans med kommentarer ovanför varje uppgift så att det blir enkelt att se vilken uppgift som är löst. 



## Krav - Besvara frågor

Skapa SQL-kod för att besvara följande frågor. När man kör din SQL-kod skall man se svaret på respektive fråga.

<!--

Joina två tabeller
Språk
Länder med högst lägst population, area
Länder i Europa, Norden, Continent, Region
LifeExpectancy
Vilka länder har kungadömen?
Vilka länder har inget independentyYear?

-->

1. Visa vilket styrelseskick de olika länderna i norden har och namnet på landets ledare.

    <details><summary>Resultat</summary>

    ```text
    +------------------------+-------------------------------+--------------------------+
    | Land                   | Styrelseskick                 | Landets ledare           |
    +------------------------+-------------------------------+--------------------------+
    | Denmark                | Constitutional Monarchy       | Margrethe II             |
    | Faroe Islands          | Part of Denmark               | Margrethe II             |
    | Finland                | Republic                      | Tarja Halonen            |
    | Iceland                | Republic                      | Ólafur Ragnar Grímsson   |
    | Norway                 | Constitutional Monarchy       | Harald V                 |
    | Svalbard and Jan Mayen | Dependent Territory of Norway | Harald V                 |
    | Sweden                 | Constitutional Monarchy       | Carl XVI Gustaf          |
    +------------------------+-------------------------------+--------------------------+
    ```

    </details>

1. Gör en rapport som visar vilka styrelseskick som är de vanligaste i världen. Visa topp fem styrelseskick.

    <details><summary>Resultat</summary>

    ```text
    +-------------------------------+---------------+
    | Styrelseskick                 | Antal länder  |
    +-------------------------------+---------------+
    | Republic                      |           122 |
    | Constitutional Monarchy       |            29 |
    | Federal Republic              |            15 |
    | Dependent Territory of the UK |            12 |
    | Monarchy                      |             5 |
    +-------------------------------+---------------+
    ```

    </details>

1. Visa landets namn och hur många språk som talas i landet. Sortera tabellen och visa först de 5 länder där flest språk talas (en rapport) och därefter de 5 länder där minst språk talas (ytterligare en rapport).

    <details><summary>Resultat</summary>

    ```text
    +--------------------+---------------------+
    | country_name       | number_of_languages |
    +--------------------+---------------------+
    | Canada             |                  12 |
    | China              |                  12 |
    | India              |                  12 |
    | Russian Federation |                  12 |
    | United States      |                  12 |
    +--------------------+---------------------+
    ```

    ```text
    +------------------------+---------------------+
    | country_name           | number_of_languages |
    +------------------------+---------------------+
    | Anguilla               |                   1 |
    | Bermuda                |                   1 |
    | Bosnia and Herzegovina |                   1 |
    | Cayman Islands         |                   1 |
    | Cuba                   |                   1 |
    +------------------------+---------------------+
    ```

    </details>

1. Visa en lista med de 5 länder som har flest officiella språk.

    <details><summary>Resultat</summary>

    ```text
    +--------------+---------------------+
    | country_name | number_of_languages |
    +--------------+---------------------+
    | South Africa |                   4 |
    | Switzerland  |                   4 |
    | Luxembourg   |                   3 |
    | Peru         |                   3 |
    | Singapore    |                   3 |
    +--------------+---------------------+
    ```

    </details>



1. Visa en lista med de städer som har störst befolkning i världen. Visa stadens namn, landets namn, och stadens befolkning. Begränsa resultatet till 10 rader.

    <details><summary>Resultat</summary>

    ```text
    +-------------------+--------------------+-----------------+
    | city_name         | country_name       | city_population |
    +-------------------+--------------------+-----------------+
    | Mumbai (Bombay)   | India              |        10500000 |
    | Seoul             | South Korea        |         9981619 |
    | São Paulo         | Brazil             |         9968485 |
    | Shanghai          | China              |         9696300 |
    | Jakarta           | Indonesia          |         9604900 |
    | Karachi           | Pakistan           |         9269265 |
    | Istanbul          | Turkey             |         8787958 |
    | Ciudad de México  | Mexico             |         8591309 |
    | Moscow            | Russian Federation |         8389200 |
    | New York          | United States      |         8008278 |
    +-------------------+--------------------+-----------------+
    ```

    </details>



1. Använd rapporten ovan men visa hur många som bor i snitt i dessa städer.

    <details><summary>Resultat</summary>

    ```text
    +--------------------+
    | average_population |
    +--------------------+
    |       9279731.4000 |
    +--------------------+
    ```

    </details>

    <details><summary>Ledtråd</summary>

    Att göra den frågan på ett dynamiskt sätt har vi ännu inte lärt oss, då får vi ta och hårdkoda lösningen. Alla vägar är tillåtna?

    ```sql
    WHERE 
        ci.population >= 8008278
    ```

    </details>



## Krav - Skapa rapporter

Skapa SQL-kod för att generera följande rapporter. Din SQL-kod skall generera **exakt samma rapport** som finns i utskriften nedan.

1. Visa de fem länder dom har flest officiella språk och lista vilka språk det är. Notera att det är ett mellanslag mellan språken.

    ```txt
    +--------------+------------------------+-----------------------------------+
    | Land         | Antal officiellaspråk  | Språk                             |
    +--------------+------------------------+-----------------------------------+
    | South Africa |                      4 |  Afrikaans, English, Xhosa, Zulu  |
    | Switzerland  |                      4 |  French, German, Italian, Romansh |
    | Belgium      |                      3 |  Dutch, French, German            |
    | Bolivia      |                      3 |  Aimará, Ketšua, Spanish          |
    | Luxembourg   |                      3 |  French, German, Luxembourgish    |
    +--------------+------------------------+-----------------------------------+
    ```

    <details><summary>Ledtråd 1</summary>

    * GROUP_CONCAT

    </details>

    <details><summary>Ledtråd 2</summary>

    * GROUP_CONCAT(sep, str, sep)

    </details>

1. Visa de nordiska länderna tillsammans med deras huvudstäder och det/de officiella språk som talas i länderna.

    ```text
    +------------------------+------------------------+-------------------+
    | Land                   | Huvudstad              | Officiella språk  |
    +------------------------+------------------------+-------------------+
    | Denmark                | København              | Danish            |
    | Faroe Islands          | Tórshavn               | Danish, Faroese   |
    | Finland                | Helsinki [Helsingfors] | Finnish, Swedish  |
    | Iceland                | Reykjavík              | Icelandic         |
    | Norway                 | Oslo                   | Norwegian         |
    | Svalbard and Jan Mayen | Longyearbyen           | Norwegian         |
    | Sweden                 | Stockholm              | Swedish           |
    +------------------------+------------------------+-------------------+
    ```

    <details><summary>Ledtråd 1</summary>

    ```sql
    GROUP_CONCAT(xxx ORDER BY xxx ASC SEPARATOR xxx)
    ```

    </details>

    <details><summary>Ledtråd 2</summary>

    ```sql
    GROUP_CONCAT(la.language ORDER BY la.language ASC SEPARATOR ' ')
    ```

    </details>

1. __ÖVERKURS UTMANING__ Klarar du av att skapa en **exakt likadan rapport** som visar vilka språk som talas mest, baserat på antalet invånare i respektive land som talar språket?

    Du får ledtrådar, om du vill. Manualen är din vän. Om du klarar det med enbart hjälp av manualen så är det bonuspoäng. Använd din Ai-kompis som en allra sista utväg.

    <details><summary>Ledtråd 1</summary>

    ```sql
    FROM countrylanguage AS la
        JOIN country AS co
    ```

    </details>

    <details><summary>Ledtråd 2</summary>

    * SUM()

    * (la.percentage / 100) * co.population

    </details>

    <details><summary>Ledtråd 3</summary>

    * ORDER BY `Antal` DESC

    </details>

    <details><summary>Ledtråd 4</summary>

    * LPAD, FORMAT, sv_SE

    </details>

    ```txt
    +------------+-----------------+
    | Språk      | Antal           |
    +------------+-----------------+
    | Chinese    |   1 191 843 539 |
    | Hindi      |     405 633 070 |
    | Spanish    |     355 029 462 |
    | English    |     347 077 867 |
    | Arabic     |     233 839 239 |
    | Bengali    |     209 304 719 |
    | Portuguese |     177 595 269 |
    +------------+-----------------+
    ```



## Avslutningsvis

Det var träning i JOIN, aggregerande funktioner och lite till. Nu har du en bra grund för SQL, SELECT och rapporter från databasen.

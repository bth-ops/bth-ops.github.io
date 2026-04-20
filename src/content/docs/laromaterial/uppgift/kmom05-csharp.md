---
title: "Uppgift: CSharp bank (kmom05)" 
description: "Uppgift att skapa ett bank-liknande program i CSharp som använder sig av transaktioner och lagrade procedurer."
revision:
    "2026-02-13": "(A) Första utgåvan."
sidebar:
    order: 0050
---

Denna uppgift görs som en del av kmom05 och den bygger vidare på den uppgiften du gjort i kmom04.

<!--
TODO
* 
-->



## Förutsättning

Du behöver ha jobbat igenom övningen "Övning: Lagrade procedurer i databas" och du behöver veta hur man använder lagrade procedurer i ett CSharp program.

Du behöver också ha färdigställt uppgiften från kmom04.



## Krav - CSharp

Utför följande krav.

1. Skapa ett CSharp projekt i katalogen `kmom/05/Bank` genom att kopiera ditt projekt från `kmom/04/Bank`.

1. Bygg vidare på det projektet. Dela upp koden i klasser. Organisera din kod så att den är DRY.

1. Koden skall passera `roslynator analyze` enligt Roslyn.



## Krav - Lagrade procedurer "flytta pengar"

Utför följande krav.

1. I filen `kmom/05/Bank/sql/setup.sql`, placerar du all SQL-kod som krävs för att skapa databas, tabeller, innehåll och procedurer. Du skall alltså jobba vidare med databasen "bank".

1. Skapa lagrade procedurer för att flytta pengar mellan konton samt för att swisha till ett konto.

1. Glöm inte transaktionsavgiften till det hemliga kontot och använd transaktioner där det behövs.

1. Uppdatera din CSharp-kod så att den använder sig av lagrade procedurer för att implementera (minst) följande kommandon.

```bash
$ dotnet run
move                      - Move 1.5 bitcoin from Adam to Eva
move <amount> <from> <to> - Move a flexible amount of bitcoin from one account to another account
swish <amount> <to>       - Add <amount> to the account <to>
```

<details>
<summary>UPPDATERING. Vilka filer vi sparar SQL i.</summary>

I en tidigare version av uppgiften förekom att vi skulle spara SQL-kod i flera olika filer. Det är ok om du gjort det.

Du kan alltid göra `source` för att länka samma flera filer, så att de kan köras som en enhet.

Däremot kan det bli enklare att hantera om all SQL-kod sparas i en fil, därför är kravet uppdaterat till att vi sparar all kod i filen `setup.sql`.

</details>



## Krav - En menydriven applikation

Ditt terminalprogram skall stödja samma menyval som fanns som krav i terminalprogrammet i kmom04.

Följande är de nya menyvalen som skall stödjas.

```bash
$ dotnet run
marketplace <search>   - Show all products on the marketplace or filter by <search>
product <search>       - Show all products in the product catalogue or filter by <search>
inventory <search>     - Show all inventory or filter by <search>

sell <customer_id> <inventory_id> <price> - Move a product from the customers inventory to the 
                                        - marketplace, offer for a price.
buy <customer_id> <marketplace_id>        - Buy a product from the marketplace to the customer
                                        - inventory, pay for it.
```

Bygg stöd för samtliga menyval ovan. 

<details>
<summary>UPPDATERING. Menyvalet `market` är borttaget.</summary>

Menyvalet `market <product_id> <price>` är borttaget för att förenkla uppgiften. Det fanns med i första utgåvan av uppgiften.

```text
market <product_id> <price>            - Add a new product (from the product table) to the 
                                      - marketplace for the specified price.
```

</details>

<details>
<summary>UPPDATERING. Menyvalet `sell` är uppdaterat.</summary>

Menyvalet `sell <customer_id> <inventory_id> <price>` hade tidigare `product_id` istället för `inventory_id`. Men det är troligen enklare att hantera en flytt som direkt pekar ut en rad i tabellen inventory, istället för att peka ut en viss produkt.

Ändringen är gjord för att förenkla uppgiften.

Så här såg det ut i första utgåvan av uppgiften. Har man gjort på det viset så är det också godkänt.

```text
sell <customer_id> <product_id> <price> - Move a product from the customers inventory to the 
                                      - marketplace, offer for a price.
```

</details>

<details>
<summary>UPPDATERING. Menyvalet `buy` är uppdaterat.</summary>

Menyvalet `buy <customer_id> <marketplace_id>` hade tidigare `product_id` istället för `marketplace_id`. Men det är troligen enklare att hantera ett köp som direkt pekar ut en rad i tabellen marketplace, istället för att peka ut en viss produkt.

Ändringen är gjord för att förenkla uppgiften.

Så här såg det ut i första utgåvan av uppgiften. Har man gjort på det viset så är det också godkänt.

```text
buy <customer_id> <product_id>          - Buy a product from the marketplace to the customer
                                      - inventory, pay for it.
```

</details>

Fortsätt att läsa för att förstå hur din databas skall byggas upp för att stödja menyvalen ovan.



## Krav - Nya tabeller

Utför följande krav.

1. Din databas skall ha en tabell som heter `product` som är en produktkatalog över "produkter" eller "items" eller "saker" som finns i din bank. Tänk "Gringotts bank", där fanns det en massa konstiga saker i bankvalven. I tabellen skall det finnas kolumner för product_id, name, description, base_price samt created_at, updated_at (TIMESTAMPS).

1. Lägg till INSERT för att lägga till minst 5 olika produkter i tabellen.

1. Din databas skall ha en tabell som heter `inventory` som är en fysisk representation av en produkt som ägs av en customer. Kolumner i tabellen skall vara inventory_id, created_at, updated_at (TIMESTAMPS) samt FK customer_id och product_id. När en produkt finns i ett inventory så ägs den av en customer.

1. Lägg till INSERT för att lägga till minst 2 olika produkter till varje customer. Det skall finnas minst 2 customers.

1. Det skall finnas en tabell som heter `marketplace` som erbjuder de produkter som är till salu. Tabellen skall innehålla kolumner för price, created_at, updated_at (TIMESTAMPS) samt relationen till vilken produkt det är och vilken kund som äger den.

1. Lägg till INSERT så att det finns minst 2 produkter till salu på marketplace.

1. När en customer vill sälja en product så flyttas den från inventory till marketplace och ett price läggs till. Kunden äger fortfarande produkten. Inga pengar byter ägare. Tänk att produkten "annonseras ut" på marketplace.

1. När en customer köper en produkt från marketplace så placeras produkten i kundens inventory. Samtidigt sker en transaktion av pengar från account så att köparen betalar produktens pris till säljaren varav 0.01 pengar flyttas till det hemliga kontot.

1. Uppdatera din tabell `account` så att den innehåller en type, som anger vilken typ av konto det är. Varje kund har alltid ett (och endast ett) transaktionskonto. Om en kund har fler konton så är dessa sparkonton (savings) eller någon annan typ. När en transaktion sker på marketplace så sker den alltid via kundernas transaktionskonton.

1. Det får inte bli noll på ett account. 

1. Skissa på ett ER-diagram i puml som visar hur dina tabeller är kopplade. Spara i filen `bank.puml`. 

1. I övrigt skall databasen fungera enligt kraven i kmom04 för uppgiften.

1. Använd PRIMARY KEY och FOREIGN KEY i dina tabeller.

1. All SQL-kod som anropas från CSharp skall hanteras av lagrade procedurer.

1. Använd transaktioner där det behövs.

<!--
1. OPTIONAL Lägg till en ASCII art på  varje produkt för at göra det lite roligare och ge möjligheten att visa upp vilken produkt man har i sitt inventory. Tänk att det är en ny form av NTF.
-->

<details>
<summary>UPPDATERING. Begreppet `quantity` är borttaget.</summary>

I tidigare utgåvor av uppgiften hanterades kolumnen `quantity` i tabellerna för inventory och marketplace. Men det gör uppgiften lite mer komplex. 

I denna uppdateringen så är quantity borttaget för att förenkla uppgiften.

Du kan välja att lägga till quantity om du vill, men uppgiften är nog redan omfattande så håll det enkelt.

</details>

<details>
<summary>UPPDATERING. Marketplace köper inte produkten.</summary>

I tidigare utgåvor av uppgiften så skedde transaktioner mellan account när en kund "sålde" en produkt till marketplace.

1. ~När en customer köper en produkt så flyttas pengar från kunden till ett konto som ägs av marketplace. Av dessa pengar flyttas 0.01 pengar till det hemliga kontot.~

1. ~När en customer säljer en produkt till marketplace så får kunden pengar från marketplace (pengar flyttas i respektive account). Av dessa pengar flyttas direkt 0.01 peng till det hemliga kontot.~

Så kan man naturligtvis så på transaktionen. Om du löst det på det viset så är det ok.

I uppdateringen så sker inget utbyte av pengar förrän varan köps av en kund.

</details>



## Avslutningsvis

Glöm inte kontrollera att lintern passerar.

Fundera på om din kod är DRY eller om det finns delar som du kan förbättra.

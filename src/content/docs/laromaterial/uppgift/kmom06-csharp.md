---
title: "Uppgift: CSharp bank (kmom06)" 
description: "Uppgift att skapa ett bank-liknande program i CSharp som använder sig av transaktioner, lagrade procedurer och triggers."
revision:
    "2026-02-20": "(A) Första utgåvan."
sidebar:
    order: 0060
---

Denna uppgift görs som en del av kmom06 och den bygger vidare på den uppgiften du gjort i kmom04 och i kmom05.

<!--
TODO
* 
-->



## Förutsättning

Du behöver ha jobbat igenom övningen "Övning: Triggers i databas".

Du behöver också ha färdigställt uppgiften från kmom04 och kmom05.



## Krav - CSharp

Utför följande krav.

1. Skapa ett CSharp projekt i katalogen `kmom/06/Bank` genom att kopiera ditt projekt från `kmom/05/Bank`.

1. Bygg vidare på det projektet. Dela upp koden i klasser. Organisera din kod så att den är DRY.

1. Koden skall passera `roslynator analyze` enligt Roslyn.



## Krav - En menydriven applikation

Ditt terminalprogram skall stödja samma menyval som fanns som krav i terminalprogrammet i kmom05.

Följande är de nya menyvalen som skall stödjas.

```bash
$ dotnet run
items <search>        - Show (or filter) all products that are in the marketplace
                      - or in the inventory, combine into one single report, one
                      - output table.
log <limit> <search>  - Show (or limit, filter) all entries in the log.
```

Bygg stöd för samtliga menyval ovan. 

Fortsätt att läsa för att förstå hur din databas skall byggas upp för att stödja menyvalen ovan.



## Krav - Nya konstruktioner

Utför följande krav.

1. Din databas skall ha en tabell som heter `log` där viktiga händelser loggas för att få en historik över vad som händer i din databas. I tabellen skall det (minst) finnas kolumner för id, when, what, account, balance, amount.

1. Skapa en trigger som loggar alla uppdateringar (AFTER UPDATE) från tabellen account.

1. Skapa en trigger som loggar alla förändringar (INSERT, DELETE) i tabellerna inventory och marketplace. Försök skapa en sträng som du sparar i loggtabellens "what" som beskriver tydligt vilken händelse det är.

1. För att lösa menyvalet "items" så skall du använda UNION.

1. Använd enbart lagrade procedurer vid själva kopplingen mot CSharp.

1. Se till att din databasmodell är uppdaterad i `bank.puml`.

1. I övrigt skall databasen fungera enligt kraven i kmom05 för uppgiften.



## Avslutningsvis

Glöm inte kontrollera att lintern passerar.

Fundera på om din kod är DRY eller om det finns delar som du kan förbättra.

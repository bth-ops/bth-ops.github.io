---
title: "Uppgift: CSharp (kmom03)" 
description: "Uppgift att skapa ett program i CSharp som visar upp rapporter från en databas."
revision:
    "2026-01-30": "(A) Första utgåvan."
sidebar:
    order: 0030
---

Denna uppgift görs som en del av kmom03.



## Förutsättning

Du behöver ha jobbat igenom övningarna "Övning databasen Classic Models" och "Övning CSharp med databasen Classic Models".



## Krav - Allmänt

Utför följande krav.

1. Skapa ett CSharp projekt i katalogen `kmom/03/ClassicModels`.

1. Kod för att koppla mot databasen skall finnas i klassen `Database`.

1. Kod för att skriva SQL-frågor skall finnas i klassen `Queries`.

1. Kod för din klass `Menu` skall finnas i `Menu.cs`. Du får skapa fler klasser om du vill.

1. Du bör organisera din kod så att den är DRY (Do not repeat yourself).

1. Koden skall passera `roslynator analyze` enligt Roslyn.



## Krav - En menydriven applikation

Skapa en menydriven applikation C# som ser ut så här för användaren.

När programmet startas så skrivs meny ut. Du kan formattera utskriften av menyn efter dina egna tankar.

```text
$ dotnet run
menu, help, h      - Print out the menu.
products <search>  - Show all products or filter by <search>
customers <search> - Show all customers or filter by <search>
quit, q            - Quit the application

> 
```

Programmet väntar därefter på användarens inmatning. Om användaren skriver menu visas menytexten. Om användaren skriver quit eller q avslutas applikationen.

Kommandot products <search> ska implementeras på följande sätt: Om användaren endast skriver products visas alla produkter. Om användaren skriver products harley görs en sökning efter strängen harley, och de rader som matchar söksträngen visas.

Kommandot customers <search> fungerar på samma sätt.




## Krav - Skapa kommandon

Ditt menydrivna program skall implementera följande kommandon och de skall vara synliga i menyn.

1. products           - Show all products

    Visa en lista av produkter, begränsa utskriften till 10 rader. Visa produktens namn tillsammans med namnet för produktlinjen och vendorn. Välj fler kolumner om du vill.

1. products <search>  - Show all products or filter by <search>

    Gör en sökning i produkttabellen och visa enbart de rader som matchar. I övrigt samma krav som ovan.

1. customers          - Show all customers

    Visa en lista av kunder, begränsa utskriften till 10 rader. Visa (minst) kundens namn, city/country och namnet på företagets salesrep.

1. customers <search> - Show all customers or filter by <search>

    Gör en sökning i kundtabellen och visa enbart de rader som matchar. I övrigt samma krav som ovan.



## Inlämning

När du är helt klar med detta kursmomentet så lämnar du in genom att göra en pull request (PR) mot din branch `bth/submit/kmom03`. [Läs instruktionen om hur du gör en PR](/website/laromaterial/instruktion/gor-en-pr-for-kmom03/).



## Avslutningsvis

Glöm inte kontrollera att lintern passerar.

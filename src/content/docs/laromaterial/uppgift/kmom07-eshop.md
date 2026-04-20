---
title: "Uppgift: EShop hantera order och orderdetaljer (kmom07)" 
description: "Uppgift att implementera delar av databasen eshop."
revision:
    "2026-03-11": "(B) Uppdatera kravet om order_del."
    "2026-02-27": "(A) Första utgåvan."
sidebar:
    order: 0070
---

Denna uppgift görs som en del av kmom07. Du jobbar vidare på den databasmodell för en eshop som du skapade i kmom04-06.

Du skall implementera schemat för databasen eshop och börja jobba med den. Första steget, när schemat är på plats, är att fylla databasen med innehåll och implementera CRUD (Create Read Update Delete) mot vissa av tabellerna i databasen med hjälp av ett terminalprogram i CSharp.

Denna uppgiften är också en del av det kommande projektet i kmom10, så den koden du skriver här kommer att vara en del av det examinerande kmom10. Det innebär att kodbasen du börjar på nu kommer att vara en del av din slutliga inlämning i kmom10.

<!--
TODO
* `orders` visade antalet orderrader (COUNT), (OUT JOIN) samt någon order som är tom.
* Ändra kommandon product -> products och customer - customers?
-->



## Förutsättning

Du har din databasmodell klar för din eshop och du har SQL-kod för att skapa tabeller och vyer.



## Krav - CSharp

Utför följande krav.

1. Skapa ett CSharp projekt i katalogen `kmom/07/Eshop`. 

1. Följ en liknande kodstruktur för ditt terminalbaserade CSharp program som du gjort i kmom04-06.

1. Dela upp koden i klasser. Organisera din kod så att den är DRY. Refaktorisera när det behövs.

1. Koden skall passera `roslynator analyze` enligt Roslyn.



## Krav - Innehåll i databasens tabeller

Utför följande krav.

1. Skapa underkatalogen `sql/` där du placerar din `setup.sql` som innehåller SQL-kod för att skapa databasen `eshop` tillsammans med tabeller och vyer. Det är fritt fram att justera SQL-koden som skapar schemat, även om det inte följer din ursprungliga ER-modell. Se framåt och gör bättre efterhand som du lär dig mer om din databas och när det finns anledning att anpassa dess schema.

1. Skapa filen `insert.sql` där du placerar SQL-kod som fyller (delar av) databasens tabeller med innehåll.

    1. Lägg in minst 3 kunder.
    1. Lägg in minst 7 produkter.
    1. Lägg in minst 5 ordrar där följande skall vara uppfyllt:
        1. En order har ingen orderrad.
        1. Fyra av ordrarna har en eller flera orderrader.
        1. En av ordrarna är markerad som beställd (se längre ned vad det innebär).

    1. Om du väljer att göra `LOAD DATA INFILE` med hjälp av csv-filer så skall csv-filerna placeras i samma katalog och sökvägar skall vara relativa.

1. Skapa filen `proc.sql` där du placerar SQL-kod som skapar lagrade procedurer, triggers och funktioner.

    1. All access från ditt terminalprogram i CSharp skall ske via lagrade procedurer.
    1. Du skall använda minst en trigger (tips finns längre ned).
    1. Du skall använda minst en funktion (tips finns längre ned).

1. Skapa filen `eshop.puml` där du placerar en uppdaterad version av din databasmodell i PlantUML format. Filen skall vara uppdaterad och spegla den databas du har skapat, det blir en del av din dokumentation av databasen. För att göra det enkelt, prova att ge koden i `setup.sql` till din Ai-kompis och fråga om den kan generera ett ER-diagram i PlantUML utifrån koden. Det kan den ofta göra, för denna delen av uppgiften är det ok att använda Ai på detta viset, se det som en variant av hur en programmerare kan använda Ai för att skapa bättre kod/dokumentation på ett effektivt sätt.



## Krav - Orderhantering

Så här skall det fungera när en kund placerar en ny order.

1. En ny order kan skapas till en kund. Det sparas en timestamp `created` för när ordern skapades.
1. En order som är skapad, men innehåller inga orderrader, har statusen "created".

1. Till en order kan man lägga till orderrader där varje orderrad innehåller en produkt, antal och ett försäljningspris. (Det pris som ligger i produkt-tabellen är inköpspriset)
1. Varje gång en orderrad läggs till, eller tas bort, så skall en timestamp `updated` ändras i order-tabellen.
1. När en order är uppdaterad så ändras dess status till "updated".

1. När ordern är klar och beställs så skall en timestamp `ordered` sättas.
1. Därmed ändras orderns status till "ordered".
1. När en order är beställd så kan man inte längre lägga till fler orderrader eller ta bort orderrader, den är låst. 

1. När du visar en lista av ordrar så skall du även visa hur många orderrader som varje order har samt orderns status.

1. När du visar en specifik order, så skall orderns väsentliga detaljer visas inklusive dess status. Du skall också visa en lista av orderrader som tillhör ordern där man ser produktens namn. Du skall även summera orderns pris.

PS. Att hantera orderns status är tänkt att göras med en funktion.

PSS. Att uppdatera orderns `updated` timestamp är tänkt att göras med en trigger.



## Krav - En menydriven applikation

Ditt terminalprogram skall byggas på samma sätt som du gjort i kmom04-06 med samma typ av meny.

Följande är de menyvalen som skall stödjas.

```bash
$ dotnet run
m, menu, help, h           - Print out the menu.
quit, q                    - Quit the application

customer <search>          - Show all customers or filter by <search>
product <search>           - Show all products or filter by <search>
orders <search>            - Show all orders or filter by <search>
order <order_id>           - Show the order, order rows and order cost.

order_create <customer_id>          - Create a new order for the customer.
order_add <order_id> <product_id> <amount> <price> - Add a new order row to the order.
order_done <order_id>               - Mark the order as done, no more order rows can be added to the order.
```

Du skall även lägga till följande menyval som tar bort en rad i en order, välj en variant av hur du implementerar kommandot, antingen via `order_row` eller via `product_id`.

```bash
order_del <order_id> <order_row>    - Remove an order row from the order.
order_del <order_id> <product_id>   - Remove a product from the order.
```

Då får gärna lägga till fler menyval som du tycker är intressanta, det är helt ok att utöka funktionaliteten i terminalprogrammet så länge som det stödjer samtliga menyval enligt ovan.



## Självtest

Kontrollera att du kan återskapa din databas enligt följande.

```bash title="Återskapa databas"
# Gå till katalogen sql/
mariadb < setup.sql
mariadb eshop < proc.sql
mariadb eshop < insert.sql
```

Flödet ovan behöver fungera, läraren testar din inlämning exakt på det viset. Det är tillåtet att dela upp din kod i fler filer och göra source på dem samt att läsa in data från till exempel csv-filer.

Filerna `proc.sql` och `insert.sql` får inte innehålla ett `USE eshop` för att välja databas. Det gör att läraren får problem vid rättning.

Kontrollera att databasen innehåller tillräckligt med data.

Provkör därefter ditt terminalprogram i CSharp och se till att det fungerar som det skall med samtliga menyval.

Kontrollera att flödet för att göra en order fungerar enligt kraven.

Säkerställ att en order kan visa status enligt kraven.

Kontrollera att du har både minst en trigger och en funktion i din databas.



## Avslutningsvis

Glöm inte kontrollera att lintern passerar.

Fundera på om din kod är DRY eller om det finns delar som du kan förbättra.

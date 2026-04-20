---
title: "Uppgift: EShop hantera lagret (kmom08)" 
description: "Uppgift att fortsätta implementera delar av databasen eshop."
revision:
    "2026-03-09": "(B) Förtydliga hur backupen tas och att det är den som används vid rättning."
    "2026-03-08": "(A) Första utgåvan."
sidebar:
    order: 0080
---

Denna uppgift görs som en del av kmom08. Du jobbar vidare på den databasmodell för en eshop som du skapade i kmom04-06 och den implementationen du gjort i kmom07.

Du skall fortsätta implementera ditt terminalprogram och bygga vidare på din eshop.

Denna uppgiften är också en del av det kommande projektet i kmom10, så den koden du skriver här kommer att vara en del av det examinerande kmom10. Det innebär att kodbasen skriver nu kommer att vara en del av din slutliga inlämning i kmom10.



## Förutsättning

Du har genomfört kmom07.



## Krav - CSharp

Utför följande krav.

1. Skapa ett CSharp projekt i katalogen `kmom/08/Eshop` genom att kopiera `kmom/07/Eshop`. 

1. Dela upp koden i klasser. Organisera din kod så att den är DRY. Refaktorisera när det behövs.

1. Koden skall passera `roslynator analyze` enligt Roslyn.



## Krav - Innehåll i databasens tabeller

Utför följande krav.

1. Du har sedan tidigare följande filer i katalogen `sql/` för att skapa databasen med dess schema och innehåll. Uppdatera dessa filer för att uppfylla kraven nedan.

    1. `setup.sql`
    1. `proc.sql`
    1. `insert.sql`

1. Ditt lager skall vara uppdelat i hyllor. Varje hylla har ett unikt id som är en bokstav följt av 3 siffror. Till exempel "A100", "A101" eller "Z999". När en produkt befinner sig i lagret så ligger den på en sådan hylla ("shelf"). Skapa så att det finns minst 5 hyllor i ditt lager varav minst två skall vara tomma och inte innehålla produkter.

1. På en hylla kan man placera en eller flera produkter. Det kan finnas flera olika produkter samtidigt på en och samma hylla. Databasen skall inte sätta någon begränsning för hur man placerar produkter på lagret.

1. Om det redan ligger en produkt på en hylla, och man lägger till ytterligare produkter, så skall antalet av den specifika produkten räknas upp. Tips INSERT ON DUPLICATE KEY UPDATE.

1. Om man tar bort produkter från en hylla så kan det bli negativt antal, det är ok, då har någon räknat fel i lagret.

1. Lägg till relevanta index till de tabeller som berörs av uppgiften. Lägg till minst tre index, förutom PK. Om du inte behöver tre index  i uppgiften, förutom PK, så leta vidare i din databasmodell och lägg till index där det behövs. Till exempel, se om förra veckans uppgift kan må bra av något index.

1. Uppdatera din databasmodell i filen `sql/eshop.puml` med egen kraft eller med hjälp av din AI-kompis.

1. När du är helt klar, skapa en backup av din databas och spara i `sql/backup.sql`. Läs mer om hur du [skapar (och verifierar) en backupfil](https://github.com/bth-databas/forum/discussions/9). 

    ```bash title="Skapa en backup av din databas."
    mariadb-dump                          \
        --routines                        \
        --triggers                        \
        --default-character-set=utf8mb4   \
        eshop > backup.sql
    ```



## Krav - En menydriven applikation

Följande är de nya menyvalen som skall stödjas.

```bash
$ dotnet run
shelfs <search>  - Show all shelfs or filter by <search>
inv <search>     - Show all shelfs and the products on them, or filter by <search>

inv_add <shelf_id> <product_id> <quantity> - Add products to a shelf
inv_del <shelf_id> <product_id> <quantity> - Remove products from a shelf
```

* Shelf = lagerhylla

Kommandot `inv` skall visa samtliga lagerhyllor, oavsett om det ligger en produkt på dem eller om hyllan är tom.

Kommandot `inv` visar produktens namn, id och antal som ligger på lagerhyllan.

Kommandot `inv` filtrerar på (minst) lagerhyllans id, produktens id, produktens namn.

Då får gärna lägga till fler menyval som du tycker är intressanta, det är helt ok att utöka funktionaliteten i terminalprogrammet så länge som det stödjer samtliga menyval enligt ovan.



## Självtest

Försäkra dig om att din backupfil fungerar. När läraren återskapar din databas så kommer följande kommando att köras.

```bash
# Gå till katalogen sql/
mariadb eshop < backup.sql
```

Kontrollera att du även kan återskapa din databas enligt följande.

```bash title="Återskapa databas"
# Gå till katalogen sql/
mariadb < setup.sql
mariadb eshop < proc.sql
mariadb eshop < insert.sql
```

Flödet ovan behöver fungera, om din backupfil inte fungerar så kan läraren välja att prova att återställa din databas från dessa filer. Det är tillåtet att dela upp din kod i fler filer och göra source på dem samt att läsa in data från till exempel csv-filer.

Filerna `proc.sql` och `insert.sql` får inte innehålla ett `USE eshop` för att välja databas. Det gör att läraren får problem vid rättning.

Kontrollera att databasen innehåller tillräckligt med data.

Provkör därefter ditt terminalprogram i CSharp och se till att det fungerar som det skall med samtliga menyval.

Kontrollera att flödet för att lägga till en produkt på en lagerhylla resulterar i rätt antal av produkten. Därefter lägga till fler av samma produkt på samma hylla och därefter plocka bort ett antal av produkten från hyllan, allt skall resultera i rätt antal av produkten på hyllan.

Säkerställ att samtliga lagerhyllor visas, även de som inte har produkter på sig.

Kontrollera att du har relevanta index på de tabeller som berörs av denna uppgift.



## Avslutningsvis

Glöm inte kontrollera att lintern passerar.

Fundera på om din kod är DRY eller om det finns delar som du kan förbättra.

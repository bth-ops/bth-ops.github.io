---
title: "Uppgift: ER-modellering - fysisk (kmom06)" 
description: "Uppgift att göra en fysisk modellering av en databas."
revision:
    "2026-02-27": "(B) Lägg till krav om att visa schema.pdf, förtydliga några krav."
    "2026-02-20": "(A) Första utgåvan."
sidebar:
    order: 0065
---

Denna uppgift görs som en del av kmom06. Du jobbar vidare på uppgiften som du jobbat med i kmom05 och kmom04.

Du skall jobba med databasmodellering och skapa en ER-modell av en databas.

Detta är sista delen av uppgiften och du skall utföra den fysiska modelleringsfasen.



## Förutsättning

Du har utfört andra delen av uppgiften och gjort en logisk ER-modell av databasen och du har sparat alla steg i dokumentet du skriver.



## Introduktion

Du skall jobba igenom de olika faserna enligt den metod som beskrivs i kokboken.

I denna specifika uppgift skall du utföra den fysiska modelleringsfasen. Det är den avslutande delen av modelleringsuppgiften.

Varje steg du gör (enligt kokbokens steg) skall du dokumentera i ett ER-dokument som du lämnar in som pdf. När du är klar finns samtliga delsteg dokumenterade i ditt dokument.

Missa inte att dokumentera varje steg i ditt ER-dokument. 



## Krav - Dokumentera alla steg i ditt ER-dokument

1. Fortsätt jobba i det ER-dokument du skapade i första delen av uppgiften.

1. Skapa en ny sida med rubrik "Fysisk modell" och utför och dokumentera alla delsteg för den fysiska modelleringsfasen, enligt kokbokens steg.

1. Skapa katalogen `kmom/06/eshop/` och spara allt ditt arbete där.

1. Generera en PDF-fil `er.pdf` av ditt kompletta dokument och spara.

1. Skapa filen `setup.sql` som skapar databasen `eshop` med character set och collate.

1. I filen `setup.sql` lägger du till SQL dör att skapa de tabeller (och vyer) som du modellerat fram. Om du behöver ändra på något så gör du det i SQL-koden som skapar databasens schema, du behöver inte gå tillbaka och modifiera din ER-modell.

1. Använd PK och FK.

1. Du behöver inte lägga till INSERT-satser i `setup.sql` för att fylla databasen, det gör du i nästa kmom när du börjar använda databasen "på riktigt".

1. Verifiera att du kan köra `setup.sql` minst två gånger efter varandra och databasen skapas korrekt.

1. Avslutningsvis så gör du reverse engineering av din färdiga databas för att generera en ER-modell, ta en skärmdump (eller liknande) av resultatet och spara den i `schema.pdf`.

Vi väntar till nästa vecka för att fylla databasen med innehåll och då börja använda den "på riktigt".



## Avslutningsvis

Försäkra dig om att ditt ER-dokument innehåller dokumentation av varje steg i kokboken.

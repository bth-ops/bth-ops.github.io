---
title: "Uppgift: ER-modellering - konceptuell (kmom04)" 
description: "Uppgift att göra en konceptuell modellering av en databas."
revision:
    "2026-02-13": "(B) Förtydliga att man kan välja vad databasen skall innehålla."
    "2026-02-08": "(A) Första utgåvan."
sidebar:
    order: 0045
---

Denna uppgift görs som en del av kmom04.

Du skall jobba med databasmodellering och skapa en ER-modell av en databas.

Detta är första delen av uppgiften och du skall utföra den konceptuella modelleringsfasen.



## Förutsättning

Du kan grunderna i ER-modellering och du har tillgång till guiden "Kokbok för databasmodellering".



## Introduktion

Du skall jobba igenom de olika faserna enligt den metod som beskrivs i kokboken.

I denna specifika uppgift skall du utföra den konceptuella modelleringsfasen. I kommande uppgifter, skall du utföra den logiska och den fysiska modelleringsfasen.

Varje steg du gör (enligt kokbokens steg) skall du dokumentera i ett ER-dokument som du lämnar in som pdf. När du är klar finns samtliga delsteg dokumenterade i ditt dokument.

Missa inte att dokumentera varje steg i ditt ER-dokument. 



## Välj bas för din modellering

Det finns generella krav på databasen som alla skall uppfylla, men därefter kan du anpassa databasen till ditt eget val. Du kan till exempel fylla databasen med den typ av data som du själv vill ha i databasen. På det viset kan du själv välja fokus för din databas, så länge det baseras på grundtanken om en e-shop och att det är den tabellstruktur som krävs för en eshop.

Den databasmodell du nu skapar skall du senare använda för att koppla till ett terminalprogram.



## Generellt krav på databasen

Databasen behöver hantera ett kundregister (kunder med kontaktdetaljer), ett produktregister (produkter med produktkod, namn, kort beskrivning och pris).

Databasen behöver också innehålla ett lager där man ser hur många av varje produkt som finns i lagret och en notering om var produkten ligger i lagret (vilken hylla). En och samma produkt kan vara utspridd över olika hyllor i lagret.

När kunden beställer en produkt så skapas en order som innehåller kundens detaljer tillsammans med vilka produkter som beställts och dess beställda antal.

Utifrån ordern skapas en plocklista som kan skickas till lagret för leverans. Plocklistan innehåller samma information som ordern, men med tillägget att varje produktrad mappas mot en lagerhylla så att lagerpersonalen kan se vilken hylla de kan hämta produkten på.

När leveransen är packad så bifogas en faktura som har samma innehåll som ordern men nu med priset per produktrad och det summerade priset.

Det skall finnas en logg där man kan se viktiga händelser i systemet, vad hände, när hände det. Det kan till exempel vara när order/faktura skapades eller raderades.

Du kan själv välja vilken typ av produkter som din databas skall hantera.



## Krav - Dokumentera alla steg i ditt ER-dokument

1. Skapa en trevlig förstasida till ditt dokument. Skriv titel och namnen på den som utfört modelleringen.

1. Lägg till en representativ bild på förstasidan.

1. Skapa en innehållsförteckning som sida 2.

1. Skapa en ny sida med rubrik "Konceptuell modell" och utför och dokumentera alla delsteg för den konceptuella modelleringsfasen, enligt kokbokens steg.

1. Generera en PDF-fil `er.pdf` av dokumentet och spara i kursrepot under `kmom/04/er.pdf`.



## Avslutningsvis

Försäkra dig om att ditt ER-dokument innehåller dokumentation av varje steg i kokboken.

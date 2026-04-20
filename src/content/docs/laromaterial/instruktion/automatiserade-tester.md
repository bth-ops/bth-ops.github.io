---
title: "Automatiserade tester" 
description: Så här kan du testa ditt eget repo inför en inlämning.
sidebar:
    order: 0060
---

När du gör en inlämning så körs ett antal automatiserade tester för att kontroller att ditt repo innehåller tom som förväntas enligt kraven.

Det är bra att säkerställa att din inlämning passerar dessa tester, innan du gör din PR.

Detta dokument ivsar hur du kan installera och använda verktyget.



## Installera och uppdatera

Du går till ditt repo och sedan installerar du verktyget som en npm-modul.

```bash
npm install @dbwebb/databas --save-dev
```

Uppdatera din lokala installtion till den senaste versionen av verktyget.

```bash
npm update @dbwebb/databas@latest
```


## Testkör ditt repo

Du kan köra tester mot ett specifikt kursmoment. Om du väljer ett högre kursmoment så kommer det även att köras tester för de tidigare kursmomenten.

För att tex testa ditt kmom03 så skriver du följande.

```bash
npx @dbwebb/databas check kmom03
```

<!--
Om du vill testa dina labbar så anger du vilka labbar som du vill testa, så här kan du testa de labbar som omfattas av kmom03.

```bash
npx @dbwebb/databas check lab lab_01 lab_02 lab_03
```
-->



## Dokumentation

Du kan läsa om verktyget via dess paket-sida [`@dbwebb/databas`](https://www.npmjs.com/package/@dbwebb/databas), därifrån kan du också nå dess källkod.

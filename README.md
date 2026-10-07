# Mit blodtryk – Firebase

Appen har Google-login og Cloud Firestore for projektet blodtryk-a1472. Loginområdet indeholder nu kun Google-login med logo samt kontoens status. Lokale migrationsknapper er fjernet. Log ind med samme Google-konto på alle enheder. Nye målinger gemmes direkte online, når du trykker Gem målerunde og ser “Gemt i Firebase”. Internet kræves.

## Opdatering

Erstat index.html, app.js, style.css og sw.js i dit eksisterende GitHub Pages-repository. De øvrige appfiler og din Firebase-opsætning bevares. Vent på publicering, og genåbn appen online for at hente opdateringen. Firestore-data ændres ikke af UI-opdateringen.

## Dato og tid

Datoer indtastes og vises i fast dansk format dd.mm.åååå. Tast fx 07102026: punktummer indsættes automatisk. Dermed afhænger feltet ikke af browserens datoformat. Den indbyggede browserkalender erstattes af et tekstfelt med numerisk tastatur. Ugyldige datoer, fx 31.02.2026, afvises. Tiden er stadig 24-timers format: 2030 bliver 20:30.

## Sessioner

Vælg samme startdato for tre sammenhængende dage. Hver morgen-/aftenrunde består af tre målinger. Sessionens gennemsnit beregnes af alle dens registrerede rå målinger og afrundes til nærmeste heltal. Antal registrerede dage vises. Appen giver ingen lægelig vurdering.

## Firebase-opsætning ved ny installation

1. Authentication → Sign-in method: aktivér Google og vælg support-mail.
2. Authentication → Settings → Authorized domains: tilføj GitHub Pages-domænet uden https:// eller sti.
3. Firestore Database: opret Standard edition, database-ID (default), europæisk placering og Production mode.
4. Firestore → Rules: erstat hele regelsættet med firestore.rules og klik Publish. Det begrænser læsning/skrivning til den aktuelle brugers /users/UID/sessions/ID.
5. Læg appfilerne i repositoryets rod og aktivér Pages fra main, / (root).

## Backup og forbindelser

JSON- og CSV-eksport samt import findes fortsat under Backup og installation. Der er ingen lokal migration i loginområdet. Eksisterende dokument-ID'er springes over ved backupimport. Eksport omfatter den senest hentede historik. Genåbn siden for at hente ændringer fra en anden enhed. Ved samtidig redigering vinder den sidst gemte version.

Ved forbindelsesproblemer beholdes tal i formularen; vent på bekræftelse fra Firebase før du lukker. Der er ikke en garanteret offlinekø. En eksport er stadig nyttig som separat kopi mod utilsigtet sletning eller redigering online.

## Kontrol

JavaScript-syntaks, datoparsning, ugyldige datoer/skudår samt cloud-adapter med simuleret Firebase er kontrolleret. Browser/iPhone og rigtig Firebase-login skal afprøves efter publicering. Din eksisterende konfiguration og firestore.rules er uændrede.

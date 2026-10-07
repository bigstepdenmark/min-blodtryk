# Mit blodtryk

En dansk, iPhone-venlig PWA uden backend, login eller eksterne biblioteker.

## Brug

1. Vælg startdatoen for en 3-dages session, fx 7. oktober. Sessionen omfatter 7., 8. og 9. oktober.
Tider indtastes og vises altid i 24-timers format, fx 08:30 eller 20:30.

2. Registrér morgen eller aften med tre målinger af overtryk, undertryk og puls.
3. Brug samme startdato til alle målerunder i sessionen. Måledatoen skal ligge inden for de tre dage.
4. Under Overblik vælges en 3-dages session. Her vises gennemsnit af blodtryk og puls, graf og alle dens målerunder. Appen viser, hvor mange af de tre dage der er registreret målinger for.
5. Når du starter næste session, vælger du en ny startdato.

Gennemsnit er det aritmetiske gennemsnit af alle registrerede rå målinger i den valgte session, afrundet til nærmeste heltal. Ingen målinger eller dage udelades automatisk. En delvist udfyldt session får også et gennemsnit, og antal målinger og registrerede dage vises. Appen giver ingen medicinsk vurdering.

## GitHub Pages

1. Opret et repository, og læg indholdet af denne mappe i repositoryets rod: index.html, app.js, style.css, sw.js, manifest.webmanifest og alle ikoner.
2. Under repositoryets Settings → Pages vælges Deploy from a branch, main og / (root).
3. Åbn den viste HTTPS-adresse i Safari på iPhone.
4. Vælg Del → Føj til hjemmeskærm. Åbn derefter appen fra hjemmeskærmen og registrér dine målinger dér.

Alternativt kan filerne lægges i en mappe på din egen HTTPS-webserver. Relative adresser understøtter en undermappe. Der er intet build-trin.

## Lokal afprøvning på computer

Kør fra denne mappe:

```sh
python3 -m http.server 8080
```

Åbn http://localhost:8080. Offline-funktion kræver HTTPS eller localhost. En løs HTML-fil i iPhones Filer-app fungerer ikke som en installerbar PWA. Afprøvning fra telefonen via en computers IP-adresse kræver HTTPS for offline-funktionen.

## Lagring og iCloud

Målinger gemmes i IndexedDB på enheden, knyttet til webadressen og browserens/appens lokale lager. Der sendes ingen målinger til serveren, og der er ingen automatisk iCloud-synkronisering. Undgå at skifte webadresse eller skifte mellem browser og hjemmeskærmsapp uden at tage backup; de kan have forskelligt lager.

Under Backup og installation kan du hente JSON-backup, gemme den i Filer → iCloud Drive og indlæse den senere. Import tilføjer kun målerunder med nye ID'er og overskriver ikke eksisterende målerunder. CSV indeholder alle rå målinger samt sessionernes startdatoer og kan åbnes i Excel. Backup og CSV indeholder dine helbredsoplysninger.

Browserdata er ikke en garanteret permanent backup. Data kan mistes ved rydning af browserdata, afinstallation, pladsproblemer eller tab af telefon. Eksportér jævnligt.

## Opdateringer

Når du ændrer appens filer, ændrer du også CACHE-versionen i sw.js (fx mit-blodtryk-v2). Den nye version henter alle lokale appfiler igen. Målingerne ligger separat i IndexedDB og bevares.

## Validering

JavaScript-syntaks, beregning af gennemsnit, gruppering af 3-dages sessioner, datogrænser og backupvalidering er kontrolleret automatisk. Browser- og iPhone-test kunne ikke gennemføres i byggemiljøet; afprøv registrering, genåbning, offlinebrug og backup efter hosting, før appen bruges som eneste dagbog.

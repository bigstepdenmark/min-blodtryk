# Mit blodtryk – Firebase-version

Din app har nu Google-login og Cloud Firestore. Den ligger fortsat på GitHub Pages. Projektet er blodtryk-a1472. Kun målinger med bekræftelsen “Gemt i Firebase” er gemt online. Internet er nødvendigt for login, hentning og gemning. Google-popup-login anvendes for at undgå problemer med redirect-login på Safari og GitHub Pages.

## 1. Tag lokal backup

Inden opdatering: hent backup fra din eksisterende app. Hvis du allerede har opdateret, findes “Hent tidligere lokal backup” i den nye version. Den læser den oprindelige IndexedDB og kræver ikke login. Brug samme webadresse og samme browser/hjemmeskærmsapp som før. Lokale målinger slettes ikke under migration.

## 2. Aktivér Google-login

Firebase Console → blodtryk-a1472 → Build → Authentication → Get started → Sign-in method → Google → Enable. Vælg support-mail og gem.

Under Authentication → Settings → Authorized domains tilføjes dit GitHub Pages-domæne, fx ismail.github.io. Brug kun domænet, uden https:// og uden /blodtryk/. Til lokal test tilføjes localhost separat.

## 3. Opret Firestore

Build → Firestore Database → Create database. Vælg Standard edition, hvis edition skal vælges, database-ID (default), en europæisk placering og Production mode. Brug gratis Spark-plan; appen kræver ikke Storage, Functions eller betalt Hosting.

## 4. Aktivér adgangsregler

Firestore Database → Rules: erstat hele indholdet med filen firestore.rules og klik Publish. Andre brede tilladelser må ikke stå tilbage i regelsættet, fordi matchende tilladelser kombineres. Reglerne tillader kun loginbrugeren at læse/skrive /users/DERES_UID/sessions/ID. Målingernes form og interval valideres også. Andre stier har ingen tilladelser.

Alle kan logge ind med Google og gemme deres egne målinger. De kan ikke læse dine. Hvis projektet kun skal tillade én bestemt Google-konto, kan reglerne senere begrænses til denne kontos Firebase UID. Service account-nøgler anvendes ikke i appen.

## 5. Opdatér GitHub Pages

Upload filerne i denne mappe til den samme rod som før. De ændrede filer er index.html, app.js, style.css og sw.js. firestore.rules skal publiceres i Firebase Console; upload til GitHub aktiverer den ikke.

Vent på GitHub Pages-publiceringen. Åbn appen online, luk og genåbn den ved behov for at aktivere den nye version. Dine tidligere målinger bevares i det lokale lager.

## 6. Flyt dine målinger

Log ind med Google. Klik “Flyt lokale målinger til Firebase”. Dialogen viser modtagerkontoen. Bekræft kun med din egen konto. Eksisterende dokument-ID'er springes over, også ved gentaget import. Hvis overførslen afbrydes halvvejs, kan du prøve igen uden at overskrive allerede overførte målinger.

Alternativt kan du indlæse din JSON-backup. Vælg Overblik for at kontrollere sessioner, gennemsnit og antal målerunder. Log ind med samme konto på en anden browser eller enhed og kontrollér, at målingerne er der, før du rydder lokale browserdata.

## Gemning og backup

Appen venter på Firebase-bekræftelse før den viser “Gemt i Firebase”. Ved netværksfejl beholdes tallene i formularen. Hvis forbindelsen går under gemning, kan Firebase vente på genetablering; luk ikke appen før bekræftelsen. Der er ikke en separat offlinekø, der er garanteret bevaret ved genåbning. Opdater målinger henter den aktuelle serverversion. Ved samtidig redigering på to enheder vinder den sidst gemte version.

Online gemning er ikke en versionsbackup: slettede og redigerede data ændres også online. Hent fortsat JSON-backup efter behov. Eksport omfatter den senest hentede historik for den indloggede konto. CSV indeholder alle rå målinger.

## 3-dages sessioner

Vælg samme startdato for tre sammenhængende dage. Hver morgen-/aftenrunde indeholder tre målinger. Sessionens gennemsnit beregnes af alle dens registrerede rå målinger, afrundet til nærmeste heltal. Antal registrerede dage vises, også når sessionen endnu ikke er færdig. Tider bruger 24-timers format. Appen giver ingen lægelig vurdering.

## Kontrol

JavaScript-syntaks og beregnings-/importlogik er kontrolleret. Cloud-adapteren er testet med simuleret Firebase for kontoadskillelse og gentaget migration. Rigtige Google-login, Firestore-regler og iPhone-adfærd kan først afprøves efter console-opsætningen. Kontrollér i Firebase Rules Playground, at uautentificeret adgang og adgang med en anden UID afvises, og at ejeren kan læse sin egen sti. Browser- og emulator-test var ikke tilgængelig under byggeriet.

Kildevejledninger: https://firebase.google.com/docs/auth/web/google-signin og https://firebase.google.com/docs/firestore/quickstart

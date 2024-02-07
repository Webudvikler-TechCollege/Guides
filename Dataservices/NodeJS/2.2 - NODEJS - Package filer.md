# Package.json & Package.lock.json

## Package.json

Package.json filen finder du i hver eneste npm pakke. Det er en fil der holder informationer om en given pakke og skal bruges af npm.

Denne fil bliver for det meste automatisk modificeret af npm - som f.eks. når du installerer et modul m.m. - men i nogle tilfælde kan du få brug for selv at skrive den.

Informationerne i filen indeholder data om pakkens navn, version og de pakker som pakken selv er afhængig af. Den faglige term for disse pakke kaldes dependencies. 

Eksempel på en simpel package.json fil:
```json
{
  "name": "nodetest",
  "version": "1.0.0",
  "dependencies": {
    "express": "^4.16.4",
    "lodash": "^4.17.11"
  }
}
```
I ovenstående eksempel kan du se nogle af de forskellige options der er i en package.json fil. Name skal være unik for den pågældende pakke hvis du vil tilføje pakken til den globale manager. 

Versionsnummeret er et sematisk nummer hvilket du kan læse om i næste kapitel.

Dependencies er en liste over de pakker som din løsning er afhængig af. Og det er her at npm bliver virkeligt effektivt da denne json fil fortæller, hvilke moduler der skal installeres.

Du kan teste dette ved at installere modulerne express og lodash.

Tjek derefter din package.json og nu skulle du gerne kunne se de to moduler under dependencies.

Slet så din node_modules folder.

Og kør følgende kommando fra din CLI (i samme folder som package.json og package-lock.json ligger i)
```
% npm i
```
Nu skulle node_modules folderen gerne være tilbage i mappen med alle de nødvendige moduler. 

Npm bruger altså json filerne til at læse hvilke dependencies der skal installeres til din løsning.

Dette er også grunden til at du ikke behøver at tilføje node_modules mappen til dit git repo. 
___
## Package-lock.json

Filen package-lock.json holder styr på modulernes versioner og hvilke sub moduler de er afhængige af og er dermed en forholdsvis stor fil.

### Dev dependencies

I visse tilfælde kan man installere pakker som kun tjener et formål under udvikling af sitet og dermed ikke skal bruges i produktion.

Dette kan du angive i npm kommandoen når du installerer pakken ved at skrive -D efter npm i kommandoen:

~$ npm i -D nodemon
Nodemon modulet sørger for at opdatere dit script når du gemmer og har derfor ikke nogen anvendelighed når sitet er i produktion.

Nu kan du også se en ny sektion i din package.json fil - nem devDependencies:
```json
{
  "name": "nodetest",
  "version": "1.0.0",
  "dependencies": {
    "express": "^4.16.4",
    "lodash": "^4.17.11"
  },
  "devDependencies": {
    "nodemon": "^1.17.5"
  }
}
```
___
## Opret et nyt projekt

Du kan bruge npm kommandoen til at oprette din package.json med.

Hvis du opretter en ny folder og stiller dig i den med kommandolinien, kan du køre kommandoen npm init:
```
% mkdir my-project
%
% cd my-projekt
%
% npm init
```
Herefter skal du svare på en række spørgsmål om dit modul - du kan bare bruge default svar ved at trykke enter.

Når du har svaret på alle spørgsmål vil din package.json automatisk blive oprettet.
___
### Semantisk versionering (SemVer)
NPM bruger semantisk versionering til deres moduler. Dette kaldes også for SemVer.

Det vil sige at man ud fra et versionsnummer kan læse, hvor store ændringer der er tale om imellem de forskellige versioner.

Vi kan starte med at kigge på versionsnumrene i vores package.json fil:
```json
{
  "name": "nodetest",
  "version": "1.0.0",
  "dependencies": {
    "express": "^4.16.4",
    "lodash": "^4.17.11"
  },
  "devDependencies": {
    "nodemon": "~1.17.5"
  }
}
```
Et versionsnummer er indelt i 3 grupper separeret med punktum og i nogle tilfælde kan nummeret have en ^ (caret / circumfleks) eller en ~ (tilde) foran.

**Forklaring:**

**Major breaking changes**
Det første tal indikerer ændringer som vil betyde at brugere skal tilpasse egen kode for at få det til at virke med den nye modulversion

**Minor backward compatible**
Det andet tal dækker over nye features i modulet - brugeren behøver ikke at ændre noget i forhold til den nye version.

**Patch changes**
Det tredje tal bruges til mindre bug fixes
Hvis der er et tilde (~) foran tallet, betyder det at opdatering kan ramme indenfor den samme minor version. Det vil sige at en version der hedder 1.2.4 kan opdateres til 1.2.x men ikke til 1.3.0.

Hvis der er en caret (^) foran tallet betyder det at en opdatering kan ramme alt indenfor den samme major version. Det vil sige at en version der hedder 1.2.1 kan opdateres til 1.x.x men ikke til 2.0.0.
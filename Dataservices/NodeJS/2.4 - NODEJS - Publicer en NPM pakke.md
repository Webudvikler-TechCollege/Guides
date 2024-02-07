# Publicer en npm pakke
I denne lektion skal du lære at publicere det modul - eller pakke - som du oprettede i foregående afsnit.

**Husk at skifte alle *heka* ud med dine egne initialer!**

Når du har publiceret din pakke kan du - og alle andre node udviklere - altid installere den igen via npm.

Du skal starte med at gå på https://www.npmjs.com og oprette en profil. Du skal have en profil der for at kunne publicere dine egne node moduler.

Det er selvfølgelig vigtigt at du husker dit brugernavn og adgangskode!

Når du har oprettet en profil skal du åbne din CLI og indtaste nedenstående:
```
% npm login
```
Indtast derefter brugernavn, password og email i de respektive felter og tryk enter.

Nu er du logget ind men før du kan publicere din pakke, skal du først lave en package.json fil med oplysninger om din pakke. Derfor skal skifte til din pakke folder (xxx-print) inde i din CLI:
```
% cd ../xxx-print/
```
Herefter skal du køre en npm init:
```
% npm init
```
Nu kommer der en række spørgsmål som du skal svare på: (du kan trykke enter for at vælge forslag i parantesen)

- pakkens navn
- versionsnummer
- description
- entry point
- test command
- git repository
- keywords
- author
- license

Når du er igennem dette er du klar til at publicere din pakke:
```
% npm publish
```
Når du har gjort det, kan du gå på nedenstående adresse og finde din pakke:

https://www.npmjs.com/package/heka-print

Efterfølgende kan du nu gå tilbage til dist folderen i din CLI og installere dit modul der:
```
% cd ../dist/
%
% npm i heka-print
```
Og til sidst skal du åbne filen /dist/index.js og fjerne den relative sti i argumentet på din require metode sådan at det ser ud som nedenstående:
```
const print = require('heka-print')
```
Nu kan du prøve at kalde filen igen med node fra din CLI.

Tillykke med dit nye modul!
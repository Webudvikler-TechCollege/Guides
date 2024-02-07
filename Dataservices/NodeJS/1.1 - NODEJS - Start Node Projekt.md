# Start et Node Project

Følgende guide vil vise hvordan du kan starte et node.js projekt.
___
## 1. Opret en ny folder til dit projekt
Find et passende navn til din folder
___
## 2. Åbn folder i VS Code
Du skal nu åbne den nye folder i VS Code. Sørg for at du kan folderen i terminalen i VS Code.
___
## 3. Initialiser dit Node.js projekt
Nu er du klar til at initialisere dit Node projekt. Det skal vi bruge npm til.

Skriv følgende i din terminal:
```
npm init
```
Du vil nu blive bedt om at udfylde nogle indstillinger i terminalen. Hvis du trykker *Enter* vil terminalen vælge det der er anført i parantesen. 

Herunder finder du en forklaring til spørgsmålene:

- package name: navnet på dit projekt
- version: versionsnummer
- description: beskrivelse af dit projekt
- entry point: den fil der skal kaldes når man åbner dit projekt
- test command: kommando til at teste dit projekt med
- git repository: url til et git repository
- keyword: søgeord til projektet
- author: forffatter(e) til projektet
- license: type af licens

Når du har udfyldt disse vil Node.js bede dig om at bekræfte og derefter vil en package.json fil blive oprettet i roden af din mappe.

Hvis du åbner denne fil kan du se dine indstillinger i JSON format. Du kan altid rette i disse oplysninger efter behov.
___
## 4. Tilføj type til din package.json fil
For at vi kan bruge import/export i vores projekt, er vi nødt til at definere projektet som et modul.

Derfor skal du tilføje nedenstående til din package.json fil:
```js
"type": "module"
```
___
## 5. Opret index.js fil
Opret en index.js fil i roden af din nye mappe.

Prøv derefter at køre følgende kommando:
```
node index.js
```
Der sker ikke rigtig noget - med mindre at du har lavet en fejl.

Det er fordi at vi skal have sat en server op i vores index fil.
___
## 6. Opsæt lokal Node server
Vi skal bruge den indbyggede http modul for at oprette en server. 
```js
import http from 'http';
``` 
Dernæst skal vi bruge metoden `createServer()` som tager to argumenter: 

- *request* er anmodningen vi sender til serveren.
- *response* er svaret vi modtager fra serveren
- *listen* er en callback function med den port som vores server skal lytte på. I dette tilfælge er den sat til port 4000.

```js
http.createServer((request, response) => {
    console.log('Hello world');
}).listen(4000)
```
Prøv nu at køre kommandoen
```js
node index.js
```
Det skulle gerne give dig et output i din terminal.

Prøv at kalde adressen http://localhost:4000/ i din browser. Kan du se at der sker noget?
___
## 7. Installer nodemon
Det kan være ret irriterende at skulle køre kommandoen `node index.js`, for at se ændringer hver gang du har redigeret og gemt en fil.

Her kan du med fordel bruge `nodemon` som er en npm pakke der automatisk opdaterer filer når de bliver gemt.

Nodemon installeres som følgende:
```
npm i -g nodemon
```
Det er en god ide at have denne pakke installeret globalt da det er et nyttigt modul at have i selve udviklingsprocessen. Du kan installere en pakke globalt ved at tilføje `-g` når du skrivee installationskommandoen.

Når nodemon er installeret kan du efterfølgende køre dine js filer med kommandoen nodemon istedet for node:
```
nodemon index.js
```
Nodemon vil overvåge den kørte fil for ændringer og automatisk køre den når du gemmer din fil. 

Derfor skal dette modul kun bruges i udviklingsfasen og ikke i produktion.
___
## 8. Output
Vi mangler stadig at se noget indhold når vi kalder sitet med en browser. 

Til at vise det skal vi bruge respons objektet fra vores server funktion.

Først skal vi definere en indholdsheader, sådan at browseren kan læse vores svar og indholdstype. 

Derefter definerer vi det indhold der skal vises på sitet.

Og til sidst fortæller vi hvor indholdet stopper.

```js
http.createServer((request, response) => {
    response.writeHead(200, {'Content-Type': 'text/html'});
    response.write('Hello World!');
    response.end();
}).listen(4000)
```
Prøv nu at kalde din side med følgende kommando:
```
nodemon index.js
```

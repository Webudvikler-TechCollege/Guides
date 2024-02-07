# Opret din egen NPM pakke
I denne lektion skal du lære at oprette et node modul.

Eksemplet her viser et simpelt modul, som kan udskrive en tekst.

Start med at oprette en ny folder. Du kan f.eks. kalde den myfirstpackage.

Derefter skal du oprette to foldere med hver deres index.js i. Din struktur skal gerne ligne den på billedet herunder:
```
> myfirstpackage
  > dist
    > index.js
  > [dine-initialer]-print
    > index.js
```
Du skal selvfølgelig udskifte [dine-initialer] med dine egne initialer. I denne guide vil jeg bruge mine egne initialer som eksempel.

Eks: 
*heka-print*. 

Dette er også navnet på dit nye modul.

I index filen i dist folderen kan du starte med at lave en require på dit modul i filen. 
```
/dist/index.js:

const print = require('heka_print')

print('My first package...');
```
Gem filen og prøv at køre den med node kommandoen i din CLI. Husk at du skal stå i den nye folder for at køre filen med en relativ sti som vist i nedenstående eksempel.
```
% node index.js
```
Det skulle gerne give en fejl da det modul, du forsøger at inkludere, ikke findes endnu.

Åbn index filen i xxx-print folderen og lav et script der udskriver noget f.eks. en console.log.

heka-print/index.js:
```js
console.log('My first page...');
```
Husk at gemme!

Normalt skal modulpakker jo ligge i forlderen node_modules men da den ikke er tilgængelig endnu, skal du bruge en relativ sti i argumentet i din require funktion inde i /dist/index.js filen. Det kan fikses ved at sætte to prikker og en skråstreg foran modulets navn i require argumentet:

/dist/index.js:
```js
const print = require('../heka_print')

print('My first package...');
```
Hvis du kører filen igen fra din CLI, kan du nu se at den udskriver teksten men den får stadig en fejl på funktionen print. Det er fordi at node forventer at modtage en funktion fra modulet. Derfor skal du over i modul filen igen og indsætte en exports funktion:

/heka-print/index.js:
```js
module.exports = function print(msg) {
    console.log("Testing from function...");
};
```
Nu kan du igen prøve at teste siden med kommandoen node og nu skulle du gerne få teksten fra modul filen. Husk at det er filen /dist/index.js du skal kalde med node i kommandolinen.

I næste afsnit kan du se hvordan du publicerer dit eget modul.
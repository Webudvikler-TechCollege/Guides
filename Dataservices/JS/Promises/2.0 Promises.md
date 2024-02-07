# Javascript Promises - Forklaring

Promises anvendes i forbindelse med asynkron programmering.

Et promise er et løfte om at der kommer et svar retur uanset om  svaret er sandt eller falsk.

Hvis vi for eksempel sender en forespørgsel til en server som et promise, ved vi ikke altid hvor lang tid serveren skal bruge på at behandle vores forespørgsel, men promise teknologien garanterer at vi får en respons og gør, at vi kan få vores kode til at vente på denne respons.

Eksempel på et simpelt Promise objekt:
```js
let myPromise = new Promise(function(resolve, reject) {
  // executor (code der skal eksekveres)
});
```
___
## Resolve / Reject

Når vi sender en forespørgsel som et promise kan den enten blive opfyldt (*resolved*) eller afvist (*rejected*). Disse argumenter kaldes *callbacks* og er funktioner 

Styrken i promises ligger så i, at vi kan sende et promise, vente på en repons og så sende det næste promise afhængig af hvilken respons vi får tilbage.
```js
let promise = new Promise((resolve, reject) => {
  // Efter 1 sekund meldes der at jobbet er udført
  setTimeout(() => resolve("done"), 1000);
});
```
I ovenstående eksempel eksekveres vores promise funktion med funktionerne *resolve* og *reject* som argumenter. 

Efter 1 sekund kaldes resolve funktionen og tilstanden på vores promise objekt ændres fra *pending* til *fullfilled*.

Det samme eksempel kan laves med en *rejection*:
```js
let promise = new Promise(function(resolve, reject) {
  // Efter 1 sekund meldes der at jobbet er afsluttet med en fejl
  setTimeout(() => reject(new Error("Noget gik galt")), 1000);
});
```
I ovenstående eksempel tilstanden på vores promise objekt ændret til *rejected*.

Eksekveringen af et promise kan kun kalde een af de to funktioner *resolve* og *reject*.

Alle andre kald til disse vil blive ignoreret.
```js
let promise = new Promise(function(resolve, reject) {
  resolve("done");

  reject(new Error("…")); // ignoreret
  setTimeout(() => resolve("…")); // ignoreret
});
```
___
## Promise sammenkædning med then, catch og finally

Et promise objekt fungerer som et link mellem den "producerende kode" og de forbrugende funktioner, som vil modtage et resultat eller en fejl. Disse funktioner kan registreres ved hjælp af metoderne .then, .catch og .finally.

### then
Den vigtigste metode er `.then`.

Syntaks eksempel:
```js
promise.then(
  function(result) { /* håndtere et vellykket resultat */ },
  function(error) { /* håndtere en fejl */ }
);
```
Det første argument for `.then` er en funktion, der kører, når vores promise er opfyldt, og modtager resultatet.

Det andet argument for `.then` er en funktion, der kører, når vores promise afvises, og modtager fejlen.

For eksempel, her er en reaktion på et vellykket løst løfte:
```js
let promise = new Promise(function(resolve, reject) {
  setTimeout(() => resolve("Done!"), 1000);
});

// resolve kører den første funktion i .then
promise.then(
  result => alert(result), // viser "færdig!" efter 1 sekund
  error => alert(error) // kører ikke
);
```
Den første funktion blev udført.

Og i tilfælde af et afslag, den anden:
```js
let promise = new Promise(function(resolve, reject) {
  setTimeout(() => reject(new Error("Ups!")), 1000);
});

// reject kører den anden funktion i .then
promise.then(
  result => alert(result), // kører ikke
  error => alert(error) // viser "Fejl: Ups!" efter 1 sekund
);
```
Hvis vi kun er interesseret i vellykkede fuldførelser, kan vi kun give ét funktionsargument til .then:
```js
let promise = new Promise(resolve => {
  setTimeout(() => resolve("Done!"), 1000);
});

promise.then(alert); // viser "færdig!" efter 1 sekund
```
___
### .catch
Hvis vi kun er interesseret i fejl, kan vi bruge null som det første argument: .then(null, errorHandlingFunction). Eller vi kan bruge .catch(errorHandlingFunction), som er nøjagtig det samme:
```js
let promise = new Promise((resolve, reject) => {
  setTimeout(() => reject(new Error("Ups!")), 1000);
});

// .catch(f) er det samme som promise.then(null, f)
promise.catch(alert); // viser "Fejl: Hov!" efter 1 sekund
```
Kaldet .catch(f) svarer altså til at vi kører en .then(null, f).
___
## Læs mere om promises
- [MDN: Using promises &raquo;](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
- [Javascript Info: Promise Basics &raquo;](https://javascript.info/promise-basics)
___
## Se video om promises
- [WebDev: JavaScript Promises In 10 Minutes &raquo;](https://www.youtube.com/watch?v=DHvZLI7Db8E)





# Javascript Promises - Asynkrone funktioner

Ved at bruge metoderne `async` og `await`, kan vi benytte os af asynkrone funktioner og dermed  undgå den lidt komplekse chaining ballade med `.then()` og `.catch()`.

Disse metoder er måske lidt nemmere at forstå og dermed også at bruge.
___
## Async
Keywordet `async` placeres foran en funktion som i eksemplet herunder:
```js
async function f() {
   retur 1;
}
```
Når vi sætter `async` foran en funktion betyder det at funktionen skal returnere et promise.

For eksempel returnerer denne funktion et opfyldt promise med resultatet 1:
```js
async function f() {
   retur 1;
}

f().then(alert); // 1
```
Vi kunne også returnere et promise, som ville give samme resultat:
```js
async function f() {
   return Promise.resolve(1);
}
f().then(alert); // 1
```
Så async sikrer altså, at vores funktion returnerer et promise. Der findes et andet keyword som kun virker i async-funktioner, og som er ganske effektivt når vi arbejder med asynkrone kald.
___
## Await
```js
// virker kun i async-funktioner
let value = await promise;
```
Nøgleordet await får JavaScript til at vente, indtil et promise bliver løst og returnerer resultatet.

Følgende er et eksempel med et promise, der løser sig på 1 sekund:
```js
async function f() {

  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("Done!"), 1000)
  });

  let result = await promise; // vent indtil løftet løser sig (*)

  alert(result); // "Færdig!"
}

// Kalder funktion
f();
```
I eksemplet "pauser" funktionskaldet ved linjen med `await` keywordet og genoptages først, når vores promise er afviklet og har returneret et resultat. 

Dermed suspenderer `await` funktionens handling, indtil et promise er afviklet, og genoptager det derefter med resultatet af det promise. Det koster ingen CPU-ressourcer, fordi JavaScript-motoren kan udføre andre opgaver i mellemtiden som at udføre andre scripts, håndtere begivenheder osv.

Denne måde er bare en mere elegant syntaks end `.then` og `.catch` metoden. Og så er det nemmere at læse og skrive.

### Await kan ikke anvendes i almindelige funktioner

Hvis vi forsøger at bruge await i en ikke-asynkron funktion, vil vi få en syntaksfejl:
```js
function f() {
  let promise = Promise.resolve(1);
  let result = await promise; // Syntax error
}
```
Vi får denne fejl, hvis vi glemmer at sætte `async` før en funktion. 

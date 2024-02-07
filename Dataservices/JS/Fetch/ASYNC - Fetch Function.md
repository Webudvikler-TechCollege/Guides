# Fetch som asynkron function

Hvis du vil undgå alt for meget then/catch chaining, kan du med fordel lave en custom function og benytte dig af en anden promise-based teknologi - nemlig *async/await*.

Med *async/await* kan du definere en asynkron function og derefter lave ventende kald i denne funktions scope.

Det betyder at du kan returnere svar direkte til funktionskaldet og så slippe du for at skulle behandle data inde i kodekæden af then og catch statements.

**Eksempel: function definition**
```js
// Definerer funktionen som asynkron med keywordet async
// og to parametre - url og options
async function myFetchFunction(url, options = null) {
    // Deklarerer respons variabel
    let response;

    // Hvis options er false...
    if(!options) {
        // Kalder fetch med url - venter på svar
        response = await fetch(url);
    } else {
        // Kalder fetch med url og options - venter på svar
        response = await fetch(url, options);
    }
    // Kalder json parser: vores kode venter på respons inden den går videre 
    let data = await response.json();
    // returnerer data
    return data;
}
```
Ovenstående funktion vil returnere respons objektet direkte ved et kald af funktionen.

**NB!** Funktionen skal være defineret som asynkron før at du kan anvende await keywordet i scopet.
___
**Eksempel 1: Named function**
```js
// Classic Function definition
async function getData() {
    const data = await myFetchData('https://url.to.my.endpoint.com');

    console.log(data);
}

// Function call
getData();
```
___
**Eksempel 2: Arrow function som en konstant**
```js
// Function variable definition
const getData = async () => {
    const data = await myFetchData('https://url.to.my.endpoint.com');

    console.log(data);
}

// Function call
getData();
```
___
**Eksempel 3: Anonym arrow function**
```js
(async () => {
    const data = await myFetchData('https://url.to.my.endpoint.com');

    console.log(data);
})();
```
___
De tre ovenstående eksempler har forskellig syntaks men returnerer det samme output.
# Javascript Fetch - en næsten simpel forklaring

Denne guide er en simpel guide til Javascripts globale Fetch API. 

*Fetch* blev tilføjet til javascript med ES6 opdateringen.

*Fetch* gør det muligt at hente og administrere dataressourcer fra en lokal eller remote fil via HTTP requests. 

*Fetch* er *promise-based*. Det betyder at metoden returnerer et *promise*, som bliver opfyldt når svaret er tilgængeligt - eller afvist, hvis svaret er falsk. Metoden *lover* altså at returnere et svar uanset om det er sandt eller falsk. Deraf betegnelsen *promise*.

Promise teknologien betyder at vi kan forlange en respons inden anden kode læses ind. 

Vi kan anvende *then/catch* til at styre dette med.

Syntaks:
```js
const fetchResource = fetch(resource [, init])
```
**Forklaring:**
- *resource* [string] URL til resource
- *init* [object] Valgfrit. Et objekt, der indeholder eventuelle brugerdefinerede indstillinger, som du vil anvende på dit request. Hvis denne ikke er sat vil dit request blive et HTTP GET request.

**Eksempel:**
```js
const url = './data.json';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(err => console.error(err))
```
Herunder ses samme kode men med forklarende kommentarer:
```js
// Foretag kald via http
fetch(url)
    // Vent på at svar parses som json
    .then(response => response.json())
    // Vent på at data logges i konsollen
    .then(data => console.log(data))
    // Vis fejl hvis der er en
    .catch(err => console.error(err))
```
Anvendelsesformen med *then/catch* kaldes også for chaining fordi vi skriver koden i en form for *kæde*.

Fordelen ved at fetch er promise based ligger i, at vi kan lave små "ventepladser" i vores kode og dermed sikre at vi får en respons inden vi går videre til næste statement.
___
### Behandling af respons data

Typisk har vi brug for at behandle de data vi får retur fra vores fetch kald. 

Her er det vigtigt at vi kender datatypen da vi enten vil kalde en egenskab eller loope et array. Det er eksempelvis ikke muligt at loope et objekt.

Hvis vi nu forestiller os at vores respons er et json objekt, som indeholder egenskaben *users* med et array af brugere som værdi. 

Behandlingen skal foregå inde i *then* kæden:
```js
// Foretag kald via http
fetch(url)
    // Vent på at svar parses som json
    .then(response => response.json())
    // Vent på at data logges i konsollen
    .then(data => {
        // Logger array users
        console.log(data.users)

        // Looper array users
        (data.users && data.users.map(item, key) => {
            console.log(`${key} ${item}`);
        }))
    })
    // Vis fejl hvis der er en
    .catch(err => console.error(err))
```
___
## Læs mere om fetch
- [Nem Fetch Turorial &raquo;](https://www.digitalocean.com/community/tutorials/how-to-use-the-javascript-fetch-api-to-get-data)








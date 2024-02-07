# Javascript Fetch med option objekt

Fetch metoden tager to argumenter, hvor det første argument er den url som skal fetches. Dette argument er obligatorisk.

Metodens andet argument er valgfrit og kan tage et request objekt med forskellige oplysninger om din forespørgsel. Hvis det ikke er angivet, vil kaldet som standard være et HTTP GET request - altså et kald der forsøger at hente data fra den pågældende url.

Følgende er et eksempel der viser et POST kald med fetch metoden:

```js
// URL til endpoint
const url = 'https://api.mediehuset.net/comments';

// Option objekt med metode og form body
const options = {
    method: 'PUT'
}

// Fetch kald med then/catch og option objekt
fetch(url, options)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(err => console.log(err));
``` 
Via dette objekt kan vi påvirke vores kald med mange forskellige elementer som *request methods*, *postdata*, *authorization headers* m.m.

De mest almindelige er:

- *method*: Request metoden som typisk er en af følgende:
    - GET (hente)
    - POST (oprette)
    - PUT (opdatere)
    - DELETE (slette)  
&nbsp;    
- *headers*: Request headers er en slags metadata med information om dit request. 

- *body*: "Kroppen" til dit request. Her kan du tilføje Form data, URLSearchParams mm. Requests af GET- eller HEAD-metoden har ikke en krop.

Du kan se en liste over de alle forskellige options [her](https://developer.mozilla.org/en-US/docs/Web/API/fetch#syntax)
___
## Fetch kald med POST metode
Nedenstående eksempel tager udgangspunkt i eksemplet med fetch funktionen fra  
[denne guide](https://github.com/Webudvikler-TechCollege/DSI/blob/main/Guides/ASYNC%20-%20Fetch%20Function.md).

Hvis vi kalde en fetch med en POST skal vi indsætte *method* og *body* i vores option objekt. Vi kan med fordel bruge javascripts [formData interface](https://javascript.info/formdata) til at tilføje vores formdata med.
```js
const getData = async () => {
    const formData = new FormData();
    formData.append('username', 'hans');
    formData.append('password', 'hans');

    const options = {
        method: 'POST',
        body: formData
    }

    const data = await myFetchFunction('https://api.mediehuset.net/token', options);
}
```
I ovenstående eksempel hentes der en token fra skolens api med brugernavn og password. Du skal selvfølgelig indsætte dine egne credentials for at det virker.
___
## Lagring af token i sessionStorage
Disse data kan vi smide i vores *sessionStorage*, som er en slags datalager i browseren. Disse data forsvinder når browser vinduet lukkes - eller din token udløber.

I eksemplet herunder kan du se hvordan du gemmer data i sessionStorage med metoden `setItem()`:
```js
...
const data = await myFetchFunction('https://api.mediehuset.net/token', options);

sessionStorage.setItem('token', JSON.Stringify(data));
```
Da vi ikke kan gemme et json objekt er vi nødt til at konvertere det til en string med `JSON.Stringify()`.

Nu kan vi altid hente vores token i sessionStorage med metoden `getItem()`. Da det ligger som en JSON string skal vi konvertere den til et objekt og det gør vi med `JSON.Parse()`:
```js
const token = JSON.Parse(sessionStorage.getItem('token'));

if(token.access_token) {
    console.log(`Du er logget ind som ${token.username}`);
}
```
___
## Fetch kald med authorization headers
Hvis vi skal kalde et endpoint som kræver en token skal vi benytte *authorization headers*:

```js
const getProctectedData = async () => {
    const token = JSON.parse(sessionStorage.getItem('token'));

    const options = {
        method: 'GET',
        headers: {
            'Authorization' : `Bearer ${token.access_token}`
        }
    }

    const data = await myFetchFunction('https://api.mediehuset.net/protecteddata', options);
}


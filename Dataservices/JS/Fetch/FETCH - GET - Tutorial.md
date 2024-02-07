# Sådan bruger du JavaScript Fetch API til at hente data

## Introduktion

Fetch API er en ny standard til at lave serverforespørgsler med *promises*, men som også indeholder mange andre funktioner.

I denne øvelse skal du oprette både GET- og POST-anmodninger ved hjælp af Fetch API.
___
### Trin 1 — Fetch Syntax
For at bruge Fetch API'en skal du bruge fetch metoden, som accepterer en URL til dit endpoint som parameter:
```js
fetch(url)
```
 
Efter `fetch()` metoden skal du tilføje promise metoden *`then()`*:
```js
.then(() => {

})
``` 
Metoden `fetch()` returnerer et promise. Hvis dette promise er resolved, udføres funktionen i `then()` metoden. Denne funktion indeholder koden til håndtering af data modtaget fra API'et.

Under then()-metoden skal du inkludere `catch()` metoden:
```js
.catch(() => {

});
```
Det API, du kalder ved hjælp af `fetch()` kan være nede, eller der kan opstå andre fejl. Hvis dette sker, vil dit kald blive afvist (reject). Catch metoden bruges til at håndtere disse afvisninger. Koden i `catch()` vil blive udført, hvis der opstår en fejl, når du kalder API'et.

Lad os lige opsummere:
```js
fetch(url)
.then(() => {

})
.catch(() => {

});
```
Med denne syntaks kan du nu gå videre til at bruge `fetch()` på et API.
___
### Trin 2 — Hent data fra en API med fetch
Følgende eksempler er baseret på Random User API. Her vil du hente en liste af tilfældige brugere som du så kan præsentere i en html liste ved hjælp af Vanilla JavaScript.

Start med at oprette en HTML-fil og tilføj en overskrift og en uordnet liste med et unikt id:
```html
<h1>Forfattere</h1>
<ul id="authors"></ul>
```
Indsæt et script-tag med en defer attribut i ​​din HTML-fils &lt;head&gt; tag, og lav en DOM-selecter til at fange dit &lt;ul&gt; tag. Brug `getElementById()` med *authors* som argument:
```html
<script>
    const ul = document.getElementById('authors');

</script>
```
Opret en konstant variabel med navn url, og angiv dennes værdi til den url i API'et, der returnerer ti tilfældige brugere:
```js
const url = 'https://randomuser.me/api/?results=10';
```
(Du kan ændre antallet af brugere i URL'en)

Hvis du sætter denne url ind som parameter på `fetch()` metoden er du klar til at kalde Random User API:
```js
fetch(url)
    .then(data => {

    })
    .catch(err => {

    });
```
I koden ovenfor anvendes fetch til at kalde et endpoint (*url*) i Random User API'et. 

Derefter modtages et svar. Svaret er ikke JSON, men et objekt med en række metoder, som kan bruges alt efter hvad du vil med den returnerede information. 

Brug metoden `json()` for at konvertere det returnerede objekt til JSON.

Tilføj `then()` metoden, som indeholder en funktion med et parameter kaldet *response*.

Dette parameter tager værdien af ​​objektet, der returneres fra vores `fetch(url)`. Brug `json()` metoden til at konvertere response paramteret til JSON-data:

```js
fetch(url)
.then(response => repsonse.json())
``` 
Vi mangler stadig at behandle JSON-data så du skal tilføje endnu en `then()` sætning med en funktion, der har argumentet data:
```js
.then(data => {

})
```
I dette funktions-scope skal du nu oprette en variablen *authors*, og pege den på værdien af *data.results*:
```js
.then(date => {
    let authors = data.results;
```
Da vi skal oprette et &lt;li&gt; element for hver forfatter med billede og navn, skal vi loope arrayet af brugere. Her kan vi med fordel benytte os af javascripts `Map()` metode:
```js
.then(data => {
    let authors = data.results;

    return authors.map(author => {

    })
})
```
For hvert index der passeres i vores array, vil Map metoden tildele det pågældende index's værdi til variblen *author*.

I map scopet kan du nu oprette dit li element med funktionen `createElement()`:
```js
...
return authors.map(function(author) {
    let li = document.createElement('li');
})
...
```
Gentag dette for at oprette et span-element og et img-element:
```js
...
let li = document.createElement('li');
let img = document.createElement('img');
let span = document.createElement('span');
...
```
I det retur data du får fra API'et, kan du finde et navn og et billede til hver enkelte bruger. Indstil kilden til forfatter billedet:
```js
...
let img = document.createElement('img');
img.src = author.billede.medium;
...
``` 
Span-elementet skal indeholde forfatterens for- og efternavn, som du kan indsætter med egenskaben innerHTML og en *template string*:
```js
...
img.src = author.billede.medium;
span.innerHTML = `${author.name.first} ${author.name.last}`;
```
Nu skal du tilføje alle elementer til din dom:
```js
append(li, img);
append(li, span);
append(ul, li);
```
Nu mangler du bare at tilføje `catch()` funktionen. Hvis der opstår fejl i kaldet - hvis API'et for eksempel er nede - vil denne funktion vil fange disse fejl:
```js
...
.catch(err => {
  console.error(err);
});
...
```
 Herunder finder du denfulde kode for det kode, du lige har oprettet:
```js
const ul = document.getElementById('authors');
const url = 'https://randomuser.me/api/?results=10';

fetch(url)
.then(resp => resp.json())
.then(data => {
  let authors = data.results;
  return authors.map(author => {
    let li = document.createElement('li');
    let img = document.createElement('img');
    let span = document.createElement('span');
    img.src = author.image.medium;
    span.innerHTML = `${author.name.first} ${author.name.last}`;
    li.appendChild(img);
    li.appendChild(span);
    ul.appendChild(li);
  })
})
.catch(err => {
  console.log(err);
});
´´´
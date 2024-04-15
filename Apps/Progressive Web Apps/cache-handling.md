# Håndtering af cache

Caching af filer er en vigtig funktion i Progressive Web Apps (PWA), da det giver mulighed for at arbejde offline og en hurtigere indlæsning. Du kan kontrollere din Service Worker og javascripts indbyggede Cache API. Herunder kan du se hvordan du kan bruge Cache API til at implementere caching i din PWA.
___
## Opret en ny cache:
```js
caches.open('my-cache').then(function(cache) {
  // Cache er åben
});
```
___
## Tilføj filer til cachen:

Når du har oprettet cachen, kan du tilføje filer til den ved hjælp af metoderne `cache.add()` eller `cache.addAll()`:
```javascript
// Array med filer
const assets = [
  '/path/to/my/file1.jpg', 
  '/path/to/my/file2.jpg'
]

caches.open('my-cache').then(cache => {
  // Tilføj enkelt fil
  cache.add('/path/to/my/file.jpg');
  // Tilføj flere filer
  cache.addAll(assets); 
});
```
___
## Hent filer fra cachen:

Du kan hente filer fra cachen ved at bruge `cache.match()` metoden:
```js
caches.match('/path/to/my/file.jpg').then(response => {
  if (response) {
    // Fil findes i cache - brug den
  } else {
    // Fil findes ikke i cache - hent den
  }
});
```
___
## Opdater filer i cachen:**

Du kan opdatere filer i cachen ved at tilføje dem igen ved hjælp af `cache.put()` metoden:
```js
caches.open('my-cache').then(cache => {
  cache.put('/path/to/my/file.jpg', new Response('new content'));
});
```
___
## Slet filer fra cachen:**

Du kan slette filer fra cachen ved at bruge `cache.delete()` metoden:

```js
caches.open('my-cache').then(cache => {
  cache.delete('/path/to/my/file.jpg');
});
```
___
## Håndter cache-fejl:

Når du arbejder med cache, er det vigtigt at håndtere fejl korrekt. Du kan bruge `catch()` metoden til at håndtere fejl:
```js
caches.open('my-cache').then(cache => {
  cache.add('/path/to/my/file.jpg').catch(error => {
    // Fejl håndtering
  });
});
```
___
## Cache og asynkrone handlinger

Når en Service Worker aktiveres, kan den udføre en række opgaver, såsom at åbne en cache, hente og lagre filer, opdatere cachen osv. Hvis en Service Worker er færdig med at udføre disse opgaver, kan den blive deaktiveret af browseren for at spare på ressourcerne.

Hvis der er behov for at udføre yderligere opgaver, efter at Service Worker er blevet aktiveret, kan `waitUntil` metoden bruges til at vente på, at disse opgaver er færdige, før Service Worker kan deaktiveres.

Et eksempel på brugen af waitUntil kan være at vente på, at en cache er åbnet og alle relevante filer er lagret i cachen, før Service Worker kan deaktiveres. Dette kan sikre, at alle filer er tilgængelige i cachen, og at brugerne ikke vil opleve nogen fejl, når de forsøger at få adgang til applikationen offline.

En typisk implementering af `waitUntil` kan se sådan ud:
```js
self.addEventListener('activate', function(event) {
  event.waitUntil(
    caches.open('my-cache').then(function(cache) {
      return cache.addAll([
        '/index.html',
        '/styles.css',
        '/app.js'
      ]);
    })
  );
});
```
Husk, caching er kun en del af opbygningen af en PWA. Du skal også implementere Service Workers og andre funktioner for at sikre, at din app fungerer offline og er pålidelig.

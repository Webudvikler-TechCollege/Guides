# Begrænsning af cache
For at undgå overload af filer i vores browsercache kan det være en god ide at rydde op og slette tidligere cachede filer - især når det kommer til den dynamiske cacher som jo lagrer alle de sider som brugeren besøger. 

Vi kan derfor med fordel lave en lille funktion i vores serviceworker, som kan hente filerne i en given cache og slette de ældste indtil at antallet af filer er den ønskede størrelse.

Her kan vi igen bruge `cache.keys()` metoden men læg mærke til at vi denne gang bruger den inde i en given cache.

Eksemplet herunder er forklaret med kommentarer:
```js
// Funktion til styring af antal filer i en given cache
const limitCacheSize = (cacheName, numberOfAllowedFiles) => {
	// Åbn den angivede cache
	caches.open(cacheName).then(cache => {
		// Hent array af cache keys 
		cache.keys().then(keys => {
			// Hvis mængden af filer overstiger det tilladte
			if(keys.length > numberOfAllowedFiles) {
				// Slet første index (ældste fil) og kør funktion igen indtil antal er nået
				cache.delete(keys[0]).then(limitCacheSize(cacheName, numberOfAllowedFiles))
			}
		})
	})
}
```
Når funktionen er oprettet skal den kaldes i serviceworkerens `fetch` event.

Det er en god ide at køre den efter at vi har tilføjet filer til den dynamiske cache:
```js
/* Fetch event */

// Kalder limit cache funktionen
limitCacheSize(dynamicCacheName, 2)
```





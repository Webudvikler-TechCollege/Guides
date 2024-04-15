# Versionering af Cache 
Du kan bruge cachens navn til at versionere dine caches med:

```js
const staticCacheName = 'site-static-v2'
```
Når man bruger denne metode er det en god ide at rydde op i tidligere versioner i cachen. Det kan gøres under *activate* eventet med følgende kode:
```js
// Activate Service Worker
self.addEventListener('activate', event => {

	event.waitUntil(
		// Rydder op i cache og sletter alle uaktuelle caches
		caches.keys().then(keys => {
			// Returnerer et array af promises
			return Promise.all(keys
				// Filterer alle keys som ikke er en del af den aktuelle cache
				.filter(key => key !== staticCacheName)
				// Sletter cache version asynkront
				.map(key => caches.delete(key)))
		})
	)
})
```
# Cache Håndtering - Avanceret
Følgende guide viser tips og tricks til en mere avanceret håndtering af din cache.
___
## Cache versionering
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
___
## Dynamisk cache
Den statiske cache består typisk af alle vores assets og sitets forside. Men det ville være for omstændigt at cache alle sider i vores app under den statiske cache. 

Her kan vi i stedet bruge en dynamisk cache, som kun lagrer sider når vi besøger dem. 

Denne cache kan vi lagre under et andet navn:
```js
const dynamicCacheName = 'site-dynamic-v1'
```
Da dynamiske cache skal lagres i takt med at vi klikker rundt i vores app, skal dette forgå under vores fetch event.

Nedenstående kode viser hvordan dette kan foregå.
```js
// Fetch event
self.addEventListener('fetch', event => {
	// Kontroller svar på request
	event.respondWith(
		// Kig efter file match i cache 
		caches.match(event.request).then(cacheRes => {
			// Returner match fra cache - ellers hent fil på server
			return cacheRes || fetch(event.request).then(fetchRes => {
				// Tilføjer nye sider til cachen
				return caches.open(dynamicCacheName).then(cache => {
					// Bruger put til at tilføje sider til vores cache
					// Læg mærke til metoden clone
					cache.put(event.request.url, fetchRes.clone())
					// Returnerer fetch request
					return fetchRes
				})
			})
		})
	)
})
```
Husk at du altid kan tjekke din cache under *Application* i browserens udviklingsværktøj ved at klikke på *Cache Storage* i menuen til venstre.

Du kan også køre sitet offline ved at sætte kryds i feltet *Offline* under *Service Workers* i menuen til venstre. Dette kan du i øvrigt også styre fra fanen Network.



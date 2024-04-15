# Fallback page

Fallback-sider (eller "backup-sider") refererer til en alternativ side, som vises til brugere, når den side, de prøver at få adgang til, ikke kan vises af en eller anden grund. Den kan sammenlignes med en 404 side.

I PWA sammenhæng er Fallback-sider typisk oprettet for at forhindre, at brugere får en fejlmeddelelse eller en tom side, når vores app er offline.

## Opsætning af en fallback side

Opret en *fallback.html* side i mappen pages (eller der hvor dine sider ligger) - den skal have samme design som resten af din app shell. 

Sæt eventuelt noget tekst ind, der fortæller brugerene at de ikke kan hente den side de forsøger at kalde. 

Da siden jo typisk skal hentes i offline tilstand skal du sørge for at skrive din fallback side til din statiske cache, sådan at den er tilgængelig i offline tilstand.

Derefter skal du fortælle din serviceworker, at den skal bruge fallback siden i tilfælde af at den får fejl ved en fetch request. Dette skal gøres under *fetch* eventet:

```js
// Fetch event
self.addEventListener('fetch', event => {

	// Kontroller svar på request
	event.respondWith(
		
		// Kig efter file match i cache 
		caches.match(event.request).then(cacheRes => {
			// Returner match fra cache / hent fil på server
			// ...
		}).catch(() => {
			// Hvis ovenstående giver fejl kaldes fallback siden			
			return caches.match('/pages/fallback.html')
		})
	)
})
```
Ovenstående vil kigge efter file requests i vores cache eller på serveren. Hvis det returnerer en catch error vil denne hente vores fallback side fra cachen.
___
## Betinget fallback side
Det er en god ide at indsætte en betingelse da vi jo kun skal returnere fallback siden ved efterspørgsler på .html sider.

Ellers vil fallback siden jo også blive returneret ved kald på andre filtyper som eksempelvis billeder, css og js filer.

Dette kan vi gøre ved at kigge efter strengen `.html` i den fil der efterspørges.

**Eksempel:**
```js
// ...
.catch(() => {
	if(event.request.url.indexOf('.html') > -1) {
		return caches.match('/pages/fallback.html')
	}
})
```
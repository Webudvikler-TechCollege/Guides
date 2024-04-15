# Introduktion til Service Worker
En serviceworker er en speciel javascript fil og hele grundstenen i en progressiv web app. 

Serviceworkeren placeres typisk i en *sw.js* fil på roden af dit website. Den dækker kun over det filscope som den er placeret i og derfor er det mest almindeligt at den placeres i rodbiblioteket.

Serviceworkeren er en slags mellemled mellem vores server og browser og kører asynkront i baggrunden.  Derfor opfører den sig ikke som de javascript filer vi normalt arbejder med - eksempelvis har en serviceworker ikke adgang til DOM.

Vi bruger serviceworker til at:

* hente indhold offline
* synkronosere din app i baggrunden
* lytte på fetch requests og push notifikationer
___
## Service Worker Livscyklus
En serviceworker har et særligt livscyklus og dette cyklus er essentielt for, hvordan serviceworkeren fungerer.

Herunder finder du en oversigt over dette cyklus:
___
**1. Registrering**

En serviceworker skal registreres i browseren og dette foregår fra en anden javascript fil. De fleste browsere er kompatible med serviceworker men det er en god ide at tjekke.

**Eksempel: (Fil: /js/app.js)**
```javascript
if('serviceWorker' in navigator) {
	navigator.serviceWorker.register('./sw.js')
	.then(reg => console.log('service worker registered', reg))
	.catch(err => console.error('service worker not registered', err)) 
}
```
____
**2. Installation**

Derefter skal serviceworkeren installeres i browseren. Her har vi mulighed for at lytte på install eventet og køre forskellige handlinger i forbindelse med installationen. F.eks. kan vi lagre nødvendige filer i browserens cache til offline brug. 

**Eksempel: (Fil: sw.js)**
```javascript
// Install Service Worker
self.addEventListener('install', event => {
	console.log('Service Worker has been installed');
})
```
____
**3. Aktivering**

Når serviceworkeren er installeret skal den aktiveres. Her har vi også mulighed for at lytte på activate eventet og køre forskellige handlinger samtidigt.

**Eksempel: (Fil: sw.js)**
```javascript
// Install Service Worker
self.addEventListener('activate', event => {
	console.log('Service Worker has been activated');
})
```
____
**4. Fetch**

Når serviceworkeren er aktiveret har vi mulighed for at lytte på alle de forskellige fetch requests der bliver sendt fra sitet. Der med kan vi bruge serviceworkeren som en slags proxy server, hvor vi kan påvirke de svar der kommer fra serveren, inden de rammer browseren.

**Eksempel: (Fil: sw.js)**
```javascript
// Fetch event
self.addEventListener('fetch', event => {
	console.log('Fetch event', event)
})
```

___
## Registrering af ny eller opdateret serviceworker

Det kan blive lidt tricky hvis vi ændrer i en eksisterende eller opretter en ny serviceworker.

En serviceworker bliver kun registreret og installeret een gang, hvis der ikke ændres i sw.js filen.

Hvis der er ændringer i sw.js filen, registreres og installeres den nye serviceworker i baggrunden, men den eksisterende (gamle) serviceworker udfører sit normale arbejde. Det betyder at den nye serviceworker bliver sat i en venteposition og først aktiveres når browservinduet opdateres eller lukkes.

Dette er for at sikre at vores App kører hvis der skulle gå noget galt under installationen af den nye serviceworker.

Man kan dog sætte en indstilling i browserens udviklingsværktøj, der tvinger installation af nye serviceworkers igennem:

1. Åbn browserens udviklingsværktøj
2. Gå til fanen Application/Applikationer
3. Klik på Serviceworker i menuen til venstre
4. Sæt kryds i feltet med Update on reload









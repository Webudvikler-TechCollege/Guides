# Web App Manifest
Et webapp manifest er en JSON-tekstfil, der indeholder oplysninger om en webapplikation, som browseren skal bruge for at installere en progressiv webapp (PWA) på en enhed, eksempelvis appens navn og ikon.

Manifestet indeholder et enkelt JSON-objekt, med key/value pairs som definerer applikationens oplysninger. Disse egenskaber kaldes for members. 

**Eksempel på et Web App Manifest:**
```json
{
	"name": "PWA CookBook",
	"short_name": "PWACookBook",
	"start_url": "./index.html",
	"id": "./index.html",
	"display": "standalone",
	"background_color": "#ffffff",
	"theme_color": "#ffffff",
	"orientation": "portrait-primary"
  }
```
Du kan læse mere om de forskellige manifest members på følgende link:
* [The Web App Manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest)

Manifestet ligger typisk i en *manifest.json* fil på roden af websitet.

Efterfølgende skal du lave en meta reference til dit manifest i dit html head tag:
```html
<link rel="manifest" href="./manifest.json">
```
Herunder finder du et link til en guide til manifest members og meta tags, som kan bruges når du udvikler progressive web apps:
* [Awesome fifs til meta og manifest](https://github.com/gokulkrishh/awesome-meta-and-manifest)
___
## Test dit manifest
Du kan efterfølgende teste dit manifest i din browsers udviklingsværktøj.

1. Åbn din browsers udviklingsværktøj
2. Gå til fanen Application/Applikationer
3. Klik på Manifest i menuen til venstre

Her kan du se om dit manifest er sat rigtigt op eller om det har nogle mangler.
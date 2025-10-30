# 📊 Guide: Opsætning af Google Analytics (GA4) i et Vanilla JavaScript projekt

> Målgruppe: Let øvede (18–20 år)  
> Teknologi: Vanilla JS (SPA med hash-router eller lignende)  
> Fokus: Simpelt setup, samtykke, pageviews og events

---

## 0️⃣ Hvad er GA4?

- **GA4** sporer trafik og events på dit site.  
- I EU skal **brugeren acceptere cookies**, før GA må sættes.  
- I en **SPA** (Single Page Application) skal du **selv fyre sidevisninger** ved ruteskift.

---

## 1️⃣ Opret GA4 og find dit Measurement ID

1. Gå til [Google Analytics](https://analytics.google.com).
2. Opret en **GA4 property** → Vælg **Web**.
3. Indtast websitets URL og navn.
4. Kopiér dit **Measurement ID** (fx `G-XXXXXXX`).

👉 Det skal bruges i koden.

---

## 2️⃣ Tilføj gtag – men kun efter samtykke

### HTML

```html
<!doctype html>
<html lang="da">
<head>
  <meta charset="utf-8" />
  <title>Sgt. Prepper</title>
  <script type="module" src="/js/app.js" defer></script>
</head>
<body>
  <!-- simpelt cookie-banner -->
  <div id="cookie-banner" class="banner hidden">
    Vi bruger cookies til statistik. 
    <button id="accept">Accepter</button>
    <button id="decline">Afvis</button>
  </div>

  <main id="app"></main>
</body>
</html>

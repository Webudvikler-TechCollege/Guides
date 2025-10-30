# Publicér et GitHub-projekt på Netlify

Netlify gør det super nemt at få et website eller en webapp online — du behøver ikke en server selv, og det hele sker automatisk hver gang du opdaterer dit projekt på GitHub.

---

## Du skal have
- Et **GitHub-login**
- Et **projekt** der allerede ligger på GitHub  
  (fx et React-projekt eller et almindeligt HTML/CSS/JS-site)
- Et **Netlify-login** → [https://www.netlify.com/](https://www.netlify.com/)  
  _(du kan logge ind med GitHub)_

---

## Trin 1 — Log ind på Netlify
1. Gå til 👉 [https://app.netlify.com](https://app.netlify.com)
2. Tryk **“Log in”**
3. Vælg **“Log in with GitHub”**
4. Giv Netlify adgang til dit GitHub (kun første gang)
5. Gå ind på Netlify i en ny fane hvis du ikke kan se indstillinger.

---

## Trin 2 — Opret et nyt site fra GitHub
1. Klik på **“Add new site” → “Import an existing project”**
2. Vælg **GitHub** som kilde
3. Vælg dit **repository (repo)** fra listen  
   _(Hvis du ikke kan se det, klik “Configure the Netlify app on GitHub” og giv adgang til repoet)_

--
## Trin 3 — Vælg build-indstillinger

### Hvis det er et almindeligt HTML-projekt
- **Build command:** _(lad stå tomt)_
- **Publish directory:** `.` (punktum = projektets rodmappe)

### Hvis det er et React-projekt (eller andet npm-baseret)
- **Build command:** `npm run build`
- **Publish directory:** `dist` eller `build` (afhængigt af dit projekt)

💡 Typisk for `vite`:
```
Build command: npm run build
Publish directory: build
```
## Trin 4 — Tryk “Deploy site”
- Netlify bygger nu dit projekt (kan tage 1–2 minutter første gang)
- Når det er færdigt, får du et link som fx `https://my-cool-project.netlify.app`

**Dit site er nu live!**
---

## Trin 5 — Giv dit site et navn (valgfrit)
1. Klik på **“Site settings” → “Change site name”**
2. Skriv fx `sgt-prepper-demo`
3. Dit link bliver så:  
   `https://sgt-prepper-demo.netlify.app`

---

## Trin 6 — Automatisk opdatering
Hver gang du **pusher ændringer** til GitHub (`git push`),  
bygger Netlify automatisk dit projekt igen og **opdaterer sitet online** 💪

---

## Ekstra tip
- Se tidligere builds under **Deploys** i Netlify.
- Hvis et build fejler, står fejlen tydeligt dér.
- Du kan tilføje et **eget domæne** (fx `mitprojekt.dk`) under **Domain settings**.

---
# NPM - Local & Global

Når du bruger NPM, kan du installere pakker enten lokalt eller globalt. 

Det afhænger typisk af, om du bruger pakken i udviklingsfasen eller produktionsfasen. I udviklingsfasen kan du få brug for pakker som ikke nødvendigvis har en rolle i produktionssitet.

Hvis du tilføjer "-g" flaget efter "npm", betyder det, at den pakke, du installerer, vil være tilgængelig på tværs af dit system og ikke kun i det aktuelle projekt.

Når du installerer en pakke globalt med "npm -g", gemmes den i en bestemt mappe på dit system. Denne mappe indeholder de globale pakker, som du har installeret, og andre programmer eller scripts kan derefter bruge disse pakker fra enhver placering på dit system.

Det er vigtigt at bemærke, at når du bruger "-g" flaget, skal du have passende tilladelser til at installere globale pakker på dit system. På nogle systemer, som f.eks. Linux, kræver det muligvis administratorrettigheder (eller brugen af sudo) for at kunne installere pakker globalt.

Eksempel:
```
npm install -g nodemon
```
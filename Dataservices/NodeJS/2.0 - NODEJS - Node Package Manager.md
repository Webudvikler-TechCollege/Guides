# Npm - Node Package Manager

Npm er en forkortelse for Node Package Manager og er et værktøj der gør det muligt for JavaScript-udviklere at genbruge og dele små pakker af kode med andre. 

Disse pakker kaldes også for moduler.

En npm pakke kan bestå af et ganske simpel kode javascript og det kan være en stor kompleks pakke som indeholder andre npm pakker.

Alle npm pakker er beskrevet og kan hentes fra npmjs.com. Da der ikke kvalitetskontrol bør du være opmærksom på pakkernes status i forhold til anvendelse og ratings.

Pakker kan også installeres direkte fra terminalen i din kode editor:

Eksempel:
```
npm install express
```
___

## Node Modules & Package.json
Når du installerer en npm pakke i dit node projekt, opretter Node.js en mappe ved navn *node_modules* og efterfølgende vil alle npm pakker blive placeret i denne folder.

Desuden opdateres configfilen *package.json* og *package-lock.json* med de installerede moduler og deres versionsnummer.

Disse config filer er vigtige altid at få med når vi vil dele vores kode på eksempelvis Github. De betyder nemlig at vi nemt kan geninstallere lige præcis de nødvendige moduler og deres versioner. Og dermed undgår vi også at skulle dele den til tider meget datatunge folder *node_modules*. 

Så husk altid at tilføje *node_modules* til jeres .gitignore fil.
___
## NPM & CLI
NPM har sin egen kommando som du kan bruge til at installere og opdatere pakker med i kommandolinien i din terminal.

NPM følger automatisk med når du har installeret node.

Du kan tjekke om npm er installeret ved at skrive følgende i kommandolinien:
```
npm
```
Du kan også tjekke versionsnummeret af din npm ved at tilføje -v:
```
npm -v
```
### Opdatering af NPM
NPM bliver hyppigere opdateret end node så det er en god ide at få det gjort en gang i mellem. Det kan du gøre med følgende kommando:
```
npm install -g npm
```
Og ja - npm kan bruges til at opdatere sig selv :)
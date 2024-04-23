# 10 Git-kommandoer, som enhver udvikler bør kende

Git er en vigtig del af det daglige arbejde med programmering (især hvis du arbejder i et team) og er meget brugt i softwareindustrien.

Da der er mange forskellige kommandoer, du kan bruge, tager det tid at mestre Git. Men nogle kommandoer bruges oftere (nogle dagligt). Så i dette indlæg vil vi dele og forklare de 10 mest brugte Git-kommandoer, som enhver udvikler bør kende.

> Note: For at forstå denne artikel skal du kende det grundlæggende i Git.
___
## 1. Git Clone
`Git clone` er en kommando som bruges til at downloade eksisterende kildekode fra et eksisiterende repository. Med andre ord laver Git clone dybest set en identisk kopi af den seneste version af et projekt i et repository og gemmer det på din computer.

**Eksempel:**
```
% git clone <https://name-of-the-repository-link>
```
For at kunne downloade et projekt fra GitHub skal du bruge en url til projektet.
Den url kan du kopiere fra ethvert GitHub repository, ved at klikke på den grønne knap til højre med teksten "Clone or download". Derefter skal du indsætte den i kommandolinjen efter *git clone*.

Dette vil downloade en kopi af projektet til en valgfri mappe på din computer, så du kan begynde at arbejde på projektet  lokalt. 
___
## 2. Git Branch
*Branches* (kan oversættes til filialer på dansk) er meget vigtige i git-verdenen. Ved at bruge branches er flere udviklere i stand til at arbejde parallelt med det samme projekt samtidigt. Vi kan bruge kommandoen `git branch` til at oprette, liste og slette grene.

**Eksempel på oprettelse af en ny filial:**
```
% git branch <branch-name>
```
Denne kommando vil oprette en branch lokalt. For at skubbe den nye branch ind i dit repository skal du bruge følgende kommando:
```
% git push -u <remote> <branch-name>
```
Se liste af branches:
```
% git branch
```
Sletning af en branch:
```
% git branch -d <branch-name>
```
___
## 3. Git Checkout
Dette er også en af de mest brugte *git* kommandoer. For at arbejde i en branch skal du først skifte til den. Vi bruger mest *git checkout* til at skifte fra en branch til en anden. Vi kan også bruge det til at tjekke filer og commits.
```
% git checkout <navn-paa-din-branch>
```
Der er nogle trin, du skal følge for at kunne skifte mellem branches:

Ændringerne i din nuværende branch skal *committes* eller *stashes*, før du skifter til en anden branch.

Den branch, du vil tjekke ud, bør eksistere i dit lokale repository.

**Der er også en genvejskommando, der giver dig mulighed for at oprette og skifte til en branch på samme tid**:
```
% git checkout -b <navn-paa-din-branch>
```
Denne kommando opretter en ny branch i dit lokale repository (-b står for branch) og tjekker branchen ud til ny lige efter den er blevet oprettet.
___
## 4. Git Status
`Git status` kommandoen giver os al den nødvendige information om den aktuelle branch.
```
% git status
```
Vi kan indsamle oplysninger som:

- Om den nuværende branch er opdateret
- Om der er commits, push eller pulls
- Uanset om filer er staged, unstaged eller untracked
- Om der er oprettet, ændret eller slettet filer
___
## 5. Git Add
Når vi opretter, ændrer eller sletter en fil, vil disse ændringer ske i vores lokale repo og vil ikke blive inkluderet i det næste commit (medmindre vi ændrer konfigurationerne).

Vi skal bruge *git add* kommandoen til at registrere ændringerne af en eller flere filer i vores næste commit.

**Sådan tilføjer du en enkelt fil:**
```
% git add <fil>
```
**Sådan tilføjer du alt på én gang:**
```
% git add -A
```
Når du kører en *git status* i din terminal, kan du se en liste over hvilke filer som er staged (tilføjet og markeret med grøn farve) og hvilke filer som er unstaged (ikke tilføjet og markeret med rød farve).

Unstaged filer vil ikke komme med i et commit.

Når du tilføjer en fil med *git add* vil den blive registreret som *staged*, blive markeret med grøn i listen og blive medtaget i næste commit.

> Vigtigt: Git add-kommandoen ændrer ikke dit repository, og ændringerne gemmes ikke, før du kører kommandoen `git commit`.
___
## 6. Git Commit
Dette er måske den mest brugte kommando i Git. Når vi når et bestemt punkt i en udvikling, vil vi gerne gemme vores ændringer (måske efter en specifik opgave eller problem).

Git commit er som at sætte et kontrolpunkt i udviklingsprocessen, som du kan gå tilbage til senere, hvis det er nødvendigt.

Vi skal også skrive en kort besked for at forklare, hvad vi har udviklet eller ændret i kildekoden.

**Eksempel:**
```
% git commit -m "commit message"
```
> Vigtigt: Git commit gemmer kun dine ændringer lokalt.
___
## 7. Git Push
Når du har foretaget dine ændringer, er den næste ting, du vil gøre, at sende dine ændringer til dit remote repository - som er GitHub i langt de fleste tilfælde. *Git push* uploader dine commits til fjernlageret.

**Eksempel:**
```
% git push <remote-url> <branch-name>
```
Men hvis din branch er helt ny, skal du også uploade den med følgende kommando:
```
% git push --set-upstream <remote-url> 
<navn-på-din-branch>
```
- eller med en shorthand:
```
% git push -u origin <navn-på-din-branch>
```
> Vigtigt: Git push uploader kun ændringer, der er committed.
___
## 8. Git Pull
`Git pull` kommandoen bruges til at hente opdateringer fra det eksterne repository. Denne kommando er en kombination af `git fetch` og `git merge`, hvilket betyder, at når vi bruger *git pull*, får den opdateringerne fra dit remote repository (*git fetch*) og anvender straks de seneste ændringer i din lokale repository (*git merge*).

**Eksempel:**
```
git pull <remote-url>
```
> Note: Denne handling kan forårsage konflikter, som du skal løse manuelt.
____
## 9. Git Merge
Når du har er færdig med udviklingen i en branch - lad os kalde den for en udviklingsbranch, og alt fungerer fint, er det sidste trin at *merge* (fusionere) denne branch med den overordnede branch (som typisk hedder  *main*, *dev* eller *master*). Dette gøres med kommandoen *git merge*.

Git merge implementerer din udviklingsbranch og alle dens commits ind i den overordnede masterbranch. Det er vigtigt at huske, at du skal placere dig i masterbranchen (*Eks: main eller master*), som du vil flette sammen med din udviklingsbranch.

Nedenstående eksempel viser en situation hvor du skal flette din udviklingsbranch ind i din masterbranch:

Først skal du skifte til din masterbranch. I dette eksempel hedder den *main* men den kan også hedder *master* eller *dev*:
```
% git checkout main
```
Før du slår de to branches sammen, bør du opdatere din lokale udviklingsbranch:
```
% git fetch
```
Endelig kan du flette din udviklingsbranch sammen med din masterbranch:
```
% git merge <navnet-på-din-branch>
```
> Tip: Sørg for, at din udviklingsbranch har den nyeste version, før du slår dine branches sammen, ellers kan du opleve  konflikter eller andre uønskede problemer.
___
## 10. Git Revert
Nogle gange er vi nødt til at fortryde de ændringer, vi har foretaget. Der er forskellige måder at fortryde vores ændringer lokalt eller eksternt (afhængigt af, hvad vi har brug for), men vi skal bruge kommandoerne med forsigtighed, da vi kan risikere at slette kodeblokke eller hele filer.

En mere sikker måde, hvorpå vi kan fortryde vores commits, er ved at bruge `git revert`. For at se vores commit-historik skal vi først bruge gits log kommando:
```
% git log --oneline
```
Kommandoen vil liste vores commits med en gul hash kode og en commit message.

Vi kan kalde denne hash-kode med en *git revert* kommando for at fortryde tilbage til den pågældende version af vores branch:
```
% git revert 6a443b1
```
Herefter vil du se en besked i din terminal om din handling  - tryk shift + q for at afslutte.

Kommandoen vil fortryde den givne commit, men vil oprette en ny commit uden at slette den gamle.

Fordelen ved at bruge git revert er, at det ikke berører commit-historikken. Det betyder, at du stadig kan se alle commits i din historie, selv de commits der er  tilbageførte.

En anden sikkerhedsforanstaltning her er, at alt sker i vores lokale system, medmindre vi skubber dem til den eksterne repo. Derfor er git revert sikrere at bruge og er den mest foretrukne metode at fortryde vores commits med.
___

### Do you git it?
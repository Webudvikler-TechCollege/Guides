# Git branches

I Git refererer *branches* til separate "grene" af kodebasen, som kan oprettes og arbejdes på uafhængigt af hinanden. Dette giver udviklere mulighed for at arbejde på forskellige dele af koden uden at påvirke hinandens arbejde. 

Når man opretter en ny branch i Git, oprettes en kopi af den aktuelle kodebase i dens nuværende tilstand. Enhver ændring, der foretages på denne branch, vil kun påvirke selvsamme branch og ikke *main branch*  eller andre branches. 

Dette giver mulighed for, at forskellige udviklere kan arbejde på forskellige branches af koden, for derefter at *merge* (sammenflette) disse branches, når arbejdet er færdigt. Når man ønsker at sammenflette branches sammen, kan man bruge Git-kommandoer som *merge* eller *rebase* til at integrere de forskellige ændringer, der er lavet på hver branch. 

Derudover kan man også slette en branch, hvis den ikke længere er nødvendig, eller hvis dens ændringer allerede er blevet integreret i main branch eller en anden branch. 

I alt giver branches i Git fleksibilitet og kontrol over, hvordan udviklingsarbejdet foregår, og hvordan forskellige dele af koden integreres.

### Git CLI Eksempler:

**Opret ny branch:**
```
% git branch <branch-name>
```
**Push branch til repository:**
```
% git push -u <remote> <branch-name>
```
**Se liste af branches:**
```
% git branch
```
**Slet branch:**
```
% git branch -d <branch-name>
```
___
## Primære branches

*Main* er den primære branch (hovedgrenen) i Git-versionstyringssystemet, der indeholder den aktuelle og fungerende kode for et projekt.

> Tidligere blev de primære branches som standard kaldt for *master* men i 2020 besluttede Git-udviklerne at ændre standardnavnet til Main i en indsats for at fjerne et sprog, der kan opfattes som diskriminerende. Derfor vil nye git repositories sandsynligvis bruge *main* som standardnavn for primære branches.

Når en ny funktion eller en opdatering til projektet skal tilføjes, oprettes normalt en separat branch fra *main* branch. Denne branch bruges så til at arbejde på de nye funktioner eller opdateringer, mens *main* branch forbliver uændret og stabil.
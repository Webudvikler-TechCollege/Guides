# Asynkron vs synkron

Når vi begynder at arbejde med javascript og kald af data ressourcer fra et API, kan vi ikke undgå at støde på begreber som synkrone og asynkrone kald. Denne guide vil forsøge at forklare betydningen af og forskellen på disse to begreber.

Man kan lidt sammenligne det med at følge en kage opskrift.

I synkron programmering vil man følge opskriften slavisk punkt for punkt og vi har en nogenlunde ide om, hvordan kagen bliver og hvornår kagen er færdigbagt.

I asynkron programmering vil alle punkter blive sat i gang med det samme og vi ved ikke helt hvad der er færdig først og hvor lang tid processen tager.

Nedenstående billede illustrerer også forskellen.

![Se det her](./images/async_vs_sync.png)
___
## Synkron programmering
Som et ganske logisk udgangspunkt læser javascript et stykke kode oppe fra og ned - fuldstændigt som vi har skrevet det i koden.

Denne indlæsning foregår ekstremt hurtigt.

Eksempel:
```js
let val_1 = 'Værdi 1';
let val_2 = 'Værdi 2';

console.log(val_1);
console.log(val_2);
```
Resultatet her vil give et kronologisk output som hedder sig:
```
> Værdi 1
> Værdi 2
```
___
## Asynkron programmering
Under en indlæsning af kode, kan der være elementer hvor vi endnu ikke kender værdien. Det kan være data fra en ekstern ressource, som vi er afhængige af længere nede i vores kode.

Et kald til en ekstern ressource tager tid og da javascript er lynhurtig vil det betyde, at hele vores kode bliver indlæst uden at få data med fra den eksterne ressource.

Derfor kan det være nødvendigt at indsætte nogle "ventepositioner" i vores kode, hvor vi ber javascript om ikke at gå videre før der er kommet et svar fra disse kald.

I følgende eksempel simulerer vi et asynkront kald med metoden setTimeOut. 

Eksempel:
```js
let val_1 = 'Værdi 1';
let val_2 = 'Værdi 2';

setTimeOut(() => {
    console.log(`Asynkront kald: ${val_1}`);
}, 100)

console.log(val_1);
console.log(val_2);
```
Selv om koden med setTimeOut er placeret før de andre outputs, vil den stadig stå i bunden.
```
> Værdi 1
> Værdi 2
> Asynkront kald: Værdi 1
```
## Videoer


- [Asynchronous Vs Synchronous Programming by WebDev](https://www.youtube.com/watch?v=Kpn2ajSa92c)

- 




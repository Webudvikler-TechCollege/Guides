Hvorfor git?

https://youtu.be/ykZbBD-CmP8

https://youtu.be/Uszj_k0DGsg

For en grundig diskussion om fordele og ulemper ved Git sammenlignet med centraliserede kildekodekontrolsystemer, se internettet. Der foregår masser af flammekrige der. Som udvikler foretrækker jeg Git frem for alle andre værktøjer i dag. Git ændrede virkelig den måde, udviklere tænker på at fusionere og forgrene. Fra den klassiske CVS/Subversion-verden, jeg kom fra, har sammensmeltning/forgrening altid været betragtet som lidt skræmmende ("pas på fusionskonflikter, de bider dig!") og noget man kun gør en gang imellem.

Men med Git er disse handlinger ekstremt billige og enkle, og de betragtes i virkeligheden som en af de centrale dele af din daglige arbejdsgang. For eksempel i CVS/Subversion-bøger diskuteres forgrening og fletning først i de senere kapitler (for avancerede brugere), mens det i hver Git-bog allerede er dækket i kapitel 3 (grundlæggende).

Som en konsekvens af dens enkelhed og gentagne karakter er forgrening og sammensmeltning ikke længere noget, man skal være bange for. Versionsstyringsværktøjer formodes at hjælpe med at forgrene/fusionere mere end noget andet.

Nok om værktøjerne, lad os gå videre til udviklingsmodellen. Den model, som jeg vil præsentere her, er i det væsentlige ikke mere end et sæt procedurer, som hvert teammedlem skal følge for at komme til en styret softwareudviklingsproces.

Decentraliseret, men centraliseret
Depotopsætningen, som vi bruger, og som fungerer godt med denne forgreningsmodel, er den med en central "sandhed"-repo. Bemærk, at denne repo kun anses for at være den centrale (da Git er en DVCS, er der ikke noget, der hedder en central repo på teknisk niveau). Vi vil referere til denne repo som oprindelse, da dette navn er kendt for alle Git-brugere.



Hver udvikler trækker og skubber til oprindelsen. Men udover de centraliserede push-pull-relationer kan hver udvikler også trække ændringer fra andre peers for at danne underhold. For eksempel kan dette være nyttigt at arbejde sammen med to eller flere udviklere om en stor ny funktion, før det igangværende arbejde skubbes til oprindelse før tid. I figuren ovenfor er der underhold af Alice og Bob, Alice og David og Clair og David.

Teknisk set betyder dette ikke mere end at Alice har defineret en Git-fjernbetjening, ved navn bob, der peger på Bobs lager og omvendt.

Hovedgrenene


I kernen er udviklingsmodellen i høj grad inspireret af eksisterende modeller derude. Den centrale repo har to branches med en uendelig levetid:

* master (main)
* develop

*Master* branch i oprindelsen bør være bekendt for enhver Git-bruger. Parallelt med mastergrenen eksisterer der en anden branch kaldet *develop*.

Vi anser oprindelse/master for at være hovedgrenen, hvor kildekoden til HEAD altid afspejler en produktionsklar tilstand.

Vi anser oprindelse/udvikling for at være hovedgrenen, hvor kildekoden til HEAD altid afspejler en tilstand med de seneste leverede udviklingsændringer til næste udgivelse. Nogle vil kalde dette "integrationsgrenen". Det er her alle automatiske natlige builds er bygget fra.

Når kildekoden i udviklingsgrenen når et stabilt punkt og er klar til at blive frigivet, skal alle ændringer flettes tilbage til
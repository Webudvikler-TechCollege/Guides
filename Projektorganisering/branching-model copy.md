Denne model blev udtænkt i 2010, nu mere end 10 år siden, og ikke ret længe efter Git selv kom til. I de 10 år er git-flow (den forgreningsmodel, der er beskrevet i denne artikel) blevet enormt populær i mange softwarehold til det punkt, hvor folk er begyndt at behandle det som en slags standard - men desværre også som et dogme eller vidundermiddel. .

I løbet af de 10 år har Git selv taget verden med en storm, og den mest populære type software, der udvikles med Git, flytter sig mere mod webapps - i hvert fald i min filterboble. Webapps leveres typisk kontinuerligt, ikke rullet tilbage, og du behøver ikke at understøtte flere versioner af softwaren, der kører i naturen.

Dette er ikke den type software, jeg havde i tankerne, da jeg skrev blogindlægget for 10 år siden. Hvis dit team udfører kontinuerlig levering af software, vil jeg foreslå, at du bruger en meget enklere arbejdsgang (som GitHub-flow) i stedet for at prøve at skyde git-flow ind i dit team.

Hvis du derimod bygger software, der er eksplicit versioneret, eller hvis du har brug for at understøtte flere versioner af din software i naturen, så kan git-flow stadig passe lige så godt til dit team, som det har været for folk i de sidste 10 år. I så fald skal du læse videre.

For at konkludere, husk altid, at universalmidler ikke eksisterer. Overvej din egen kontekst. Lad være med at hade. Bestem selv.

I dette indlæg præsenterer jeg den udviklingsmodel, som jeg har introduceret for nogle af mine projekter (både på arbejde og privat) for omkring et år siden, og som har vist sig at være meget vellykket. Jeg har tænkt mig at skrive om det i et stykke tid nu, men jeg har aldrig rigtig fundet tiden til at gøre det grundigt, før nu. Jeg vil ikke tale om nogen af projekternes detaljer, kun om forgreningsstrategien og release management.



Hvorfor git?
For en grundig diskussion om fordele og ulemper ved Git sammenlignet med centraliserede kildekodekontrolsystemer, se internettet. Der foregår masser af flammekrige der. Som udvikler foretrækker jeg Git frem for alle andre værktøjer i dag. Git ændrede virkelig den måde, udviklere tænker på at fusionere og forgrene. Fra den klassiske CVS/Subversion-verden, jeg kom fra, har sammensmeltning/forgrening altid været betragtet som lidt skræmmende ("pas på fusionskonflikter, de bider dig!") og noget man kun gør en gang imellem.

Men med Git er disse handlinger ekstremt billige og enkle, og de betragtes i virkeligheden som en af de centrale dele af din daglige arbejdsgang. For eksempel i CVS/Subversion-bøger diskuteres forgrening og fletning først i de senere kapitler (for avancerede brugere), mens det i hver Git-bog allerede er dækket i kapitel 3 (grundlæggende).

Som en konsekvens af dens enkelhed og gentagne karakter er forgrening og sammensmeltning ikke længere noget, man skal være bange for. Versionsstyringsværktøjer formodes at hjælpe med at forgrene/fusionere mere end noget andet.

Nok om værktøjerne, lad os gå videre til udviklingsmodellen. Den model, som jeg vil præsentere her, er i det væsentlige ikke mere end et sæt procedurer, som hvert teammedlem skal følge for at komme til en styret softwareudviklingsproces.

Decentraliseret, men centraliseret
Depotopsætningen, som vi bruger, og som fungerer godt med denne forgreningsmodel, er den med en central "sandhed"-repo. Bemærk, at denne repo kun anses for at være den centrale (da Git er en DVCS, er der ikke noget, der hedder en central repo på teknisk niveau). Vi vil referere til denne repo som oprindelse, da dette navn er kendt for alle Git-brugere.



Hver udvikler trækker og skubber til oprindelsen. Men udover de centraliserede push-pull-relationer kan hver udvikler også trække ændringer fra andre peers for at danne underhold. For eksempel kan dette være nyttigt at arbejde sammen med to eller flere udviklere om en stor ny funktion, før det igangværende arbejde skubbes til oprindelse før tid. I figuren ovenfor er der underhold af Alice og Bob, Alice og David og Clair og David.

Teknisk set betyder dette ikke mere end at Alice har defineret en Git-fjernbetjening, ved navn bob, der peger på Bobs lager og omvendt.

Hovedgrenene


I kernen er udviklingsmodellen i høj grad inspireret af eksisterende modeller derude. Den centrale repo har to hovedgrene med en uendelig levetid:

mestre
udvikle
Mastergrenen i oprindelsen bør være bekendt for enhver Git-bruger. Parallelt med mastergrenen eksisterer der en anden gren kaldet udvikle.

Vi anser oprindelse/master for at være hovedgrenen, hvor kildekoden til HEAD altid afspejler en produktionsklar tilstand.

Vi anser oprindelse/udvikling for at være hovedgrenen, hvor kildekoden til HEAD altid afspejler en tilstand med de seneste leverede udviklingsændringer til næste udgivelse. Nogle vil kalde dette "integrationsgrenen". Det er her alle automatiske natlige builds er bygget fra.

Når kildekoden i udviklingsgrenen når et stabilt punkt og er klar til at blive frigivet, skal alle ændringer flettes tilbage til
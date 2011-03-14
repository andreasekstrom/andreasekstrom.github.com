Varför ska JAG använda Cucumber?
================================

(På måndag kommer Anthony Eden till Valtech och pratar om "Taking Cucumber to the next level". Det är i allafall jag excalterad över. )

I veckan så hade Anthony Eden en bejublad session om "Taking Cucumber to the next level". Slides från detta kommer snart. 

I samband med detta tänkte vi ta tillfället i akt att beskriva för de som inte känner så mycket om BDD och Cucumber. 

Jag tänkte ta ett litet exempel. Tänk dig att du jobbar med en webbplats åt en liten biograf som tidigare bara haft fysisk bokning av biljetter.
Tänk dig också att du jobbar i ett Scrumteam och att ni i förra iterationen implementerat grundfunktionaliteten för  
Då skulle det kunna finnas en User Story i backloggen som ser ut så här:

	Som biobesökare
	vill jag kunna boka biljett online
	För att slippa gå till biografen för att boka biljett

Sen kommer man fram till acceptanskriterier för detta, t.ex. :
	1) När användare klickar boka så kommer han till betalsajten
	2) Det ska inte gå att boka om det är fullsatt

Vi fokuserar nu bara på påstående 2. Om man nöjer sig med det kriteriet som det är skrivet ovan, så öppnar det upp för en mängd olika tolkningar. (_Här är det förstås A och O att diskutera med sin produktägare_). Menar vi att man ska få ett felmeddelande när man klickar på boka? eller ska man inte ens se en boka knapp? Eller ska man få fullsatt informationen tidigare i kedjan?  

det är här Cucumber kommer in i bilden. Det är ett utmärkt sätt att ta fram exempel och sedan dokumentera vad man kommit överens om och låta det guida vidare utveckling.

	scenario: Köpa biljett när det är fullsatt
	Givet att film "Alien" har "0" platser kvar
	När jag söker efter "Alien"
	Så ska jag inte se en köpknapp
	Och ska jag få meddelande "fullsatt"  

Cucumber använder sig av Givet-när-så-formatet (Given-When-Then) och är specifikt utvecklat för att tilltala domänexperter. Det första meddelande man möts av på Cucumbers hemsida är: "BDD that talks to domain experts first and code second". Förutom att vara helt förståeligt för alla inblandade i utvecklingsarbetet, så är detta faktiskt körbar kod. Det finns förstås en mer teknisk sida på detta och det är att dessa sk. "steps" ("Givet..." osv.) behöver översättas till vad det betyder för varje given applikation. Men det kommer jag inte att gå in på i denna korta bloggpost.

Med dessa typer av scenarior (det kan finnas ett eller flera för varje acceptanskriterie) blir det lätt för utvecklare att fokusera på att lösa ett visst problem.
Precis som i TDD (Test Driven Utveckling) så gäller att man som utvecklare ska implementera minsta möjliga kod för att detta scenario ska fungera. På det sättet får man en applikation som _bara hanterar det som det finns behov av_ (jämför de applikationer där man "tar höjd" för alla eventuella framtida användningssätt). Denna typ av utveckling brukar kallas "outside-in", där man går från ett scenario som beskriver ett verkligt behov och jobbar sig inåt mot inre modellen av applikationen.
 
Om det är en webbapplikation man utvecklar så har Cucumber utmärkta möjligheter att driva en verklig webbläsare. Med rätt hantering av sina scenarior får man:
* Design - Vägledning med acceptanskriterier (som exemplet ovan)
* Dokumentation - Beskrivning över "vad hanterar systemet"
* Regressionstester - Med ett Continuous Integration verktyg kan dessa scenarior köras varje natt eller t.om. varje gång en utvecklare gör en förändring

Blev ni intresserade att veta mer?
----------------------------------

Det här var bara ett kort exempel. Vill ni lära er mer finns mängder av tutorials som visar hur man kommer igång rent tekniskt. En bra början är: http://cukes.info/ 
Om ni vill titta på ett exempel på ett av de projekt där vi på Valtech provat att använda Cucumber kan ni se på http://www.slideshare.net/agilasverige/bdd-s-knyter-vi-ihop-scken  (som jag presenterade på Agila Sverige 2010)

Username: aek
Password: andrease
http://www.valtechlabs.se/wp-login.php


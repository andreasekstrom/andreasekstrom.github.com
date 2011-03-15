---
layout: default
title: Varför ska DU använda Cucumber?
---

I måndags hade Anthony Eden ett intressant föredrag och efterföljande diskussion om "Taking Cucumber to the next level".
Slides och video från detta finns här: __todo__

--------------

I samband med detta tänkte vi ta tillfället i akt att beskriva grunderna för de som inte känner så mycket om BDD och Cucumber.

Jag tänkte ta ett litet exempel. Tänk dig att du jobbar med en webbplats åt en liten biograf som tidigare bara haft fysisk bokning av biljetter.
Tänk dig också att du jobbar i ett Scrumteam och att ni i förra iterationen implementerat grundfunktionaliteten för att söka ut en film. 
Då skulle det kunna finnas en User Story i backloggen som ser ut så här:

	Som biobesökare
	vill jag kunna boka biljett online
	för att slippa gå till biografen för att boka biljett

Sen kommer man fram till acceptanskriterier för detta, t.ex. :

	1) När användare klickar boka så kommer han till betalsajten
	2) Det ska inte gå att boka om det är fullsatt

Vi fokuserar nu bara på påstående 2. Om man nöjer sig med det kriteriet som det är skrivet ovan, så öppnar det upp för en mängd olika tolkningar. _(Här är det förstås A och O att diskutera med sin produktägare)_. Menar vi att man ska få ett felmeddelande när man klickar på boka? eller ska man inte ens se en boka knapp? Eller ska man få fullsatt informationen tidigare i kedjan?  

Det är här Cucumber kommer in i bilden. Det är ett utmärkt sätt att ta fram exempel och sedan dokumentera vad man kommit överens om och låta det guida vidare utveckling.

	Scenario: Köpa biljett när det är fullsatt
	Givet att film "Alien" har "0" platser kvar
	När jag söker efter "Alien"
	Så ska jag inte se en köpknapp
	Och ska jag få meddelande "fullsatt"  

Cucumber använder sig av Givet-när-så-formatet (Given-When-Then) och är specifikt utvecklat för att tilltala domänexperter. Det första meddelande man möts av på Cucumbers hemsida är: "BDD that talks to domain experts first and code second". Förutom att vara helt förståeligt för alla inblandade i utvecklingsarbetet, så är detta faktiskt körbar kod. Det finns förstås en mer teknisk sida på detta och det är att dessa sk. "steps" ("Givet..." osv.) behöver översättas till vad det betyder för varje given applikation. Men det kommer jag inte att gå in på i denna korta bloggpost.

Med dessa typer av scenarior (det kan finnas ett eller flera för varje acceptanskriterie) blir det lätt för utvecklare att fokusera på att lösa ett visst problem.
Precis som i TDD (Test Driven Utveckling) så gäller att man som utvecklare ska implementera minsta möjliga kod för att detta scenario ska fungera. På det sättet får man en applikation som _bara hanterar det som det finns behov av_ (jämför de applikationer där man "tar höjd" för alla eventuella framtida användningssätt). Denna typ av utveckling brukar kallas "outside-in", där man går från ett scenario som beskriver ett verkligt behov och jobbar sig inåt mot inre modellen av applikationen.

Med rätt hantering av sina scenarior får man:
* Design - Vägledning med acceptanskriterier (som exemplet ovan)
* Dokumentation - Beskrivning över "vad hanterar systemet"
* Regressionstester - Med ett Continuous Integration verktyg kan dessa scenarior köras varje natt eller t.om. varje gång en utvecklare gör en förändring

Cucumber har sin _sweetspot_ vid utveckling av webbapplikationer, och i synnerhet Rails-applikationer, där det finns väldigt bra integration för att köra sina scenarier i simulerad eller verklig webbläsare (via Selenium), och mängder med fördefinierade "web_steps" som mappar Cucumber-steps till webbläsarhändelse (t.ex. "fyll i fält X", "klicka på knapp Y" osv. ) 

Blev ni intresserade att veta mer?
----------------------------------

Det här var bara ett kort exempel. Vill ni lära er mer finns mängder av tutorials som visar hur man kommer igång rent tekniskt. En bra början är: [http://cukes.info/][0]
 
Om ni vill titta på ett exempel på arbetet i ett av de projekt där vi på Valtech provat att använda Cucumber kan ni se på [BDD - Så knyter vi ihop säcken][1]  (som jag presenterade på Agila Sverige 2010)

Jag kan också rekommendera ["The RSpec Book"][2] som ger mycket tips för Cucumber och Rspec, men också beskriver processen för att arbeta med dessa i agila projekt.

Lycka till!

[0]: http://cukes.info/
[1]: http://www.slideshare.net/agilasverige/bdd-s-knyter-vi-ihop-scken
[2]: http://www.pragprog.com/titles/achbd/the-rspec-book
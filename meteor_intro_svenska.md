Nytt år! Nya paradigmer för webbutveckling?
==========================================

I mer än 10 års tid så har webbssajter utvecklats på ungefär samma sätt. En användare matar in en länk till ett hyperlänkat dokument, och kan genom att klicka på länkar navigera och ladda ned andra HTML-dokument (grunden för world wide web).

Men på senare år så har fler och fler av de webbsajter vi utvecklat snarare haft karaktären av applikationer än hyperlänkade dokument. Med kraftfullare javascript-motorer så har webbläsaren förvandlats till en plattform för att köra applikationer, snarare än en enkel läsare av dokument.
Det är nu många år sen Ajax gjorde sitt inträde, och gjorde att vi inte behöver ladda om en hel sida bara för att en liten del av sidan ändras. I början utvecklades dessa nästan helt utan ramverksstöd. Men numera finns det finns en hel del ramverk som försöker göra det lättare att skriva dessa "single-page applikationer", såsom [Backbone.js](http://backbonejs.org/), [Ember.js](http://emberjs.com/) och [Angular.js](http://angularjs.org/).

Ett av de (i mitt tycke) mest intressanta i den skaran av ramverk är [Meteor](https://www.meteor.com/). Meteor utmanar många av de sätt vi utvecklar applikationer på idag.

Publish/Subscribe
-----------------

I fler och fler av dagens webapplikationer så vill vi automatiskt få uppdateringar när något förändras. Om du t.ex. bevakar en forumtråd så vill du inte manuellt behöva ladda om webläsaren för att få se nya kommentarer, eller om du jobbar tillsammans med någon i t.ex. ett gemensamt dokument eller mindmap så vill du antagligen omedelbart få reda på förändringar i dessa, utan att behöva ladda om någonting. Det är för den typen av applikationer som Meteor verkligen är anpassat för. Klienter får automatiskt uppdateringar för de data de prenumererar på. Detta sker m.h.a. att varje klient har en [Websocket](http://en.wikipedia.org/wiki/WebSocket)-connection uppkopplad till servern, där förändringar i data skickas.

Data on the wire
----------------

I Meteor så hämtas i regel bara HTML vid första anropet. Tanken är att sedan bara sända data (förändringar) och låta klienten bestämma vad som ska renderas.

Javascript everywhere
---------------------

Meteor är ett s.k. fullstack-ramverk, där server-delen skrivs i javascript ([Node.js](http://nodejs.org/)) och klientdelen i javascript. Meteor har också ett intressant sätt att se på server och klient. Du kan nämligen välja att viss kod ska köras både på klient och server.

Database everywhere
-------------------

Detta är en sak som ter sig lite märkligt i början, men med hjälp av Publish/Subscribe så har klienten en egen "MongoDB databas" i webbläsaren (kallad minimongo). Detta gör att man kan använda samma API för databas-access på klient- och serversida. Databasen på klienten (minimongo) är alltså en typ av cache av en delmängd av databasen på serversidan, med den finessen att cachen automatiskt uppdateras. Om man t.ex. prenumererar på de 10 senaste kommentarerna i en chattjänst, så kommer de automatiskt att uppdateras på alla anslutna klienter när en ny kommentar läggs till på server-sidan. Till Meteor 1.0 kommer ingen annan datakälla än MongoDB stödjas, men man kan nog förvänta sig att det sedan kommer adapters för andra databaser.

Latency compensation
--------------------

Även om servern är långt från klienten, eller med en dålig uppkoppling, så är tanken att Meteor-applikationer alltid ska ge svar inom millisekunder. Eftersom databasen finns även på klienten så kan uppdatering och tillägg ske även om klienten för tillfället inte har kontakt med servern. När servern sedan svarar så synkas databaserna automatiskt. Det gör att vi kan få väldigt responsiva applikationer, en känska av att de svarar utan någon fördröjning alls.

Exempel på detta ovan?
----------------------

För några veckor sedan så höll jag en kompetenslunch om Meteor på Valtech, där jag försökte belysa dessa saker i en demo. Titta gärna på [demo-anteckningarna](https://github.com/andreasekstrom/demo-meteor-leaderboard) för att lära er mer om detta.

Does it scale?
--------------

Den viktiga frågan som alla nya ramverk ställs inför! Det återstår att se. Än vet jag inte om någon Meteor-applikation med 10000-tals samtidiga användare.
Men prestanda och skalbarhet är definitivt någonting som är på Meteor-teamets radar, se t.ex. : [Scaling Meteor with the MongoDB oplog](https://www.meteor.com/blog/2013/12/18/david-glasser-on-scaling-meteor-with-the-mongodb-oplog) för mer info.


Kommer 2014 bli året då Meteor (eller idéerna Meteor står för) slår igenom på bred front? Kanske. Det återstår att se.

Några saker som talar för Meteor är:

* [Välfinansierad open source](https://www.meteor.com/blog/2012/07/25/meteors-new-112-million-development-budget)
* Redan stor och växande utvecklar-community (För närvarande 80 Meteor meetup-grupper i 31 länder)
* Meteor 1.0 förväntas inom några månader...
* Enkel hosting av applikationer (Om jag förstått affärsmodellen rätt, så är tanken att i.o.m. Meteor 1.0 lansera "Galaxy", som är en hosting-plattform helt anpassad för Meteor-applikationer)

Om ni vill bli inspirerade av vad som är möjligt så rekommenderar jag den [officiella Meteor videon](https://www.meteor.com/authcast)
När ni väl blivit inspirerade så har de samlat en massa bra länkar för att lära sig mer på [https://www.meteor.com/learn-meteor](https://www.meteor.com/learn-meteor).

För egen del så har jag sen jag började följa Meteor och Meteor-communityn lärt mig en massa nytt om javascript, Node.js och MongoDB. Bara det är värt en del!

Din första Meteor app?
----------------------

Om du kör Windows så är det ännu inte officiellt supportat (ska komma någon gång efter 1.0), men det finns en [inofficiell support](http://win.meteor.com/).
Om du kör Mac eller Linux så skriv in dessa fyra rader kod i kommandoraden, så kommer du att både installera Meteor och deploya din första Meteor "hello world"-applikation!

    curl https://install.meteor.com | /bin/sh
    meteor create myapp
    cd myapp
    meteor deploy <any-name>.meteor.com

Meteor-teamet hostar nu gratis din nyskapade app på http://<any-name>.meteor.com !

Happy hacking!

---
title: De status van de inventaris controleert ontwikkeling en prestatiesoverwegingen
description: Lees enkele ideeën en overwegingen voor het uitvoeren van voorraadstatuscontroles voor Adobe Commerce.
feature: Best Practices, Inventory
topic: Development, Performance
role: Architect, Developer
level: Intermediate, Experienced
doc-type: Tutorial
duration: 0
last-substantial-update: 2024-05-09T00:00:00Z
jira: KT-15462
exl-id: bd2be562-5738-4398-8afb-2faeb0ba6b83
source-git-commit: 84f9139181bf57d967494da97d4d27d297513c31
workflow-type: tm+mt
source-wordcount: '1932'
ht-degree: 0%

---

# De status van de inventaris controleert ontwikkeling en prestatiesoverwegingen

Nauwkeurigheid met inventarisatie is een zeer belangrijke overweging. Er zijn enkele native functies die kunnen helpen ervoor te zorgen dat dit risico zo laag mogelijk is, zoals back orders en het vaststellen van de drempel voor het buiten de voorraad houden. Beide onderwerpen kunnen op [ Experience League ](https://experienceleague.adobe.com/nl/docs/commerce-admin/inventory/configuration/backorders) voor verdere verklaring worden gelezen.

Er zijn projecten en gebruiksgevallen waarin een Adobe Commerce-winkel een statuscontrole van de voorraad in real-time moet uitvoeren. Deze zelfstudie biedt inzicht in de afhandeling van dit gesprek met ontwikkelings- en prestatieoverwegingen.

## Valideren als dit verzoek absoluut noodzakelijk is

Bereid u voor om met het gesprek te gaan met zoveel mogelijk informatie. Het belangrijkste is te verifiëren dat de native functionaliteit niet acceptabel is voor dit project. Zoek de redenering achter dit verzoek om te controleren of de native mogelijkheden van Adobe Commerce dit verzoek niet uitvoeren.

Een andere overweging betreft de kosten voor het ontwikkelen, testen en onderhouden van deze functie. Enkel omdat sommige belanghebbenden het nodig vinden, betekent dit niet dat het een vereiste is. Er zijn kosten verbonden aan het uitvoeren van inventarisbevestiging buiten de kernfunctionaliteit van Adobe Commerce. Deze kosten komen voort uit technische schulden, meer tests en validatie, alsook uit documentatie over het gebruik en ondersteunende documenten voor de architectuur ervan.

## Bepalen wat een aanvaardbare voorraadupdatecadentie is

Overweeg inventariscontroles en hoe deze worden uitgevoerd in drie benaderingen. Elke heeft voordelen en beperkingen. Ze worden ook complexer en vereisen meer tests en nadenken voor foutafhandeling. Herinner wanneer u besluit om een douaneroute te gaan, zijn er toegevoegde verantwoordelijkheden en overwegingen. Een paar voorbeelden zouden een fallback proces, controle, het testen en het oplossen van problemenvallen aan het ontwikkelingsteam omvatten. Een paar goede punten om te omvatten zijn nieuwe ondersteunende documentatie, opleiding en controle om ervoor te zorgen dat het ontwikkelingsteam de volledige eigenschap kan steunen. Een bijkomend neveneffect is dat het ontwikkelingsteam volledig eigenaar is van het proces en niet langer gebruikmaakt van de native functionaliteit die wordt geboden door de Adobe Commerce-kerntoepassing. Ondersteuning van Adoben kan niet helpen bij dit aanpassingsniveau.

De eerste aanpak is het gebruik van de native functionaliteit. Native functionaliteit is het minste risico en biedt veel voordelen. Op deze manier kunt u vertrouwen op alle bestaande documentatie en zelfstudies die Adobe Commerce voor het gebruik van de functie biedt. Er zijn veel aspecten aan voorraadbeheer, dus het gebruik van wat bij de aanvraag wordt geleverd, zou de eerste overweging moeten zijn. Er zijn echter gevallen waarin de gegevens die op het moment van de bestelling in de handel werden aangetroffen, niet geheel correct zijn. Een voorbeeld voor hoe dingen uit synchronisatie kunnen komen is dat de verkoop buiten de toepassing van Adobe Commerce direct in het systeem van het ordebeheer wordt toegestaan. Een reden is dat, om ervoor te zorgen dat de juiste inventarisniveaus in Adobe Commerce worden weergegeven, een soort integratie nodig is om de Adobe Commerce-informatie zo nauwkeurig mogelijk te houden. Als oververkopen niet acceptabel is, is het toevoegen van een drempelwaarde voor het niet langer in voorraad hebben een goede methode om de verkoop van objecten te stoppen voordat je op nul komt. De native synchronisatiefunctionaliteit voor Adobe Commerce is maximaal 1 keer per dag. Dit is voldoende voor sommige gevallen van gebruik, hoewel het niet vaak genoeg voorkomt voor andere. Gelieve te lezen [ Geplande invoer en de uitvoer ](https://experienceleague.adobe.com/nl/docs/commerce-admin/systems/data-transfer/data-scheduled-import-export) voor meer gedetailleerde informatie.

De tweede aanpak zou `near real-time` zijn. Bijna real-time gebruikt nog steeds de native functionaliteit. Dit omvat echter extra werk om een integratie te bieden die regelmatig handel voedt om de inventaris volgens een schema bij te werken. Bijvoorbeeld elk uur. Bij deze optie moet er rekening mee worden gehouden hoe een integratie werkt, maar het is een goede aanpak om de &quot;bulk api&quot; te gebruiken en wat middleware de gegevens te laten transformeren en de gegevens naar de handel te duwen. Kijk naar het gebruik van Adobe App Builder of vergelijkbare platforms om het grootste deel van het werk te doen en druk de informatie op een frequentere cadence naar Adobe Commerce.

De derde aanpak en de meest complexe met de meeste risico&#39;s en verantwoordelijkheid is Live inventariscontroles in real-time naar een externe API of gegevensbron. Het uitvoeren van een inventariscontrole in real time aan een extern systeem is riskant en heeft verscheidene andere elementen die moeten worden overwogen. Hier zijn slechts een klein aantal andere zaken die moeten worden geëvalueerd:

* Kan het externe systeem REST- of GraphQL-verzoeken accepteren
* zijn er om het even welke grenzen aan het eindpunt zoals X aantal verzoeken per minuut die niet met het websiteverkeer kunnen samenvallen
* Wat gebeurt er met de responstijd onder belasting?
* Wat gebeurt wanneer de reactietijden lang zijn, beëindigt u dit automatisch en gebruikt een reserveoptie zoals de inheemse inventaris.
* Welk type controle beschikbaar is om ervoor te zorgen dat API-aanvragen binnen de tolerantiegrenzen vallen

## Overwegingen bij het overwegen van niet-native voorraadbeheer

Houd de aanpassingen zo complex mogelijk.
Hoe plat de organisatie van de voorraad kan zijn, is het slechts 1 SKU en de totale hoeveelheid beschikbare voorraad OF zijn er andere kenmerken die in overweging moeten worden genomen.

Als de inventarisinformatie vrij vlak is, bijvoorbeeld een sku en de totale beschikbare hoeveelheid, worden de opties voor bijna real-time uitgebreid. Het concept van bijna real time betekent dat er een achtergrondverrichting is die de inventaris van de bron verzamelt, en dan een opslagmotor bevolkt die moet worden gebruikt om op het verzoek te antwoorden. Hiervoor kunt u dingen als Redis, Mongo of andere niet-relationele databases gebruiken. Deze opties zijn handig omdat ze erg snel zijn en uitstekend werken voor sleutel-/waardeparen. Als de gegevens een beetje complexer zijn, dan zal het gebruiken van een relatiegegevensbestand, of binnen of buiten de handelstoepassing, waarschijnlijk vereist zijn. Door dit van het handelsgegevensbestand te ontladen, houdt u de kernhandelstoepassing geïsoleerd van deze transacties. Een andere reeks voordelen bespaart I/O van de handelstoepassing, cpu, RAM en anderen van gebruik. In plaats van de bronnen van de Adobe Commerce-toepassingsservers te gebruiken, kunt u beter de nieuwe API&#39;s gebruiken om de gegevens van de externe opslag te halen.  Dit zal waarschijnlijk middleware nodig hebben helpen om het even welke gegevens transformeren. Controleer vervolgens of de opvragende toepassing het resultaat naar behoren kan ophalen. Door Adobe App Builder met API-net te gebruiken, kunnen de gegevens worden getransformeerd en correct worden geretourneerd.

Het gebruik van Adobe App Builder met API-net is ook een ideale optie als er meerdere inventarisbronnen zijn.


## De uitvoeringslogica verplaatsen naar een locatie buiten het proces

Adobe Developer App Builder biedt een uniform uitbreidbaarheidskader van derden voor het integreren en creëren van aangepaste ervaringen om oplossingen voor Adoben uit te breiden. Adobe Commerce kan Adobe Developer App Builder gebruiken. Dit zou een uitstekend gebruiksgeval zijn om sommige functionaliteit uit te breiden die normaal in de kerntoepassing voorkomt en het van plaats beweegt. Door functionaliteit uit de Commerce-toepassing te verwijderen, verkleint u het aantal modules en de complexiteit van de Commerce-toepassing. Een lager aantal aanpassingen tijdens het proces vermindert de complexiteit voor upgrade en onderhoud.

Voor inspiratie voor hoe dit zou kunnen worden verwezenlijkt, heeft het team bij Adobe één of andere documentatie gecreeerd die een grote bron van inspiratie kan zijn en werkende codesteekproeven verstrekt. Wanneer een winkelier een product aan het winkelwagentje toevoegt, controleert een voorraadbeheersysteem van derden of het item in voorraad is. Als dat het geval is, moet het product worden toegevoegd. Anders geeft u een foutbericht weer.  Voor codesteekproeven en verdere informatie gaan naar {de Gevallen van het Gebruik van 0} Webhaak [&#128279;](https://developer.adobe.com/commerce/extensibility/webhooks/use-cases/#add-product-to-cart).

## Wanneer voorraadcontroles worden uitgevoerd

Wanneer om te controleren of de inventaris nog beschikbaar is zal uiteindelijk aan de ondernemingspersoneel, de softwarearchitect met wat input van andere belangrijke belanghebbenden zijn. Een paar geschikte tijden zijn bijvoorbeeld het toevoegen van een item aan het winkelwagentje en het invoeren van de afrekenworkflow. Eventuele andere gebeurtenissen voegen eenvoudig belasting toe aan de back-endsystemen wanneer dit niet nodig is. Houd er rekening mee dat het doel is om een inventarisprobleem alleen af te vangen wanneer dit van het grootste belang is. Andere controles zijn misschien leuk om te hebben, maar als ze van invloed kunnen zijn op het algemene doel voor statuscontroles van de inventaris, moeten ze zorgvuldig worden overwogen en alleen worden toegestaan als de belanghebbenden van het bedrijfsleven of anderen zich bewust zijn van het potentiële risico voor extra belasting op de back-endsystemen.

## Onderzoek hoe de inventarisbron

Er is een uitgebreid onderzoek van de externe inventarisbron nodig. Items die moeten worden geëvalueerd, zijn beschikbare API-opties, ondersteuning voor GraphQL en verwachte responstijden. Als de inventarisbron een beperkte verbindingsbandbreedte heeft of nooit bedoeld om in een echt - tijdverzoek werd gebruikt, wordt de capaciteit voor gebruik uitgesloten en architect moet in plaats daarvan bijna - in real time overwegen.  Als de API aanvraagtijden de bepaalde parameters overschrijden, zal het ook dit van een levensvatbare optie uitsluiten.  Een voorbeeld hiervan zijn de api-responsen 200MS® voor één keer, maar bij matige belasting stijgen ze tot 500 tot 900MS®.  Dit zou waarschijnlijk alleen maar erger worden met meer belasting en regelt de live inventarisaanroepen niet meer beschikbaar zijn.

Zorg ervoor dat u de responstijden van de API test met eenvoudige verzoeken en met een hoog volume dat vergelijkbaar is met het verwachte verkeer op de livesite. Herinner me om alle gebieden van handel tezelfdertijd te testen om echte wereldscenario&#39;s te simuleren. Als de verwachting een live inventarisvraag op productpagina&#39;s zou moeten voorkomen, wanneer het bekijken van en het uitgeven van een karretje en tijdens controle, moet het ladingstests alle deze tezelfdertijd simuleren om echt klantengedrag en de verwachting voor een opslag na te bootsen.

## Opties voor alternatieven

Als de inventarisbron uitvalt en er bewaking beschikbaar is, wordt het gebruik van de native mogelijkheden van Adobe Commerce aanbevolen. Met een goede controle kan de ervaring van de klant echter dynamisch veranderen om het verlies van voorraadcontroles in real time weer te geven. Dit kan betekenen dat een verkoop of gebeurtenis vroegtijdig wordt geannuleerd of van de vertoning wordt verwijderd om oververkopen te voorkomen. De verwachting voor wat te doen wanneer de inventarisbron om het even welke reden is neer moet worden overwogen en met de archiefeigenaar worden besproken zodat iedereen zich bewust is van om het even welk automatisch proces dat in die ongelukkige omstandigheden overneemt.

## Conclusie

Het besluit om inventariscontroles in real time uit te voeren is aanzienlijk. Ervoor zorgen dat de eigenaar van de website, het ontwikkelingsteam en anderen volledig zijn opgeleid en zich bewust zijn van alle voordelen en potentiële valkuilen, ligt op de leider van de ontwikkelaar of architect. Een doordacht plan dat de redenen en een fallback-proces bestrijkt, is essentieel voor succes.

Live inventariscontroles kunnen worden uitgevoerd, maar hiervoor is onderzoek nodig en moet worden nagedacht over het testen en valideren tijdens de kwaliteitscontrole. Door ervoor te zorgen dat de belasting wordt getest en dat de geautomatiseerde tests worden beëindigd, kunt u ervoor zorgen dat alle mogelijke problemen worden opgepakt en getrigeerd.

Door na te gaan welke acties moeten worden uitgevoerd als de bewaking een trend van mislukte oproepen aan het externe systeem detecteert of als de responstijden boven aanvaardbare drempelwaarden liggen, kan de site online blijven en de klant de minste irritatie bieden. De opties van de reserve kunnen zo eenvoudig zijn zoals het uitzetten van de externe inventariscontroles en het gebruiken van de inheemse functionaliteit of kunnen zo geavanceerd zijn zoals het onbruikbaar maken van een bevordering, het op de hoogte stellen van het ontwikkelingsteam van de escalerende kwesties of zelfs het herverpletteren van verzoeken aan een tweede of derde achterste deelsysteem als beschikbaar. Hoe het fallback-mechanisme wordt uitgevoerd, moet gewoon als de daadwerkelijke implementatie worden beschouwd, omdat elke integratie op een gegeven moment problemen heeft. Alles wat geautomatiseerd is of handmatig moet worden uitgevoerd, moet duidelijk worden gedocumenteerd.

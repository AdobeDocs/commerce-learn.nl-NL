---
title: Code opnieuw gebruiken met Adobe Commerce optimaliseren
description: Leer hoe u code hergebruikt in Adobe Commerce met Global Reference Architecture-patronen, waardoor de prestaties en compatibiliteit in meerdere versies worden verbeterd.
kt: 15773
doc-type: tutorial
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
badge: label="Bijgedragen door Tony Evers, Sr. Technical Architect, Adobe" type="Informative" url="https://www.linkedin.com/in/evers-tony/" tooltip="Bijgedragen door Tony Evers"
topic: Architecture, Commerce, Development
old-role: Architect, Developer
role: Developer, User, Leader
level: Beginner, Intermediate
exl-id: 5475ade8-028c-4b24-a563-60dcda5ba93a
source-git-commit: 79d57d2c04c42a8dc23b5735e72e841b7e51cc63
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---

# Implementatietechnieken voor algemene referentiearchitectuur

{{only-for-on-prem-commerce-cloud}}

Er zijn verschillende manieren om code opnieuw te gebruiken met Adobe Commerce. Deze vier implementatietechnieken hebben elk hun eigen voordelen. De voorbeelden in dit artikel zijn van eenvoudige naar complexere volgorde geordend. Kies de strategie die het beste bij uw project en toekomstige routekaart past. Een migratie van de ene strategie naar de andere kan tijdrovend zijn.

## Wanneer gebruikt u de globale referentiearchitectuur

De globale verwijzingsarchitectuur kan waardevol zijn, afhankelijk van het aantal instanties u bezit. Een instantie is een standalone installatie van Adobe Commerce die zijn eigen gegevensbestand gebruikt. Tel het aantal productiedatabanken om te weten hoeveel instanties u bezit. Als u meer dan één instantie handhaaft, of als u dit scenario in de toekomst voorziet, kunt u van globale verwijzingsarchitectuur profiteren. Hoe meer functionaliteit de instanties delen, hoe meer waarde een algemene verwijzingsarchitectuur toevoegt.

In elk van deze scenario&#39;s is het raadzaam te onderzoeken met behulp van meerdere instanties van Adobe Commerce.

1. **Verschillende Eigenaars van de Opslag**: Als u code voor veelvoudige opslageigenaars handhaaft, elk met hun eigen afzonderlijke opslag, kunnen de afzonderlijke instanties nodig zijn om hun individuele vereisten effectief te handhaven.
2. **Naleving van Nationale Regels**: Bepaalde verordeningen vereisen dat de klantengegevens binnen specifieke gebieden moeten worden opgeslagen. In dergelijke gevallen zijn afzonderlijke gevallen van essentieel belang om de naleving van deze verordeningen te waarborgen.
3. **Operationele Variaties over Geografische Regio&#39;s**: Het werken in veelvoudige gebieden kan verschillende onderhoudsprogramma&#39;s en vereisten betekenen. Door afzonderlijke instanties te gebruiken, kunt u deze variaties op een efficiënte manier beheren.
4. **de Verkoop van de Flits van hoge intensiteit**: De opslag die grote flitsverkoop leidt vereist vaak geoptimaliseerde serverprestaties. De specifieke infrastructuur die door afzonderlijke instanties wordt verstrekt verzekert optimale prestaties tijdens dergelijke hoge vraagperiodes.
5. **Belangrijke Verschillen tussen Merken of Landen**: Wanneer het verschil tussen merken of landen groot is, leidt het gebruiken van één enkele instantie in code die slechts voor sommige merken of landen wordt gebruikt. De afzonderlijke instanties kunnen prestaties en stabiliteit verbeteren door onnodige code voor merken en landen te elimineren die het niet nodig hebben.

## Algemene referentiearchitectuur

Naast &#39;geen GRA-patroon&#39; zijn er vier stijlen van GRA-patronen.

![ 5 pictogrammen van patronen GRA: geen GRA, spleet, bulk, scheidt en monorepo.](/help/assets/global-reference-architecture/gra-patterns-horizontal.png){align="center"}

### Geen GRA-patroon

![ een pictogram dat &quot;geen GRA&quot;toont ](/help/assets/global-reference-architecture/no-gra.png){align="center"}

Wanneer geen GRA-patroon wordt gebruikt, is elke Adobe Commerce-instantie een unieke toepassing. Er is geen hergebruik van code, behalve door code handmatig van de ene instantie naar de andere te verplaatsen. Deze kopieën lopen altijd uiteen. De hoeveelheid inspanning om ervoor te zorgen dat elke instantie de zelfde veranderingen maar nog werkt zoals verwacht kan overweldigend worden. In dit scenario hebben drie instanties driemaal de onderhoudsinspanning van één instantie nodig.

![ een diagram dat 3 opslag toont, waar elk een exemplaar van de vroegere, met unieke ontwikkeling die in alle 3 exemplaren gebeurt.](/help/assets/global-reference-architecture/no-gra-pattern-diagram.png){align="center"}

### Het gesplitste Git GRA-patroon

![ een pictogram dat het &quot;gespleten&quot;patroon van GRA ](/help/assets/global-reference-architecture/split-git.png){align="center"} toont

Dit patroon bestaat uit Git-opslagplaatsen voor ontwikkeling en één Git-opslagplaats per instantie. Elk bestand in de instantie wordt onderhouden in een van de opslagplaatsen voor ontwikkelaars. Ze komen samen als een vlecht die de hele GRA vormt. Elke coderegel bestaat alleen in één ontwikkelingsopslagplaats en wordt met behulp van de omschakelingstechniek op de instanties geïnstalleerd, wat leidt tot hergebruik van code.

![ een diagram dat toont waar de code in een gesplitst patroon GRA ](/help/assets/global-reference-architecture/split-git-gra-pattern-diagram.png){align="center"} wordt opgeslagen

### Het GRA-patroon van bulkpakketten

![ een pictogram dat het &quot;bulk&quot;patroon GRA ](/help/assets/global-reference-architecture/bulk-packages.png){align="center"} vertegenwoordigt

De Adobe Commerce-kernmodules en modules van derden worden rechtstreeks geïnstalleerd via Composer-opslagruimten. Git-opslagruimten kunnen worden gebruikt als composer-opslagruimten. In dit patroon wordt de gehele gedeelde GRA-codebase gehost in één of enkele Git-opslagruimten en geïnstalleerd via Composer. Het belangrijkste kenmerk is dat meerdere modules, taalpakketten of thema&#39;s in één composerpakket worden ondergebracht, waardoor de ontwikkeling wordt vereenvoudigd.

![ een diagram dat toont waar de code in een bulkpakkettenGRA patroon ](/help/assets/global-reference-architecture/bulk-gra-pattern-diagram.png){align="center"} wordt opgeslagen

### Het GRA-patroon van de afzonderlijke pakketten

![ een pictogram dat het &quot;afzonderlijke pakketten&quot;patroon GRA ](/help/assets/global-reference-architecture/separate-packages.png){align="center"} vertegenwoordigt

Elke Adobe Commerce-module, taalpakket of elk thema wordt geïnstalleerd als een apart composerpakket. Elke aanpassing heeft een eigen Git-opslagplaats. Dit betekent ultieme flexibiliteit in de samenstelling van de instanties en heeft een betrouwbaar beheer van composerafhankelijkheid. Voor het optimaliseren van prestaties, worden alle pakketten weerspiegeld in één enkele privé composer bewaarplaats.

![ een diagram dat toont waar de code in een afzonderlijk patroon van pakkettenGRA ](/help/assets/global-reference-architecture/separate-packages-gra-pattern-diagram.png){align="center"} wordt opgeslagen

### Het monorepo GRA-patroon

![ een pictogram dat het &quot;monorepo&quot;patroon GRA ](/help/assets/global-reference-architecture/monorepo.png){align="center"} vertegenwoordigt

Alle ontwikkeling vindt plaats in één enkele codeopslagplaats. Automatisering genereert pakketten voor nieuwe versies en publiceert deze naar een composer-opslagplaats. Het patroon combineert de lage ontwikkelingsoverhead van de bulkpakketaanpak met de flexibiliteit van de afzonderlijke pakketaanpak. Het monorepopatroon is ook ideaal voor het uitvoeren van geautomatiseerde functionele tests.

![ een diagram dat toont waar de code in een patroon van monorepo GRA ](/help/assets/global-reference-architecture/monorepo-gra-pattern-diagram.png){align="center"} wordt opgeslagen

## Een GRA-patroon kiezen

De keuze voor een GRA-patroon wordt gemaakt door de complexiteit van het project, de behoefte aan flexibiliteit en het vermogen van het ontwikkelingsteam om zich aan te passen te beoordelen.

Teams met weinig Adobe Commerce-ervaring kunnen het best eenvoudig beginnen. Maar als het project vanwege zijn kenmerken een complexer GRA-patroon vereist, moet u geen compromissen sluiten.

Gemeenschappelijke projectkenmerken voor elk patroon:

1. **Geen patroon GRA**: Enige instantie van Adobe Commerce zonder plannen om uit te breiden. Meerdere gevallen van Adobe Commerce met minimale onderlinge uniformiteit.

2. **Splitst het patroon van Git GRA**: De teams die Composer voor hun aanpassingen wensen te vermijden, in de meeste gevallen is het Bulk pakketpatroon een aangewezen patroon aan Splitst Git.

3. **Bulk pakketGRA patroon**: De codebase van de aanpassing met hoge onderlinge afhankelijkheid. Exemplaren hebben allemaal zeer vergelijkbare combinaties van aangepaste pakketten. Geen regelmatige promotie of vernietiging van afzonderlijke pakketten. Teams die weinig ervaring hebben met codebeheer en die eenvoud nodig hebben.

4. **Afzonderlijke pakketten GRA patroon**: Het flexibele beheer van het versiewerkingsgebied nodig. In de komende vijf jaar worden maximaal 50 aangepaste pakketten verwacht. Potentieel, globale en regionale lagen van gemeenschappelijke code. Er zijn geen plannen om naar een Monorepo-patroon te migreren. Het team is technisch deskundig en heeft strikte procesnaleving.

5. **patroon Monorepo GRA**: Alle kenmerken van het afzonderlijke patroon GRA van pakketten. De komende vijf jaar worden meer dan 50 pakketten verwacht. Noodzaak van uitgebreide geautomatiseerde tests. Ondersteuning voor letterlijke omgevingen. Complexe codebase op bedrijfsniveau die moet worden geschaald zonder onderhoudskosten aan een gelijk tarief te schalen.

### De kosten van een verkeerde keuze

Migratie van het ene patroon naar het andere is mogelijk. In het onderstaande diagram ziet u de mate van impact van de overgang van het ene naar het andere patroon. Groene lijnen tonen een lage impact, gele en amberkleurige lijnen tonen een matig complexe tot complexe migratie.

![ een diagram dat gekleurde pijlen tussen alle 4 patronen toont GRA, die op het niveau van moeilijkheid wijzen om zich van één naar andere te bewegen.](/help/assets/global-reference-architecture/wrong-choice.png){align="center"}

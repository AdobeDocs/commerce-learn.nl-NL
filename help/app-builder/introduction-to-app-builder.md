---
title: Uitbreidbaarheid buiten proces voor Adobe Commerce
description: Meer informatie over Adobe App Builder en waarom dit een belangrijk aspect is van de uitbreidbaarheid zonder processen.
landing-page-description: Leer wat App Builder is en hoe deze kan helpen met ontwikkelingsstrategieën voor Adobe Commerce.
kt: 11433
doc-type: tutorial
audience: all
last-substantial-update: 2023-01-24T00:00:00Z
source-git-commit: 336581ac6b695d8b847d88daadeb3784ece97ae7
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 0%

---


# Inleiding tot App Builder

Adobe Commerce-ontwikkeling heeft altijd gebruikgemaakt van procesrekbaarheid. Het in-proces model vereist om het even welke nieuwe code om met verbeteringen, de PHP versie van de server, en vele andere essentiële servertoepassingen en de diensten compatibel te zijn die de Handel gebruikt. Adobe Developer App Builder maakt gebruik van externe uitbreidbaarheid om deze compatibiliteitsproblemen te voorkomen.

## App Builder voor Adobe Commerce {#project-firefly}

>[!VIDEO](https://video.tv.adobe.com/v/3412839)

Adobe Developer App Builder is een serverloos uitbreidbaarheidsplatform voor het integreren en maken van aangepaste ervaringen voor het uitbreiden van Adobe-oplossingen. Het is nu beschikbaar voor Adobe Commerce. Met App Builder kunt u veilige en schaalbare apps maken die de eigen functies voor handel uitbreiden en integreren met oplossingen van derden. Als ontwikkelaar kunt u nu profiteren van de uitbreidbaarheid buiten het proces met Adobe Commerce en die op zijn beurt directe en langetermijnvoordelen biedt.

App Builder biedt een geïntegreerd extern uitbreidingsframework voor het integreren en maken van aangepaste toepassingen die een uitbreiding vormen [!DNL Adobe Commerce]. Aangezien dit uitbreidbaarheidskader op Adobe infrastructuur wordt gebouwd, kunnen de ontwikkelaars de microdiensten van de douane bouwen en uitbreiden en integreren [!DNL Adobe Commerce] voor andere Adobe-oplossingen en integratie van derden.

App Builder biedt klanten een manier om de app uit te breiden [!DNL Adobe Commerce] in verschillende gebruiksgevallen:

* uitbreidbaarheid met middleware - Sluit externe systemen aan op Adobe-toepassingen door aangepaste connectors te maken of gebruik te maken van een reeks vooraf gebouwde integraties.
* de uitbreidbaarheid van de kerndiensten - breid kerntoepassingsmogelijkheden door het standaardgedrag met douaneeigenschappen en bedrijfslogica uit te breiden.
* uitbreidbaarheid van gebruikerservaring - breid kernervaring uit om bedrijfsvereisten te steunen of klant-specifieke digitale eigenschappen, opslagronts, en achterkantoortoepassingen te bouwen.

App Builder (voorheen bekend als Project Firefly) is een cloudgebaseerde oplossing, wat betekent dat deze automatisch wordt geschaald. Deze service wordt ook wereldwijd gedistribueerd zodat u de beste prestaties kunt leveren, ongeacht uw geografische locatie.

## Waarom moet u meer weten over App Builder

Aangezien Adobe Commerce geen volledig SAAS-product is, kan de code die u ontwikkelt, complexiteit en upgradeproblemen toevoegen. Door uit-van-procesrekbaarheid, zoals App Builder te gebruiken, kunt u douane, unieke functionaliteit aan uw opslag van Adobe Commerce verstrekken zonder in-proces methodes te vereisen.

Andere voordelen zijn:

* Dankzij de ontkoppelde functies is het sneller om te starten.
* Upgrades zijn nu eenvoudiger. De aangepaste functies bevinden zich buiten de handelsbalans, waardoor compatibiliteitsproblemen tijdens de upgrade worden voorkomen.
* Door functies en logica buiten de handel te verplaatsen, worden bronnen vrijgemaakt die normaal worden gebruikt door ontwikkelingsmethoden in processen.

## Architectuur {#architecture}

In plaats van een out-of-the-box oplossing biedt Adobe Developer App Builder een algemeen, consistent en gestandaardiseerd ontwikkelingsplatform voor het uitbreiden van Adobe Cloud-oplossingen zoals Adobe Commerce, met inbegrip van:

* Adobe Developer Console wordt gebruikt voor de ontwikkeling van aangepaste microservices en extensies. Ontwikkel en beheer projecten terwijl de toegang tot van alle hulpmiddelen en APIs nodig om stoppen en integratie tot stand te brengen.
* Open-source-gereedschappen, SDK&#39;s en bibliotheken om aangepaste extensies en integratie te maken. Gebruik Spectrum Reageren (Adobe UI toolkit) om één gemeenschappelijke UI voor alle Adobe te hebben apps.
* services zoals I/O-runtime voor het hosten van infrastructuur op platformloze Adobe en I/O-gebeurtenissen voor op gebeurtenissen gebaseerde integratie. Adobe biedt ook out-of-the-box ondersteuning voor het opslaan van gegevens en bestanden.
* Adobe Experience Cloud waar u extensies en integratie verzendt die u wilt publiceren in uw Experience Cloud Org. Systeembeheerders kunnen deze extensies controleren, beheren en goedkeuren. Nadat u de aangepaste App Builder-extensies en -gereedschappen hebt gepubliceerd, zijn deze beschikbaar naast andere Adobe Experience Cloud-apps.

Het volgende diagram illustreert hoe een standaardtoepassing die op App Builder wordt gebouwd deze functionaliteit gebruikt:

![Architectuur](/help/assets/app-builder/firefly-architecture.jpeg)

Voor meer details over de architectuur van App Builder, zie [Overzicht van architectuur](https://developer.adobe.com/app-builder/docs/guides/).

## Amazon Sales Channel-extensie {#amazon-sales-channel-extension}

De volgende zelfstudies tonen hoe u Adobe Commerce met een App Builder-extensie kunt verbinden met Amazon Sales Channel.

* [technisch overzicht App Builder](../app-builder/app-builder-technical-overview.md)
* [uitbreidbaarheidskader](../app-builder/extensibility-framework-commerce-eventing.md)
* [functionele demonstratie App Builder](../app-builder/app-builder-functional-demonstration.md)

## Aan de slag met App Builder {#additional-resources}

Adobe heeft de volgende documentatie gemaakt om u te helpen aan de slag te gaan met App Builder:

* [Aan de slag met App Builder](https://developer.adobe.com/app-builder/docs/getting_started/)

## Doorgaan met leren met documentatie {#appbuilder-documentation}

App Builder biedt video&#39;s en documentatie voor ontwikkelaars, inclusief hulplijnen en documentatie voor naslagwerken om uw eigen aangepaste toepassingen te helpen ontwikkelen:

* [Documentatie voor App Builder](https://developer.adobe.com/app-builder/docs/overview/)
* [Video&#39;s over App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Een van de voorbeeldtoepassingen uitproberen {#appbuilder-codesamples}

Klaar om te beginnen met ontwikkelen? De volgende koppeling bevat voorbeeldtoepassingen waarmee u aan de slag kunt gaan:

* [Code-labels voor App Builder op de Adobe Developer-website](https://developer.adobe.com/app-builder/docs/resources/)

## Ondersteuning {#support}

Voor verzoeken om ontwikkelaarsondersteuning gebruikt u de [Forum Experience League](https://experienceleaguecommunities.adobe.com/t5/app-builder/ct-p/project-firefly) voor hulp.

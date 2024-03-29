---
title: Uitbreidbaarheid buiten proces voor Adobe Commerce
description: Leer over Adobe App Builder en waarom dit een belangrijk aspect is van uitbreidbaarheid zonder processen.
landing-page-description: Leer wat App Builder is en hoe het kan helpen met ontwikkelingsstrategieën voor Adobe Commerce.
short-description: Leer wat App Builder is en hoe het kan helpen met ontwikkelingsstrategieën voor Adobe Commerce.
kt: 11433
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-16
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 94f8d82a-4a95-46ea-8eed-edf9bed5760c
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 5%

---

# Inleiding tot App Builder

Adobe Commerce-ontwikkeling heeft in het verleden gebruikgemaakt van procesrekbaarheid. Het in-proces model vereist om het even welke nieuwe code om met verbeteringen, de PHP versie van de server, en vele andere essentiële servertoepassingen en de diensten compatibel te zijn die de Handel gebruikt. Adobe Developer App Builder maakt gebruik van externe uitbreidbaarheid om deze compatibiliteitsproblemen te voorkomen.

## App Builder voor Adobe Commerce {#app-builder}

>[!VIDEO](https://video.tv.adobe.com/v/3412839?quality=12&learn=on)

Adobe Developer App Builder is een serverloos uitbreidbaarheidsplatform voor het integreren en creëren van douaneervaringen om Adobe oplossingen uit te breiden, en het is nu beschikbaar voor Adobe Commerce. Met App Builder kunt u veilige en schaalbare apps maken die de eigen functies voor handel uitbreiden en integreren met oplossingen van derden. Als ontwikkelaar kunt u nu profiteren van de uitbreidbaarheid buiten het proces met Adobe Commerce en die op zijn beurt directe en langetermijnvoordelen biedt.

App Builder biedt een geïntegreerd extern uitbreidingsframework voor het integreren en maken van aangepaste toepassingen die een uitbreiding vormen [!DNL Adobe Commerce]. Aangezien dit uitbreidbaarheidskader is gebaseerd op de infrastructuur van de Adobe, kunnen ontwikkelaars aangepaste microservices bouwen en uitbreiden en integreren [!DNL Adobe Commerce] voor andere Adobe-oplossingen en integratie van derden.

App Builder biedt klanten een manier om de app uit te breiden [!DNL Adobe Commerce] in verschillende gebruiksgevallen:

* uitbreidbaarheid met middleware - Sluit externe systemen aan op Adobe-toepassingen door aangepaste connectors te maken of gebruik te maken van een reeks vooraf gebouwde integraties.
* de uitbreidbaarheid van de kerndiensten - breid kerntoepassingsmogelijkheden door het standaardgedrag met douaneeigenschappen en bedrijfslogica uit te breiden.
* uitbreidbaarheid van gebruikerservaring - breid kernervaring uit om bedrijfsvereisten te steunen of klant-specifieke digitale eigenschappen, opslagronts, en achterkantoortoepassingen te bouwen.

Adobe Developer App Builder is een cloudgebaseerde oplossing, wat betekent dat deze automatisch wordt geschaald. Deze service wordt ook wereldwijd gedistribueerd zodat u de beste prestaties kunt leveren, ongeacht uw geografische locatie.

## Waarom moet u meer weten over App Builder?

Aangezien Adobe Commerce geen volledig SAAS-product is, kan de code die u ontwikkelt, complexiteit en upgradeproblemen toevoegen. Door uit-van-procesrekbaarheid, zoals App Builder te gebruiken, kunt u douane, unieke functionaliteit aan uw opslag van Adobe Commerce verstrekken zonder in-proces methodes te vereisen.

Andere voordelen zijn:

* Dankzij de ontkoppelde functies is het sneller om te starten.
* Upgrades zijn nu eenvoudiger. De aangepaste functies bevinden zich buiten de handelsbalans, waardoor compatibiliteitsproblemen tijdens de upgrade worden voorkomen.
* Door functies en logica buiten de handel te verplaatsen, worden bronnen vrijgemaakt die normaal worden gebruikt door ontwikkelingsmethoden in processen.

## Architectuur {#architecture}

In plaats van een out-of-the-box oplossing biedt Adobe Developer App Builder een algemeen, consistent en gestandaardiseerd ontwikkelingsplatform voor het uitbreiden van Adobe Cloud-oplossingen zoals Adobe Commerce, met inbegrip van:

* Adobe Developer Console wordt gebruikt voor de ontwikkeling van aangepaste microservices en extensies. Ontwikkel en beheer projecten terwijl de toegang tot van alle hulpmiddelen en APIs nodig om stoppen en integratie tot stand te brengen.
* Open-source-gereedschappen, SDK&#39;s en bibliotheken om aangepaste extensies en integratie te maken. Gebruik React Spectrum (UI toolkit van Adobe) om één gemeenschappelijke UI voor alle Adobe apps te hebben.
* services zoals I/O-runtime voor het hosten van infrastructuren op het serverplatform van de Adobe en I/O-gebeurtenissen voor op gebeurtenissen gebaseerde integratie. Adobe biedt ook out-of-the-box ondersteuning voor het opslaan van gegevens en bestanden.
* Adobe Experience Cloud waar u extensies en integratie verzendt die u wilt publiceren in uw Experience Cloud Org. Systeembeheerders kunnen deze extensies controleren, beheren en goedkeuren. Nadat u de aangepaste App Builder-extensies en -gereedschappen hebt gepubliceerd, zijn deze beschikbaar naast andere Adobe Experience Cloud-apps.

Het volgende diagram illustreert hoe een standaardtoepassing die op App Builder wordt gebouwd deze functionaliteit gebruikt:

![Architectuur](/help/assets/app-builder/app-builder-architecture.jpeg)

Voor meer details over de architectuur van App Builder, zie [Overzicht van architectuur](https://developer.adobe.com/app-builder/docs/guides/){target="_blank"}.

## Amazon Sales Channel-extensie {#amazon-sales-channel-extension}

>[!IMPORTANT]
>
>De verlenging van de Sales Channel van Amazon is nog in ontwikkeling en is nog niet officieel vrijgegeven.  Deze video&#39;s en zelfstudies zijn bedoeld om u te laten zien hoe u Adobe Developer App Builder kunt gebruiken voor een praktijkvoorbeeld.

De volgende zelfstudies tonen hoe u Adobe Commerce kunt verbinden met een Amazon-Sales Channel met een App Builder-extensie.

* [technisch overzicht App Builder](../app-builder/app-builder-technical-overview.md)
* [uitbreidbaarheidskader](../app-builder/extensibility-framework-commerce-eventing.md)
* [functionele demonstratie App Builder](../app-builder/app-builder-functional-demonstration.md)

## Aan de slag met App Builder {#additional-resources}

Een overzicht van de composable commerce strategie, die de aanvankelijke opstelling omvat, kan door het volgende blogbericht te lezen worden gevonden:

[Hoe de Hulp van de Bouwer van de App zaken behendigheid voor uw handelsplatform drijft](https://business.adobe.com/blog/how-to/how-app-builder-helps-you-implement-a-composable-commerce-strategy){target="_blank"}

Adobe heeft de volgende documentatie gemaakt om u te helpen aan de slag te gaan met App Builder:

* [Aan de slag met App Builder](https://developer.adobe.com/app-builder/docs/getting_started/){target="_blank"}

## Doorgaan met leren met documentatie {#appbuilder-documentation}

App Builder biedt video&#39;s en documentatie voor ontwikkelaars, inclusief hulplijnen en documentatie voor naslagwerken om uw eigen aangepaste toepassingen te helpen ontwikkelen:

* [Documentatie voor App Builder](https://developer.adobe.com/app-builder/docs/overview/){target="_blank"}
* [Video&#39;s over App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o){target="_blank"}

## Een van de voorbeeldtoepassingen uitproberen {#appbuilder-codesamples}

Klaar om te beginnen met ontwikkelen? De volgende koppeling bevat voorbeeldtoepassingen waarmee u aan de slag kunt gaan:

* [Code-labels voor App Builder op de Adobe Developer-website](https://developer.adobe.com/app-builder/docs/resources/){target="_blank"}

## Ondersteuning {#support}

Voor verzoeken om ontwikkelaarsondersteuning gebruikt u de [Forum Experience League](https://experienceleaguecommunities.adobe.com/t5/app-builder/ct-p/project-firefly){target="_blank"} voor hulp.

{{$include /help/_includes/app-builder-related-links.md}}

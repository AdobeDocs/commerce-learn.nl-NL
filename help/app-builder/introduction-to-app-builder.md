---
title: Uitbreidbaarheid buiten proces voor Adobe Commerce
description: Meer informatie over Adobe App Builder en waarom dit een belangrijk aspect is van de uitbreidbaarheid zonder processen.
landing-page-description: Leer wat app builder is en hoe het kan helpen met Adobe Commerce-ontwikkelingsstrategieën.
kt: 11433
doc-type: tutorial
audience: all
last-substantial-update: 2023-01-11T00:00:00Z
source-git-commit: ef0fa95e776b97ddbaf30e0acd1340e30f12738f
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---


# Buiten-de-procesrekbaarheid

Adobe Commerce is historisch ontwikkeld met dezelfde opslagplaats als de hoofdtoepassing.  Dit wordt tijdens het proces genoemd.  Deze techniek is zeer goed en biedt de ontwikkelaar een verwacht mechanisme voor het uitbreiden van de toepassing.  Dat is echter een prijskaartje.  Telkens wanneer u nieuwe code aan codebase toevoegt moet het met om het even welke verbeteringen compatibel zijn.  U moet ook compatibel zijn met de servers PHP versie evenals vele andere servertoepassingen en de diensten die de handel zal gebruiken.  Adobe Developer App Builder voldoet aan dezelfde vereisten voor het uitbreiden van de functionaliteit, maar verplaatst deze van de site.  De code en de logica zijn volledig extern en deze methode wordt bedoeld als out-of-process.

## App Builder voor Adobe Commerce {#project-firefly}

>[!VIDEO](https://video.tv.adobe.com/v/3412839)

Adobe Developer App Builder biedt ontwikkelaars een uitbreidbaarheidskader om [!DNL Adobe Commerce] om uit-van-procesrekbaarheid te verstrekken.

App Builder biedt een geïntegreerd extern uitbreidingsframework voor het integreren en maken van aangepaste toepassingen die een uitbreiding vormen [!DNL Adobe Commerce]. Aangezien dit uitbreidbaarheidskader op Adobe infrastructuur wordt gebouwd, kunnen de ontwikkelaars douanemicrodiensten bouwen evenals uitbreiden en integreren [!DNL Adobe Commerce] voor Adobe-oplossingen en andere integratie van derden.

App Builder biedt klanten een manier om de app uit te breiden [!DNL Adobe Commerce] in verschillende gebruiksgevallen:

* uitbreidbaarheid met middleware - Sluit externe systemen aan op Adobe-toepassingen door aangepaste connectors te maken of gebruik te maken van een reeks vooraf gebouwde integraties.
* de uitbreidbaarheid van de kerndiensten - breid kerntoepassingsmogelijkheden door het standaardgedrag met douaneeigenschappen en bedrijfslogica uit te breiden.
* uitbreidbaarheid van gebruikerservaring - breid kernervaring uit om bedrijfsvereisten te steunen of klant-specifieke digitale eigenschappen, opslagronts, en achterkantoortoepassingen te bouwen.

App Builder (voorheen bekend als Project Firefly) is een cloudgebaseerde oplossing, wat betekent dat deze automatisch wordt geschaald. Deze service wordt ook wereldwijd gedistribueerd zodat u de beste prestaties kunt leveren, ongeacht uw geografische locatie.

## Waarom moet u meer weten over App Builder

Aangezien Adobe Commerce geen volledig SAAS is, kan de code die u ontwikkelt of installeert complexiteit toevoegen en upgradeproblemen veroorzaken. Door gebruik te maken van externe uitbreidbaarheid, zoals App Builder, kunt u uw Adobe Commerce-winkel aangepaste, unieke functionaliteit bieden zonder dat procesmethoden vereist zijn.

Andere voordelen zijn:

* Dankzij de ontkoppelde functies is het sneller om te starten.
* Upgrades zijn nu eenvoudiger. De douanefuncties zijn buiten de handelscodebase, die verenigbaarheidskwesties wanneer bevordering verhindert.
* Als u functies en logica buiten de handel verplaatst, maakt u bronnen die normaal worden gebruikt door ontwikkelingsmethoden in processen.

## Architectuur {#architecture}

In plaats van een out-of-the-box oplossing biedt Adobe Developer App Builder een algemeen, consistent en gestandaardiseerd ontwikkelingsplatform voor het uitbreiden van Adobe Cloud-oplossingen zoals Adobe Commerce, met inbegrip van:

* Adobe Developer Console wordt gebruikt voor de ontwikkeling van aangepaste microservices en extensies. Ontwikkel en beheer projecten terwijl de toegang tot van alle hulpmiddelen en APIs nodig om stoppen en integratie tot stand te brengen.
* Open-source-gereedschappen, SDK&#39;s en bibliotheken om aangepaste extensies en integratie te maken. Gebruik Spectrum Reageren (Adobe UI toolkit) om één gemeenschappelijke UI voor alle Adobe te hebben apps.
* services zoals I/O-runtime voor het hosten van infrastructuur op platformloze Adobe en I/O-gebeurtenissen voor op gebeurtenissen gebaseerde integratie. Adobe biedt ook out-of-the-box ondersteuning voor het opslaan van gegevens en bestanden.
* Adobe Experience Cloud waar u extensies en integratie verzendt die u wilt publiceren in uw Experience Cloud Org. Systeembeheerders kunnen deze extensies controleren, beheren en goedkeuren. Nadat u de aangepaste App Builder-extensies en -gereedschappen hebt gepubliceerd, zijn deze beschikbaar naast andere Adobe Experience Cloud-apps.

Het volgende diagram illustreert hoe een standaardtoepassing die op App Builder wordt gebouwd deze functionaliteit gebruikt:

![Architectuur](/help/assets/app-builder/firefly-architecture.jpeg)

Voor meer details over de architectuur van App Builder, zie [Overzicht van architectuur](https://developer.adobe.com/app-builder/docs/guides/).

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


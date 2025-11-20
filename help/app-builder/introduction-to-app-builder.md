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
source-git-commit: 241f99eaed68488b952e8ed76186499ca1a20417
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 6%

---

# Inleiding tot App Builder

Adobe Commerce-ontwikkeling heeft in het verleden gebruikgemaakt van procesrekbaarheid. Het in-process model vereist om het even welke nieuwe code compatibel te zijn met verbeteringen, de PHP versie van de server, en vele andere essentiële servertoepassingen en de diensten die Commerce gebruikt. Adobe Developer App Builder maakt gebruik van externe uitbreidbaarheid om deze compatibiliteitsproblemen te voorkomen.

## App Builder voor Adobe Commerce {#app-builder}

>[!VIDEO](https://video.tv.adobe.com/v/3412839?quality=12&learn=on)

Adobe Developer App Builder is een serverloos uitbreidbaarheidsplatform voor het integreren en creëren van aangepaste ervaringen om Adobe-oplossingen uit te breiden. Het is nu beschikbaar voor Adobe Commerce. Met App Builder kunt u veilige en schaalbare toepassingen maken die de eigen Commerce-functionaliteit uitbreiden en integreren met oplossingen van derden. Als ontwikkelaar kunt u nu profiteren van de uitbreidbaarheid buiten het proces met Adobe Commerce en die op zijn beurt directe en langetermijnvoordelen biedt.

App Builder biedt een geïntegreerd extern uitbreidingsframework voor het integreren en maken van aangepaste toepassingen die [!DNL Adobe Commerce] uitbreiden. Aangezien dit uitbreidingsframework is gebaseerd op de Adobe-infrastructuur, kunnen ontwikkelaars aangepaste microservices bouwen en [!DNL Adobe Commerce] uitbreiden en integreren in andere Adobe-oplossingen en integratie met andere bedrijven.

App Builder biedt klanten een manier om [!DNL Adobe Commerce] in verschillende gebruiksgevallen uit te breiden:

* uitbreidbaarheid met middleware - Sluit externe systemen aan op Adobe-toepassingen door aangepaste connectors te maken of gebruik te maken van een reeks vooraf gebouwde integraties.
* de uitbreidbaarheid van de kerndiensten - breid kerntoepassingsmogelijkheden door het standaardgedrag met douaneeigenschappen en bedrijfslogica uit te breiden.
* uitbreidbaarheid van gebruikerservaring - breid kernervaring uit om bedrijfsvereisten te steunen of klant-specifieke digitale eigenschappen, opslagronts, en achterkantoortoepassingen te bouwen.

Adobe Developer App Builder is een cloudgebaseerde oplossing, wat betekent dat deze automatisch wordt geschaald. Deze service wordt ook wereldwijd gedistribueerd zodat u de beste prestaties kunt leveren, ongeacht uw geografische locatie.

## Waarom moet je meer weten over App Builder?

Aangezien Adobe Commerce geen volledig SAAS-product is, kan de code die u ontwikkelt, complexiteit en upgradeproblemen toevoegen. Door gebruik te maken van externe uitbreidbaarheid, zoals App Builder, kunt u uw Adobe Commerce-winkel aangepaste, unieke functionaliteit bieden zonder dat hiervoor procesmethoden nodig zijn.

Andere voordelen zijn:

* Dankzij de ontkoppelde functies is het sneller om te starten.
* Upgrades zijn nu eenvoudiger. De aangepaste functies bevinden zich buiten de Commerce-codebase, waardoor compatibiliteitsproblemen tijdens de upgrade worden voorkomen.
* Als u functies en logica buiten Commerce verplaatst, maakt u bronnen die normaal worden gebruikt door ontwikkelmethoden in processen.

## Architectuur {#architecture}

Adobe Developer App Builder biedt in plaats van een out-of-the-box oplossing een gemeenschappelijk, consistent en gestandaardiseerd ontwikkelingsplatform voor het uitbreiden van Adobe Cloud-oplossingen zoals Adobe Commerce, met inbegrip van:

* Adobe Developer Console wordt gebruikt voor de ontwikkeling van aangepaste microservices en extensies. Ontwikkel en beheer projecten terwijl de toegang tot van alle hulpmiddelen en APIs nodig om stoppen en integratie tot stand te brengen.
* Open-source-gereedschappen, SDK&#39;s en bibliotheken om aangepaste extensies en integratie te maken. Gebruik de React Spectrum (de toolkit van de UI van Adobe) om één gemeenschappelijke UI voor alle Adobe apps te hebben.
* services zoals I/O-runtime voor het hosten van infrastructuur op Adobe Server-serverplatform en I/O-gebeurtenissen voor op gebeurtenissen gebaseerde integratie. Adobe biedt ook offline ondersteuning voor het opslaan van gegevens en bestanden.
* Adobe Experience Cloud waar u extensies en integratie verzendt die u wilt publiceren in uw Experience Cloud Org. Systeembeheerders kunnen deze extensies controleren, beheren en goedkeuren. Nadat u de aangepaste App Builder-extensies en -gereedschappen hebt gepubliceerd, zijn deze beschikbaar naast andere Adobe Experience Cloud-apps.

In het volgende diagram ziet u hoe een standaardtoepassing die op App Builder is gebouwd deze functies gebruikt:

![&#x200B; Architectuur &#x200B;](/help/assets/app-builder/app-builder-architecture.jpeg)

Voor meer details over de architectuur van App Builder, zie het [&#x200B; Overzicht van de Architectuur &#x200B;](https://developer.adobe.com/app-builder/docs/guides/){target="_blank"}.

## Aan de slag met App Builder {#additional-resources}

Een overzicht van de composable commerce strategie, die de aanvankelijke opstelling omvat, kan door het volgende blogbericht te lezen worden gevonden:

[&#x200B; Hoe de hulp van App Builder bedrijfs behendigheid voor uw handelsplatform &#x200B;](https://business.adobe.com/blog/how-to/how-app-builder-helps-you-implement-a-composable-commerce-strategy){target="_blank"} drijft

Adobe heeft de volgende documentatie gemaakt om u te helpen aan de slag te gaan met App Builder:

* [&#x200B; Aan de slag App Builder &#x200B;](https://developer.adobe.com/app-builder/docs/getting_started/){target="_blank"}

## Doorgaan met leren met documentatie {#appbuilder-documentation}

App Builder biedt video&#39;s en documentatie voor ontwikkelaars, waaronder handleidingen en documentatie voor naslagwerken om uw eigen aangepaste toepassingen te helpen ontwikkelen:

* [&#x200B; documentatie van App Builder &#x200B;](https://developer.adobe.com/app-builder/docs/overview/){target="_blank"}
* [&#x200B; de video&#39;s van App Builder &#x200B;](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o){target="_blank"}

## Een van de voorbeeldtoepassingen uitproberen {#appbuilder-codesamples}

Klaar om te beginnen met ontwikkelen? De volgende koppeling bevat voorbeeldtoepassingen waarmee u aan de slag kunt gaan:

* [&#x200B; de Etiketten van de Code van App Builder op de Website van Adobe Developer &#x200B;](https://developer.adobe.com/app-builder/docs/resources/){target="_blank"}

## Ondersteuning {#support}

Voor de verzoeken van de ontwikkelaarsteun, gebruik het [&#x200B; forum van Experience League &#x200B;](https://experienceleaguecommunities.adobe.com/t5/app-builder/ct-p/project-firefly){target="_blank"} voor hulp.

{{$include /help/_includes/app-builder-related-links.md}}

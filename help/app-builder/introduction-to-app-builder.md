---
title: Uitbreiding buiten het proces voor Adobe commerce
description: Meer informatie over Adobe app Builder en waarom het een belangrijk aspect is van de uitbreidbaarheid buiten het proces.
landing-page-description: Leer wat is app Builder en hoe u dit kunt helpen bij Adobe commerce-Ontwikkel strategieën.
short-description: Ontdek wat App Builder is en hoe dit kan helpen met Adobe Commerce-ontwikkelingsstrategieën.
kt: 11433
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-16T00:00:00Z
exl-id: 94f8d82a-4a95-46ea-8eed-edf9bed5760c
source-git-commit: edb98cf6544954d741c43beb39f4056326c7d26b
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 0%

---

# Inleiding tot App Builder

Adobe Commerce-ontwikkeling heeft altijd gebruikgemaakt van procesrekbaarheid. Het in-proces model vereist om het even welke nieuwe code om met verbeteringen, de PHP versie van de server, en vele andere essentiële servertoepassingen en de diensten compatibel te zijn die de Handel gebruikt. Adobe Developer App Builder maakt gebruik van externe uitbreidbaarheid om deze compatibiliteitsproblemen te voorkomen.

## App Builder voor Adobe Commerce {#app-builder}

>[!VIDEO](https://video.tv.adobe.com/v/3412839?quality=12&learn=on)

Adobe Developer App Builder is een serverloos uitbreidbaarheidsplatform voor het integreren en maken van aangepaste ervaringen voor het uitbreiden van Adobe-oplossingen. Het is nu beschikbaar voor Adobe Commerce. Met App Builder kunt u veilige en schaalbare apps maken die de eigen functies van Commerce uitbreiden en integreren met oplossingen van derden. Als ontwikkelaar kunt u nu profiteren van de uitbreidbaarheid van buiten het proces met Adobe Commerce en die op zijn beurt directe en langdurige voordelen biedt.

App Builder biedt een geïntegreerd uitbreidbaarheidsframework van derden voor het integreren en maken van aangepaste toepassingen die [!DNL Adobe Commerce]. Omdat dit uitbreidbaarheidsframework is gebaseerd op Adobe-infrastructuur, kunnen ontwikkelaars aangepaste microservices bouwen en deze uitbreiden en integreren [!DNL Adobe Commerce] voor andere Adobe-oplossingen en externe integraties.

App Builder biedt klanten een manier om de [!DNL Adobe Commerce] in verschillende gebruiksgevallen :

* uitbreidbaarheid van middleware - Verbind externe systemen met Adobe-toepassingen door aangepaste connectoren te bouwen of profiteer van een suite van vooraf gebouwde integraties.
* uitbreidbaarheid van kernservices - Breid de kerntoepassingsmogelijkheden uit door het standaardgedrag uit te breiden met aangepaste functies en bedrijfslogica.
* uitbreidbaarheid van gebruikerservaring – Breid de kern ervaring uit om bedrijfsvereisten te ondersteunen of om klantspecifieke digitale eigenschappen, webwinkels en back-uptoepassingen te ontwikkelen.

Adobe Developer app Builder is een op de cloud gebaseerde oplossing, wat inhoudt dat deze automatisch wordt geschaald. Deze service wordt ook overal gedistribueerd om de beste prestaties te bieden, ongeacht de geografische locatie.

## Waarom zou je meer te weten komen over app Builder

Omdat Adobe commerce geen volledig SAAS-product is, kunt u met de code die u ontwikkelt, complexiteits-en upgrade problemen toevoegen. Door out-of-process-uitbreidbaarheid te gebruiken, zoals app Builder, kunt u aan uw Adobe commerce store een aangepaste, unieke functionaliteit aanbieden zonder in-process-methoden te vereisen.

Andere voordelen zijn:

* Met losgekoppelde functies duurt het sneller starten van het opstarten.
* Upgrades zijn nu eenvoudiger. De aangepaste functies bevinden zich buiten de commerce-code voor handel, waardoor compatibiliteitsproblemen worden voorkomen tijdens de upgrade.
* Door functies en logica buiten commerce te verplaatsen maakt u bronnen beschikbaar die normaalgesproken worden gebruikt door in-process ontwikkel methoden.

## Architecture {#architecture}

In plaats van een kant-en-klare oplossing biedt Adobe Developer App Builder een algemeen, consistent en gestandaardiseerd ontwikkelplatform voor het uitbreiden van Adobe Cloud-oplossingen zoals Adobe Commerce, inclusief:

* Adobe Developer Console wordt gebruikt voor de ontwikkeling van aangepaste microservices en extensies. Bouw en beheer projecten met alle tools en API’s die nodig zijn om plug-ins en integraties te maken.
* Open-source-gereedschappen, SDK&#39;s en bibliotheken om aangepaste extensies en integratie te maken. Gebruik Spectrum Reageren (Adobe UI toolkit) om één gemeenschappelijke UI voor alle Adobe te hebben apps.
* services zoals I/O-runtime voor het hosten van infrastructuur op platformloze Adobe en I/O-gebeurtenissen voor op gebeurtenissen gebaseerde integratie. Adobe biedt ook out-of-the-box ondersteuning voor het opslaan van gegevens en bestanden.
* Adobe Experience Cloud waar u extensies en integraties verzendt die u wilt publiceren in uw Experience Cloud Org. Systeembeheerders kunnen deze extensies reviseren, beheren en goedkeuren. Na publicatie zijn uw aangepaste App Builder-extensies en -gereedschappen beschikbaar naast andere Adobe Experience Cloud-apps.

In het volgende diagram ziet u hoe een standaardtoepassing die is ontwikkeld met App Builder deze functies gebruikt:

![Architectuur](/help/assets/app-builder/app-builder-architecture.jpeg)

Voor meer informatie over de App Builder-architectuur raadpleegt u de [Overzicht van architectuur](https://developer.adobe.com/app-builder/docs/guides/){target="_blank"}.

## Amazon Sales Channel-extensie {#amazon-sales-channel-extension}

>[!IMPORTANT]
>
>De uitbreiding van het Amazon-verkoopkanaal verloopt nog steeds in ontwikkeling en is niet officieel uitgebracht.  Deze Video&#39;s en zelfstudies zijn bedoeld om je te laten zien hoe je de Adobe Developer app Builder gebruikt voor een praktische gebruiks transactie.

De volgende zelfstudies tonen hoe u Adobe Commerce kunt verbinden met het verkoopkanaal van Amazon met behulp van een app Builder-extensie.

* [technische overzicht van de app-overzichtsfunctie](../app-builder/app-builder-technical-overview.md)
* [uitbreidbare Framework](../app-builder/extensibility-framework-commerce-eventing.md)
* [functie voor het maken van functionele demonstratie-apps](../app-builder/app-builder-functional-demonstration.md)

## Aan de slag met de app Builder {#additional-resources}

Een overzicht van composable commerce strategy, die de eerste opzet bevat, is te vinden door het volgende blogbericht te lezen:

[Hoe de Hulp van de Bouwer van de App zaken behendigheid voor uw handelsplatform drijft](https://business.adobe.com/blog/how-to/how-app-builder-helps-you-implement-a-composable-commerce-strategy){target="_blank"}

Adobe heeft de volgende documentatie gemaakt om u te helpen aan de slag te gaan met App Builder:

* [Aan de slag met App Builder](https://developer.adobe.com/app-builder/docs/getting_started/){target="_blank"}

## Doorgaan met leren met documentatie {#appbuilder-documentation}

App Builder biedt video&#39;s en documentatie voor ontwikkelaars, inclusief handleidingen en documentatie met naslaginformatie om uw eigen aangepaste toepassingen te helpen ontwikkelen:

* [Documentatie App Builder](https://developer.adobe.com/app-builder/docs/overview/){target="_blank"}
* [Video&#39;s over App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o){target="_blank"}

## Een van de voorbeeldtoepassingen uitproberen {#appbuilder-codesamples}

Klaar voor ontwikkeling? De volgende koppeling bevat voorbeeldtoepassingen om u te helpen aan de slag te gaan:

* [App Builder code Labs op de website van Adobe Developer](https://developer.adobe.com/app-builder/docs/resources/){target="_blank"}

## Niet {#support}

Voor ondersteuningsaanvragen voor ontwikkelaars kunt u het [ competitie forum ](https://experienceleaguecommunities.adobe.com/t5/app-builder/ct-p/project-firefly) {target="_blank"} van Experience gebruiken voor hulp.

{{$include /help/_includes/app-builder-related-links.md}}

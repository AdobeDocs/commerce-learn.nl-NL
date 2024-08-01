---
title: Meer informatie over de Commerce Integration Starter Kit met belangrijke mappen en automatiseringsscripts
description: Meer informatie over de organisatie van broncode in de startkit voor Commerce Integration. ​
landing-page-description: Source Code Organization verkennen in een Commerce Integration Starter Kit
kt: 15868
doc-type: video
duration: 420
audience: all
last-substantial-update: 2024-7-30
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
role: Architect, Developer
level: Intermediate
source-git-commit: 11daa4b29dafe5fcecf6b75cf2269b87f65c4612
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# Source-code-organisatie voor de Adobe Starter Kit

Meer informatie over de organisatie van de broncode in de Adobe Commerce Integration starter kit. &#x200B; Onderzoek de structuur van het project, en benadruk zeer belangrijke omslagen zoals `actions` en `scripts`, en hun respectieve inhoud. &#x200B; De map &#39;actions&#39; bevat submappen zoals `ingestion` en `webhook` die essentiële code bevatten voor gebeurtenisafhandeling en -tracking. U leert ook meer over de mappen `starter-kit-info` en `scripts` . De map `scripts` richt zich op automatiseringsscripts zoals `commerce-event-subscribe` en `onboarding` die de configuratie van gebeurtenissen en de instellingen van de provider in het project stroomlijnen.
&#x200B;
Ontdek de logica achter de broncodestructuur en geef in detail aan hoe de mappen `commerce` en `external` in elke entiteitsmap gebeurtenissen verwerken die afkomstig zijn van verschillende systemen. In de video wordt uitgelegd wat de rol is van de map `consumer` bij het verzenden van gebeurtenissen naar de juiste runtimeactie van de gebeurtenishandler, zodat de verwerking naadloos verloopt. De video behandelt ook het mechanisme voor het opnieuw proberen dat in de runtimeacties wordt geïmplementeerd om mislukte gebeurtenissen effectief af te handelen. &#x200B;Begrijp de organisatie en de functionaliteit van broncode in de starter kit van de Integratie van Adobe Commerce, die waardevolle inzichten in gebeurtenisbehandeling, automatiseringsmanuscripten, en configuratiemontages aanbieden.

## Publiek

* Ontwikkelaars die willen begrijpen hoe de broncode wordt ingedeeld in sleutelmappen, zoals `actions` en `scripts` .
* Meer informatie over de map `actions` bevat submappen zoals `ingestion` en ` webhook` die essentiële code bevatten voor het afhandelen van gebeurtenissen en het bijhouden van implementaties.
* Ontwikkelaars die meer willen weten over de map `actions` die mappen bevat voor entiteiten zoals `customer` , `order` , `product` en `stock` .

## Video-inhoud

* Begrijp dat de vier hoofdmappen: `actions`, `scripts`, `test` en `utils` , met focus op de mappen `actions` en `scripts` tijdens de sessie. &#x200B;
* Leer meer over de map `actions` en hoe deze belangrijke submappen bevat, zoals `ingestion` en `webhook` .
* Ontdek de map `actions` en waarom er specifieke mappen zijn voor entiteiten zoals `customer` , `order` , `product` en `stock` , elk met runtimeacties die zijn gestructureerd in `commerce` - en `external` -mappen om gebeurtenissen van Commerce en systemen van derden effectief te beheren. &#x200B;
* Leer het belang om de code in de `starter-kit-info` omslag niet te veranderen, die een runtime actie bevat die door Adobe wordt gebruikt om projectplaatsingen te volgen die op de startuitrusting worden gebaseerd. &#x200B;
* Begrijp de `scripts` -map die automatiseringsscripts zoals `commerce-event-subscribe` en `onboarding` bevat, die gebeurtenisconfiguratie, leveranciersinstellingen en de configuratie van de Adobe I/O Events-module in Commerce automatiseren. &#x200B;

  >[!VIDEO](https://video.tv.adobe.com/v/3431691?learn=on)

  {{$include /help/_includes/starter-kit-related-links.md}}
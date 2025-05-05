---
title: De native functionaliteit van een Retriemechanisme gebruiken
description: Gebruik Adobe I/O Events' retry mechanism voor veerkrachtige toepassingen, inclusief retry conditions en visual indicators.
landing-page-description: Begrijp en gebruik het ingebouwde mechanisme van Adobe I/O Events opnieuw proberen om toepassingsveerkracht te verbeteren en gebeurtenisactiveringen effectief te beheren.
kt: 15872
doc-type: video
duration: 314
audience: all
last-substantial-update: 2024-7-31
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
role: Architect, Developer
level: Intermediate
source-git-commit: eb548dd83e3bab7a4a1486cd2cbd88efcc060121
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# Adobe I/O Events opnieuw uitproberen van de hefboomwerking voor toepassingsveerkracht

In de video wordt een uitgebreide handleiding beschreven voor het gebruik van het ingebouwde heruitzettingsmechanisme van Adobe I/O Events om de veerkracht van de toepassing te verbeteren. Leer hoe specifieke HTTP-antwoordstatuscodes gebeurtenispogingen activeren. Adobe I/O Events maakt gebruik van exponentiële en vaste back-offstrategieën voor nieuwe pogingen, waarbij de intervallen van 1 minuut tot 15 minuten toenemen. In de documentatie wordt ook beschreven hoe hertry-indicatoren worden weergegeven in de ontwikkelaarsconsole, met visuele aanwijzingen zoals waarschuwingspictogrammen en cirkelvormige pijlen die mislukte en opnieuw beproefde gebeurtenissen aangeven.

Leer hoe het mechanisme voor opnieuw proberen functioneert binnen de context van de acties bij &#39;consumer&#39;-runtime en bepaal of een gebeurtenis opnieuw wordt geprobeerd. Succesvolle reacties worden aangegeven met een statuscode van 200, terwijl foutreacties een foutobject met het kenmerk &#39;statusCode&#39; bevatten. De runtimeactie &#39;consumer&#39; bepaalt de HTTP-antwoordcode die moet worden geretourneerd op basis van downstreamverwerkingsresultaten, waardoor een efficiënte gebeurtenisafhandeling en eventuele succesvolle activeringen worden gegarandeerd.

## Publiek

* Ontwikkelaars die de specifieke HTTP-antwoordstatuscodes willen begrijpen die gebeurtenispogingen activeren.
* Teams die willen leren over de exponentiële en vaste back-offstrategieën die worden gebruikt door Adobe I/O Events voor retry.
* Ontwikkelaars die willen begrijpen hoe visuele indicatoren in de ontwikkelaarsconsole ontbroken en opnieuw geprobeerd gebeurtenissen vertegenwoordigen.

## Video-inhoud

* Adobe I/O Gebeurtenissen hebben een ingebouwd out-of-the-box retry mechanisme dat automatisch gebeurtenisactiveringen herprobeert die op specifieke de statuscodes van de HTTP- reactie worden gebaseerd.
* Het door Adobe I/O Events uitgevoerde hertestmechanisme omvat exponentiële en vaste back-upstrategieën.
* Visuele indicatoren in de ontwikkelaarsconsole, zoals waarschuwingspictogrammen voor ontbroken gebeurtenissen en cirkelpijlpictogrammen voor opnieuw geprobeerd gebeurtenissen.
* De runtimeacties van de &#39;consument&#39; spelen een cruciale rol bij het bepalen van de juiste statuscodes voor HTTP-reacties voor gebeurtenisafhandeling.

>[!VIDEO](https://video.tv.adobe.com/v/3449079?learn=on&captions=dut)

{{$include /help/_includes/starter-kit-related-links.md}}

## Gerelateerde documentatie

* [ Webhaak kan een gebeurtenis niet behandelen ](https://developer.adobe.com/events/docs/support/faq/#what-happens-if-my-webhook-is-unable-to-handle-a-specific-event-but-handles-all-other-events-gracefully)
* [ WebHaak neer en duidelijk als instabiel ](https://developer.adobe.com/events/docs/support/faq/#what-happens-if-my-webhook-is-down-why-is-my-event-registration-marked-as-unstable)

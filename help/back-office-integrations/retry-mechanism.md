---
title: De native functionaliteit van een Retriemechanisme gebruiken
description: Gebruik Adobe I/O Events's retry-mechanisme voor veerkrachtige toepassingen, inclusief hertestomstandigheden en visuele indicatoren.
landing-page-description: Begrijp en gebruik het ingebouwde mechanisme voor het opnieuw proberen van Adobe I/O Events om de veerkracht van de toepassing te verbeteren en gebeurtenisactiveringen effectief te beheren.
kt: 15872
doc-type: video
duration: 314
audience: all
last-substantial-update: 2024-7-31
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
old-role: Architect, Developer
role: Developer
level: Intermediate
exl-id: 412060b3-76ae-4c27-bf96-8eb2a0f0d0e8
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# Adobe I/O Events-mechanisme voor opnieuw proberen gebruiken voor de veerkracht van toepassingen

In de video wordt een uitgebreide handleiding gegeven over het gebruik van het ingebouwde hertestmechanisme van Adobe I/O Events om de veerkracht van toepassingen te verbeteren. Leer hoe specifieke HTTP-antwoordstatuscodes gebeurtenispogingen activeren. Adobe I/O Events hanteert exponentiële en vaste back-upstrategieën voor herpogingen, waarbij de intervallen van 1 minuut tot 15 minuten toenemen. In de documentatie wordt ook beschreven hoe hertry-indicatoren worden weergegeven in de ontwikkelaarsconsole, met visuele aanwijzingen zoals waarschuwingspictogrammen en cirkelvormige pijlen die mislukte en opnieuw beproefde gebeurtenissen aangeven.

Leer hoe het mechanisme voor opnieuw proberen functioneert binnen de context van de acties bij &#39;consumer&#39;-runtime en bepaal of een gebeurtenis opnieuw wordt geprobeerd. Succesvolle reacties worden aangegeven met een statuscode van 200, terwijl foutreacties een foutobject met het kenmerk &#39;statusCode&#39; bevatten. De runtimeactie &#39;consumer&#39; bepaalt de HTTP-antwoordcode die moet worden geretourneerd op basis van downstreamverwerkingsresultaten, waardoor een efficiënte gebeurtenisafhandeling en eventuele succesvolle activeringen worden gegarandeerd.

## Publiek

* Ontwikkelaars die de specifieke HTTP-antwoordstatuscodes willen begrijpen die gebeurtenispogingen activeren.
* Teams die willen leren over de exponentiële en vaste back-offstrategieën die Adobe I/O Events gebruikt voor herpogingen.
* Ontwikkelaars die willen begrijpen hoe visuele indicatoren in de ontwikkelaarsconsole ontbroken en opnieuw geprobeerd gebeurtenissen vertegenwoordigen.

## Video-inhoud

* Adobe I/O Events heeft een ingebouwd out-of-the-box mechanisme voor opnieuw proberen dat automatisch gebeurtenisactiveringen herprobeert op basis van specifieke HTTP-antwoordstatuscodes.
* Het door Adobe I/O Events ingevoerde hertestmechanisme omvat exponentiële en vaste back-upstrategieën.
* Visuele indicatoren in de ontwikkelaarsconsole, zoals waarschuwingspictogrammen voor ontbroken gebeurtenissen en cirkelpijlpictogrammen voor opnieuw geprobeerd gebeurtenissen.
* De runtimeacties van de &#39;consument&#39; spelen een cruciale rol bij het bepalen van de juiste statuscodes voor HTTP-reacties voor gebeurtenisafhandeling.

>[!VIDEO](https://video.tv.adobe.com/v/3431695?learn=on)

{{$include /help/_includes/starter-kit-related-links.md}}

## Gerelateerde documentatie

* [&#x200B; Webhaak kan een gebeurtenis niet behandelen &#x200B;](https://developer.adobe.com/events/docs/support/faq/#what-happens-if-my-webhook-is-unable-to-handle-a-specific-event-but-handles-all-other-events-gracefully)
* [&#x200B; WebHaak neer en duidelijk als instabiel &#x200B;](https://developer.adobe.com/events/docs/support/faq/#what-happens-if-my-webhook-is-down-why-is-my-event-registration-marked-as-unstable)

---
title: Inleiding GraphQL
description: Meer informatie over het gebruik van GraphQL op Adobe Commerce en [!DNL Magento Open Source]. Gebruik GraphQL GET en POST oproepen voor Adobe Commerce en [!DNL Magento Open Source].
landing-page-description: Meer informatie over het gebruik van GraphQL op Adobe Commerce en [!DNL Magento Open Source]. Gebruik GraphQL GET en POST oproepen voor Adobe Commerce en [!DNL Magento Open Source].
short-description: Meer informatie over het gebruik van GraphQL op Adobe Commerce en [!DNL Magento Open Source]. Gebruik GraphQL GET en POST oproepen voor Adobe Commerce en [!DNL Magento Open Source].
kt: 11524
doc-type: tutorial
audience: all
last-substantial-update: 2022-12-13T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 8ea823da-24a3-4627-885c-4b3279b9142c
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# Inleiding GraphQL

GraphQL is al snel de industriestandaard geworden voor de manier waarop krachtige clienttoepassingen met een back-end spreken. Het is een steeds relevanter onderwerp voor Adobe Commerce-ontwikkelaars, omdat het platform zijn mogelijkheden op het gebied van headless implementaties blijft uitbreiden.

Als je nog geen ervaring hebt met GraphQL, richt deze sectie je naar de basisbeginselen en het basisgebruik.

## Wat is GraphQL?

GraphQL is een specificatie voor een unieke API-querytaal en de runtime die gegevens verschaft als reactie op die querytaal.

Traditionele web-API&#39;s zoals REST hebben goed gefunctioneerd voor verschillende systemen die gegevens heen en weer doorgeven, maar bieden minder dan piekprestaties voor moderne toepassingen zoals Progressive Webben Application. In dergelijke toepassingen worden de front-end en back-end lagen van de _zelfde_ de toepassing communiceert via web-API. De gestarte aanpak van regelingen als REST biedt vaak niet de juiste flexibiliteit in deze context, waar veel soorten gegevens snel moeten worden opgehaald.

GraphQL stelt een client in staat om een expressieve beschrijving te geven _exact_ de gegevens die het nodig heeft. In plaats van het vereisen van veelvoudige netwerkverzoeken om veelvoudige gegevenstypes op te halen, kan één enkel verzoek voor vele types vragen. En, worden de reacties gehouden len door (in een formaat intuïtief het weerspiegelen van de vraag) slechts de types en gebieden te omvatten die worden gevraagd.

De runtime die de GraphQL-specificatie implementeert, kan in elke taal worden samengesteld. Adobe Commerce en [!DNL Magento Open Source] gebruiken
[graphql-php](https://webonyx.github.io/graphql-php/){target="_blank"} PHP-implementatie en bouwt er zijn eigen lagen bovenop.

[De volledige GraphQL-documentatie weergeven](https://graphql.org/learn){target="_blank"}

## Een GraphQL-client gebruiken

U hebt een GUI GraphQL-client nodig om codevoorbeelden en zelfstudies uit te testen. Er zijn verschillende opties:

* [Altair](https://altairgraphql.dev/){target="_blank"} is een uitstekende en volledig uitgeruste client die speciaal voor GraphQL is gebouwd. Adobe gebruikt Altair in doorloopvideo&#39;s.
* Als u de bureaubladtoepassing niet wilt installeren, zijn er ook Altair-extensies die direct in de toepassing worden uitgevoerd
  [Chroom](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja){target="_blank"}, Firefox, or [Edge](https://microsoftedge.microsoft.com/addons/detail/altair-graphql-client/kpggioiimijgcalmnfnalgglgooonopa){target="_blank"} browser.
* [GraphiQL](https://github.com/graphql/graphiql/tree/main/packages/graphiql){target="_blank"} is een implementatie van de GraphQL IDE van de GraphQL Foundation. Dit is geen installatieprogramma, maar een pakket dat u kunt gebruiken om de interface zelf te maken.
* Als u al vertrouwd bent met [Postman](https://www.postman.com/){target="_blank"}, heeft het behoorlijke steun voor GraphQL query&#39;s, hoewel het niet zo volledig is uitgerust als een speciale GraphQL client.

In uw GraphQL-client moet u uw aanvragen naar het URL-pad verzenden `/graphql` op je Adobe Commerce of [!DNL Magento Open Source] -instantie. Als u liever een bestaande instantie voor uw tests wilt gebruiken, kunt u de demo van het thema Venia (de voorbeeldimplementatie van PWA Studio) gebruiken: `https://venia.magento.com/graphql`

{{$include /help/_includes/graphql-rest-related-links.md}}

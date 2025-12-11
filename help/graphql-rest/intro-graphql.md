---
title: Inleiding GraphQL
description: Leer hoe u GraphQL kunt gebruiken op Adobe Commerce en  [!DNL Magento Open Source] . Gebruik GraphQL GET en POST-aanroepen voor Adobe Commerce en  [!DNL Magento Open Source] .
short-description: Leer hoe te om GraphQL GET en POST vraag voor Adobe Commerce en  [!DNL Magento Open Source] te gebruiken.
kt: 11524
doc-type: video
audience: all
last-substantial-update: 2023-10-12T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: 8ea823da-24a3-4627-885c-4b3279b9142c
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# Inleiding GraphQL

Dit is deel 1 van de reeks voor GraphQL en Adobe Commerce. GraphQL is al snel de industriestandaard geworden voor de manier waarop krachtige clienttoepassingen met een back-end spreken. Het is een steeds relevanter onderwerp voor Adobe Commerce-ontwikkelaars, omdat het platform zijn mogelijkheden op het gebied van headless implementaties blijft uitbreiden.

Als je nog geen ervaring hebt met GraphQL, richt deze sectie je naar de basisbeginselen en het basisgebruik.

>[!VIDEO](https://video.tv.adobe.com/v/3424117?learn=on)

## Verwante video&#39;s en zelfstudies over GraphQL in deze serie

* [Deel 2 GraphQL - Vragen](../graphql-rest/graphql-queries.md)
* [Deel 3 GraphQL - Mutaties](../graphql-rest/graphql-mutations.md)
* [&#x200B; Deel 4 GraphQL - Schema &#x200B;](../graphql-rest/graphql-schema.md)

## Wat is GraphQL?

GraphQL is een specificatie voor een unieke API-querytaal en de runtime die gegevens verschaft als reactie op die querytaal.

Traditionele web-API&#39;s zoals REST hebben goed gefunctioneerd voor verschillende systemen die gegevens heen en weer doorgeven, maar bieden minder dan piekprestaties voor moderne toepassingen, zoals Progressieve webtoepassingen. In toepassingen als dit, de front-end en achterste deellagen van de _zelfde_ toepassing communiceren via Web API. De gestarte aanpak van regelingen als REST biedt vaak niet de juiste flexibiliteit in deze context, waar veel soorten gegevens snel moeten worden opgehaald.

GraphQL staat een cliënt toe om _precies_ precies te beschrijven het heeft nodig. In plaats van het vereisen van veelvoudige netwerkverzoeken om veelvoudige gegevenstypes op te halen, kan één enkel verzoek voor vele types vragen. En, worden de reacties gehouden len door (in een formaat intuïtief het weerspiegelen van de vraag) slechts de types en gebieden te omvatten die worden gevraagd.

De runtime die de GraphQL-specificatie implementeert, kan in elke taal worden samengesteld. Adobe Commerce en [!DNL Magento Open Source] gebruiken de
[&#x200B; grafisch-php &#x200B;](https://webonyx.github.io/graphql-php/){target="_blank"} PHP implementatie en bouwt zijn eigen lagen bovenop het.

[&#x200B; Mening de volledige documentatie van GraphQL &#x200B;](https://graphql.org/learn){target="_blank"}

## Een GraphQL-client gebruiken

U hebt een GUI GraphQL-client nodig om codevoorbeelden en zelfstudies uit te testen. Er zijn verschillende opties:

* [&#x200B; Altair &#x200B;](https://altairgraphql.dev/){target="_blank"} is een uitstekende en volledig gekenmerkte cliënt die specifiek voor GraphQL wordt gebouwd. Adobe gebruikt Altair in doorloopvideo&#39;s.
* Als u de bureaubladtoepassing niet wilt installeren, zijn er ook Altair-extensies die direct in de toepassing worden uitgevoerd
  [&#x200B; Chrome &#x200B;](https://chromewebstore.google.com/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja){target="_blank"}, Firefox, of [&#x200B; browser van Edge &#x200B;](https://microsoftedge.microsoft.com/addons/detail/altair-graphql-client/kpggioiimijgcalmnfnalgglgooonopa){target="_blank"}.
* [&#x200B; GraphiQL &#x200B;](https://github.com/graphql/graphiql/tree/main/packages/graphiql){target="_blank"} is een implementatie van winde van GraphQL van de Stichting van GraphQL. Dit is geen installatieprogramma, maar een pakket dat u kunt gebruiken om de interface zelf te maken.
* Als u reeds vertrouwd met [&#x200B; Postman &#x200B;](https://www.postman.com/){target="_blank"} bent, heeft het fatsoenlijke steun voor de vragen van GraphQL, hoewel het niet zo volledig zoals een specifieke cliënt van GraphQL wordt voorzien.

In uw GraphQL-client moet u uw aanvragen indienen bij het URL-pad `/graphql` op uw Adobe Commerce- of [!DNL Magento Open Source] -instantie. Als u liever een bestaande instantie voor uw tests wilt gebruiken, gebruikt u de demo van het thema Venia (de voorbeeldimplementatie van PWA Studio): `https://venia.magento.com/graphql`

{{$include /help/_includes/graphql-rest-related-links.md}}

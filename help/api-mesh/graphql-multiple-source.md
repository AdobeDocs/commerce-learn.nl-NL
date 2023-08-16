---
title: Een GraphQL met meerdere bronnen maken voor gebruik in API-net
description: Ontdek hoe u meerdere bronnen kunt gebruiken voor API Mesh op Adobe Commerce en [!DNL Adobe App Builder]. Meer informatie over enkele algemene fouten en hoe u deze kunt oplossen.
landing-page-description: Ontdek hoe u API Mesh kunt gebruiken in Adobe Commerce en  [!DNL Adobe App Builder]. Leer hoe u een net maakt met meerdere bronnen en hoe u enkele algemene fouten oplost.
short-description: Ontdek hoe u API Mesh kunt gebruiken in Adobe Commerce en  [!DNL Adobe App Builder]. Leer hoe u een net maakt met meerdere bronnen en hoe u enkele algemene fouten oplost.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Architect, Developer
level: Beginner, Intermediate
exl-id: d788a068-9d20-4db0-a0eb-fd897873253d
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 8%

---

# Een net maken met meerdere bronnen

Deze video helpt ontwikkelaars te begrijpen hoe ze een net met meerdere bronnen kunnen maken in API Mesh voor Adobe Developer App Builder. In deze video ziet u hoe u een net met meerdere bronnen maakt en fouten herkent. Ga voor meer informatie en codevoorbeelden naar [Een net maken](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1){target="_blank"}.

## Voor wie is deze video?

* Iedereen die nieuw is voor het API-net
* Ontwikkelaars die meerdere API- en GraphQL-bronnen willen combineren

## Video-inhoud

* Hoe wordt het gebruikt [transformaties](https://developer.adobe.com/graphql-mesh-gateway/gateway/transforms/){target="_blank"} om het standaardbronschema te wijzigen
* Hoe te om fouten, zoals naamconflicten, schemabeschikbaarheid, en andere kwesties van de schemasyntaxis problemen op te lossen
* Het net bijwerken met een gewijzigde configuratie

>[!VIDEO](https://video.tv.adobe.com/v/3414125?quality=12&learn=on)

## Het JSON-configuratiebestand maken

API Mesh gebruikt een JSON-configuratiebestand om uw bronhandlers te definiëren. Het JSON-bestand bevat een `sources` array die de bronnen voor het net bevat. Hier is een voorbeeld van een net met meerdere bronnen.

```json
{
"meshConfig": {
    "sources": [
      {
        "name": "Commerce",
        "handler": {
          "graphql": {
            "endpoint": "https://venia.magento.com/graphql/"
          }
        }
      },
      {
        "name": "Example",
        "handler": {
          "graphql": {
            "endpoint": "https://www.example.com/graphql/"
          }
        }
      }
    ]
  }
}
```

{{$include /help/_includes/api-mesh-related-links.md}}

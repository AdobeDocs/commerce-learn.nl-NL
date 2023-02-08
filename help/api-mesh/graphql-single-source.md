---
title: Een GraphQL-aanvraag voor één bron maken voor gebruik in API-net
description: Ontdek hoe u API Mesh kunt gebruiken op Adobe Commerce en [!DNL Adobe App Builder]. Meer informatie over het maken van een aanvraag met één bron.
landing-page-description: Ontdek hoe u API Mesh kunt gebruiken op Adobe Commerce en [!DNL Adobe App Builder]. Meer informatie over het maken van een aanvraag met één bron.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
source-git-commit: b6d501c5c852e1cc2cf1f05f91b5a9d96ac7d036
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# GraphQL API-net met één bron maken

De video helpt een ontwikkelaar begrijpen hoe te om een GraphQL reverse volmacht tot stand te brengen en één enkele bron heeft. Houd er rekening mee dat voor GraphQL Mesh een openbaar toegankelijke URL met een geldig GraphQL-schema is vereist. In de video wordt ook uitgelegd hoe u uw eerste zoon instelt voor gebruik met uw website voor handel. Voor basiscodevoorbeelden die in de video zijn gebruikt, gaat u naar [Een net maken](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1).

## Voor wie is deze video?

* Iedereen die nieuw is voor het API-net
* Ontwikkelaars die meerdere grafische bronnen willen gebruiken
* Iedereen die moet weten hoe te om het netwerklusje en filter door grafisch te filtreren

## Video-inhoud

* API gebruiken als reverse-proxy
* JSON-configuratie met de Adobe Developer-opdrachtregelinterface
* Het nieuwe GraphQL-eindpunt openen

>[!VIDEO](https://video.tv.adobe.com/v/3414124)

## Het JSON-configuratiebestand maken

Voor Adobe App Builder om informatie over al uw bronnen te krijgen, definieert u deze in een JSON-configuratie. Elke bron is een element in een array en u kunt een of meer elementen hebben. Hier is een voorbeeld van één bron

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
      }
    ]
  }
}
```

{{$include /help/_includes/api-mesh-related-links.md}}

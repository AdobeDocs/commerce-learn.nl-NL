---
title: Een GraphQL met meerdere bronnen maken voor gebruik in API-net
description: Ontdek hoe u meerdere bronnen kunt gebruiken voor API Mesh op Adobe Commerce en [!DNL Adobe App Builder]. Meer informatie over enkele algemene fouten en hoe u deze kunt oplossen.
landing-page-description: Ontdek hoe u API Mesh kunt gebruiken op Adobe Commerce en [!DNL Adobe App Builder]. Leer over het creëren van een verzoek dat veelvoudige bronnen heeft en hoe te om sommige gemeenschappelijke fouten op te lossen.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
source-git-commit: b6d501c5c852e1cc2cf1f05f91b5a9d96ac7d036
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Meerdere GraphQL API-bronnetten maken

De video helpt een ontwikkelaar begrijpen hoe een GraphQL reverse-proxy met meerdere bronnen kan worden gemaakt. In deze video ziet u hoe u verschillende bronnen kunt aansluiten, fouten kunt identificeren en wijzigingen in de it kunt opslaan. Voor basiscodevoorbeelden die in de video zijn gebruikt, gaat u naar [Een net maken](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1).

## Voor wie is deze video?

* Iedereen die nieuw is voor het API-net
* Ontwikkelaars die meerdere grafische bronnen willen gebruiken
* Iedereen die moet weten hoe te om het netwerklusje en filter door grafisch te filtreren

## Video-inhoud

* Hoe het complexe schema van de Attributen API van de Douane van een tweede bron het standaardbronschema kan met voeten treden
* De configuratie van het api-net aanpassen om rekening te houden met het tweede overschrijvende schema
* Hoe te om fouten problemen op te lossen die in het proces zoals noemend conflict, schemabeschikbaarheid en andere syntaxis zouden kunnen voorkomen SDL
* Voorbeeld van veelvoorkomende fouten na pogingen om schema&#39;s aan te sluiten
* Het api-net na bewerkingen opnieuw samenstellen
* Wijzigingen opslaan in it na wijziging van API-netconfiguratie

>[!VIDEO](https://video.tv.adobe.com/v/3414125)

## Het JSON-configuratiebestand maken

Voor Adobe App Builder om informatie over al uw bronnen te krijgen, definieert u deze in een JSON-configuratie. Elke bron is een element in een array en u kunt een of meer elementen hebben. Hier ziet u een voorbeeld van een meervoudige bronaanvraag die samen worden samengevoegd om een enkele reactie te vormen.

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
        "name": "ERP",
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

---
title: Eén GraphQL-bronnet maken in API-net
description: Ontdek hoe u API Mesh kunt gebruiken op Adobe Commerce en  [!DNL Adobe App Builder] . Meer informatie over het maken van een net met één bron.
landing-page-description: Ontdek hoe u API Mesh kunt gebruiken op Adobe Commerce en  [!DNL Adobe App Builder] . Meer informatie over het maken van een net met één bron.
short-description: Ontdek hoe u API Mesh kunt gebruiken op Adobe Commerce en  [!DNL Adobe App Builder] . Meer informatie over het maken van een net met één bron.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: 9a78457a-1539-49c0-ac69-4bbfc6786137
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Een net met één bron maken

Deze video helpt ontwikkelaars te begrijpen hoe ze een net met één bron kunnen maken in API Mesh for Adobe Developer App Builder. Voor dit basisvoorbeeld om te werken zoals verwacht, hebt u een openbaar toegankelijke API of het eindpunt van GraphQL nodig. In de video wordt ook uitgelegd hoe u een eenvoudig `mesh.json` -bestand kunt maken voor gebruik met uw Commerce-instantie. Voor meer details en codesteekproeven, leidt het bezoek [ tot een netwerk ](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1){target="_blank"}.

## Voor wie is deze video?

* Iedereen die nog geen API-net heeft
* Ontwikkelaars die meerdere GraphQL- en API-bronnen willen combineren
* Iedereen die moet weten hoe te om het netwerklusje en filter door GraphQL te filtreren

## Video-inhoud

* API-net gebruiken als een reverse-proxy
* Een net maken van een JSON-configuratiebestand
* Het nieuwe GraphQL-eindpunt openen

>[!VIDEO](https://video.tv.adobe.com/v/3414124?quality=12&learn=on)

## Het JSON-configuratiebestand maken

API Mesh gebruikt een JSON-configuratiebestand om uw bronhandlers te definiëren. Het JSON-bestand bevat een `sources` -array die de bronnen voor uw net bevat. Hier is een voorbeeld van een net met één bron.

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

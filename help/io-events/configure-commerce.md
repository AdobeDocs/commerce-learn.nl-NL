---
title: Adobe Commerce configureren
description: Leer hoe u Adobe Commerce configureert voor het gebruik van gebeurtenissen in Adobe Developer App Builder.
landing-page-description: Leer hoe u Adobe Commerce configureert om het gebeurtenismechanisme te gebruiken voor gebruik door Adobe Developer App Builder.
short-description: Leer hoe u Adobe Commerce configureert om het gebeurtenismechanisme te gebruiken voor gebruik door Adobe Developer App Builder.
kt: 11889
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-21T00:00:00Z
feature: App Builder, Configuration, Backend Development
topic: Commerce, Architecture
old-role: Architect, Developer
role: Developer, User
level: Beginner, Intermediate
exl-id: b8062042-2e90-4750-92ef-d55a76f2d842
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Adobe Commerce configureren

Leer hoe u Adobe Commerce configureert om gebeurtenissen beschikbaar te maken. De extra documentatie die bij [&#x200B; wordt gevonden installeert Adobe I/O Events voor Adobe Commerce &#x200B;](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Voor wie is deze video?

* Ontwikkelaars die nog niet bekend zijn met Adobe Commerce en Adobe Developer App Builder gebruiken I/O-gebeurtenissen en moeten een Adobe App Builder-project maken.

## Video-inhoud {#video-content}

* Configuratie van de Adobe I/O-gebeurtenissen in de Commerce-beheerder
* Een persoonlijke sleutel opslaan in de Commerce-beheerder
* De unieke id opslaan in de Commerce-beheerder
* Een gebeurtenisprovider maken

>[!VIDEO](https://video.tv.adobe.com/v/3415799?quality=12&learn=on)

## Nuttige opdrachten {#useful-commands}

```bash
bin/magento events:create-event-provider --label "my_provider" --description "Provides out-of-process extensibility for Adobe Commerce"

bin/magento events:subscribe observer.catalog_product_save_after --fields=name --fields=price
```

{{$include /help/_includes/io-events-related-links.md}}

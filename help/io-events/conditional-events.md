---
title: Meer informatie over het gebruik van voorwaardelijke gebeurtenissen in Adobe Commerce
description: Leer hoe u voorwaardelijke gebeurtenissen kunt gebruiken voor gebruik in Adobe Developer App Builder.
landing-page-description: Leer hoe u voorwaardelijke Adobe Commerce-gebeurtenissen kunt gebruiken.
short-description: Leer hoe u voorwaardelijke Adobe Commerce-gebeurtenissen kunt gebruiken.
kt: 11890
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-21T00:00:00Z
feature: App Builder, Eventing, Backend Development
topic: Commerce, Architecture
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 03787aa3-051b-4a35-b2e8-ecf6762b5eb4
source-git-commit: e02da0901c01871360bcc556666e310acd7c7224
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Voorwaardelijke Adobe Commerce-gebeurtenissen

Meer informatie over voorwaardelijke gebeurtenissen in Adobe Commerce die kunnen worden gebruikt in Adobe Developer App Builder. De extra documentatie die bij [ wordt gevonden installeert de Gebeurtenissen van Adobe I/O voor Adobe Commerce ](https://developer.adobe.com/commerce/extensibility/events/conditional-events/){target="_blank"} .

## Voor wie is deze video?

* Ontwikkelaars die nog niet bekend zijn met Adobe Commerce en Adobe Developer App Builder gebruiken I/O-gebeurtenissen en moeten een Adobe App Builder-project maken.

## Video-inhoud {#video-content}

* Meer informatie over voorwaardelijke gebeurtenissen
* Meer informatie over het juiste gebruik van het nieuwe XML-bestand io_events.xml
* Leer hoe u voorwaardelijke gebeurtenissen configureert
* Regels definiëren voor gebruik in voorwaardelijke gebeurtenissen
* Leer hoe u gebeurtenissen kunt registreren in de Commerce-instanties `app/etc/config.php`

>[!VIDEO](https://video.tv.adobe.com/v/3415806?quality=12&learn=on)

## Nuttige opdrachten {#useful-commands}

```bash
bin/magento events:subscribe plugin.magento.catalog.model.resource_model.product.save --fields=sku --fields=qty --fields=category_id

bin/magento events:subscribe plugin.magento.catalog.model.resource_model.product.save_low_stock --parent=plugin.magento.catalog.model.resource_model.product.save --fields=sku --fields=qty --fields=category_id --rules="qty|lessThan|20" --rules="category_id|in|3,4,5"

cat app/etc/config.php

bin/magento events:list

bin/magento events:list -v
```

{{$include /help/_includes/io-events-related-links.md}}

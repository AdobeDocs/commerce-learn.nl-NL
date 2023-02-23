---
title: Meer informatie over het gebruik van voorwaardelijke gebeurtenissen in Adobe Commerce
description: Leer hoe u voorwaardelijke gebeurtenissen kunt gebruiken in Adobe Developer App Builder.
landing-page-description: Leer hoe u voorwaardelijke Adobe Commerce-gebeurtenissen kunt gebruiken.
kt: 11890
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-21T00:00:00Z
source-git-commit: f5de9191315c7df2eaca4ee51d03b30e2a2fac99
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Voorwaardelijke Adobe Commerce-gebeurtenissen

Meer informatie over voorwaardelijke gebeurtenissen in Adobe Commerce die kunnen worden gebruikt in Adobe Developer App Builder. Aanvullende documentatie gevonden op [Adobe I/O-gebeurtenissen installeren voor Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/conditional-events/){target="_blank"}.

## Voor wie is deze video?

* Ontwikkelaars die nog niet bekend zijn met Adobe Commerce en Adobe Developer App Builder, gebruiken I/O-gebeurtenissen en moeten een Adobe App Builder-project maken.

## Video-inhoud {#video-content}

* Meer informatie over voorwaardelijke gebeurtenissen
* Meer informatie over het juiste gebruik van het nieuwe XML-bestand io_events.xml
* Leer hoe u voorwaardelijke gebeurtenissen configureert
* Regels definiëren voor gebruik in voorwaardelijke gebeurtenissen
* Leer hoe u gebeurtenissen kunt registreren in de instanties Commerce `app/etc/config.php`

>[!VIDEO](https://video.tv.adobe.com/v/3415806)

## Nuttige opdrachten {#useful-commands}

```bash
bin/magento events:subscribe plugin.magento.catalog.model.resource_model.product.save --fields=sku --fields=qty --fields=category_id

bin/magento events:subscribe plugin.magento.catalog.model.resource_model.product.save_low_stock --parent=plugin.magento.catalog.model.resource_model.product.save --fields=sku --fields=qty --fields=category_id --rules="qty|lessThan|20" --rules="category_id|in|3,4,5"

cat app/etc/config.php

bin/magento events:list

bin/magento events:list -v
```

{{$include /help/_includes/io-events-related-links.md}}

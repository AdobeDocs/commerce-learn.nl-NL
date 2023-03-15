---
title: Leer hoe u in Adobe Commerce een module maakt voor het gebruik van gebeurtenissen.
description: Leer hoe te om de module van de Handel tot stand te brengen om gebeurtenissen te gebruiken.
landing-page-description: Leer hoe u een Adobe Commerce-module kunt maken voor het gebruik van gebeurtenissen.
short-description: Learn how to create an Adobe Commerce module to use events.
kt: 11891
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-21T00:00:00Z
source-git-commit: 67d21ca23cdccc87cdeed4a08a3ebb48e5bd1030
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Ontwikkeling Adobe Commerce-module

Leer hoe u gebeurtenissen kunt registreren, ondersteunde gebeurtenissen kunt zoeken en hoe u een nieuw XML-bestand kunt gebruiken `io_events.xml` in de ontwikkeling van aangepaste modules. De video laat ontwikkelaars ook zien hoe ze geregistreerde gebeurtenissen kunnen vinden die kunnen worden gebruikt en hoe ze het abonnement op gebeurtenissen die al gedefinieerd kunnen zijn, kunnen opzeggen. Aanvullende documentatie gevonden op [Adobe I/O-gebeurtenissen installeren voor Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Voor wie is deze video?

* Ontwikkelaars die nog geen ervaring hebben met Adobe Commerce en Adobe Developer App Builder, gebruiken I/O-gebeurtenissen.

## Video-inhoud {#video-content}

* Gebeurtenissen registreren bij Handel voor gebruik in Adobe Developer App Builder
* Gebeurtenissen identificeren die kunnen worden geregistreerd
* Leer hoe u gebeurtenissen kunt registreren in io_events.xml
* Leer hoe u gebeurtenissen kunt registreren in de instanties Commerce `app/etc/config.php`
* Leer hoe u uw abonnement op een gebeurtenis opzegt

>[!VIDEO](https://video.tv.adobe.com/v/3415802)

## Nuttige opdrachten {#useful-commands}

```bash
bin/magento events:list:all Magento_Catalog

bin/magento events:info plugin.magento.catalog.api.category_repository.save

bin/magento events:subscribe observer.catalog_category_save_after --fields=entity_id --fields=parent_id

cat app/etc/config.php

bin/magento events:unsubscribe observer.catalog_category_save_after

bin/magento events:list
```

{{$include /help/_includes/io-events-related-links.md}}

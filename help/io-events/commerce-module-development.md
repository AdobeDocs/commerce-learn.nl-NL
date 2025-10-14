---
title: Leer hoe u in Adobe Commerce een module maakt voor het gebruik van gebeurtenissen.
description: Leer hoe u een Commerce-module kunt maken voor het gebruik van gebeurtenissen.
landing-page-description: Leer hoe u een Adobe Commerce-module kunt maken voor het gebruik van gebeurtenissen.
short-description: Leer hoe u een Adobe Commerce-module kunt maken voor het gebruik van gebeurtenissen.
kt: 11891
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-21T00:00:00Z
feature: App Builder, Eventing, Backend Development
topic: Commerce, Architecture
role: Architect, Developer
level: Beginner, Intermediate
exl-id: e8103fe0-116a-499c-ae0a-3ad0511f44d0
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Ontwikkeling Adobe Commerce-module

Leer hoe u gebeurtenissen registreert, ondersteunde gebeurtenissen zoekt en hoe u een nieuw XML-bestand `io_events.xml` gebruikt in aangepaste moduleontwikkeling. De video laat ontwikkelaars ook zien hoe ze geregistreerde gebeurtenissen kunnen vinden die kunnen worden gebruikt en hoe ze het abonnement op gebeurtenissen die al gedefinieerd kunnen zijn, kunnen opzeggen. De extra documentatie die bij [&#x200B; wordt gevonden installeert de Gebeurtenissen van Adobe I/O voor Adobe Commerce &#x200B;](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"} .

## Voor wie is deze video?

* Ontwikkelaars die nog niet bekend zijn met Adobe Commerce en Adobe Developer App Builder gebruiken I/O-gebeurtenissen.

## Video-inhoud {#video-content}

* Gebeurtenissen registreren in Commerce voor gebruik in Adobe Developer App Builder
* Gebeurtenissen identificeren die kunnen worden geregistreerd
* Leer hoe u gebeurtenissen kunt registreren in io_events.xml
* Leer hoe u gebeurtenissen kunt registreren in de Commerce-instanties `app/etc/config.php`
* Leer hoe u uw abonnement op een gebeurtenis opzegt

>[!VIDEO](https://video.tv.adobe.com/v/3430653?quality=12&learn=on&captions=dut)

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

---
title: Leer hoe u IO-gebeurtenissen installeert voor Adobe Commerce 2.4.6
description: Leer hoe u modules installeert die nodig zijn voor IO-gebeurtenissen in Adobe Commerce 2.4.6 voor gebruik in Adobe Developer App Builder
landing-page-description: Leer hoe u verschillende modules installeert die nodig zijn voor Adobe Commerce 2.4.6.
short-description: Leer hoe u verschillende modules installeert die nodig zijn voor Adobe Commerce 2.4.6.
kt: 11887
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-22T00:00:00Z
badge: Adobe Commerce 2.4.6
feature: App Builder, Eventing
topic: Commerce, Architecture
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: 41b31ed8-04c5-4d50-aaff-abc3718b5957
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Installatie van Adobe Commerce 2.4.6

Leer hoe u verschillende nieuwe modules in Adobe Commerce installeert met Composer for versie 2.4.6. De extra documentatie die bij [&#x200B; wordt gevonden installeert Adobe I/O Events voor Adobe Commerce &#x200B;](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Voor wie is deze video?

* Ontwikkelaars die nog niet bekend zijn met Adobe Commerce en Adobe Developer App Builder gebruiken I/O Events.

## Video-inhoud {#video-content}

* Opdrachten voor externe hosting
* Opdrachten voor Adobe Commerce Cloud
* Adobe Commerce Cloud moet worden bewerkt

>[!VIDEO](https://video.tv.adobe.com/v/3430641?captions=dut&quality=12&learn=on)

## Nuttige opdrachten {#useful-commands}

Er zijn verschillende opdrachten die enigszins verschillen, afhankelijk van de hostomgeving of het gebruik van Adobe Commerce Cloud.

### Op locatie hosten {#on-premise}

```bash
bin/magento events:generate:module

bin/magento module:enable --all

bin/magento setup:upgrade && bin/magento setup:di:compile
```

### Adobe Commerce op Cloud {#adobe-commerce-cloud}

```bash
composer info magento/ece-tools
```

Commerce Cloud `.magento.env.yaml` :

```yaml
stage:
  global:
    ENABLE_EVENTING: true
```

{{$include /help/_includes/io-events-related-links.md}}

---
title: Leer hoe u IO-gebeurtenissen installeert voor Adobe Commerce 2.4.5
description: Leer hoe u modules installeert die nodig zijn voor IO-gebeurtenissen in Adobe Commerce 2.4.5 voor gebruik in Adobe Developer App Builder
landing-page-description: Leer hoe u met behulp van composer verschillende modules installeert die nodig zijn voor Adobe Commerce 2.4.5.
short-description: Leer hoe u met behulp van composer verschillende modules installeert die nodig zijn voor Adobe Commerce 2.4.5.
kt: 11886
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-22T00:00:00Z
badge: Adobe Commerce 2.4.5
feature: App Builder, Eventing
topic: Commerce, Architecture
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: e0adfd85-5a3d-44ba-aab5-ecd7c61715cf
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Installatie van Adobe Commerce 2.4.5

Leer hoe u verschillende nieuwe modules in Adobe Commerce installeert met Composer for versie 2.4.5. Hiermee worden de vereiste modules ingesteld die in de Adobe Commerce-toepassing moeten worden gebruikt. De extra documentatie die bij [&#x200B; wordt gevonden installeert Adobe I/O Events voor Adobe Commerce &#x200B;](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Voor wie is deze video?

* Ontwikkelaars met I/O-gebeurtenissen die nog niet bekend zijn bij Adobe Commerce en Adobe Developer App Builder

## Video-inhoud {#video-content}

* Installatie van vereiste modules met behulp van composer
* Opdrachten voor externe hosting
* Opdrachten voor Adobe Commerce Cloud
* Adobe Commerce Cloud moet worden bewerkt

>[!VIDEO](https://video.tv.adobe.com/v/3430645?captions=dut&quality=12&learn=on)

## Nuttige opdrachten {#useful-commands}

Er zijn verschillende opdrachten die enigszins verschillen, afhankelijk van de hostomgeving of het gebruik van Adobe Commerce Cloud.

### Op locatie hosten {#on-premise}

```bash
composer require magento/commerce-eventing=^1.0 --no-update

composer update

bin/magento events:generate:module

bin/magento module:enable --all

bin/magento setup:upgrade && bin/magento setup:di:compile
```

### Adobe Commerce op Cloud {#adobe-commerce-cloud}

```bash
composer require magento/commerce-eventing=^1.0 --no-update

composer update

composer info magento/ece-tools
```

Commerce Cloud `.magento.env.yaml` :

```yaml
stage:
  global:
    ENABLE_EVENTING: true
```

{{$include /help/_includes/io-events-related-links.md}}

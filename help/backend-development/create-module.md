---
title: Een module maken
description: Maak een pagina waarop één parameter wordt geretourneerd.
topic: Development
kt: 5602
doc-type: video
activity: use
exl-id: 941c04ee-54b8-4b81-b77d-fff5875927f0
source-git-commit: 32d1366758fa6453a48570cfd08d10a93559a974
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Een module maken

Module is een structuurelement van [!DNL Commerce] - het hele systeem is gebaseerd op modules. De eerste stap bij het maken van een aanpassing is meestal het bouwen van een module.

## Voor wie is deze video?

- Ontwikkelaars

## Stappen om een module toe te voegen

- Maak de modulemap.
- Maak het bestand etc/module.xml.
- Maak het bestand registration.php.
- Stel de bak/magento opstelling in werking.
- Voer een upgradescript uit om de nieuwe module te installeren.
- Controleer of de module werkt.

>[!VIDEO](https://video.tv.adobe.com/v/35792?learn=on)

### module.xml

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Training_Sales">
        <sequence>
            <module name="Magento_Sales"/>
        </sequence>
    </module>
</config>
```

### registration.php

```PHP
<?php

use Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'Training_Sales',
    __DIR__);
```

## Nuttige bronnen

- [Module naslaggids](https://developer.adobe.com/commerce/php/module-reference/)

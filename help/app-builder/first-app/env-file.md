---
title: Het .env-bestand
description: Meer informatie over de bestandstypen in het .env-bestand voor deze voorbeeldtoepassing
landing-page-description: Meer informatie over Adobe Developer App Builder die wordt gebruikt met Adobe Commerce en over de typen inhoud die worden gebruikt in het .env-bestand
kt: 12423
doc-type: tutorial
audience: all
last-substantial-update: 2023-3-13
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 934fcdd1-ee61-4914-89ce-f6f04b1bc763
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# Het .env-bestand genereren en configureren {#env-file}

`.env` is een speciaal bestand dat geen deel uitmaakt van de voorbeeldmodule, maar dat belangrijk is voor gebruik in uw Adobe Developer App Builder-toepassing. Dit bestand bevat geheimen en andere informatie. Wijs dit bestand niet toe aan een opslagplaats voor code.

## Voor wie is deze video?

* Ontwikkelaars die nog geen ervaring hebben met Adobe Commerce, gebruiken Adobe App Builder die meer informatie over het bestand `.env` wil.

## Video-inhoud

* Inleiding tot het .env-bestand en het doel ervan
* Het .env-bestand genereren
* Hoe kan ik het bestand toevoegen om nieuwe geheimen toe te voegen
* Maak geen gebruik van dit bestand omdat het vertrouwelijke informatie bevat

>[!VIDEO](https://video.tv.adobe.com/v/3416593?quality=12&learn=on)

## Codevoorbeeld

```bash
# Specify your secrets here
# The .env file must not be committed to source control
## Adobe I/O Runtime credentials
AIO_runtime_auth=abcd1234-aaa-bbb-ccc-12345:Abcdd12345asdfadsfadsfee2323232323232
AIO_runtime_namespace=12345-someworkspace-stage
AIO_runtime_apihost=https://adobeioruntime.net
## Adobe I/O Console service account credentials (JWT) Api Key
SERVICE_API_KEY=

# You can include some commerce OAUTH credentials too, our sample module will use this
#COMMERCE_BASE_URL=https://somecommercewebsite.com/
#COMMERCE_CONSUMER_KEY=abcebdme5bvafnemk0mdeeiyfq123
#COMMERCE_CONSUMER_SECRET=ffff86sqws3pss5hhuofiqgq4t04rrr11
#COMMERCE_ACCESS_TOKEN=gdddfccronj098r4m04zyq773s5o64
#COMMERCE_ACCESS_TOKEN_SECRET=ggg7nb19jhr5gi9jzfan9ggzipe8yrus
```

Deze statische waarden worden gebruikt in de voorbeeldmodule in bestand `actions/commerce.index.js` .

```javascript
        const oauth = getCommerceOauthClient(
            {
                url: params.COMMERCE_BASE_URL,
                consumerKey: params.COMMERCE_CONSUMER_KEY,
                consumerSecret: params.COMMERCE_CONSUMER_SECRET,
                accessToken: params.COMMERCE_ACCESS_TOKEN,
                accessTokenSecret: params.COMMERCE_ACCESS_TOKEN_SECRET
            },
            logger
        )
```

{{$include /help/_includes/app-builder-first-app-related-links.md}}

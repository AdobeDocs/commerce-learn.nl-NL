---
title: Het bestand app.config.yaml
description: Leer meer over de bestandstypen in het bestand app.config.yaml voor deze voorbeeldtoepassing.
landing-page-description: Meer informatie over Adobe Developer App Builder die wordt gebruikt met Adobe Commerce en over welke bestandstypen in app.config.yaml worden weergegeven.
kt: 12929
doc-type: tutorial
audience: all
last-substantial-update: 2023-3-13
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: ff5f1811-ca93-494e-8e5c-a5e0c7bb673d
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Beschrijving en gebruik van het bestand app.config.yaml {#app-config-yaml}

Dit bestand bepaalt de configuratie voor de toepassing.

## Voor wie is deze video?

* Nieuwe Adobe Commerce-ontwikkelaars met beperkte ervaring met Adobe App Builder die meer leren over `app.config.yaml` in de voorbeeldtoepassing.

## Video-inhoud

* Het besproken bestand `app.config.yaml`
* Hoe zijn definities gekoppeld aan andere `.js` -bestanden

>[!VIDEO](https://video.tv.adobe.com/v/3416592?quality=12&learn=on)

## Codevoorbeeld

```bash
# Specify your secrets here
# This file must not be committed to source control
## Adobe I/O Runtime credentials
AIO_runtime_auth=abcd1234-aaa-bbb-ccc-12345:Abcdd12345asdfadsfadsfee2323232323232
AIO_runtime_namespace=12345-someworkspace-stage
AIO_runtime_apihost=https://adobeioruntime.net
## Adobe I/O Console service account credentials (JWT) Api Key
SERVICE_API_KEY=

# You can also include commerce OAuth credentials, our sample module will use the following example credentials:
#COMMERCE_BASE_URL=https://somecommercewebsite.com/
#COMMERCE_CONSUMER_KEY=abcebdme5bvafnemk0mdeeiyfq123
#COMMERCE_CONSUMER_SECRET=ffff86sqws3pss5hhuofiqgq4t04rrr11
#COMMERCE_ACCESS_TOKEN=gdddfccronj098r4m04zyq773s5o64
#COMMERCE_ACCESS_TOKEN_SECRET=ggg7nb19jhr5gi9jzfan9ggzipe8yrus
```

Deze statische waarden worden gebruikt in de voorbeeldmodule in het bestand `actions/commerce.index.js`

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

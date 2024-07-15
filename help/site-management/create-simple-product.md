---
title: Een eenvoudig product maken
description: Leer hoe u een eenvoudig product maakt met de REST API en de Commerce Admin.
kt: 14446
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-11-14T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
exl-id: 62ba8e71-dcff-4c72-8850-029be2c42620
source-git-commit: a9712c4354967e8e53c421878be8b83bb6056e6d
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Een eenvoudig product maken

Leer hoe u een eenvoudig product maakt met de REST API en de Adobe Commerce Admin.

## Voor wie is deze video?

- Webmanagers
- Handelshandelaren
- Nieuwe Adobe Commerce-ontwikkelaars die willen leren hoe u in Adobe Commerce producten kunt maken met de REST API.

## Video-inhoud

>[!VIDEO](https://video.tv.adobe.com/v/3425650?learn=on)

## Een product maken met krullen

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=a42da0096288718c9556f77549c6305f; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "product": {
    "sku": "some-product-sku",
    "name": "My curl created product test",
    "attribute_set_id": 4,
    "price": 222,
    "type_id": "simple"
  }
}
```

## Een product ophalen met krullen

```bash
curl --location '{{your.url.here}}rest/default/V1/products/some-product-sku' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=3b797a6cc3c5c71f2193109fb9838b12'
```

## Aanvullende bronnen

- [ Adobe Developer REST zelfstudies ](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/) {target="_blank"}
- [ Adobe Commerce REST ReDoc ](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products) {target="_blank"}

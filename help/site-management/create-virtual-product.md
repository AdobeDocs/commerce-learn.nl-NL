---
title: Een virtueel product maken
description: Leer hoe u een virtueel product maakt met de REST API en de Commerce Admin.
kt: 14464
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-11-15T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
exl-id: 5149b6b4-5fbf-467a-a412-6dce7188bcb9
source-git-commit: a9712c4354967e8e53c421878be8b83bb6056e6d
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Een virtueel product maken

Leer hoe u een virtueel product maakt met de REST API en de Adobe Commerce Admin.

## Voor wie is deze video?

- Webmanagers
- Handelshandelaren
- Nieuwe Adobe Commerce-ontwikkelaars die willen leren hoe u in Adobe Commerce producten kunt maken met de REST API.

## Video-inhoud

>[!VIDEO](https://video.tv.adobe.com/v/3425723?learn=on)

## Een virtueel product maken met krullen

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=2cd97649bcf4ee5b45b23f8eb940e3a0; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "product": {
    "sku": "postman-rest-virtual-product-test",
    "name": "POSTMAN virtual product test",
    "attribute_set_id": 4,
    "price": 44,
    "type_id": "virtual"
  }
}
'
```

## Een product ophalen met krullen

```bash
curl --location '{{your.url.here}}/rest/default/V1/products/Admin-created-virtual-product' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=2cd97649bcf4ee5b45b23f8eb940e3a0; private_content_version=564dde2976849891583a9a649073f01e'
```

## Aanvullende bronnen

- [ Adobe Developer REST zelfstudies ](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/) {target="_blank"}
- [ Adobe Commerce REST ReDoc ](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products) {target="_blank"}

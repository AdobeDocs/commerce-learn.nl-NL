---
title: Een gegroepeerd product maken
description: Leer hoe u een gegroepeerd product maakt met de REST API en de Commerce Admin.
kt: 14585
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-11-30T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
exl-id: 3ad7125b-ef6d-4ea0-9fa7-8fc9eb399ec1
source-git-commit: 76a67af957b0d8c1eb64ad42f92412f338650d4b
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Een gegroepeerd product maken

Een gegroepeerd product bestaat uit eenvoudige zelfstandige producten die als groep worden aangeboden. U kunt variaties van één enkel product aanbieden of hen groeperen door seizoen of thema. Voordat u een gegroepeerd product maakt, controleert u of alle eenvoudige producten die u in de groep wilt opnemen, beschikbaar zijn in Adobe Commerce en maakt u alle producten die niet bestaan.

In deze zelfstudie leert u hoe u een gegroepeerd product kunt maken met de REST API en de Adobe Commerce Admin.

Gebruik de REST API om een groepsproduct te maken in de Admin:

1. Maak een leeg gegroepeerd product.
1. Eenvoudige producten maken voor gebruik in het gegroepeerde product.
1. Vul het lege gegroepeerde product met eenvoudige producten.
1. Maak een leeg gegroepeerd product en koppel de eenvoudige producten.

   Wanneer u eenvoudige producten aan het gegroepeerde product associeert, wordt het attribuut van de soortorde (`position`) in de lading gebruikt door frontend om de bijbehorende producten in een gewenste orde te tonen. Als het kenmerk `position` niet is opgegeven, worden de producten weergegeven in de volgorde waarin ze aan het gegroepeerde product zijn toegevoegd.

Maak eerst de eenvoudige producten wanneer u gegroepeerde producten maakt met Adobe Commerce Admin. Wanneer u klaar bent om het gegroepeerde product te creëren, associeer de eenvoudige producten door hen aan het gegroepeerde product in één partij toe te wijzen.

## Voor wie is deze video?

- Webmanagers
- Handelshandelaren
- Nieuwe Adobe Commerce-ontwikkelaars die willen leren hoe ze gegroepeerde producten in Adobe Commerce kunnen maken met de REST API.

## Video-inhoud

>[!VIDEO](https://video.tv.adobe.com/v/3425920?learn=on)

## Instellen voor het gegroepeerde product

In dit voorbeeld zijn er drie eenvoudige (eerst gemaakte) producten en een gegroepeerd product. Twee eenvoudige producten worden geassocieerd met het gegroepeerde product, en dan wordt het derde eenvoudige product toegevoegd aan het gegroepeerde product.

## Het eerste eenvoudige product maken met cURL

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=a42da0096288718c9556f77549c6305f; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "product": {
    "sku": "product-sku-one",
    "name": "Simple product one",
    "attribute_set_id": 4,
    "price": 1.11,
    "type_id": "simple"
  }
}
```

## Het tweede eenvoudige product maken met cURL

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=a42da0096288718c9556f77549c6305f; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "product": {
    "sku": "product-sku-two",
    "name": "Simple Product two",
    "attribute_set_id": 4,
    "price": 2.22,
    "type_id": "simple"
  }
}
```

## Het derde eenvoudige product maken met cURL

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=a42da0096288718c9556f77549c6305f; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "product": {
    "sku": "product-sku-three",
    "name": "Simple product three",
    "attribute_set_id": 4,
    "price": 3.33,
    "type_id": "simple"
  }
}
```

## Een leeg gegroepeerd product maken met cURL

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=28a020734488eef2600f8d5c7f302b53; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
    "product":{
        "sku":"my-new-grouped-product",
        "name":"This is my New Grouped Product",
        "attribute_set_id":4,
        "type_id":"grouped",
        "visibility":4
    }
}
'
```

## Voeg de eerste en tweede eenvoudige producten toe aan het gegroepeerde product

```bash
curl --location '{{your.url.here}}/rest/default/V1/products/my-new-grouped-product/links' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=28a020734488eef2600f8d5c7f302b53; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
    "items":[
        {
            "sku":"my-new-grouped-product",
            "link_type":"associated",
            "linked_product_sku":"product-sku-one",
            "linked_product_type":"simple",
            "position":1,
            "extension_attributes":{
            "qty":1
            }
        },
        {
            "sku":"my-new-grouped-product",
            "link_type":"associated",
            "linked_product_sku":"product-sku-two",
            "linked_product_type":"simple",
            "position":2,
            "extension_attributes":{
            "qty":1
            }
        }
    ]
}
'
```

## Het derde eenvoudige product toevoegen aan het bestaande gegroepeerde product

Neem het juiste positienummer op (alles behalve `1` of `2` ) dat wordt gebruikt voor de eerste twee producten die oorspronkelijk aan het gegroepeerde product zijn gekoppeld. In dit voorbeeld is de positie `4` .

```bash
curl --location --request PUT '{{your.url.here}}/rest/default/V1/products/my-new-grouped-product/links' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=9e61396705e9c17423eca2bdf2deefb2' \
--data '{
    "entity":{
        "sku":"my-new-grouped-product",
        "link_type":"associated",
        "linked_product_sku":"product-sku-three",
        "linked_product_type":"simple",
        "position":4,
        "extension_attributes":{
            "qty":1
        }
    }
}

'
```

## Een eenvoudig product uit een gegroepeerd product verwijderen

Om [ een eenvoudig product ](https://developer.adobe.com/commerce/webapi/rest/tutorials/grouped-product/) van een gegroepeerd product te schrappen, gebruik: `DELETE /V1/products/{sku}/links/{type}/{linkedProductSku}`.

Als u wilt weten wat u als `{type}` wilt gebruiken, gebruikt u xdebug om de aanvraag vast te leggen en de $linkTypes: `related`, `crosssell`, `uupsell` en `associated` te evalueren.
![ Gegroepeerde de verbindingstypes van Product - alt tekst ](/help/assets/site-management/catalog/grouped-types.png " Gegroepeerde productverbindingstypes die tijdens xdebug zitting ") worden gevangen

Wanneer de eenvoudige producten aan het gegroepeerde product worden gekoppeld, bevatte de lading een paar secties gelijkend op:

```bash
        {
            "sku":"my-new-grouped-product",
            "link_type":"associated",
            "linked_product_sku":"product-sku-two",
            "linked_product_type":"simple",
            "position":2,
            "extension_attributes":{
            "qty":1
            }
        }
```

In de payload geeft de `link_type` value `associated` de `{type}` -waarde op die in de aanvraag DELETE wordt vereist. De aanvraag-URL is vergelijkbaar met `/V1/products/my-new-grouped-product/links/associated/product-sku-three` .

Zie het cURL-verzoek om het eenvoudige product te verwijderen met de `product-sku-three` SKU van het gegroepeerde product met de `my-new-grouped-product` SKU:

```bash
curl --location --request DELETE '{{your.url.here}}rest/default/V1/products/my-new-grouped-product/links/associated/product-sku-three' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=9e61396705e9c17423eca2bdf2deefb2'
```

## Een gegroepeerd product ophalen met cURL

```bash
curl --location '{{your.url.here}}rest/default/V1/products/some-grouped-product-sku' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=3b797a6cc3c5c71f2193109fb9838b12'
```

## Aanvullende bronnen

- [ creeer en beheer gegroepeerde producten ](https://developer.adobe.com/commerce/webapi/rest/tutorials/grouped-product/){target="_blank"} 
- [ Gegroepeerd Product ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-grouped.html?lang=nl-NL){target="_blank"} 
- [ Adobe Developer REST zelfstudies ](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"} 
- [ Adobe Commerce REST ReDoc ](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"} 

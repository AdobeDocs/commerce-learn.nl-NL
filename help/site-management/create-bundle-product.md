---
title: Een bundelproduct maken
description: Leer hoe u een bundelproduct maakt met de REST API en de Commerce Admin.
kt: 14589
doc-type: video
audience: all
activity: use
last-substantial-update: 2024-1-8
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
exl-id: 5d688e6a-ae8c-4a55-b16c-5d3ae2d1bfd5
source-git-commit: 765bf4159892416e02ea1e9b8e4fa69e396d40af
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# Een bundelproduct maken

Een bundelproduct is een manier om verschillende producten onder een ouder product te groeperen. Deze kindproducten kunnen een bepaalde reeks producten zijn of een paar variaties aanbieden die flexibele configuratieopties voor klanten verstrekken. De de producttypes van de bundel nemen wat langer aan opstelling, en u moet wat planning doen alvorens u hen vormt. Het aanbieden van gebundelde producten verbetert echter de boodschapervaring doordat het voor klanten gemakkelijker wordt om hun productselecties aan te passen.

U kunt bijvoorbeeld een productbundel met de naam `Learning to surf` in uw webwinkel aanbieden. De bundel is het ouderproduct dat als container voor de toegewezen kindproducten dient die beschikbare opties specificeren:

- Een standaard surfbord
- Een typisch surfbordleash
- Rood surfboardvinnen

Wanneer extra flexibiliteit gewenst is, wordt aanbevolen om verschillende opties voor onderliggende producten toe te staan. Dit vereist een complexer gebruik van opties en onderliggende producten. De laatste opties zijn als u het vorige voorbeeld wilt uitvouwen:

- Een standaard surfbord
- Een typisch surfbordleash
- Keuze van vinkleur:
   - Rood
   - Blauw
   - Geel

Of de bundel een statische groep eenvoudige producten of verscheidene producten met variaties is, de flexibele configuratieopties maken de types van bundelproduct een uniek en krachtig handelsmiddel voor de opslag van Adobe Commerce.

Voordat u een bundelproduct maakt, controleert u of alle eenvoudige producten die u in het bundelproduct wilt opnemen, beschikbaar zijn in Adobe Commerce. Maak een bestand dat niet bestaat.

In deze zelfstudie leert u hoe u een bundelproduct kunt maken met de REST API en de Adobe Commerce Admin.

Gebruik de REST API om een bundelproduct te definiëren:

1. Maak eenvoudige producten voor gebruik in het bundelproduct.
1. Maak een bundelproduct en koppel de eenvoudige producten.
1. Haal het bundelproduct en alle bijbehorende opties op.
1. Verwijder een optie uit één sectie van de bundelproducten.
1. Herstel de opties voor een bundelproduct.

Wanneer u bundelproducten maakt met Adobe Commerce Admin, kunt u eerst de eenvoudige producten maken of met het geautomatiseerde gereedschap eenvoudige producten maken met een wizard.

## Voor wie is deze video?

- Webmanagers
- Handelshandelaren
- Nieuwe Adobe Commerce-ontwikkelaars die willen leren hoe u in Adobe Commerce bundelproducten kunt maken met de REST API

## Video-inhoud

>[!VIDEO](https://video.tv.adobe.com/v/3426797?learn=on)

## Producten maken met REST

Met de volgende opdrachten maakt u alle producten die nodig zijn om het bundelproduct in dit voorbeeld te definiëren: vijf eenvoudige producten en één bundelproduct met drie opties.

Voordat u de aanvraag verzendt, werkt u het voorbeeld bij met waarden voor de omgeving.

- Wijzig `"attribute-set": 4` in het vervangen van `4` door de id van de kenmerkset in uw omgeving.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "10-ft-beginner-surfboard",
    "name": "10 Foot Beginner surfboard",
    "attribute_set_id": 4,
    "price": 100,
    "type_id": "simple",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      }
    }
  }
}
'
```

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "8-ft-surboard-leash",
    "name": "8 Foot surboard leash",
    "attribute_set_id": 4,
    "price": 50,
    "type_id": "simple",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      }
    }
  }
}
'
```

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "red-fins-and-fin-plugs",
    "name": "Red fins and fin plugs",
    "attribute_set_id": 4,
    "price": 15,
    "type_id": "simple",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      }
    }
  }
}
'
```

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "blue-fins-and-fin-plugs",
    "name": "Blue fins and fin plugs",
    "attribute_set_id": 4,
    "price": 15,
    "type_id": "simple",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      }
    }
  }
}
'
```

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "yellow-fins-and-fin-plugs",
    "name": "Yellow fins and fin plugs",
    "attribute_set_id": 4,
    "price": 15,
    "type_id": "simple",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      }
    }
  }
}
'
```

## Een bundelproduct maken en de eenvoudige producten toewijzen als opties

Maak een bundelproduct door het volgende verzoek om POST te verzenden.

Voordat u de aanvraag verzendt, werkt u het voorbeeld bij met waarden voor de omgeving.

- Wijzig `"attribute_set_id": 4,` en vervang `4` door de id van de kenmerkset in uw omgeving.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "beginner-surfboard",
    "name": "Beginner Surfboard",
    "attribute_set_id": 4,
    "status": 1,
    "visibility": 4,
    "type_id": "bundle",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      },
      "bundle_product_options": [
        {
          "option_id": 0,
          "position": 1,
          "sku": "surfboard-essentials",
          "title": "Beginners 10ft Surfboard",
          "type": "checkbox",
          "required": true,
          "product_links": [
            {
              "sku": "10-ft-beginner-surfboard",
              "option_id": 1,
              "qty": 1,
              "position": 1,
              "is_default": false,
              "price": 100,
              "price_type": 0,
              "can_change_quantity": 0
            }
          ]
        },
        {
          "option_id": 1,
          "position": 2,
          "sku": "surboard-leash",
          "title": "Surfboard leash",
          "type": "checkbox",
          "required": true,
          "product_links": [
            {
              "sku": "8-ft-surboard-leash",
              "option_id": 2,
              "qty": 1,
              "position": 1,
              "is_default": false,
              "price": 50,
              "price_type": 0,
              "can_change_quantity": 0
            }
          ]
        },
        {
          "option_id": 3,
          "position": 2,
          "sku": "surfboard-color",
          "title": "Choose a color for the fins and fin plugs",
          "type": "radio",
          "required": true,
          "product_links": [
            {
              "sku": "red-fins-and-fin-plugs",
              "option_id": 2,
              "qty": 1,
              "position": 1,
              "is_default": false,
              "price": 0,
              "price_type": 0,
              "can_change_quantity": 0
            },
            {
              "sku": "blue-fins-and-fin-plugs",
              "option_id": 2,
              "qty": 1,
              "position": 2,
              "is_default": false,
              "price": 0,
              "price_type": 0,
              "can_change_quantity": 0
            },
            {
              "sku": "yellow-fins-and-fin-plugs",
              "option_id": 3,
              "qty": 1,
              "position": 3,
              "is_default": false,
              "price": 0,
              "price_type": 0,
              "can_change_quantity": 0
            }
          ]
        }
      ]
    },
    "custom_attributes": [
      {
        "attribute_code": "price_view",
        "value": "0"
      }
    ]
  },
  "saveOptions": true
}
'
```

## Een optie uit een bundelproduct verwijderen

Verwijder een onderliggend product uit een bundelproduct zonder het product uit de catalogus te verwijderen door het volgende DELETE-verzoek via cURL te verzenden.

```bash
curl --location --request DELETE '{{your.url.here}}/rest/default/V1/bundle-products/beginner-surfboard/options/35/children/blue-fins-and-fin-plugs' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3'
```

## Productopties herstellen

Wanneer u de opties voor bundelproducten bijwerkt, moet u alle opties opnemen die u aan dit product wilt koppelen. Als uw oorspronkelijke optieset drie producten bevatte en één werd verwijderd, omvat alle drie opties in het verzoek van de POST om ervoor te zorgen dat de productbundel alle opties specificeert. Als u alleen de optie hebt opgenomen die u hebt verwijderd, bevat de bijgewerkte productbundel alleen die optie.

Zoek de optie-id door de reactie van de aanmaak voor het bundelproduct te bekijken. In dat antwoord is de waarde `option_id` `35` .

```json
...
,
            {
                "option_id": 35,
                "title": "added back color options for fins and fin plugs",
                "required": true,
                "type": "radio",
                "position": 2,
                "sku": "beginner-surfboard",
                "product_links": [
                    {
                        "id": "77",
                        "sku": "red-fins-and-fin-plugs",
                        "option_id": 35,
                        "qty": 1,
                        "position": 1,
                        "is_default": false,
                        "price": 15,
                        "price_type": null,
                        "can_change_quantity": 0
                    },
                    {
                        "id": "78",
                        "sku": "blue-fins-and-fin-plugs",
                        "option_id": 35,
                        "qty": 1,
                        "position": 2,
                        "is_default": false,
                        "price": 15,
                        "price_type": null,
                        "can_change_quantity": 0
                    },
                    {
                        "id": "79",
                        "sku": "yellow-fins-and-fin-plugs",
                        "option_id": 35,
                        "qty": 1,
                        "position": 3,
                        "is_default": false,
                        "price": 15,
                        "price_type": null,
                        "can_change_quantity": 0
                    }
                ]
            }
...
```

Werk de productbundel bij om de optie toe te voegen u door het volgende verzoek van de POST te voorleggen schrapte.

```bash
curl --location '{{your.url.here}}/rest/default/V1/bundle-products/options/add' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "option": {
    "option_id": 35,
    "title": "Choose a color for the fins and fin plugs",
    "required": true,
    "type": "radio",
    "position": 2,
    "sku": "beginner-surfboard",
    "product_links": [
      {
        "sku": "red-fins-and-fin-plugs",
        "option_id": 35,
        "qty": 1,
        "position": 1,
        "is_default": false,
        "price": 0,
        "price_type": null,
        "can_change_quantity": 0,
        "extension_attributes": {}
      },
      {
        "sku": "blue-fins-and-fin-plugs",
        "option_id": 35,
        "qty": 1,
        "position": 2,
        "is_default": false,
        "price": 0,
        "price_type": null,
        "can_change_quantity": 0,
        "extension_attributes": {}
      },
      {
        "sku": "yellow-fins-and-fin-plugs",
        "option_id": 35,
        "qty": 1,
        "position": 3,
        "is_default": false,
        "price": 0,
        "price_type": null,
        "can_change_quantity": 0,
        "extension_attributes": {}
      }
    ],
    "extension_attributes": {}
  }
}'
```

## Aanvullende bronnen

- [ creeer een leerprogramma van het bundelproduct ](https://developer.adobe.com/commerce/webapi/rest/tutorials/bundle-product/){target="_blank"} 
- [ Bundel Product ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-bundle.html){target="_blank"} 
- [ Adobe Developer REST zelfstudies ](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"} 
- [ Adobe Commerce REST ReDoc ](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"} 

---
title: Een configureerbaar product maken
description: Leer hoe u een configureerbaar product maakt met de REST API en de Commerce Admin.
kt: 14586
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-12-15T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
exl-id: 112bec9a-0f8e-4252-8c52-f486a5e663b5
source-git-commit: 765bf4159892416e02ea1e9b8e4fa69e396d40af
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---

# Een configureerbaar product maken

Een configureerbaar product is een bovenliggend product van meerdere eenvoudige producten. Definieer een configureerbaar product waarbij de koper een of meer keuzes moet maken om een specifieke productvariatie te selecteren. Als het product bijvoorbeeld een shirt is, moet de koper de grootte en de kleur kiezen om het shirt te selecteren.

Hoewel een configureerbaar product meer SKU&#39;s gebruikt en aanvankelijk iets langer aan opstelling kan nemen, kan het u tijd in het eind besparen. Als u uw zaken wilt kweken, is het configureerbare producttype een goede keus voor producten met veelvoudige opties.

Voordat u een configureerbaar product maakt, controleert u of alle eenvoudige producten die u in het configureerbare product wilt opnemen, beschikbaar zijn in Adobe Commerce. Maak een bestand dat niet bestaat.

In deze zelfstudie leert u hoe u een configureerbaar product kunt maken met de REST API en de Adobe Commerce Admin.

Gebruik de REST API om een configureerbaar product te maken:

1. Krijg de attributen voor een [ geplaatst attribuut ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-sets.html?lang=nl-NL) om de aantallen van identiteitskaart voor verdere API vraag te gebruiken.
1. Creeer eenvoudige producten voor gebruik in het configureerbare product.
1. Maak een leeg configureerbaar product en koppel de eenvoudige producten.
1. Stel de productkenmerken in voor het configureerbare product.
1. Vul het lege configureerbare product met eenvoudige producten.
1. Krijg het configureerbare product en alle attributen.
1. Krijg de toegewezen kindproducten voor het configureerbare product.
1. Verwijder de associatie van eenvoudige producten met configureerbare producten.

Wanneer het creëren van configureerbare producten van Adobe Commerce Admin, kunt u of de eenvoudige producten eerst creëren, of het geautomatiseerde hulpmiddel gebruiken dat tot nieuwe eenvoudige producten voor gebruik gebruikend de tovenaar leidt.

## Voor wie is deze video?

- Webmanagers
- Handelshandelaren
- Nieuwe Adobe Commerce-ontwikkelaars die willen leren hoe u configureerbare producten in Adobe Commerce kunt maken met de REST API

## Video-inhoud

>[!VIDEO](https://video.tv.adobe.com/v/3426381?learn=on)

## De kleurkenmerken ophalen met cURL

In dit voorbeeld wordt het gehele kenmerk dat met alle afzonderlijke kenmerken is ingesteld, geretourneerd voor kenmerk set 10. Het kan lang zijn, honderden regels zijn niet ongewoon. Als u de reactie bekijkt, staat de ID van het kenmerk voor kleur waarschijnlijk in het midden. U kunt de zoekopdracht naar deze waarden versnellen door grep of andere methoden te gebruiken om de resultaten te zoeken. Mijn antwoord was bijna regel 665 en is opgenomen in het volgende fragment uit het JSON-antwoord.

```json
...
{
        "attribute_id": 93,
        "attribute_code": "color",
        "frontend_input": "select",
        "entity_type_id": "4",
        "is_required": false,
        "options": [
            {
                "label": " ",
                "value": ""
            },
            {
                "label": "Red",
                "value": "13"
            },
            {
                "label": "Blue",
                "value": "14"
            },
            {
                "label": "Green",
                "value": "15"
            }
        ],
...
```


Als u de kenmerken-id&#39;s wilt ophalen om het configureerbare product in te stellen, werkt u het `attribute-sets/10/attributes` -gedeelte van de volgende cURL-aanvraag bij om `10` te vervangen door de id van de kenmerkset in uw omgeving. In dit verzoek wordt de methode GET gebruikt.

```bash
curl --location '{{your.url.here}}rest/V1/products/attribute-sets/10/attributes' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Het eerste eenvoudige product maken met cURL

### Omgevings-id&#39;s en productdetails aanpassen

Maak het eerste eenvoudige product met behulp van de API en verzend de volgende POST request via cURL.

Voordat u de aanvraag verzendt, werkt u het voorbeeld bij met waarden voor de omgeving.

- Wijzig `"attribute-set": 10` in het vervangen van `10` door de id van de kenmerkset in uw omgeving.
- Wijzig `"value": "13"` in het vervangen van `13` door de waarde uit de omgeving.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "product": {
    "sku": "Kids-Hawaiian-Ukulele-red",
    "name": "Kids Hawaiian Ukulele Red",
    "attribute_set_id": 10,
    "price": 12.50,
    "status": 1,
    "visibility": 1,
    "type_id": "simple",
    "weight": "0.5",
    "extension_attributes": {
        "stock_item": {
            "qty": "10",
            "is_in_stock": true
        }
    },
    "custom_attributes": [
        {
            "attribute_code": "color",
            "value": "13"
        }
    ]
  }
}
'
```

## Het tweede eenvoudige product maken met cURL

Maak het tweede eenvoudige product met behulp van de API en verzend de volgende POST request via cURL.

Voordat u de aanvraag verzendt, werkt u het voorbeeld bij met waarden voor de omgeving.

- Wijzig `"attribute_set_id": 10,` en vervang `10` door de id van de kenmerkset in uw omgeving.
- Wijzig `"value": "14"` en vervang `14` door de waarde uit de omgeving.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "product": {
    "sku": "Kids-Hawaiian-Ukulele-Blue",
    "name": "Kids Hawaiian Ukulele Blue",
    "attribute_set_id": 10,
    "price": 15,
    "status": 1,
    "visibility": 1,
    "type_id": "simple",
    "weight": "0.5",
    "extension_attributes": {
        "stock_item": {
            "qty": "20",
            "is_in_stock": true
        }
    },
    "custom_attributes": [
        {
            "attribute_code": "color",
            "value": "14"
        }
    ]
  }
}
'
```

## Het derde eenvoudige product maken met cURL

Maak het derde eenvoudige product door het volgende verzoek om POST via cURL te verzenden.

Voordat u de aanvraag verzendt, werkt u het voorbeeld bij met waarden voor de omgeving.

- Wijzig `"attribute_set_id": 10,` in het vervangen van `10` door de id van de kenmerkset in uw omgeving.
- Wijzig `"value": "15"` en vervang `15` door de waarde uit de omgeving.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "product": {
    "sku": "Kids-Hawaiian-Ukulele-Green",
    "name": "Kids Hawaiian Ukulele Green",
    "attribute_set_id": 10,
    "price": 25,
    "status": 1,
    "visibility": 1,
    "type_id": "simple",
    "weight": "0.5",
    "extension_attributes": {
        "stock_item": {
            "qty": "30",
            "is_in_stock": true
        }
    },
    "custom_attributes": [
        {
            "attribute_code": "color",
            "value": "15"
        }
    ]
  }
}
'
```

## Een leeg configureerbaar product maken met cURL

Maak een leeg configureerbaar product door de volgende POST met cURL te verzenden.

Voordat u de aanvraag verzendt, werkt u het voorbeeld bij met waarden voor de omgeving.

- Wijzig `"attribute_set_id": 10,` en vervang `10` door de id van de kenmerkset in uw omgeving.
- Wijzig `"value": "93"` en vervang `93` door de waarde uit de omgeving.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "product": {
    "sku": "Kids-Hawaiian-Ukulele",
    "name": "Kids Hawaiian Ukulele",
    "attribute_set_id": 10,
    "status": 1,
    "visibility": 4,
    "type_id": "configurable",
    "weight": "0.5",
    "custom_attributes": [
        {
            "attribute_code": "color",
            "value": "93"
        }
    ]
  }
}'
```

## De beschikbare opties voor het configureerbare product instellen

Stel de beschikbare opties voor het configureerbare product in door het volgende verzoek van de POST via cURL te verzenden.

Voordat u de aanvraag verzendt, wijzigt u `"attribute_id": 93,` in Vervangen door de id van het kenmerk van `93` vanuit de omgeving.

```bash
curl --location '{{your.url.here}}/rest/default/V1/configurable-products/Kids-Hawaiian-Ukulele/options' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "option": {
    "attribute_id": "93",
    "label": "Color",
    "position": 0,
    "is_use_default": true,
    "values": [
      {
        "value_index": 9
      }
    ]
  }
}'
```

Als u vergeet om de opties voor het configureerbare product (ouder) te plaatsen, krijgt u een fout wanneer u probeert om een kindproduct aan het configureerbare product te associëren. Het foutbericht is vergelijkbaar met het volgende voorbeeld:

`{"message":"The parent product doesn't have configurable product options.","trace":"#0 [internal function]: Magento\\ConfigurableProduct\\Model\\LinkManagement->addChild('Kids-Hawaiian-U...'}`

## Koppel het kindproduct aan configureerbaar

U hebt nu drie eenvoudige producten gemaakt:

- `"Kids Hawaiian Ukulele Red"` ,
- `"Kids-Hawaiian-Ukulele-Blue"`
- `"Kids-Hawaiian-Ukulele-Green"`

Voeg deze eenvoudige producten als kinderen van het configureerbare product toe door het volgende verzoek van de POST te verzenden. Voor elk product een afzonderlijk verzoek indienen.

Werk voor elke aanvraag de waarde `childSKU` bij met de waarde voor het onderliggende product dat u toevoegt. In het volgende voorbeeld wordt het eenvoudige product `kids-Hawaiian-Ukulele-red` toegewezen aan het configureerbare product met de SKU `Kids-Hawaiian-Ukulele-red` .


```bash
curl --location '{{your.url.here}}rest/default/V1/configurable-products/Kids-Hawaiian-Ukulele/child' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "childSku": "Kids-Hawaiian-Ukulele-red"
}
'
```

## Een configureerbaar product ophalen met cURL

Nu u een configureerbaar product met drie toegewezen kind SKUs hebt gecreeerd. U kunt de gekoppelde id&#39;s voor de toegewezen producten zien door het volgende GET-verzoek via cURL te verzenden. Dit verzoek keert gedetailleerde informatie over het configureerbare product terug.

```json
...
        "configurable_product_links": [
            155,
            157,
            156
        ]
...
```

Het volgende gebruikt de methode van de GET

```bash
curl --location '{{your.url.here}}/rest/default/V1/products/Kids-Hawaiian-Ukulele' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Krijg het kindproduct verbonden aan een configureerbaar product

Keer slechts de kinderen verbonden aan het configureerbare product terug door het volgende verzoek van de GET te verzenden. Het antwoord zal alle kenmerken voor het kindproduct met inbegrip van SKU en prijs omvatten.

Het volgende gebruikt de methode van de GET

```bash
curl --location '{{your.url.here}}/rest/default/V1/configurable-products/kids-hawaiian-ukulele/children' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Een onderliggend product verwijderen of verwijderen uit het configureerbare bovenliggende product

U kunt een onderliggend product uit een configureerbaar product verwijderen zonder het product uit de catalogus te verwijderen door het volgende DELETE-verzoek via cURL te verzenden.

```bash
curl --location --request DELETE '{{your.url.here}}/rest/default/V1/configurable-products/Kids-Hawaiian-Ukulele/children/Kids-Hawaiian-Ukulele-Blue' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Aanvullende bronnen

- [ creeer een configureerbare productleerprogramma ](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/){target="_blank"} 
- [ Configureerbaar Product ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html?lang=nl-NL){target="_blank"} 
- [ Adobe Developer REST zelfstudies ](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"} 
- [ Adobe Commerce REST ReDoc ](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"} 

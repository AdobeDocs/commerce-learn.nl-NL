---
title: Een downloadbaar product maken
description: Leer hoe u een downloadbaar product maakt met de REST API en de Adobe Commerce Admin.
kt: 14464
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-11-16T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
source-git-commit: 043d873e9b649455202de9df137c7283d92a2a4a
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# Een downloadbaar product maken

Leer hoe u een downloadbaar product maakt met de REST API en de Adobe Commerce Admin.

## Voor wie is deze video?

- Webmanagers
- Handelshandelaren
- Nieuwe Adobe Commerce-ontwikkelaars die willen leren hoe u in Adobe Commerce producten kunt maken met de REST API

## Video-inhoud

>[!VIDEO](https://video.tv.adobe.com/v/3425753?learn=on)

## Toegestane downloadbare domeinen

U moet opgeven welke domeinen zijn toegestaan voor downloaden. Domeinen worden toegevoegd aan het project `env.php` bestand via de opdrachtregel. De `env.php` bestandsgegevens over de domeinen die downloadbare inhoud mogen bevatten. Er treedt een fout op als een downloadbaar product wordt gemaakt met de REST API _voor_  de `php.env` bestand is bijgewerkt:

```bash
{
    "message": "Link URL's domain is not in list of downloadable_domains in env.php."
}
```

Maak verbinding met de server om het domein in te stellen: `bin/magento downloadable:domains:add www.example.com`

Wanneer dat voltooid is, `env.php` wordt gewijzigd binnen de _downloadbaar_domeinen_ array.

```php
    'downloadable_domains' => [
        'www.example.com'
    ],
```

Nu wordt het domein toegevoegd aan de `env.php`kunt u een downloadbaar product maken in de Adobe Commerce Admin of met de REST API.

Zie [Configuratieverwijzing](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-envphp.html#downloadable_domains) voor meer informatie. Zie [CLI-referentie voor Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-operations/reference/magento-open-source.html#downloadable%3Adomains%3Aadd voor meer informatie.

>[!IMPORTANT]
>In sommige versies van Adobe Commerce kan de volgende fout optreden wanneer een product wordt bewerkt in Adobe Commerce Admin. Het product wordt gemaakt met de REST API, maar de gekoppelde download heeft een `null` prijs.

`Deprecated Functionality: number_format(): Passing null to parameter #1 ($num) of type float is deprecated in /app/vendor/magento/module-downloadable/Ui/DataProvider/Product/Form/Modifier/Data/Links.php on line 228`.

Gebruik de API voor bijwerken van koppelingen om deze fout te corrigeren: `POST V1/products/{sku}/downloadable-links.`

Zie de [Een productdownloadkoppeling bijwerken met cURL](#update-downloadable-links) voor meer informatie.

## Een downloadbaar product maken met cURL (downloaden vanaf externe server)

In dit voorbeeld ziet u hoe u een downloadbaar product maakt met cURL wanneer het te downloaden bestand zich niet op dezelfde server bevindt. Dit is een typisch geval van gebruik als het dossier in een S3 emmertje of een andere digitale manager van activa wordt opgeslagen.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=b78cae2338f12d846d233d4e9486607e; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "product": {
    "sku": "POSTMAN-download-product-1",
    "name": "POSTMAN download product-1",
    "attribute_set_id": 4,
    "price": 9.9,
    "status": 1,
    "visibility": 4,
    "type_id": "downloadable",
    "extension_attributes": {
        "website_ids": [
            1
        ],
        
        "downloadable_product_links": [
            {
                "title": "My url link",
                "sort_order": 1,
                "is_shareable": 1,
                "price": 0,
                "number_of_downloads": 0,
                "link_type": "url",
                "link_url": "{{location.url.where.file.exists}}/some-file.zip",
                "sample_type": "url",
                "sample_url": "{{location.url.where.file.exists}}/sample-file.zip"
            }
        ],
        "downloadable_product_samples": []
    },
    "product_links": [],
    "options": [],
    "media_gallery_entries": [],
    "tier_prices": []
  }
}
'
```

## Een downloadbaar product maken met cURL (downloaden van de Commerce-toepassingsserver)

In dit voorbeeld wordt getoond hoe u cURL gebruikt om een downloadbaar product te maken van de Adobe Commerce Admin wanneer het bestand wordt opgeslagen op dezelfde server als de Adobe Commerce-toepassing.

In dit geval kiest de beheerder die de catalogus beheert `upload file`, wordt het bestand overgebracht naar de `pub/media/downloadable/files/links/` directory.  Met Automatisering worden de bestanden op basis van het volgende patroon gemaakt en verplaatst naar de respectievelijke locaties:

- Elk geüpload bestand wordt opgeslagen in een map op basis van de eerste twee tekens van de bestandsnaam.
- Wanneer het uploaden wordt geïnitieerd, leidt de toepassing van de Handel tot of gebruikt bestaande omslagen om het dossier over te brengen.
- Wanneer u het bestand downloadt, wordt `link_file` van het pad gebruikt het deel van het pad dat aan het pad is toegevoegd `pub/media/downloadable/files/links/` directory.

Als het geüploade bestand bijvoorbeeld een naam heeft `download-example.zip`:

- Het bestand wordt geüpload naar het pad `pub/media/downloadable/files/links/d/o/`.
De submappen `/d` en `/d/o` worden gemaakt als deze niet bestaan.

- Het laatste pad naar het bestand is `/pub/media/downloadable/files/links/d/o/download-example.zip`.

- De `link_url` waarde voor dit voorbeeld is `d/o/download-example.zip`

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=571f5ebe48857569cd56bde5d65f83a2; private_content_version=9f3286b427812be6aec0b04cae33ba35' \
--data '{
  "product": {
    "sku": "sample-local-download-file",
    "name": "A downloadable product with locally hosted download file",
    "attribute_set_id": 4,
    "price": 33,
    "status": 1,
    "visibility": 4,
    "type_id": "downloadable",
    "extension_attributes": {
        "website_ids": [
            1
        ],
        "downloadable_product_links": [
            {
                "title": "an api version of already upload file",
                "sort_order": 1,
                "is_shareable": 1,
                "price": 0,
                "number_of_downloads": 0,
                "link_type": "file",
                "link_file": "/d/o/downloadable-file-demo-file-upload.zip",
                "sample_type": null
            }
        ],
        "downloadable_product_samples": []
    },
    "product_links": [],
    "options": [],
    "media_gallery_entries": [],
    "tier_prices": []
  }
}'
```

## Een product ophalen met krullen

```bash
curl --location '{{your.url.here}}/rest/default/V1/products/POSTMAN-download-product-1' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=b78cae2338f12d846d233d4e9486607e; private_content_version=564dde2976849891583a9a649073f01e'
```

## Het product bijwerken met Postman {#update-downloadable-links}

Het eindpunt gebruiken `rest/all/V1/products/{sku}/downloadable-links`
De `SKU` Dit is de product-id die is gegenereerd toen het product werd gemaakt. In het onderstaande codevoorbeeld is dit bijvoorbeeld het nummer 39, maar zorg ervoor dat dit wordt bijgewerkt zodat de id van uw website wordt gebruikt. Hiermee werkt u de koppelingen naar de downloadbare producten bij.

```json
{
  "link": {
    "id": 39,
    "title": "My swagger update",
    "sort_order": 0,
    "is_shareable": 0,
    "price": 0,
    "number_of_downloads": 0,
    "link_type": "url",
    "link_file": "{{your.url.here}}/some-file.zip",
    "link_url": "{{your.url.here}}/some-file.zip",
    "link_file_content": {
      "file_data": "{{your.url.here}}/some-file.zip",
      "extension_attributes": {}
    }
  },
  "isGlobalScopeContent": true
}
```

## Een productdownloadkoppeling bijwerken met CURL

Wanneer u een koppeling voor het downloaden van een product bijwerkt via cURL, bevat de URL de SKU voor het product dat wordt bijgewerkt.  In het volgende codevoorbeeld, SKU is `abcd12345`. Als u de opdracht verzendt, wijzigt u de waarde zodat deze overeenkomt met de SKU voor het product dat u wilt bijwerken.

```bash
curl --location '{{your.url.here}}/rest/all/V1/products/abcd12345/downloadable-links' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=fa5d76f4568982adf369f758e8cb9544; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "link": {
    "id": {{The ID of the download link for example 39}},
    "title": "My update",
    "sort_order": 0,
    "is_shareable": 0,
    "price": 0,
    "number_of_downloads": 0,
    "link_type": "url",
    "link_file": "{{your.url.here}}/some-file.zip",
    "link_url": "{{your.url.here}}/some-file.zip",
    "link_file_content": {
      "file_data": "{{your.url.here}}/some-file.zip",
      "extension_attributes": {}
    }
  },
  "isGlobalScopeContent": true
}'
```

## Aanvullende bronnen

- [Downloadbaar producttype](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-downloadable.html){target="_blank"}
- [Configuratiegids voor downloadbare domeinen](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-envphp.html#downloadable_domains){target="_blank"}
- [Toevoegen aan downloadbare domeinen in .env.php](https://experienceleague.adobe.com/docs/commerce-operations/reference/magento-open-source.html#downloadable%3Adomains%3Aadd){target="_blank}
- [Adobe Developer REST-zelfstudies](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [Adobe Commerce REST ReDoc](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}

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
exl-id: 90753b8d-eca0-4868-b40e-9563d2b0e1e8
source-git-commit: eba043cd4169cd762653557bf9283b8d6a208ef0
workflow-type: tm+mt
source-wordcount: '584'
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

U moet opgeven welke domeinen zijn toegestaan voor downloaden. Domeinen worden via de opdrachtregel toegevoegd aan het `env.php` -bestand van het project. In het `env.php` -bestand worden de domeinen beschreven die downloadbare inhoud mogen bevatten. Een fout komt voor als een downloadbaar product gebruikend REST API _wordt gecreeerd alvorens_ het `php.env` dossier wordt bijgewerkt:

```bash
{
    "message": "Link URL's domain is not in list of downloadable_domains in env.php."
}
```

Maak verbinding met de server om het domein in te stellen: `bin/magento downloadable:domains:add www.example.com`

Zodra dat volledig is, wordt `env.php` gewijzigd binnen de _downloadable_domain_ serie.

```php
    'downloadable_domains' => [
        'www.example.com'
    ],
```

Nu het domein aan `env.php` wordt toegevoegd, kunt u een downloadbaar product in Adobe Commerce Admin of door REST API te gebruiken tot stand brengen.

Zie [ Verwijzing van de Configuratie ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-envphp.html#downloadable_domains) om meer te leren.

>[!IMPORTANT]
>In sommige versies van Adobe Commerce kan de volgende fout optreden wanneer een product wordt bewerkt in Adobe Commerce Admin. Het product wordt gemaakt met de REST API, maar de gekoppelde download heeft een prijs `null` .

`Deprecated Functionality: number_format(): Passing null to parameter #1 ($num) of type float is deprecated in /app/vendor/magento/module-downloadable/Ui/DataProvider/Product/Form/Modifier/Data/Links.php on line 228`.

Gebruik de API voor bijwerken om deze fout te corrigeren: `POST V1/products/{sku}/downloadable-links.`

Zie [ een verbinding van de productdownload bijwerken gebruikend cURL ](#update-downloadable-links) sectie voor meer info.

## Een downloadbaar product maken met cURL (downloaden vanaf externe server)

In dit voorbeeld ziet u hoe u een downloadbaar product maakt met cURL wanneer het te downloaden bestand zich niet op dezelfde server bevindt. Dit is een typisch geval van gebruik als het dossier in een S3 emmertje of een andere digitale manager van activa wordt opgeslagen.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=b78cae2338f12d846d233d4e9486607e; private_content_version=564dde2976849891583a9a649073f01' \
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

## Een downloadbaar product maken met cURL (downloaden vanaf Commerce-toepassingsserver)

In dit voorbeeld wordt getoond hoe u cURL gebruikt om een downloadbaar product te maken van de Adobe Commerce Admin wanneer het bestand wordt opgeslagen op dezelfde server als de Adobe Commerce-toepassing.

In dit geval wordt het bestand overgebracht naar de map `pub/media/downloadable/files/links/` wanneer de beheerder van de catalogus `upload file` kiest.  Met Automatisering worden de bestanden op basis van het volgende patroon gemaakt en verplaatst naar de respectievelijke locaties:

- Elk geüpload bestand wordt opgeslagen in een map op basis van de eerste twee tekens van de bestandsnaam.
- Wanneer het uploaden wordt gestart, maakt of gebruikt de Commerce-toepassing bestaande mappen om het bestand over te brengen.
- Wanneer u het bestand downloadt, gebruikt de sectie `link_file` van het pad het gedeelte van het pad dat aan de map `pub/media/downloadable/files/links/` is toegevoegd.

Als het geüploade bestand bijvoorbeeld de naam `download-example.zip` heeft:

- Het bestand wordt geüpload naar het pad `pub/media/downloadable/files/links/d/o/` .
De submappen `/d` en `/d/o` worden gemaakt als ze niet bestaan.

- Het laatste pad naar het bestand is `/pub/media/downloadable/files/links/d/o/download-example.zip` .

- De `link_url` -waarde voor dit voorbeeld is `d/o/download-example.zip`

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
De `SKU` is de product-id die is gegenereerd toen het product werd gemaakt. In het onderstaande codevoorbeeld is dit bijvoorbeeld het nummer 39, maar zorg ervoor dat dit wordt bijgewerkt zodat de id van uw website wordt gebruikt. Hiermee werkt u de koppelingen naar de downloadbare producten bij.

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

Wanneer u een koppeling voor het downloaden van een product bijwerkt via cURL, bevat de URL de SKU voor het product dat wordt bijgewerkt.  In het volgende codevoorbeeld, is SKU `abcd12345`. Als u de opdracht verzendt, wijzigt u de waarde zodat deze overeenkomt met de SKU voor het product dat u wilt bijwerken.

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

- [ Downloadbaar Type van Product ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-downloadable.html){target="_blank"} 
- [ Downloadbare Gids van de Configuratie van Domeinen ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-envphp.html#downloadable_domains){target="_blank"} 
- [ Adobe Developer REST zelfstudies ](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"} 
- [ Adobe Commerce REST ReDoc ](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"} 

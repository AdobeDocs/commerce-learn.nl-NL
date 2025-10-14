---
title: Hoe kan ik-gegevens opvragen
description: Leer hoe u gegevens voor een Adobe Commerce Optimizer-instantie kunt opvragen.
feature: Saas, Storefront
topic: Commerce
role: Developer
level: Beginner
doc-type: Tutorial
duration: 182
last-substantial-update: 2025-08-13T00:00:00Z
jira: KT-18548
exl-id: bad3d926-2952-4bac-b685-adb16f009f8d
source-git-commit: 5d34c2e3b93c937139e88fa2f75dc6046f7093fc
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Query-gegevens Adobe Commerce Optimizer

Leer hoe u via GraphQL query&#39;s uitvoert op gegevens in een Adobe Commerce Optimizer-instantie.

## Voor wie is deze video?

* Commerce Solution Architect en ontwikkelaars

## Video-inhoud

* Query-gegevens uitvoeren met GraphQL
* De jq gebruiken om de json beter leesbaar te maken

>[!VIDEO](https://video.tv.adobe.com/v/3470806?learn=on&enablevpops&captions=dut)

## Codevoorbeelden

U moet waarden als `{{insert-your-graphql-endpoint-url}}` , `{{insert-your-ac-view-id}}` en `{{your-search-query-string}}` uitwisselen met de waarden die nodig zijn voor de query.

Standaardvoorbeeldquery

```bash
curl '{{insert-your-graphql-endpoint-url}}' \
-H 'Content-Type: application/json' \
-H 'AC-View-ID: {{insert-your-ac-view-id}}' \
-d '{"query": "query ProductSearch($search: String!) { productSearch( phrase: $search, page_size: 10, current_page: 2) { items { productView { sku name description shortDescription images { url } ... on SimpleProductView { attributes { label name value } price { regular { amount { value currency } } roles } } } } } }", "variables": { "search": "{{your-search-query-string}}"}}'
```

Standaardvoorbeeldquery met `jq` om de uitvoer vrij af te drukken

```bash
curl '{{insert-your-graphql-endpoint-url}}' \
-H 'Content-Type: application/json' \
-H 'AC-View-ID: {{insert-your-ac-view-id}}' \
-d '{"query": "query ProductSearch($search: String!) { productSearch( phrase: $search, page_size: 10, current_page: 2) { items { productView { sku name description shortDescription images { url } ... on SimpleProductView { attributes { label name value } price { regular { amount { value currency } } roles } } } } } }", "variables": { "search": "{{your-search-query-string}}"}}' | jq .
```

## Gerelateerde inhoud

* [&#x200B; Begonnen het worden met Merchandising API &#x200B;](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api/#make-your-first-request){target="_blank"}
* [[!DNL Adobe Commerce Optimizer]  Gids &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce/optimizer/overview){target="_blank"}

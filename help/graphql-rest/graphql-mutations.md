---
title: Een mutatie uitvoeren met GraphQL
description: Ontvang een inleiding over het uitvoeren van een mutatie met GraphQL op Adobe Commerce en [!DNL Magento Open Source]. Voer uw eerste mutatie uit gebruikend de vraag van de POST.
landing-page-description: Ontvang een inleiding over het uitvoeren van een mutatie met GraphQL op Adobe Commerce en [!DNL Magento Open Source]. Voer uw eerste mutatie uit gebruikend de vraag van de POST.
short-description: Ontvang een inleiding over het uitvoeren van een mutatie met GraphQL op Adobe Commerce en [!DNL Magento Open Source]. Voer uw eerste mutatie uit gebruikend de vraag van de POST.
kt: 13938
doc-type: video
audience: all
last-substantial-update: 2023-10-12T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 6b82ffda-925f-4a81-8ca5-49a2b8ab4929
source-git-commit: 2041bbf1a2783975091b9806c12fc3c34c34582f
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Mutaties

Dit is deel 3 van de reeks voor GraphQL en Adobe Commerce. Mutaties zijn de mogelijkheid om waarden op te slaan, bij te werken en te retourneren met GraphQL.


>[!VIDEO](https://video.tv.adobe.com/v/3424121?learn=on)

## Verwante video&#39;s en zelfstudies over GraphQL in deze serie

* [Deel 1 GraphQL - Inleiding](../graphql-rest/intro-graphql.md)
* [Deel 2 GraphQL - Vragen](../graphql-rest/graphql-queries.md)
* [Deel 4 GraphQL - Schema](../graphql-rest/graphql-schema.md)

## Voorbeeldmutatie

Elke volledige API-specificatie moet de mogelijkheid bieden om niet alleen query&#39;s uit te voeren, maar ook om gegevens te maken en bij te werken.

REST maakt onderscheid tussen verzoeken die gegevens veranderen en die die niet met het verzoektype of &quot;werkwoord&quot; (GET vs. POST of PUT).
Bij gebruik van GraphQL worden query&#39;s voor gegevenswijziging onderscheiden door de `mutation` trefwoord dat overeenkomt met een ander hoofdtype in het schema dat op de server is gedefinieerd.

Bekijk deze voorbeeldmutatie voor het toevoegen van een product aan de kar van een gebruiker. (Dit vereist een kartidentiteitskaart die voor de het programma geopende klantenzitting of gebruikend werd geproduceerd `createEmptyCart` mutatie.)

```graphql
mutation doAddToCart(
    $cartId: String!,
    $cartItems: [CartItemInput!]!
) {
    addProductsToCart(
        cartId: $cartId
        cartItems: $cartItems
    ) {
        cart {
            total_quantity
            prices {
                grand_total {
                    value
                }
            }
        }
    }
}
```

U kunt zich voorstellen dat de bovenstaande mutatie wordt verzonden in een verzoek samen met het volgende Variables-woordenboek:

```json
{
  "cartId": "{cart-id}",
  "cartItems": [
    {
      "quantity": 1,
      "sku": "VT01-RN-XS"
    }
  ]
}
```

Tot slot zou je een reactie als deze kunnen krijgen:

```json
{
  "data": {
    "addProductsToCart": {
      "cart": {
        "total_quantity": 1,
        "prices": {
          "grand_total": {
            "value": 35.2
          }
        }
      }
    }
  }
}
```

Het belangrijkste om op te merken dat in het bovenstaande voorbeeld, behalve het gebruik van de `mutation` trefwoord in plaats van `query`, is de syntaxis identiek aan een query. Net als query&#39;s omvat de mutatie:

* De naam van een willekeurige bewerking (`doAddToCart`)
* Een lijst met variabelen (bijvoorbeeld `$cartId`)
* Een beginveld (`addProductsToCart`) met argumenten (bijvoorbeeld `cartId`, ingesteld op de waarde van `$cartId`) tussen haakjes
* Een subselectie van velden tussen accolades

Met de subselectie voor velden kunt u op flexibele wijze de velden definiëren die u wilt retourneren (van het type dat is toegewezen als de geretourneerde waarde van `addProductsToCart` - `AddProductsToCartOutput`) nadat de mutatie is voltooid.

Zoals eerder is uitgelegd, beginnen velden die in een GraphQL-schema zijn gedefinieerd, op een hoofdtype voor query&#39;s (doorgaans aangeduid als een `Query`). Op dezelfde manier bestaat er een ander worteltype voor mutaties (die typisch als worden bedoeld `Mutation`). `addProductsToCart` is een veld op dat basistype.

Een paar andere opmerkingen over het bovenstaande voorbeeld:

* De `!` achtervoegsel teken `String` en `CartItemInput` Hiermee wordt aangegeven dat de variabele verplicht is.
* De vierkante haakjes (`[]`) rond de `CartItemInput` type opgegeven voor `$cartItems` Geef een lijst van dat type op in plaats van één waarde.

{{$include /help/_includes/graphql-rest-related-links.md}}

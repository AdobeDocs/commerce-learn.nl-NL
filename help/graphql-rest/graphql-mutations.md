---
title: Een mutatie uitvoeren met GraphQL
description: Krijg een inleiding over het uitvoeren van een mutatie gebruikend GraphQL op Adobe Commerce en  [!DNL Magento Open Source]. Voer uw eerste mutatie uit gebruikend POST vraag.
landing-page-description: Krijg een inleiding over het uitvoeren van een mutatie gebruikend GraphQL op Adobe Commerce en  [!DNL Magento Open Source]. Voer uw eerste mutatie uit gebruikend POST vraag.
short-description: Krijg een inleiding over het uitvoeren van een mutatie gebruikend GraphQL op Adobe Commerce en  [!DNL Magento Open Source]. Voer uw eerste mutatie uit gebruikend POST vraag.
kt: 13938
doc-type: video
audience: all
last-substantial-update: 2023-10-12T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: 6b82ffda-925f-4a81-8ca5-49a2b8ab4929
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Mutaties

Dit is deel 3 van de reeks voor GraphQL en Adobe Commerce. Mutaties zijn de mogelijkheid om waarden op te slaan, bij te werken en te retourneren met GraphQL.


>[!VIDEO](https://video.tv.adobe.com/v/3424121?learn=on)

## Verwante video&#39;s en zelfstudies over GraphQL in deze serie

* [Deel 1 GraphQL - Inleiding](../graphql-rest/intro-graphql.md)
* [Deel 2 GraphQL - Vragen](../graphql-rest/graphql-queries.md)
* [ Deel 4 GraphQL - Schema ](../graphql-rest/graphql-schema.md)

## Voorbeeldmutatie

Elke volledige API-specificatie moet de mogelijkheid bieden om niet alleen query&#39;s uit te voeren, maar ook om gegevens te maken en bij te werken.

REST maakt onderscheid tussen verzoeken die gegevens veranderen en verzoeken die niet met het verzoektype of &quot;werkwoord&quot; (GET vs. POST of PUT).
Bij het gebruik van GraphQL wordt onderscheid gemaakt tussen query&#39;s voor gegevenswijziging en het trefwoord `mutation` dat overeenkomt met een andere query
hoofdtype in het schema dat op de server is gedefinieerd.

Bekijk deze voorbeeldmutatie voor het toevoegen van een product aan de kar van een gebruiker. (Hiervoor is een kaart-id vereist die is gegenereerd
voor de aangemelde klantensessie of met behulp van de `createEmptyCart` -mutatie.)

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

Het belangrijkste wat u moet weten over het bovenstaande voorbeeld is dat, afgezien van het gebruik van het trefwoord `mutation` in plaats van `query` ,
de syntaxis is identiek aan een query. Net als query&#39;s omvat de mutatie:

* Een willekeurige bewerkingsnaam (`doAddToCart`)
* Een lijst met variabelen (bijvoorbeeld `$cartId`)
* Een beginveld (`addProductsToCart`) met argumenten (bijvoorbeeld `cartId` , ingesteld op de waarde `$cartId` ) tussen haakjes
* Een subselectie van velden tussen accolades

Met de subselectie van velden kunt u op flexibele wijze de velden definiëren die u wilt retourneren (van het type dat is toegewezen als de
retourwaarde `addProductsToCart` - `AddProductsToCartOutput` ) nadat de mutatie is voltooid.

Zoals eerder is uitgelegd, beginnen velden die zijn gedefinieerd in een GraphQL-schema op een hoofdtype voor query&#39;s (worden doorgaans een `Query` genoemd). Op dezelfde manier
er is een ander hoofdtype voor mutaties (wordt meestal `Mutation` genoemd). `addProductsToCart` is een veld
op dat basistype.

Een paar andere opmerkingen over het bovenstaande voorbeeld:

* De tekens `!` achtervoegsel `String` en `CartItemInput` geven aan dat de variabele verplicht is.
* De vierkante haakjes (`[]`) rondom het `CartItemInput` type dat is opgegeven voor `$cartItems` , geven een lijst aan
van dat type in plaats van één enkele waarde.

{{$include /help/_includes/graphql-rest-related-links.md}}

---
title: Schema taal met GraphQL
description: Meer informatie over het schema dat bij GraphQL is betrokken. Lees een beschrijving van het schema, samen met enkele interessante patronen en manieren om het schema te lezen.
landing-page-description: Dit is een inleiding op GraphQL. Inzicht krijgen in het schema en hoe sommige elementen worden geïnterpreteerd
short-description: Dit is een inleiding op GraphQL. Inzicht krijgen in het schema en hoe sommige elementen worden geïnterpreteerd
kt: 13939
doc-type: video
audience: all
last-substantial-update: 2023-10-12T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 6b59db07-b99e-47ae-9ccb-d4904afc8251
source-git-commit: 2041bbf1a2783975091b9806c12fc3c34c34582f
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Schema

Dit is deel 4 van de reeks voor GraphQL en Adobe Commerce. De gebruikte query&#39;s en mutaties zijn afhankelijk van een specifieke gegevensgrafiek die op de server wordt geïmplementeerd. De GraphQL-runtime gebruikt deze grafiek om de query op te lossen. De GraphQL-specificatie definieert een agnostische taal voor het uitdrukken van de typen en relaties van de gegevensgrafiek.

>[!VIDEO](https://video.tv.adobe.com/v/3424123?learn=on)

## Verwante video&#39;s en zelfstudies over GraphQL in deze serie

* [Deel 1 GraphQL - Inleiding](../graphql-rest/intro-graphql.md)
* [Deel 2 GraphQL - Vragen](../graphql-rest/graphql-queries.md)
* [Deel 3 GraphQL - Mutaties](../graphql-rest/graphql-mutations.md)

## Voorbeeldschema

Hier is een afgekort typeschema dat de vragen en de mutaties steunt u tot dusver hebt bekeken:

```graphql
input FilterMatchTypeInput {
  match: String
}

type Money {
  value: Float
}

type Country {
  id: String
  full_name_english: String
}

interface ProductInterface {
  sku: String
  name: String
  related_products: [ProductInterface]
}

type CategoryFilterInput {
  name: FilterMatchTypeInput
}

type CategoryProducts {
  items: [ProductInterface]
}

type CategoryTree {
  name: String
  products(pageSize: Int, currentPage: Int): CategoryProducts
}

type CategoryResult {
  items: [CategoryTree]
}

type Products {
  items: [ProductInterface]
}

type Query {
  country (id: String): Country
  categories (filters: CategoryFilterInput): CategoryResult
  products (search: String): Products
}

input CartItemInput {
  sku: String!
  quantity: Float!
}

type CartPrices {
  grand_total: Money
}

type Cart {
  prices: CartPrices
  total_quantity: Float!
}

type AddProductsToCartOutput {
  cart: Cart!
}

type Mutation {
  addProductsToCart(cartId: String!, cartItems: [CartItemInput!]!): AddProductsToCartOutput
}
```

U kunt in [ de documentatie van GraphQL ](https://graphql.org/learn/schema/){target="_blank"}  delven om over de details van het typesysteem, met inbegrip van syntaxis voor sommige concepten te leren hier niet vertegenwoordigd. Het bovenstaande voorbeeld spreekt echter voor zich. (Let ook op hoe vergelijkbaar de syntaxis is met query-syntaxis.) Het definiëren van een GraphQL-schema is eenvoudig een kwestie van het uitdrukken van de beschikbare argumenten en velden van een bepaald type, samen met de typen van die velden. Elk complex veldtype moet zelf een definitie hebben, enzovoort, door de structuur heen, totdat u eenvoudige scalaire typen krijgt, zoals `String` .

De declaratie `input` is in alle opzichten hetzelfde als een declaratie `type` , maar definieert een type dat kan worden gebruikt als invoer voor een argument. Noteer ook de declaratie `interface` . Dit dient een functie min of meer dezelfde als interfaces in PHP. Andere types erven van deze interface.

De syntaxis `[CartItemInput!]!` ziet er lastig uit, maar is uiteindelijk redelijk intuïtief. `!` _binnen_ verklaart de steun dat elke waarde in de serie niet-krachteloos moet zijn, terwijl één _buiten_ verklaart dat de seriewaarde zelf niet-krachteloos (bijvoorbeeld, een lege serie) moet zijn.

>[!NOTE]
>
>De logica voor hoe gegevens worden opgehaald en volgens een schema worden opgemaakt, en hoe dergelijke logica aan bepaalde types in kaart wordt gebracht, is tot de runtime van GraphQL implementatie. Implementaties moeten echter een conceptuele flow volgen die zinvol is in het licht van een begrip van geneste velden: er wordt een bewerking voor het oplossen van problemen uitgevoerd die aan het root `Query` - of `Mutation` -type is gekoppeld, die elk veld onderzoekt dat in de aanvraag is opgegeven. Voor elk gebied dat aan een complex type oplost, wordt een gelijkaardige oplossing gedaan voor dat type, etc., tot alles in scalaire waarden heeft opgelost.

{{$include /help/_includes/graphql-rest-related-links.md}}

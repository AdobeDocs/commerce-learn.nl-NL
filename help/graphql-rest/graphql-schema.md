---
title: Schema taal met GraphQL
description: Meer informatie over het schema dat bij GraphQL is betrokken. Lees een beschrijving van het schema, samen met enkele interessante patronen en manieren om het schema te lezen.
landing-page-description: Dit is een inleiding op GraphQL. Inzicht krijgen in het schema en hoe sommige elementen worden geïnterpreteerd
short-description: Dit is een inleiding op GraphQL. Inzicht krijgen in het schema en hoe sommige elementen worden geïnterpreteerd
kt: 11524
doc-type: tutorial
audience: all
last-substantial-update: 2022-12-13T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 6b59db07-b99e-47ae-9ccb-d4904afc8251
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Schema

De gebruikte query&#39;s en mutaties zijn afhankelijk van een specifieke gegevensgrafiek die op de server wordt geïmplementeerd. De GraphQL-runtime gebruikt deze grafiek om de query op te lossen. De GraphQL-specificatie definieert een agnostische taal voor het uitdrukken van de typen en relaties van de gegevensgrafiek.

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

U kunt delven in [de GraphQL-documentatie](https://graphql.org/learn/schema/){target="_blank"} om over de details van het typesysteem, met inbegrip van syntaxis voor sommige concepten te leren hier niet wordt vertegenwoordigd. Het bovenstaande voorbeeld spreekt echter voor zich. (Let ook op hoe vergelijkbaar de syntaxis is met query-syntaxis.) Het definiëren van een GraphQL-schema is eenvoudig een kwestie van het uitdrukken van de beschikbare argumenten en velden van een bepaald type, samen met de typen van die velden. Elk complex veldtype moet zelf een definitie hebben, enzovoort, door de boom, tot u aan eenvoudige scalaire types zoals krijgt `String`.

De `input` verklaring is in alle opzichten een `type` maar definieert een type dat als invoer voor een argument kan worden gebruikt. Let ook op het `interface` verklaring. Dit dient een functie min of meer dezelfde als interfaces in PHP. Andere types erven van deze interface.

De syntaxis `[CartItemInput!]!` ziet er lastig uit, maar is uiteindelijk redelijk intuïtief. De `!` _binnenkant_ het haakje declareert dat elke waarde in de array niet null moet zijn, terwijl de waarde _buiten_ declareert dat de arraywaarde zelf niet null moet zijn (bijvoorbeeld een lege array).

>[!NOTE]
>
>De logica voor hoe gegevens worden opgehaald en volgens een schema worden opgemaakt, en hoe dergelijke logica aan bepaalde types in kaart wordt gebracht, is tot de runtime van GraphQL implementatie. De implementaties, echter, zouden een conceptuele stroom moeten volgen die in het licht van een begrip rond genestelde gebieden zinvol is: Een resolutieverrichting verbonden aan de wortel `Query` of `Mutation` type wordt uitgevoerd, dat elk gebied onderzoekt dat in het verzoek wordt gespecificeerd. Voor elk gebied dat aan een complex type oplost, wordt een gelijkaardige oplossing gedaan voor dat type, etc., tot alles in scalaire waarden heeft opgelost.

{{$include /help/_includes/graphql-rest-related-links.md}}

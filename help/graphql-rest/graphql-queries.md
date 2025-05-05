---
title: Een query uitvoeren met GraphQL
description: Leer hoe te om een vraag uit te voeren gebruikend GraphQL op Adobe Commerce en  [!DNL Magento Open Source]. Dit is een inleiding aan GraphQL gebruikend GET en POST vraag.
landing-page-description: Leer hoe te om een vraag uit te voeren gebruikend GraphQL op Adobe Commerce en  [!DNL Magento Open Source]. Dit is een inleiding aan GraphQL gebruikend GET en POST vraag.
short-description: Leer hoe te om een vraag uit te voeren gebruikend GraphQL op Adobe Commerce en  [!DNL Magento Open Source]. Dit is een inleiding aan GraphQL gebruikend GET en POST vraag.
kt: 13937
doc-type: video
audience: all
last-substantial-update: 2023-10-12T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 443d711d-ec74-4e07-9357-fbbe0f774853
source-git-commit: 2041bbf1a2783975091b9806c12fc3c34c34582f
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# GraphQL-query&#39;s

Dit is deel 2 van de reeks voor GraphQL en Adobe Commerce. In deze zelfstudie en video leert u meer over GraphQL-query&#39;s en hoe u deze kunt uitvoeren tegen Adobe Commerce.

>[!VIDEO](https://video.tv.adobe.com/v/3450064?learn=on&captions=dut)

## Verwante video&#39;s en zelfstudies over GraphQL in deze serie

* [Deel 1 GraphQL - Inleiding](../graphql-rest/intro-graphql.md)
* [Deel 3 GraphQL - Mutaties](../graphql-rest/graphql-mutations.md)
* [ Deel 4 GraphQL - Schema ](../graphql-rest/graphql-schema.md)

## Voorbeeld van GraphQL Syntax

Laten we meteen naar de GraphQL-querysyntaxis duiken met een volledig voorbeeld. (Herinner me, kunt u dit tegen https://venia.magento.com/graphql proberen.)

Bekijk de volgende GraphQL-query, die stuk voor stuk wordt opgesplitst:

```graphql
{
    country (
        id: "US"
    ) {
        id
        full_name_english
    }

    categories(
        filters: {
            name: {
                match: "Tops"
            }
        }
    ) {
        items {
            name
            products(
                pageSize: 10,
                currentPage: 2
            ) {
                items {
                    sku
                }
            }
        }
    }
}
```

Een plausibele reactie van een GraphQL-server voor de bovenstaande query zou kunnen zijn:

```json
{
  "data": {
    "country": {
      "id": "US",
      "full_name_english": "United States"
    },
    "categories": {
      "items": [
        {
          "name": "Tops",
          "products": {
            "items": [
              {
                "sku": "VSW06"
              },
              {
                "sku": "VT06"
              },
              {
                "sku": "VSW07"
              },
              {
                "sku": "VT07"
              },
              {
                "sku": "VSW08"
              },
              {
                "sku": "VT08"
              },
              {
                "sku": "VSW09"
              },
              {
                "sku": "VT09"
              },
              {
                "sku": "VSW10"
              },
              {
                "sku": "VT10"
              }
            ]
          }
        }
      ]
    }
  }
}
```

In het bovenstaande voorbeeld wordt uitgegaan van het GraphQL-schema voor Adobe Commerce dat buiten de box wordt weergegeven en dat op de server is gedefinieerd. In deze aanvraag
U kunt meerdere typen gegevens tegelijk opvragen. De query geeft exact de gewenste velden weer en de geretourneerde gegevens worden opgemaakt
vergelijkbaar met de query zelf.

>[!NOTE]
>
>GraphQL-clients verduisteren de vorm van de HTTP-aanvraag die daadwerkelijk wordt verzonden, maar dit is gemakkelijk te ontdekken. Als u een op browser-gebaseerde cliënt gebruikt, neem het [!UICONTROL Network] lusje waar wanneer een vraag wordt verzonden. U ziet dat de aanvraag een onbewerkte hoofdtekst bevat die bestaat uit &quot;query: `{string}`&quot;, waarbij `{string}` gewoon de onbewerkte tekenreeks van de gehele query is. Als het verzoek als GET wordt verzonden, zou de vraag in plaats daarvan in de parameter van het vraagkoord &quot;vraag&quot;kunnen worden gecodeerd. In tegenstelling tot REST, maakt het HTTP- verzoektype niet uit, slechts de inhoud van de vraag.


## Zoeken naar wat je wilt

`country` en `categories` in het voorbeeld vertegenwoordigen twee verschillende &#39;query&#39;s&#39; voor twee verschillende soorten gegevens. In tegenstelling tot een traditioneel API-paradigma zoals REST, dat afzonderlijke en expliciete eindpunten voor elk gegevenstype definieert. GraphQL geeft u de flexibiliteit om één enkel eindpunt met een uitdrukking te vragen die vele soorten gegevens in één keer kan halen.

Op dezelfde manier specificeert de vraag precies de gebieden die voor zowel `country` (`id` en `full_name_english`) als `categories` (`items` worden gewenst, die zelf een subselectie van gebieden) heeft, en de gegevens u achterspiegels ontvangt die gebiedsspecificatie. Er zijn waarschijnlijk nog veel meer velden beschikbaar voor deze gegevenstypen, maar u krijgt alleen de gewenste velden terug.


>[!NOTE]
>
>U kunt opmerken dat de terugkeerwaarde voor `items` eigenlijk een _serie_ van waarden is, maar u selecteert niettemin direct subfields voor het. Wanneer het type van een gebied een lijst is, begrijpt GraphQL impliciet subselecties om op elk punt in de lijst toe te passen.

## Argumenten

Terwijl de velden die u wilt retourneren, tussen de accolades van elk type zijn opgegeven, worden benoemde argumenten en waarden voor deze velden tussen haakjes achter de typenaam opgegeven. Argumenten zijn vaak optioneel en hebben vaak invloed op de manier waarop queryresultaten worden gefilterd, opgemaakt of op een andere manier worden getransformeerd.

U geeft een `id` -argument door aan `country` , waarbij u opgeeft welk land u wilt opvragen, en een `filters` -argument voor `categories` .

## Velden helemaal omlaag

Hoewel u `country` en `categories` wellicht als afzonderlijke query&#39;s of entiteiten wilt zien, bestaat de volledige structuur die in de query wordt uitgedrukt, eigenlijk alleen uit velden. De expressie van `products` verschilt syntactisch niet van die van `categories` . Beide zijn velden, en er is geen verschil tussen hun constructie.

Elke GraphQL-gegevensgrafiek heeft één &#39;root&#39;-type (meestal `Query` genoemd) om de structuur te starten. De typen die vaak als entiteiten worden beschouwd, worden toegewezen aan velden in deze hoofdmap. Met de voorbeeldquery wordt eigenlijk één algemene query voor het hoofdtype uitgevoerd en worden de velden `country` en `categories` geselecteerd. Vervolgens selecteert u subvelden van die velden enzovoort, mogelijk verschillende niveaus diep. Wanneer het retourneringstype van een veld een complex type is (bijvoorbeeld een type met eigen velden in plaats van een scalair type), blijft u de gewenste velden selecteren.

Dit concept van geneste velden is ook de reden waarom u argumenten voor `products` (`pageSize` en `currentPage`) kunt doorgeven, net als voor het veld op hoofdniveau `categories` .

![ de Boom van het Gebied van GraphQL ](../assets/graphql-field-tree.png)

## Variabelen

Probeer een andere query:

```graphql
query getProducts(
    $search: String
) {
    products(
        search: $search
    ) {
        items {
            ...productDetails
            related_products {
                ...productDetails
            }
        }
    }
}

fragment productDetails on ProductInterface {
    sku
    name
}
```

Het eerste ding om van nota te nemen is toegevoegd het sleutelwoord `query` vóór het openen van de steun van de vraag, samen met een verrichtingsnaam (`getProducts`). Deze naam van de bewerking is willekeurig en komt niet overeen met iets in het serverschema. Deze syntaxis is toegevoegd ter ondersteuning van de introductie van variabelen.

In de vorige vraag, hebt u hard-gecodeerde waarden voor de argumenten van uw gebieden direct, als koorden of gehelen. De GraphQL-specificatie biedt echter ondersteuning van de eerste klasse voor het scheiden van gebruikersinvoer van de hoofdquery met behulp van variabelen.

In de nieuwe query gebruikt u haakjes vóór het accolade openen van de gehele query om een `$search` variabele te definiëren (variabelen gebruiken altijd de syntaxis van het voorvoegsel van het dollarteken). Deze variabele wordt aan het argument `search` for `products` doorgegeven.

Wanneer een query variabelen bevat, wordt verwacht dat het GraphQL-verzoek een afzonderlijk JSON-gecodeerd woordenboek met waarden naast de query zelf bevat. Voor de vraag hierboven, zou u volgende JSON van veranderlijke waarden naast het vraaglichaam kunnen verzenden:

```json
{
    "search": "VT01"
}
```

>[!NOTE]
>
>Als u deze query&#39;s probeert uit te voeren op de Venia-voorbeeldsite in plaats van op uw eigen Adobe Commerce-instantie, zijn de geretourneerde resultaten waarschijnlijk leeg voor `related_products` .

In om het even welke GraphQL-bewuste cliënt die u voor het testen (zoals Altair en GraphiQL) gebruikt, steunt UI het ingaan van de variabelen JSON afzonderlijk van de vraag.

Zoals u ziet dat de feitelijke HTTP-aanvraag voor een GraphQL-query de hoofdtekst van de query &#39;&#39;query: `{string}`&#39;&#39; bevat, bevat elke aanvraag met een Variables-woordenboek gewoon een extra &#39;variables: `{json}`&#39; in dezelfde hoofdtekst, waarbij `{json}` de JSON-tekenreeks met de variabelenwaarden is.

De nieuwe vraag gebruikt ook a _fragment_ (`productDetails`) om de zelfde gebiedsselectie op veelvoudige plaatsen opnieuw te gebruiken. [ las meer over fragmenten ](https://graphql.org/learn/queries/#fragments){target="_blank"}  in de documentatie van GraphQL.

{{$include /help/_includes/graphql-rest-related-links.md}}

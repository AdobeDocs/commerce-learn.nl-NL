---
title: Bekijk de nieuwe REST-API's van klanten
description: Ontdek hoe u de nieuwe REST-API's van klanten kunt gebruiken in Adobe Commerce Cloud Service. Ideaal voor architecten en ontwikkelaars.
feature: REST, Customers, Saas
topic: Development, Integrations
role: Architect, Developer
level: Beginner
doc-type: Tutorial
duration: 225
last-substantial-update: 2026-01-27T00:00:00Z
jira: KT-20160
source-git-commit: ad2cfb4b38d739b03e0c2fff8bcd88d77d6e4b12
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# REST-API voor klanten

Leer nieuwe REST-API&#39;s voor klanten te gebruiken in Adobe Commerce as a Cloud Service. Deze zelfstudie is ideaal voor architecten en ontwikkelaars die API-oplossingen willen integreren en optimaliseren.

## Voor wie is deze video?

* Achterste ontwikkelaars die verantwoordelijk zijn voor de opbouw van integratie met Adobe Commerce
* Technische architecten die de werkschema&#39;s van het klantenbeheer voor headless handelsimplementaties ontwerpen

## Video-inhoud

* Verificatie met Adobe IMS waarbij server-naar-server referenties worden gebruikt voor het verkrijgen van een toegangstoken voor API-aanvragen
* De juiste REST API-eindpuntnotatie gebruiken voor Commerce as a Cloud Service
* Klantenaccounts programmatisch maken en bijwerken met POST- en PUT-verzoeken met de juiste JSON-payloads

>[!VIDEO](https://video.tv.adobe.com/v/3479361/?learn=on&enablevpops)

## Codevoorbeelden

Alvorens te beginnen, verzamel alle vereiste waarden van [&#x200B; Experience Cloud &#x200B;](https://experience.adobe.com) en [&#x200B; Adobe Developer Console &#x200B;](https://developer.adobe.com/console). Als u deze waarden klaar hebt, bent u verzekerd van een vloeiend installatieproces.

>[!NOTE]
>
>Zorg ervoor u in de correcte organisatie werkt. De selectie van uw organisatie bepaalt welke instanties en omgevingen zichtbaar zijn in zowel Experience Cloud als Developer Console.

### Instantiedetails - experience.adobe.com

De instantiedetails bevatten dingen als uw Instantie-id, GraphQL-eindpunten, referenties.

### Details ontwikkelaar - https://developer.adobe.com/console/

In Developer Console beheert u uw API-referenties, waaronder client-id&#39;s, clientgeheimen en toegangstokens. U kunt ook nieuwe referentietypen maken, zoals Server-naar-server of Native App-verificatie.

## Vereisten

| Item | Waarde | Waar is deze waarde? |
|--- |--- |--- |
| Instantie-id | `<instance_id>` | experience.adobe.com |
| REST Endpoint | `<rest_endpoint>` | experience.adobe.com |
| Client-id | `<client_id>` | developer.adobe.com/console |
| Clientgeheim | `<client_secret>` | developer.adobe.com/console |


## Stap 1: Get Token van de Toegang (server-aan-server Authentificatie)

>[!IMPORTANT]
>
> De variabelen in dit voorbeeld zijn niet geldig. Gebruik de &lt;client_id> en &lt;client_geheime> op basis van uw projectreferenties.

```bash
curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'grant_type=client_credentials&client_id=<client_id>&client_secret=<client_secret>&scope=openid,AdobeID,email,additional_info.projectedProductContext,profile,commerce.aco.ingestion,commerce.accs,org.read,additional_info.roles'
```

**Antwoord van de Steekproef:**

```json
{
  "access_token": "eyJhbGciOiJSUzI1NiIs...",
  "token_type": "bearer",
  "expires_in": 86399
}
```

## Stap 2: Een klant maken

>[!IMPORTANT]
>
> De URL in dit voorbeeld is niet geldig. Gebruik de URL van de REST-basis. Uitwisseling &#39;&lt;rest_eindpunt>&#39; met uw URL. Het ziet er ongeveer zo uit als `https://na1-sandbox.api.commerce.adobe.com/AbCYab34cdEfGHiJ27123` .
>
> Dit eindpunt heeft /rest/ als deel van URL niet. Als dit wordt opgenomen, treedt er een fout op.

**Eindpunt:** `POST /V1/customers`

```bash
curl -X POST \
  "<rest_endpoint>/V1/customers" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <ACCESS_TOKEN>" \
  -d '{
    "customer": {
      "email": "john.doe@example.com",
      "firstname": "John",
      "lastname": "Doe",
      "store_id": 1,
      "website_id": 1
    },
    "password": "TempPa55word!"
  }'
```

**Reactie:**

```json
{
  "id": 5,
  "group_id": 1,
  "created_at": "2026-01-23 20:40:15",
  "updated_at": "2026-01-23 20:40:15",
  "created_in": "Default Store View",
  "email": "john.doe@example.com",
  "firstname": "John",
  "lastname": "Doe",
  "store_id": 1,
  "website_id": 1,
  "addresses": [],
  "disable_auto_group_change": 0
}
```

## Stap 3: Een klant bijwerken

>[!IMPORTANT]
>
> De URL in dit voorbeeld is niet geldig. Gebruik de URL van de REST-basis. Uitwisseling &#39;&lt;rest_eindpunt>&#39; met uw URL. Het ziet er ongeveer zo uit als `https://na1-sandbox.api.commerce.adobe.com/AbCYab34cdEfGHiJ27123` .

Het getal `5` in het volgende voorbeeld is de id van de eerder gemaakte klant met POST `"id": 5,` . Ben zeker om `5` in om het even welke identiteitskaart te veranderen in uw verzoek werd teruggekeerd.

**Eindpunt:** `PUT /V1/customers/{customerId}`

```bash
curl -X PUT \
  "<rest_endpoint>/V1/customers/5" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <ACCESS_TOKEN>" \
  -d '{
    "customer": {
      "id": 5,
      "email": "john.doe@example.com",
      "firstname": "John",
      "lastname": "Doe-Updated"
    }
  }'
```

**Reactie:**

```json
{
  "id": 5,
  "group_id": 1,
  "created_at": "2026-01-23 20:40:15",
  "updated_at": "2026-01-23 20:40:30",
  "created_in": "Default Store View",
  "email": "john.doe@example.com",
  "firstname": "John",
  "lastname": "Doe-Updated",
  "store_id": 1,
  "website_id": 1,
  "addresses": []
}
```

## Volledig script (alles-in-één)

>[!IMPORTANT]
>
> De variabelen in dit voorbeeld zijn niet geldig. Gebruik de client-id en het clientgeheim van uw projectreferenties. Gebruik de URL van de REST-basis. Uitwisseling &#39;&lt;rest_eindpunt>&#39; met uw REST eindpunt URL van experience.adobe.com. Het ziet er ongeveer zo uit als `https://na1-sandbox.api.commerce.adobe.com/AbCDefGHiJ1234567` .

```bash
#!/bin/bash

# Configuration be sure to update these with your projects unique values
CLIENT_ID="<client_id>"
CLIENT_SECRET="<client_secret>"
REST_ENDPOINT="<rest_endpoint>"

# Step 1: Get Access Token
echo "Getting access token..."
ACCESS_TOKEN=$(curl -s -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d "grant_type=client_credentials&client_id=${CLIENT_ID}&client_secret=${CLIENT_SECRET}&scope=openid,AdobeID,email,additional_info.projectedProductContext,profile,commerce.aco.ingestion,commerce.accs,org.read,additional_info.roles" | jq -r '.access_token')

echo "Token obtained: ${ACCESS_TOKEN:0:50}..."

# Step 2: Create Customer
echo ""
echo "Creating customer..."
CREATE_RESPONSE=$(curl -s -X POST \
  "${REST_ENDPOINT}/V1/customers" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ${ACCESS_TOKEN}" \
  -d '{
    "customer": {
      "email": "john.doe@example.com",
      "firstname": "John",
      "lastname": "Doe",
      "store_id": 1,
      "website_id": 1
    },
    "password": "TempPa55word!"
  }')

echo "Create Response:"
echo "$CREATE_RESPONSE" | jq .

# Extract customer ID
CUSTOMER_ID=$(echo "$CREATE_RESPONSE" | jq -r '.id')
echo "Customer ID: $CUSTOMER_ID"

# Step 3: Update Customer
echo ""
echo "Updating customer..."
curl -s -X PUT \
  "${REST_ENDPOINT}/V1/customers/${CUSTOMER_ID}" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ${ACCESS_TOKEN}" \
  -d "{
    \"customer\": {
      \"id\": ${CUSTOMER_ID},
      \"email\": \"john.doe@example.com\",
      \"firstname\": \"john\",
      \"lastname\": \"Doe-Updated\"
    }
  }" | jq .
```

## Belangrijke opmerkingen over deze zelfstudie

1. **Weg URL**: Gebruik `https://<server>.api.commerce.adobe.com/<tenant-id>/V1/customers` — **NIET** `https://<host>/rest/<store-view-code>/V1/customers`
1. **Authentificatie**: Dit leerprogramma gebruikte Server-aan-Server (`client_credentials` subsidietype)
1. **Vereiste Reikwijdte**: `commerce.accs`
1. **Symbolische Verval**: 86400 seconden (24 uren)

## Verwijzingen

* [&#x200B; de Nota&#39;s van de Versie van Adobe Commerce as a Cloud Service &#x200B;](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/release-notes)
* [&#x200B; REST API Verwijzing SaaS &#x200B;](https://developer.adobe.com/commerce/webapi/reference/rest/saas/)
* [&#x200B; Gids van de Authentificatie van de Gebruiker &#x200B;](https://developer.adobe.com/commerce/webapi/rest/authentication/user/)

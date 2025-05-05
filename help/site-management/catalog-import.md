---
title: Meer informatie over opties voor het importeren van catalogi die bij Adobe Commerce horen
description: Leer hoe u een aantal native opties gebruikt om uw catalogus te importeren in uw Adobe Commerce-winkel.
kt: 13634
doc-type: tutorial
audience: all
activity: use
last-substantial-update: 2023-8-15
feature: Backend Development, Data Import/Export, REST
topic: Commerce, Administration, Content Management
role: Admin, User
level: Beginner, Intermediate
exl-id: 18713a44-df39-4b94-91ce-c7efeb4ce2b3
source-git-commit: b0fe49352b00a68554e662327cd66983c30d8285
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# Opties voor het importeren van een catalogus

Er zijn enkele native methoden voor het importeren van een catalogus naar Adobe Commerce. Elke methode heeft zijn eigen redenering voor gebruik samen met voor- en nadelen die in overweging moeten worden genomen.

Kies een van de onderstaande opties voor meer informatie.

>[!BEGINTABS]

>[!TAB  Handmatig ]

## De producten handmatig maken {#manual-import}

Als u een beperkte catalogus hebt en updates niet vaak worden uitgevoerd, kunt u deze handmatig maken. Het kost tijd om elk product in te voeren en enige beperkte training voor het gebruik van de Commerce Admin. Handmatig catalogusbeheer is niet de juiste optie voor de meeste winkels, maar in bepaalde situaties kan het zinvol zijn. Om extra documentatie voor dit proces te zien, creeer het bezoek [ een product ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html){target="_blank"} . Vergeet niet dat u meerdere methoden kunt gebruiken om uw catalogus te beheren. Handmatige bewerkingen moeten echter beperkt blijven wanneer de catalogus eenmaal is geautomatiseerd. Geautomatiseerde updates hebben de mogelijkheid om wijzigingen die handmatig worden uitgevoerd, te overschrijven en veroorzaken daarom verwarring. Zodra de integratie met Adobe Commerce om de catalogus te beheren automatisering en APIs gebruikt, wordt het geadviseerd om beheer van de catalogus van admin door [ gebruikersrollen en toestemmingen ](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html){target="_blank"} te beperken .

### Wanneer denkt u over deze aanpak

- Zeer kleine catalogus, bijvoorbeeld minder dan 50 producten
- Updates komen niet vaak voor
- U hebt alle productdetails, afbeeldingen en video&#39;s en u wilt niet de tijd nemen om te leren hoe u de gegevens omzet in CSV
- U wilt afbeeldingen en video&#39;s toevoegen wanneer u de producten maakt
- Uw team is `not` vertrouwd met API&#39;s en hoe OAUTH werkt

>[!TAB  Admin CSV ]

## CSV-importprogramma voor beheerders {#admin-csv}

Met dit gereedschap kan een eigenaar van een winkel een catalogus importeren met behulp van een CSV-recht van de commercebeheerder.
[ de Gegevens van de Invoer van Admin van Commerce ](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/import/data-import.html){target="_blank"} 

Pros:
Het uploaden van een CSV van admin is een directe voorwaartse benadering van catalogusbeheer. Zo kunt u sneller productupdates voor catalogi uitvoeren naar een catalogus van gematigde grootte.

Cons:

- Langzaam
- De maximale grootte van het uploadbestand die op de server is gedefinieerd, kan niet eenvoudig worden aangepast door de eigenaar van de winkel.
- Hiervoor is beheerderstoegang vereist en iemand moet de handeling uitvoeren. De automatisering is beperkt
- De invoer van het programma wordt beperkt tot 1x per dag maximum
- De bijbehorende afbeeldingen en video&#39;s moeten afzonderlijk worden geüpload

### Wanneer denkt u over deze aanpak

- Grootte catalogus is matig
- Updates worden niet meer dan eenmaal per dag uitgevoerd
- u hebt toegang tot serverconfiguraties voor het geval dat u de maximale uploadgrootte van bestanden moet verhogen
- Uw team is `not` vertrouwd met API&#39;s en hoe OAUTH werkt

>[!TAB  Bulk REST API ]

## Bulk REST API {#bulk-rest-api}

De grote REST API maakt automatisering en frequentere updates mogelijk. Deze API is sneller dan het gebruiken van het admin uploaden van CSV.
[ Bulk eindpunten documentatie ](https://developer.adobe.com/commerce/webapi/rest/use-rest/bulk-endpoints/){target="_blank"} 

Pros:
De mogelijkheid om grote gegevenssets te importeren die niet de CSV-indeling hebben.

Cons:

- De bijbehorende afbeeldingen en video&#39;s moeten afzonderlijk worden geüpload
- Kan worden beperkt door bandbreedtebeperkingen voor de hostingprovider

### Wanneer denkt u over deze aanpak

- Catalogus is elke grootte
- Updates komen vaak voor, meer dan 1x per dag is acceptabel
- De tijd om te importeren is belangrijk maar niet kritiek en een korte vertraging bij de verwerking van de invoergegevens is aanvaardbaar
- De gegevens zijn niet gestructureerd in CSV-indeling en u kunt ze niet transformeren via automatisering

>[!TAB  ASYNC REST API ]

## ASYNC REST API {#async-rest-api}

Een asynchroon Webeindpunt onderschept berichten aan een Web API en schrijft hen aan de berichtrij. Telkens wanneer het systeem een dergelijke API-aanvraag accepteert, wordt een UUID-id gegenereerd. Adobe Commerce neemt deze UUID op wanneer het bericht aan de wachtrij wordt toegevoegd. Dan, leest een consument de berichten van de rij en voert hen één voor één uit.
[ Asynchrone documentatie van Webeindpunten ](https://developer.adobe.com/commerce/webapi/rest/use-rest/asynchronous-web-endpoints/){target="_blank"} 

Pros:

- Snel gegevens importeren
- Het bereik van de winkel wordt ondersteund of u kunt `all` opgeven om de bewerking uit te voeren in alle bestaande winkels

Cons:

- GET-verzoek wordt niet ondersteund

### Wanneer denkt u over deze aanpak

- Invoer komt vaak voor
- Geen kwestie met een kleine vertraging vanaf de tijd zij via API worden voorgelegd en dan van de berichtrij worden verwerkt.


>[!TAB  CSV REST API ]

## CSV REST API {#csv-rest-api}

Met deze API-optie is het importeren extreem snel in vergelijking met alle andere native opties.

[ de gegevens van de Invoer REST CSV api ](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"} 
Pros:

- Snelste methode om de binnenkomende gegevens te verwerken
- Kan meerdere keren per dag worden uitgevoerd
- De gegevens kunnen worden samengeperst gebruikend gzip voor grote verzoeken om de grenzen van de HTTP- verzoekgrootte te vermijden.

Cons:

- De bijbehorende afbeeldingen en video&#39;s moeten afzonderlijk worden geüpload
- De gegevens moeten een CSV-indeling hebben

### Wanneer denkt u over deze aanpak

- Catalogus is elke grootte
- Updates komen vaak voor, meer dan 1x per dag is acceptabel
- De totale importtijd is belangrijk
- De gegevens hebben al de CSV-indeling of kunnen gemakkelijk worden getransformeerd via automatisering

>[!ENDTABS]

## Aanvullende bronnen

- [ de Gegevens van de Invoer gebruikend nieuwe REST CSV ](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"} 
- [ de belangrijkste documentatie van de Gegevens van de Invoer ](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/import/data-import.html){target="_blank"} 
- [ versie 2.4.6 van Adobe Commerce versienota&#39;s ](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/adobe-commerce/2-4-6.html){target="_blank"} 
- [ Gebruikers, rollen, en toestemmingen ](../site-management/users-roles-permissions.md){target="_blank"}

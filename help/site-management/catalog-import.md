---
title: Meer informatie over opties voor het importeren van catalogi die bij Adobe Commerce horen
description: Leer hoe u een aantal native opties gebruikt om uw catalogus te importeren in uw Adobe Commerce-winkel.
kt: 13634
doc-type: tutorial
audience: all
activity: use
last-substantial-update: 2023-8-15
feature: Backend Development, Catalogs, Data Import/Export, REST
topic: Commerce, Administration, Content Management
role: Admin, User
level: Beginner, Intermediate
source-git-commit: 0bda6347f2288953c653fe137580ef46384107f8
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# Opties voor het importeren van een catalogus leren gebruiken

Er zijn enkele native methoden voor het importeren van een catalogus naar Adobe Commerce. Elke methode heeft zijn eigen redenering voor gebruik samen met voor- en nadelen die in overweging moeten worden genomen.

Kies een van de onderstaande opties voor meer informatie.

>[!BEGINTABS]

>[!TAB Handmatig]

## De producten handmatig maken {#manual-import}

Als u een beperkte catalogus hebt en updates niet vaak worden uitgevoerd, kunt u deze handmatig maken. Het vereist tijd om elk product en wat beperkte opleiding in te gaan hoe te om Admin van de Handel te gebruiken. Handmatig catalogusbeheer is niet de juiste optie voor de meeste winkels, maar in bepaalde situaties kan het zinvol zijn. Voor meer documentatie over dit proces gaat u naar [Een product maken](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html){target="_blank"}. Do not forget, you can use more than one method to manage your catalog, however once automation is used, manual edits must be limited. Automated updates have the opportunity to overwrite any changes performed manually, and therefore cause confusion. Once the integration with Adobe Commerce to manage the catalog is using automation and APIs, it is advised to restrict management of the catalog from the admin through [user roles and permissions](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html){target="_blank"}.



### Wanneer denkt u over deze aanpak

- Zeer kleine catalogus, bijvoorbeeld minder dan 50 producten
- Updates komen niet vaak voor
- U hebt alle productdetails, afbeeldingen en video&#39;s en u wilt niet de tijd nemen om te leren hoe u de gegevens omzet in CSV
- U wilt afbeeldingen en video&#39;s toevoegen wanneer u de producten maakt
- Uw team is `not` bekend met API&#39;s en hoe OAUTH werkt



>[!TAB CSV-beheer]

## CSV-importprogramma voor beheerders {#admin-csv}

Met dit gereedschap kan een eigenaar van een winkel een catalogus importeren met behulp van een CSV-recht van de commercebeheerder.
[Gegevens importeren uit Commerce Admin](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/import/data-import.html){target="_blank"}

Pros: Het uploaden van een CSV van admin is een directe voorwaartse benadering van catalogusbeheer. Zo kunt u sneller productupdates voor catalogi uitvoeren naar een catalogus van gematigde grootte.

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
- Uw team is `not` bekend met API&#39;s en hoe OAUTH werkt



>[!TAB Bulk REST API]

## Bulk REST API {#bulk-rest-api}

De grote REST API maakt automatisering en frequentere updates mogelijk. Deze API is sneller dan het gebruiken van het admin uploaden van CSV.
[Documentatie voor eindpunten van opsommingstekens](https://developer.adobe.com/commerce/webapi/rest/use-rest/bulk-endpoints/){target="_blank"}

Pros: de mogelijkheid om grote gegevenssets te importeren die niet de CSV-indeling hebben.

Cons:

- De bijbehorende afbeeldingen en video&#39;s moeten afzonderlijk worden geüpload
- Kan worden beperkt door bandbreedtebeperkingen voor de hostingprovider
- U moet opties-kenmerk-id&#39;s gebruiken en niet de labels



### Wanneer denkt u over deze aanpak

- Catalogus is elke grootte
- Updates komen vaak voor, meer dan 1x per dag is acceptabel
- Tijd om te importeren is belangrijk, maar niet belangrijk
- De gegevens zijn niet gestructureerd in CSV-indeling en u kunt ze niet transformeren via automatisering



>[!TAB ASYNC REST API]

## ASYNC REST API {#async-rest-api}

Een asynchroon Webeindpunt onderschept berichten aan een Web API en schrijft hen aan de berichtrij. Telkens wanneer het systeem een dergelijke API-aanvraag accepteert, wordt een UUID-id gegenereerd. Adobe Commerce neemt deze UUID op wanneer het bericht aan de wachtrij wordt toegevoegd. Dan, leest een consument de berichten van de rij en voert hen één voor één uit.
[Asynchrone documentatie over webeindpunten](https://developer.adobe.com/commerce/webapi/rest/use-rest/asynchronous-web-endpoints/){target="_blank"}

Pros:

- Snel gegevens importeren
- Winkelbereik wordt ondersteund of u kunt opgeven `all` om verrichting op alle bestaande opslag uit te voeren

Cons:

- GET-verzoek wordt niet ondersteund
- U moet de id&#39;s van het optiekenmerk gebruiken in plaats van de labels


### Wanneer denkt u over deze aanpak

- Invoer komt vaak voor
- Geen kwestie met een kleine vertraging vanaf de tijd zij via API worden voorgelegd en dan van de berichtrij worden verwerkt.



>[!TAB CSV REST API]

## CSV REST API {#csv-rest-api}

Met deze API-optie is het importeren extreem snel in vergelijking met alle andere native opties.

[Gegevens REST CSV api importeren](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"}
Pros:

- Snelste methode om de binnenkomende gegevens te verwerken
- Kan meerdere keren per dag worden uitgevoerd
- De gegevens kunnen worden samengeperst gebruikend gzip voor grote verzoeken om de grenzen van de HTTP- verzoekgrootte te vermijden.

Cons:

- De bijbehorende afbeeldingen en video&#39;s moeten afzonderlijk worden geüpload
- U moet de id&#39;s van het optiekenmerk gebruiken en niet de labels
- De gegevens moeten een CSV-indeling hebben

### Wanneer denkt u over deze aanpak

- Catalogus is elke grootte
- Updates komen vaak voor, meer dan 1x per dag is acceptabel
- De totale importtijd is belangrijk
- De gegevens hebben al de CSV-indeling of kunnen gemakkelijk worden getransformeerd via automatisering



>[!ENDTABS]

## Aanvullende bronnen

- [Gegevens importeren met de nieuwe REST CSV](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"}
- [Hoofddocumentatie van gegevens importeren](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/import/data-import.html){target="_blank"}
- [Opmerkingen bij de release Adobe Commerce versie 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/adobe-commerce/2-4-6.html){target="_blank"}
- [Gebruikers, rollen en machtigingen](../site-management/users-roles-permissions.md){target="_blank"}

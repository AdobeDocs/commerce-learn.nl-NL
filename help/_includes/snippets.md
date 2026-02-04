---
title: Edition-banners
description: Hergebruikte visuele elementen voor het noteren van een functie of pagina's die op een specifieke uitgave van toepassing zijn
source-git-commit: 180bfd303df77d95c88fa518253ddff6a67c76d4
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Edition-banners

## Alleen EE-functie {#ee-feature}

<table style="border:1px solid red">
<tr><td><img alt="Adobe Commerce-functie" src="../assets/adobe-logo.svg" width="20" height="20" /> De exclusieve eigenschap slechts in Adobe Commerce (<a href="https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html#product-editions"> leert meer </a>)</td></tr>
</table>

## Alleen B2B-functie {#b2b-feature}

<table style="border:1px solid green">
<tr><td><img alt="Adobe Commerce-functie" src="../assets/b2b.svg" width="20" height="20" /> Exclusieve eigenschap beschikbaar slechts met <a href="https://experienceleague.adobe.com/docs/commerce-admin/b2b/guide-overview.html"> B2B voor Adobe Commerce </a></td></tr>
</table>

## 400 kwesties {#avoid-400-error}

>[!CAUTION]
>
>Wanneer het uitvoeren van API vraag, zorg ervoor dat één of andere soort searchCriteria wordt gebruikt. U zou ook het gebruiken van paginering kunnen overwegen. Als het resultaat van Adobe Commerce te groot is, is mogelijk aan de Adobe Developer App Builder-capaciteit voldaan en wordt het bestand onverwacht afgesloten. Het resultaat is een onjuist resultaat van de reactie als een fout van 400.\
> Stel dat het nodig is om alle huidige producten van Adobe Commerce op te vragen. De resulterende URL lijkt op `{{base_url}}rest/V1/products?searchCriteria=all` . Afhankelijk van de grootte van de catalogus die de geretourneerde pagina bevat, is de json mogelijk te groot om door App Builder te worden gebruikt. Gebruik in plaats daarvan paginering en doe een aantal verzoeken om te voorkomen dat `Response is not valid 'message/http'.`

## Alleen PaaS en Commere Cloud {#only-for-on-prem-commerce-cloud}


**Deze informatie is op van toepassing:**

| Op voorgrond | Adobe Commerce Cloud | Adobe Commerce as a Cloud Service | Aobe Commerce Optimizer |
| --- | --- | --- | --- |
| Ja | Ja | Nee | Nee |

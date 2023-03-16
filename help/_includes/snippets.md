---
title: Edition-banners
description: Hergebruikte visuele elementen voor het noteren van een functie of pagina's die op een specifieke uitgave van toepassing zijn
source-git-commit: 8c7c64ddff456815b0a1649f497e917da8b8fca0
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# Edition-banners

## Alleen EE-functie {#ee-feature}

<table style="border:1px solid red">
<tr><td><img alt="Adobe Commerce-functie" src="../assets/adobe-logo.svg" width="20" height="20" /> Alleen exclusieve functie in Adobe Commerce (<a href="https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html#product-editions">Meer informatie</a>)</td></tr>
</table>

## Alleen B2B-functie {#b2b-feature}

<table style="border:1px solid green">
<tr><td><img alt="Adobe Commerce-functie" src="../assets/b2b.svg" width="20" height="20" /> Exclusieve functie alleen beschikbaar met <a href="https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html#product-editions">B2B voor Adobe Commerce</a></td></tr>
</table>

## 400 kwesties {#avoid-400-error}

>[!CAUTION]
>
>Wanneer het uitvoeren van API vraag, zorg ervoor dat één of andere soort searchCriteria wordt gebruikt. U zou ook het gebruiken van paginering kunnen overwegen. Als het resultaat van Adobe Commerce te groot is, is mogelijk aan de Adobe Developer App Builder-capaciteit voldaan en wordt het bestand onverwacht afgesloten. Het resultaat is een onjuist resultaat van de reactie als een fout van 400.\
> Stel dat het nodig is om alle huidige producten van Adobe Commerce op te vragen. De resulterende URL lijkt op `{{base_url}}rest/V1/products?searchCriteria=all`. Afhankelijk van de grootte van de catalogus die door de geretourneerde waarde wordt geretourneerd, is de json mogelijk te groot voor gebruik door App Builder. Gebruik in plaats daarvan paginering en doe enkele verzoeken om te voorkomen dat `Response is not valid 'message/http'.`

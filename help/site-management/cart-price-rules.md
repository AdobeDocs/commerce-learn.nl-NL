---
title: Een regel voor een startprijs maken
description: Leer hoe u regels voor winkelwagenprijzen kunt maken die kortingen op winkelwagentjes toepassen op basis van een aantal voorwaarden.
doc-type: feature video
audience: all
activity: use
last-substantial-update: 2022-12-28T00:00:00Z
feature: Configuration, System, Catalogs, Customers, Shopping Cart
topic: Commerce, Administration
role: Admin, Leader, User
level: Beginner, Intermediate
exl-id: ae8cab73-8a8b-4266-8205-b7397633e9bf
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Een regel voor een startprijs maken

Met de prijsregels voor winkelwagentjes worden op basis van een aantal voorwaarden kortingen toegepast op objecten in het winkelwagentje. De korting kan automatisch worden toegepast wanneer aan de voorwaarden wordt voldaan of wanneer de klant een geldige couponcode invoert. Als deze korting wordt toegepast, wordt deze in het winkelwagentje weergegeven onder het subtotaal. Een prijsregel voor winkelwagentjes kan worden gebruikt wanneer dat nodig is voor een seizoen of promotie door de status en het datumbereik ervan te wijzigen.

## Voor wie is deze video?

- eCommerce-markten
- Webmanagers

## Video-inhoud

>[!VIDEO](https://video.tv.adobe.com/v/343835?quality=12&learn=on)

## Problemen met prijsweergave

Er zijn sommige unieke scenario&#39;s die elk lijnpunt vereisen om hun verstrekte korting te tonen maar de waarden kunnen niet precies aanpassen. De reden hiervoor is dat een korting op de winkelprijregel wordt toegepast op meerdere producten, maar dat de waarden niet gelijkmatig worden verdeeld in twee decimalen.

>[!BEGINSHADEBOX]

Regel voor winkelwagenprijs = 10% korting toegepast op 2 producten in de winkelwagentje, zodat de prijsregel van kracht wordt: totaal aantal objecten in winkelwagentje is 2 Acties passen procent van de korting op de productprijs toe en dat kortingsbedrag is 10

Er worden 2 objecten aan het winkelwagentje toegevoegd, elk $19,95

Om het kortingsbedrag te krijgen vermenigvuldig de de prijstijden van het product 0.1

19,95 x 0,1 = 1,995

Dit is de kwestie, we hebben 3 decimalen, in plaats van 2. Het omzetten van deze naar dollars is nu een probleem

>[!ENDSHADEBOX]

### De oplossing

Als je nadenkt over de website-eigenaar, die de enige is die door deze uitgave wordt beïnvloed, werd bepaald dat het meest geschikt was om elk object dat met de korting in dollars werd besteld, te tonen. Om ervoor te zorgen dat het volledige orderbedrag correct wordt berekend, is besloten het eerste item te afronden en de andere het derde decimaalteken. Bekijk dit scenario:

>[!BEGINSHADEBOX]

Dezelfde korting van 10% als boven de regel voor het winkelwagentje in feite Twee producten aan het winkelwagentje toevoegen die 19,95 zijn

Elk product krijgt $1,995 in kortingen Product 1 - 19,95 x 0,1 = 1,995 2 - 19,95 x 0,1 = 1,995

In totaal wordt 3,99 euro als korting aan de klant verstrekt

Wanneer het tonen van de lijnpunten aan de opslageigenaar in admin, moeten wij het eerste punt aanpassen en het rond tot 2.000. De tweede punten wij drukken derde decimaal Product 1 = 2.00 Product 2 = 1.99

De totale korting op de twee producten die nu bij elkaar worden opgeteld, komt overeen met de werkelijke korting die aan een klant wordt gegeven.
>[!ENDSHADEBOX]

Hier is een schermafbeelding zoals deze in de beheerder zou worden weergegeven voor een volgorde met dit scenario:

![Admin-weergave met geordende items met verschillende waarden](../assets/commerce-admin-cart-price-rule-values-different.png)

### Andere mogelijke oplossingen en waarom deze niet werden gebruikt

>[!BEGINSHADEBOX]

Dezelfde korting van 10% als boven de regel voor het winkelwagentje in feite Twee producten aan het winkelwagentje toevoegen die 19,95 zijn

Elk product zou $1.995 in kortingen moeten krijgen, maar als wij enkel hen rond maken, toont het teveel korting.

Product 1 - 19,95 x 0,1 = 1,995 Product 2 - 19,95 x 0,1 = 1,995

Converteren naar ronde items Product 1 Nieuwe waarde is 2.00 Product 2 Nieuwe waarde is 2.00

Een totaal van 3,99 dollar werd in feite als korting aan de klant verstrekt, maar als we het afronden, zou het laten zien dat er $4,00 is gegeven, en dat is onjuist.

2.00 + 2.00 = $4.00

>[!ENDSHADEBOX]

Vergelijkbare kwestie als de derde decimaal voor alle punten werd gelaten vallen, zou het te weinig verstrekte korting tonen.

>[!BEGINSHADEBOX]

Dezelfde korting van 10% als boven de regel voor het winkelwagentje in feite Twee producten aan het winkelwagentje toevoegen die 19,95 zijn

Elk product zou $1.995 in kortingen moeten krijgen, echter als wij enkel de derde decimaal laten vallen, gebeurt dit: Product 1 - 19,95 x 0,1 = 1,995 Product 2 - 19,95 x 0,1 = 1,995

Omzetten in een derde decimaal voor alle items Product 1 Nieuwe waarde is 1,99 Product 2 Nieuwe waarde is 1,99

In totaal werd 3,99 dollar per stuk als een korting aan de klant verstrekt, maar als we de derde decimaal laten vallen, zou dat aantonen dat er $3,98 is gegeven, en dat is onjuist.

1.99 + 1.99 = $3.98

>[!ENDSHADEBOX]


## Aanvullende bronnen

- [Een regel voor winkelprijzen maken - [!DNL Commerce] Handleiding voor het verhandelen en promoten van objecten](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create.html)
- [Couponcodes - [!DNL Commerce] Handleiding voor het verhandelen en promoten van objecten](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-coupon.html)

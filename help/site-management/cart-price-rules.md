---
title: Een regel voor een startprijs maken
description: Leer hoe u regels voor winkelwagenprijzen kunt maken die kortingen op winkelwagentjes toepassen op basis van een aantal voorwaarden.
doc-type: feature video
audience: all
activity: use
last-substantial-update: 2022-12-28T00:00:00Z
feature: Configuration, System, Customers, Shopping Cart
topic: Commerce, Administration
role: Admin, Leader, User
level: Beginner
duration: 171
jira: KT-17148
exl-id: ae8cab73-8a8b-4266-8205-b7397633e9bf
source-git-commit: d290ba1d9c8892b4322aeb19d3c65d9d8087a309
workflow-type: tm+mt
source-wordcount: '687'
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

Regel voor winkelwagenprijs = 10% korting toegepast op 2 producten in de winkelwagen
Voorwaarde voor het van kracht worden van de prijsregel: het totaal van de artikelen in de winkelwagen is 2
De acties passen percent van de korting van de productprijs toe en dat kortingsbedrag is 10

Er worden 2 objecten aan het winkelwagentje toegevoegd, elk $19,95

Om het kortingsbedrag te krijgen vermenigvuldig de de prijstijden van het product 0.1

19,95 x 0,1 = 1,995

Dit is de kwestie, we hebben 3 decimalen, in plaats van 2. Het omzetten van dit naar dollars is nu een probleem

>[!ENDSHADEBOX]

### De oplossing

Als je nadenkt over de website-eigenaar, die de enige is die door deze uitgave wordt beïnvloed, werd bepaald dat het meest geschikt was om elk object dat met de korting in dollars werd besteld, te tonen. Om ervoor te zorgen dat het volledige orderbedrag correct wordt berekend, is besloten het eerste item te afronden en de andere het derde decimaalteken. Bekijk dit scenario:

>[!BEGINSHADEBOX]

Dezelfde korting van 10% als boven de regel voor winkelwagentjes in feite
Voeg 2 producten aan de kar toe die 19.95 zijn

Elk product krijgt $ 1,995 in kortingen
Product 1 - 19,95 x 0,1 = 1,995
2 - 19,95 x 0,1 = 1,995

In totaal wordt 3,99 euro als korting aan de klant verstrekt

Wanneer het tonen van de lijnpunten aan de archiefeigenaar in admin,
We moeten het eerste item aanpassen en het afronden tot 2.000. De tweede items die we op de derde decimaal plaatsen
Product 1 = 2,00
Product 2 = 1,99

De totale korting van de twee producten nu wanneer samengeteld komt overeen met de werkelijke korting die aan een klant is verstrekt.
>[!ENDSHADEBOX]

Hier is een schermafbeelding zoals deze in de beheerder zou worden weergegeven voor een volgorde met dit scenario:

![ mening Admin die bevolen punten met verschillende waarden toont ](../assets/commerce-admin-cart-price-rule-values-different.png)

### Andere mogelijke oplossingen en waarom deze niet werden gebruikt

>[!BEGINSHADEBOX]

Dezelfde korting van 10% als boven de regel voor winkelwagentjes in feite
Voeg 2 producten aan de kar toe die 19.95 zijn

Elk product krijgt $ 1,995 in kortingen,
maar als we ze gewoon rond laten lopen , geeft het te veel korting .

Product 1 - 19,95 x 0,1 = 1,995
Product 2 - 19,95 x 0,1 = 1,995

Omzetten in alle items afronden
Product 1 Nieuwe waarde is 2,00
Product 2 Nieuwe waarde is 2,00

In totaal werd 3,99 EUR per jaar als korting aan de klant verstrekt,
maar als we naar boven zouden komen , zou dat laten zien dat er 4 , 00 dollar is gegeven , en dat is onjuist .

2,00 + 2,00 = $ 4,00

>[!ENDSHADEBOX]

Vergelijkbare kwestie als de derde decimaal voor alle punten werd gelaten vallen, zou het te weinig verstrekte korting tonen.

>[!BEGINSHADEBOX]

Dezelfde korting van 10% als boven de regel voor winkelwagentjes in feite
Voeg 2 producten aan de kar toe die 19.95 zijn

Elk product zou $1.995 in kortingen moeten krijgen, echter als wij enkel de derde decimaal laten vallen, gebeurt dit:
Product 1 - 19,95 x 0,1 = 1,995
Product 2 - 19,95 x 0,1 = 1,995

Omzetten in een derde decimaal voor alle items
Product 1 Nieuwe waarde is 1,99
Product 2 Nieuwe waarde is 1,99

In totaal werd 3,99 EUR per jaar als korting aan de klant verstrekt,
als we echter de derde decimaal laten vallen , zou dat laten zien dat er $3,98 is gegeven , en dat is onjuist .

1,99 + 1,99 = $ 3,98

>[!ENDSHADEBOX]


## Aanvullende bronnen

- [ creeer een Regel van de Prijs van de Kar -  [!DNL Commerce]  Gids van Verkoop en Bevorderingen ](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create.html?lang=nl-NL)
- [ Codes van de Coupon -  [!DNL Commerce]  Handelsversie en Gids van Bevorderingen ](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-coupon.html?lang=nl-NL)

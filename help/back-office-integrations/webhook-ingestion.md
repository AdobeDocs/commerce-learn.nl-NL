---
title: Vorm, opstellend, en pas een Ingestie Webhaak aan
description: Leer hoe u een ingesloten webhaak instelt en aanpast om de communicatie tussen Commerce en een extern back-office systeem te vergemakkelijken.
landing-page-description: Leer hoe u de Commerce Integration Starter Kit kunt gebruiken om Commerce te integreren met een extern back-office systeem met behulp van een ingestion webhaak.
kt: 15870
doc-type: video
duration: 593
audience: all
last-substantial-update: 2024-7-30
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
role: Architect, Developer
level: Intermediate
source-git-commit: 45c018813ed8d5487e1491e09afc34e2de39c5b2
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Vorm, stel, en pas een ingeschrevenwebhaak op

Meer informatie over het instellen en aanpassen van een ingesettenwebhaak voor de integratie van Commerce met een extern back-office systeem. &#x200B; Deze video verklaart hoe webhaak beperkingen in gebeurtenismededeling tussen systemen kan richten door een openbaar beschikbaar eindpunt te verstrekken om berichten van het derdesysteem aan de Adobe IO Eventing API aan te passen. Het proces bestaat uit het configureren van de webhaak in het `actions.config.yaml` -bestand, het inschakelen ervan in het `app.config.yaml` -bestand en het implementeren ervan om de juiste functionaliteit te garanderen.

De video behandelt de stappen om de code van de website te wijzigen om derdegebeurtenissen in formaten te vertalen compatibel met de geabonneerde gebeurtenistypen van de integratie. Er wordt gesproken over het toevoegen van een `event-mapping.json` -bestand om deze vertaling te vergemakkelijken en het belang van het opnieuw implementeren van de runtimeactie na het aanbrengen van wijzigingen wordt benadrukt. &#x200B; De video benadrukt ook het belang van het valideren en transformeren van inkomende gebeurtenisladingen om zich aan het verwachte schema te richten, die succesvolle verwerking en integratie met Commerce API verzekeren voor het creëren van klanten.

## Publiek

* Ontwikkelaars die een ingesloten webhaak willen instellen
* Iedereen die code voor gebeurtenisvertaling wil aanpassen
* Ontwikkelaars en architecten die het belang van verificatie en loonbeheer willen begrijpen

## Video-inhoud

* Configuratie en implementatie: in de video wordt het belang benadrukt van het configureren van de ingesloten webhaak in het `actions.config.yaml` -bestand en het inschakelen ervan in het `app.config.yaml` -bestand. Het benadrukt ook de behoefte om het project opnieuw op te stellen na het aanbrengen van veranderingen om de webhaakfuncties correct te verzekeren.
* Aanpassing voor compatibiliteit: het is van cruciaal belang dat u de code van de webhaak aanpast om gebeurtenissen van derden te vertalen in indelingen die zijn afgestemd op de gebeurtenistypen die zijn geabonneerd door de integratie. &#x200B; Deze aanpassing zorgt voor naadloze communicatie tussen systemen en een geslaagde verwerking van gebeurtenissen.
* Implementatie van verificatie: Bedrijven zijn verantwoordelijk voor de implementatie van verificatiemechanismen die geschikt zijn voor hun behoeften om ongeoorloofde verzoeken te voorkomen wanneer de ingestitiewebhaak wordt gebruikt. Deze stap is van essentieel belang voor het behoud van de veiligheid en integriteit van de integratie.
* Payload-validatie en -transformatie: het valideren en transformeren van inkomende gebeurtenisladingen die overeenkomen met het verwachte schema is essentieel voor een geslaagde verwerking en integratie met de Commerce API. &#x200B; Door velden op de juiste manier bij te snijden en toe te wijzen, kan de integratie efficiënt werken met de benodigde gegevens.

>[!VIDEO](https://video.tv.adobe.com/v/3431694?learn=on)

{{$include /help/_includes/starter-kit-related-links.md}}

## Codevoorbeelden

* [&#x200B; Web-haak van de Douane Ingesie &#x200B;](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit/customize-ingestion-webhook)
* [&#x200B; voeg binningsplanner &#x200B;](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit/add-ingestion-scheduler) toe

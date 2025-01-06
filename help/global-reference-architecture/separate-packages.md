---
title: Afzonderlijke pakketten Algemene referentiearchitectuur
description: Optimaliseer Adobe Commerce met Aparte Pakketten GRA. Leer installatie, voordelen, en beste praktijken voor flexibel, versioned pakketbeheer.
kt: 16727
doc-type: tutorial
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
topic: Architecture, Commerce, Development
role: Architect, Developer, User, Leader
level: Beginner, Intermediate
source-git-commit: 916586d3b71b8b74baa04af2ab39abc86ec94f5b
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 0%

---


# Het globale referentiearchitectuurpatroon van de Afzonderlijke Pakketten

In deze handleiding wordt uitgelegd hoe u Adobe Commerce instelt met het GRA-patroon (Separate Packages Global Reference Architecture).

Bij het GRA-patroon voor afzonderlijke pakketten wordt één Git-opslagplaats gebruikt voor elk gemeenschappelijk pakket en een Git-opslagplaats voor elke Adobe Commerce-instantie. Gemeenschappelijke pakketten worden via Composer weergegeven met een privécomposer-opslagplaats.

Dit globale referentiearchitectuurpatroon is volledig gebaseerd op composers en is ontworpen om optimaal te profiteren van alle Composer-functies.

![ een diagram dat toont waar de code in een Afzonderlijk patroon van Pakketten GRA ](/help/assets/global-reference-architecture/separate-packages-gra-pattern-diagram.png){align="center"} wordt opgeslagen

## Voordelen en nadelen van dit patroon

Voordelen:

- Hergebruik van code via een gedeelde opslagplaats voor code
- Volledige flexibiliteit bij de installatie van pakketten. Elk GRA-pakket kan afzonderlijk worden bijgewerkt, gedowngradeerd of ondersteund
- Volledige ondersteuning voor semantische versioning
- Geen speciaal gereedschap, complexe infrastructuur of speciale vertakkingsstrategie vereist
- Ondersteuning voor alle pakkettypen die door Composer worden ondersteund

Nadelen:

- De ontwikkeling binnen dit GRA-patroon is in het begin iets moeilijker, er is een kleine leercurve
- Mogelijkheid om combinaties van pakketten in te voeren die niet in dezelfde configuratie zijn ontwikkeld, vereist strikte testprocedures

## Adobe Commerce instellen met het GRA-patroon voor afzonderlijke pakketten

### De mappenstructuur

De uiteindelijke mapstructuur van een volledige Adobe Commerce-installatie met het GRA-patroon voor afzonderlijke pakketten ziet er als volgt uit:

```text
.
├── app/
│   └── etc/
│       └── config.php
├── composer.json
└── composer.lock
```

De mappen `app/code` , `app/i18n` en `app/design` worden met opzet weggelaten. Met de GRA voor afzonderlijke pakketten wordt elk pakket van Composer geïnstalleerd. Zelfs als het pakket slechts in één Adobe Commerce-instantie is geïnstalleerd.

### De opslagplaats voorbereiden

Maak een opslagplaats voor de eerste Adobe Commerce-instantie, die een webwinkel voor merk X vertegenwoordigt.

```bash
mkdir gra-separate-brand-x
cd gra-separate-brand-x
composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition .
git init
git remote add origin git@github.com:AntonEvers/gra-separate-brand-x.git 
git add composer.json composer.lock
git commit -m 'initialize Brand X repository'
git push -u origin main
```

Installeer Adobe Commerce met `bin/magento setup:install` . Leg de resulterende waarde vast `app/etc/config.php` .

### Pakketopslagplaatsen maken

Elk pakket in dit globale referentiearchitectuurpatroon heeft een eigen Git-opslagplaats. Hieronder vindt u voorbeeldpakketten met Adobe Commerce-modules die een GRA-module, een externe module en een lokale module vertegenwoordigen.

- <https://github.com/AntonEvers/module-example-gra>
- <https://github.com/AntonEvers/module-example-3rdparty>
- <https://github.com/AntonEvers/module-example-local>

Gebruik de voorbeelden om uw eigen pakketten te maken.

### Verzamelopslagruimten voor metapakketten maken

Metapakketten bepalen het bereik van de algemene GRA-codebase in dit GRA-patroon. Zij bepalen wat in de stichting is: welke combinatie pakketversies altijd samen worden geïnstalleerd. Een voorbeeld:

```json
{
    "name": "antonevers/gra-meta-foundation",
    "type": "metapackage",
    "require": {
        "antonevers/gra-component-foundation": "~1.0",
        "antonevers/module-gra": "~1.0",
        "antonevers/module-3rdparty": "~1.0",
        "magento/composer-dependency-version-audit-plugin": "~0.1",
        "magento/composer-root-update-plugin": "~2.0",
        "magento/product-enterprise-edition": "2.4.6-p3"
    }
}
```

Het bovenstaande fragment is composer.json van een metapakket. Omdat metapakketten alleen een bestand composer.json en geen andere code bevatten. De bovenstaande code is ook het volledige pakket metampagnes. Plaats het in een Git-opslagplaats en u hebt een installeerbare opslagplaats voor metapakketcomposers. Het vereist één voorbeeldmodule GRA en een derdemodule, evenals de kern van Adobe Commerce. Het vereist ook de gra-component-stichting, die in het volgende hoofdstuk zal worden verklaard.

Metapakketten zijn een manier om pakketten te bundelen zonder afhankelijkheden tussen de pakketten te maken. Dus zelfs als er geen technische afhankelijkheid is tussen pakketten, met een metapakket, kunt u ervoor zorgen dat ze samen worden geïnstalleerd. Als u deze metapakket in uw project vereist, dan wordt om het even welk pakket of metapakket dat de metapakket vereist geïnstalleerd. Als u dus een leeg composerproject maakt en u alleen dit pakket nodig hebt, installeert Composer Adobe Commerce en de GRA en de module van derden.

Op deze manier kunt u ervoor zorgen dat elke winkel dezelfde set basispakketten bevat.

Op dezelfde manier kunt u een metapakket definiëren waarmee store x wordt gedefinieerd. Het vereist het stichtingsmetapakket, dat de volledige stichting GRA vereist, plus een lokale module:

```json
{
    "name": "antonevers/gra-meta-brand-x",
    "type": "metapackage",
    "require": {
        "antonevers/gra-meta-foundation": "~1.0",
        "antonevers/module-local": "~1.0"
    }
}
```

Het metapakket Brand-X is optioneel. U kunt het merkmetapakket ook overslaan en deze gebiedsdelen direct in uw project van de Composer van de opslag vereisen. Het voordeel van het maken van een metapakket voor lokale modules is dat u geen functievertakkingen en eigenschaptrekkingsverzoeken op de opslagplaats van de Git hebt, slechts in de pakketbewaarplaatsen. Het is een veiligheidsmaatregel. Daarnaast kunt u semantische versies toepassen op de pakketrepositories en verschillende Git-tags gebruiken voor uw hoofdproject, bijvoorbeeld om benoemde releases bij te houden. Het is aan u.

### GRA-basisbestanden buiten de directory van de leverancier

Soms moet u bestanden buiten de map van de leverancier opslaan. Bijvoorbeeld `.gitignore` , bestanden die in de map of domeinverificatiebestanden van `dev/` worden weergegeven. Het pakkettype magento2-component is hiervoor ontworpen. Kijk naar <https://github.com/AntonEvers/gra-component-foundation>.

```json
{
    "name": "antonevers/gra-component-foundation",
    "type": "magento2-component",
    "require": {
        "magento/magento-composer-installer": "*"
    },
    "extra": {
        "map": [
            [
                "src/gitignore",
                ".gitignore"
            ]
        ]
    }
}
```

Dit pakket heeft het type magento2-component en bevat een map src die bestanden host die naar de Adobe Commerce-hoofdmap worden gekopieerd. De toewijzing in dit dossier kopieert `/src/gitignore` aan `/.gitignore` in het belangrijkste project Composer.

Op deze manier kunt u ook bestanden buiten de directory van de leverancier van uw GRA-stichting maken.

### Een GRA-stichtingsmodule ontwikkelen

De ontwikkeling gebeurt binnen de verkopersfolder. Vraag de Composer om de basispakketten van de bron te installeren. Hiermee worden pakketten uitgecheckt vanuit Git in plaats van ze te installeren vanuit een gedownload archief.

```bash
rm -r vendor/antonevers/*
composer install --prefer-source
```

Met deze opdracht zijn pakketten in de naamruimte antonevers uitgecheckt met behulp van Git. Wanneer u de leverancier/antonevers/module-gra folder ingaat, gaat u ook de module-gra opslagplaats van de it in. U kunt nu vertakkingen maken, uitchecken en samenvoegen en deze vertakkingen direct vanuit de directory van leveranciers ontwikkelen.

### Inclusief modules van derden bij de oprichting van de GRA

Voeg pakketten van derden toe aan het GRA-metapakket. Als code van derden niet beschikbaar is om te worden geïnstalleerd vanuit een Composer-opslagplaats, maakt u er een pakket voor. Maak een Git-repo, voeg de inhoud van de pakketten toe (alles wat zich in app/code/Vendor/Package zou bevinden) en zorg ervoor dat er een geldig composer.json-bestand aanwezig is in de hoofdmap van de opslagplaats. U kunt dit pakket nu installeren via Composer.

## Een persoonlijke Composer-opslagplaats instellen

Een privéopslagplaats is niet verplicht in de wereldwijde referentiearchitectuur. Het maakt plaatsingen en installatie sneller, vermindert bewaargegevensconfiguratie in composer.json, en het verhoogt veiligheid. Credentials naar andere Composer-opslagplaatsen en de Adobe Commerce Marketplace worden opgeslagen in uw persoonlijke opslagruimte. Geen gevoelige referenties meer gebundeld met de code of op ontwikkelaarsmachines.

Bovendien bieden sommige privéopslagruimten extra functies, zoals e-mailmeldingen, wanneer een van uw winkels een kwetsbaarheid voor beveiliging in een van de afhankelijkheden bevat.

De traagheidskwestie is wat voorkomt wanneer u veelvoudige bewaarplaatsen VCS in composer.json hebt. Elke Composer-opslagplaats moet worden gelezen bij upgrades en 50 opslagplaatsen voor 50 pakketten hebben minstens 50 keer de overhead van slechts één Composer-opslagplaats.

![ een diagram dat toont waar de vertraging voorkomt wanneer een composer bewaarplaats ](/help/assets/global-reference-architecture/separate-packages-without-mirror-diagram.png){align="center"} mist

Neem een Composer-spiegel op in de vorm van een privécomposer-opslagplaats. De spiegel bevat een kopie van alle pakketten van andere composer-opslagplaatsen en van alle door Git gehoste pakketten. Met een persoonlijke Composer-opslagplaats krijgt u bovendien een fijnkorrelig toegangsbeheer.

Met Git-synchronisatie detecteert een persoonlijke Composer-opslagplaats automatisch nieuwe pakketten in uw Git-opslagruimten en nieuwe versies van bestaande pakketten.

U kunt uw eigen privéopslagruimte hosten met Satis: <https://composer.github.io/satis/> . Zie een voorbeeld van een openbare gegevensopslagruimte op <https://antonevers.github.io/gra-composer-repository/> . Dit repo wordt gebruikt als composer opslagplaats in de codevoorbeelden. Er zijn aanvullende maatregelen nodig om een satis-gegevensbank privé te maken.

Er zijn oplossingen die u kunt configureren en vergeten: Private Packagist <https://packagist.com/> , die wordt gemaakt door dezelfde personen die Composer of JFrog Artifactory <https://jfrog.com/artifactory/> hebben geschreven.

## Code leveren

Met metapakketten, zijn er 3 stappen om code te leveren.

1. Wijzigingen samenvoegen in pakketten en de gewijzigde pakketten verfraaien.
2. (Optioneel, alleen als nieuwe pakketten worden toegevoegd) Vereisen de nieuwe pakketten in metapakketten en versen de metapakketten.
3. (Optioneel, alleen als nieuwe pakketten worden toegevoegd) Vereisen de nieuwe metapakketten in Adobe Commerce en implementeren.

Implementatiebereik wordt beheerd met pakketversies. Door het maken van een stabiele versie van een pakket is dit pakket klaar voor productie.

Als u een nieuwe versie wilt maken, voert u een composer-update uit in het hoofdproject Composer, dat de volledige opslaginstallatie bevat. Alle nieuwste versies van pakketten worden geïnstalleerd.

## Versioning

Versioning in een Aparte Pakketten GRA is een synoniem aan het etiketteren van modules in Git. Met Git-tags maakt u genummerde versies van uw pakketten die door Composer worden geïnstalleerd.
De juiste versioning benadering laat uw pakketten automatisch stromen, terwijl ook veilig blijft.

Twee voorbeelden:

```json
{
    "name": "antonevers/gra-meta-foundation",
    "type": "metapackage",
    "require": {
        "antonevers/gra-component-foundation": "1.1.4",
        "antonevers/module-gra": "1.0.0",
        "antonevers/module-3rdparty": "1.3.89"
    }
}
```

In dit voorbeeld wordt een strikte definitie van afhankelijkheden getoond. Er zijn 3 pakketten vereist in exacte versies. Composer-update met deze metapakket in uw installatie doet niets. Deze 3 pakketten worden altijd in deze exacte versies geïnstalleerd, zelfs als een nieuwere versie beschikbaar is.

```json
{
    "name": "antonevers/gra-meta-foundation",
    "type": "metapackage",
    "require": {
        "antonevers/gra-component-foundation": "~1.0",
        "antonevers/module-gra": "~1.0",
        "antonevers/module-3rdparty": "~1.0"
    }
}
```

Dit voorbeeld toont een losse definitie van gebiedsdelen. Met `~1.0` kan elke versie van deze pakketten worden geïnstalleerd als deze groter is dan of gelijk is aan `1.0.0` en kleiner dan `2.0.0` , met een voorkeur voor de hoogst beschikbare versie. Meer informatie over het definiëren van versieafhankelijkheden vindt u in <https://getcomposer.org/doc/articles/versions.md> :

> De operator ~ kan het best worden uitgelegd door een voorbeeld: `~1.2` is gelijk aan `>=1.2 <2.0.0` , terwijl `~1.2.3` gelijk is aan `>=1.2.3 <1.3.0` .

Zodra u een nieuwe versie van een van de genoemde pakketten vrijgeeft, wordt deze automatisch geïnstalleerd met een Composer-update.

Semantische versioning toepassen. U kunt op <https://semver.org/> alles leren over semantische versies. Vooral de veelgestelde vragen moeten worden gelezen. Met semantische versioning worden de getallen in &quot;1.0.0&quot; MAJOR.MINOR.PATCH genoemd. Kleine en patchreleases van een verpakking moeten veilig worden geïntroduceerd zonder de toepassing te onderbreken.
U kunt automatisch patches opnemen en handmatig kleine upgrades kiezen. Houd er rekening mee dat dit extra overhead kost door elke kleine wijziging handmatig te kiezen:

```json
{
    "name": "antonevers/gra-meta-foundation",
    "type": "metapackage",
    "require": {
        "antonevers/gra-component-foundation": "~1.1.0",
        "antonevers/module-gra": "~1.0.0",
        "antonevers/module-3rdparty": "~1.3.0"
    }
}
```

Natuurlijk werkt dit alleen als u semantische versies consistent toepast, altijd. En niet alleen in metapakketten, maar de vereisten van uw regelmatige pakketten zouden gebiedsdelen ook losjes moeten bepalen. Als u één strikte afhankelijkheid in uw systeem hebt, is dat pakket beperkt tot de strikte definitie.

U kunt deze strikte afhankelijkheden zoeken door composer te typen, is afhankelijk van \&lt;naam pakket\>. Zie <https://getcomposer.org/doc/03-cli.md#depends-why> voor meer informatie.

## Vertakkingsstrategie

U kunt verschillende vertakkingsstrategieën gebruiken om dit globale patroon van de verwijzingsstrategie te steunen, op voorwaarde dat de belangrijkste tak de enige tak is waar u uw pakketten versieert. Als u de versie in verschillende vertakkingen toepast, bestaat het risico dat de functionaliteit tussen de versies willekeurig verloren gaat. Maak alleen stabiele versies op de hoofdvertakking.

Maak alleen functievertakkingen in uw pakketopslagruimten. Niet in de opslaginstallatieruimten. Je winkel kunt nog wijzigingen aanbrengen met behulp van Composer. Vermijd de noodzaak van Git-samenvoegingen in de implementatieruimte.

Branchetypen die veel voorkomen in vertakkingsstrategieën en opslagplaatsen, moeten bestaan in:

**de takken van de Eigenschap**: bestaan in uw pakketbewaarplaatsen, nergens anders.

**vertakkingen van de Versie**: worden gecreeerd in om het even welke bewaarplaats: pakketten, metapakketten, opslaginstallatierapporten. Wanneer u een versie plant, groepeert veranderingen in versiestakken van pakketten alvorens hen te versioning. Stel dat u een release voorbereidt met de codenaam &quot;Unicorn&quot;. U kunt een vertakking met één release maken in pakketten met wijzigingen. Voeg daar om het even wat in samen en dan vereist &quot;dev-release-unicorn als 1.4.0&quot;in uw metapakket. Meer informatie over aliassen om te zien wat daar gebeurt: <https://getcomposer.org/doc/articles/aliases.md> .

**vertakkingen QA/Dev**: gelijkend op versie takken.

**Belangrijkste tak**: moet in elke bewaarplaats bestaan en zou altijd de tak moeten zijn die productie of een productie-klaar staat vertegenwoordigt. De hoofdvertakking is waar u code codeert om versies vrij te geven.
Zorg ervoor dat u een vertakkingsstrategie kiest met weinig onderhoudsoverhead. Bijvoorbeeld, is het samenvoegen van de belangrijkste tak terug in QA, UAT, versie, of dev takken na een hotfix versie een overheadonderhoudstaak. Hoe meer pakketten, des te meer opslagruimten en des te meer herhaalde overheadtaken.

Gebruik een gereedschap zoals mixu/gr om routinetaken uit te voeren op meerdere Git-opslagplaatsen in een batch: <https://github.com/mixu/gr>

## Naamconventies

Met het afzonderlijke patroon van Pakketten GRA, maken de pakketten deel uit van de stichting GRA als het stichtingsmetapakket hen vereist. Voeg pakketten toe of verwijder pakketten uit het metapakket om hen binnen en uit de stichting te bewegen.

Metapakketten bieden flexibiliteit aan het installatiebereik van pakketten. Het is extra belangrijk dat de namen van de verpakkingen geen woorden bevatten die betrekking hebben op het beoogde gebruik van de verpakking. De naam antonevers/module-gra-store-locator kan verwarrend worden wanneer u besluit dat pakket uit de stichting te nemen GRA. Vermijd bereik (GRA, stichting, lokaal). Vermijd regio (EMEA, Spanje, Global). Vermijd zeker de naam van de opslag waarvoor een pakket wordt gebouwd. Kies namen die alleen betrekking hebben op de functionaliteit die in het pakket is toegevoegd. Op die manier kunt u ze overal waar u maar wilt hergebruiken, ook in onvoorziene toekomstige scenario&#39;s. De naam antonevers/module-store-locator zou uitstekend zijn.

Zorg ervoor dat gerelateerde pakketten worden weergegeven in overzichten. Bouw namen van algemeen aan specifiek. Dus antonevers/module-b2b-belastingvrijstelling in plaats van antonevers/belastingvrijstelling-module-b2b.

## Codevoorbeelden

De codevoorbeelden van dit blogbericht zijn gecombineerd in een set Git-opslagplaatsen, die u kunt gebruiken om af te spelen met de concepttest.

- Een voorbeeld van een productiearchief: <https://github.com/AntonEvers/gra-separate-brand-x>
- Een voorbeeld van een basismodule: <https://github.com/AntonEvers/module-example-gra>
- Een voorbeeldmodule van derden: <https://github.com/AntonEvers/module-example-3rdparty>
- Een lokale voorbeeldmodule: <https://github.com/AntonEvers/module-example-local>
- Een voorbeeld van een metapakket voor de basis: <https://github.com/AntonEvers/gra-meta-foundation>
- Een voorbeeld van een lokale metapack (optioneel): <https://github.com/AntonEvers/gra-meta-brand-x>
- Een voorbeeld van een Composer-opslagplaats: <https://github.com/AntonEvers/gra-composer-repository>
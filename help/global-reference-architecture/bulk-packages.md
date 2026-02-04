---
title: Adobe Commerce optimaliseren met Bulk Packages Global Reference Architecture
description: Leer hoe u Adobe Commerce instelt met behulp van de Bulk Packages Global Reference Architecture voor efficiënt codebeheer en versiebeheer.
jira: KT-16726
doc-type: tutorial
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
topic: Architecture, Commerce, Development
badge: label="Bijgedragen door Tony Evers, Sr. Technical Architect, Adobe" type="Informative" url="https://www.linkedin.com/in/evers-tony/" tooltip="Bijgedragen door Tony Evers"
old-role: Architect, Developer
role: Developer, User, Leader
level: Beginner, Intermediate
exl-id: ac63e31e-3047-410a-a6f9-a578b495bd8c
source-git-commit: 79d57d2c04c42a8dc23b5735e72e841b7e51cc63
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 0%

---

# Het globale patroon van de verwijzingsarchitectuur van Pakketten van het Bulk

{{only-for-on-prem-commerce-cloud}}

In deze handleiding wordt uitgelegd hoe u Adobe Commerce instelt met het GRA-patroon (Bulk Packages Global Reference Architecture).

Het GRA-patroon van bulkpakketten bestaat uit één Git-opslagplaats die alle algemene aanpassingen host. Deze enkele Git-opslagplaats wordt via Composer weergegeven als één composer-pakket, dat meerdere Adobe Commerce-modules bevat.

![ een diagram dat toont waar de code in een bulkpakkettenGRA patroon ](/help/assets/global-reference-architecture/bulk-gra-pattern-diagram.png){align="center"} wordt opgeslagen

## Voordelen en nadelen van dit patroon

Voordelen:

- Codehergebruik via een gedeelde gegevensopslagruimte
- Flexibiliteit om verschillende historische versies van GRA op verschillende instanties te installeren, toelatend gefaseerde versies
- Flexibiliteit om veelvoudige belangrijke versies van GRA te steunen en te handhaven
- Steun voor semantische versioning van de GRA
- Eenvoudig, hebben de ontwikkelaars niet meer vaardigheden nodig dan in regelmatige enig-opslagontwikkelingspatronen
- Geen speciaal gereedschap, complexe infrastructuur of speciale vertakkingsstrategie vereist
- De combinatie van pakketten in een release wordt altijd samen ontwikkeld en getest

Nadelen:

- Alleen mogelijk om de volledige GRA te upgraden, inclusief alle pakketten in de GRA.
- Geen ondersteuning in het GRA-bulkpakket voor composerpakketten, met uitzondering van Adobe Commerce-modules, taalpakketten en thema&#39;s, zodat er geen metapakketten, magento2-componentpakketten, Composer-plug-ins en -patches worden ondersteund

## Adobe Commerce instellen met het patroon Git splitsen

### De mappenstructuur

Met het GRA-bestand voor bulkpakketten worden alle herbruikbare code geïnstalleerd via Composer-opslagruimten. Code die specifiek is voor één instantie, bevindt zich in de Git-opslagruimte van die instantie. Instantiespecifieke code wordt niet opnieuw gebruikt in andere instanties van Adobe Commerce.

De uiteindelijke mapstructuur van een volledige Adobe Commerce-installatie met het GRA-patroon voor bulkpakketten ziet er als volgt uit:

```text
.
├── app/
│   └── etc/
│       └── config.php
├── composer.json
├── composer.lock
└── packages/
    └── local/
```

De mappen `app/code`, `app/i18n` en `app/design` worden met opzet weggelaten, omdat Composer de code in deze mappen niet evalueert. Dientengevolge, worden de gebiedsdelen die in de pakketten worden verklaard niet automatisch geïnstalleerd. Met het GRA-patroon van bulkpakketten wordt dit probleem opgelost door een aangepaste code in `packages/` te installeren en die map als een composeropslagplaats te behandelen. Composer symboliseert pakketten binnen `packages/` naar `vendor/` .

### De Git-opslagruimten voorbereiden

Maak twee Git-opslagruimten voor de gedeelde GRA-code en voor de eerste opslag. Begin met de gegevensopslagplaats GRA, die de volgende dossierstructuur heeft:

Het resultaat is de volgende mappenstructuur:

```text
.
├── composer.json
└── src/
    ├── GraOne/
    │   ├── composer.json
    │   └── registration.php
    ├── GraTwo/
    │   ├── composer.json
    │   └── registration.php
    └── registration.php
```

Deze mapstructuur vermeldt alleen het bestand composer.json en het bestand registration.php van de modules GraOne en GraTwo. In werkelijkheid zijn er meer bestanden in deze modules.

Voer deze opdrachten uit om de Git-opslagplaats te starten:

```bash
mkdir gra-bulk-foundation
cd gra-bulk-foundation
git init
git remote add origin git@github.com:AntonEvers/gra-bulk-foundation.git
vim composer.json # see code snippet below for contents
git add composer.json
git commit -m 'initialize GRA foundation repository'
git push -u origin main
```

De inhoud van het bestand composer.json:

```json
{
    "name": "antonevers/gra-bulk-foundation",
    "description": "Shared code repository",
    "type": "library",
    "license": [
        "OSL-3.0",
        "AFL-3.0"
    ],
    "require": {},
    "autoload": {
        "files": [
            "src/registration.php"
        ],
        "psr-0": {
            "": "src/"
        }
    }
}
```

Wijzig de naamruimte van het pakket composer.json in uw eigen naamruimte.

De inhoud van het bestand src/registration.php:

```php
<?php

declare(strict_types=1);

$pathList[] = dirname(__DIR__) . '/src/*/*/registration.php';
foreach ($pathList as $path) {
    $files = glob($path, GLOB_NOSORT | GLOB_ERR);
    if ($files === false) {
        throw new RuntimeException('glob() returned error while searching in \'' . $path . '\'');
    }
    foreach ($files as $file) {
        require_once $file;
    }
}
```

Het bestand registration.php zoekt naar andere bestanden registration.php in de Adobe Commerce-modules en voert deze uit.

Maak de twee voorbeeldmodules met behulp van de code in <https://github.com/AntonEvers/gra-bulk-foundation> . Composer evalueert niet de bestanden composer.json in de voorbeeldmodules. Ze zijn er als gewoonte. Als u besluit om de modules naar een andere plaats te verplaatsen, worden de composer.json- dossiers opnieuw noodzakelijk.

### Opslagopslagplaats instellen

De implementatieopslagplaats bevat de volledige Adobe Commerce-installatie, inclusief de GRA-code. Maak de implementatieopslagplaats:

```bash
mkdir gra-bulk-brand-x
cd gra-bulk-brand-x
composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition .
git init
git remote add origin git@github.com:AntonEvers/gra-bulk-brand-x.git 
git add composer.json composer.lock
git commit -m 'initialize Brand X repository'
git push -u origin main
```

Installeer Adobe Commerce met `bin/magento setup:install` . Installeer de GRA-voorbeeldmodules in de implementatieopslagplaats met Composer:

```bash
composer config repositories.gra-foundation vcs git@github.com:AntonEvers/gra-bulk-foundation.git
composer require antonevers/gra-bulk-foundation:@dev
bin/magento module:enable AntonEvers_GraOne AntonEvers_GraTwo
bin/magento test:gra-one
bin/magento test:gra-two
git add app/etc/config.php composer.json composer.lock
git commit -m 'install GRA foundation'
git push origin main
```

Dat laatste bevel in de volgende output zou moeten resulteren om te bewijzen dat de module geïnstalleerd en werkend is:

```bash
GRA One module is installed successfully and working!
GRA Two module is installed successfully and working!
```

U kunt meerdere bulkpakketten maken om code te ordenen. Bijvoorbeeld een bulkpakket van derden voor code van derden dat niet beschikbaar is via Composer. Alles wat u traditioneel in `app/code` installeert, moet nu in de map `src/` van het bulkpakket staan. Een uitzondering op die regel is code die slechts in één instantie wordt gebruikt. Deze pakketten worden lokale pakketten genoemd.

### Lokale pakketten installeren

De plaatsingsbewaarplaats bewaart lokale pakketten. Zij leven niet in het GRA-bulkpakket. De locatie van de lokale pakketten is niet `app/code` , maar `packages/local` . Instruct Composer to treat this directory as a repository:

```bash
composer config repositories.local path 'packages/local/*/*'
git add composer.json
git commit -m 'initialize local composer package storage'
git push origin main
```

Voeg de voorbeeldmodule toe die wordt gehost op <https://github.com/AntonEvers/module-example-local> :

```bash
mkdir -p packages/local
cd packages/local
mkdir antonevers
cd antonevers
curl -OL https://github.com/AntonEvers/module-example-local/archive/refs/heads/main.zip
unzip main.zip
rm main.zip
mv module-example-local-main module-local
git add module-local
cd ../../..
composer require antonevers/module-local:@dev
bin/magento module:enable AntonEvers_Local
bin/magento test:local
```

Dat laatste bevel in de volgende output zou moeten resulteren om te bewijzen dat de module geïnstalleerd en werkend is:

```bash
Local module is installed successfully and working!
```

Leg de lokale module vast aan de merkenopslagplaats:

```bash
git add packages/local/antonevers/module-local app/etc/config.php composer.json composer.lock 
git commit -m 'add local module'
git push origin main
```

## Overzicht van codelocaties

Alleen als de derde geen installatie aanbiedt via een Composer-opslagplaats, kunt u modules van derden opslaan in de `src/` -directory van de gegevensopslagruimte of een speciaal bulkpakket van derden.

- **kern van Adobe Commerce**: beschikbaar door repo.magento.com.
- **modules van de Derde**: beschikbaar door de Marketplace of de eigen bewaarplaats van de Composer van een verkoper.
- **de optie van de de fallback van derdemodules**: opgeslagen in `src/` van een bulkpakket.
- **de stichtingscode van GRA**: opgeslagen in `src/` van het pakket van de stichting bulkgoederen.
- **Lokale code**: opgeslagen in de `packages/local` folder van de plaatsingsbewaarplaats.

## Een GRA-module ontwikkelen

Installeer het bulkpakket van de bron om Git in de bulkpakketmap in te schakelen:

```bash
rm -r vendor/antonevers/gra-bulk-foundation
composer install --prefer-source
```

Het bulkpakket is uitgecheckt met behulp van Git. Wanneer u de map `vendor/antonevers/gra-bulk-foundation` invoert, voert u ook de Git-opslagplaats voor gra-bulkobjecten in. U kunt vertakkingen maken, uitchecken en samenvoegen in deze directory.

Voeg Composer-afhankelijkheden toe aan het bestand composer.json in de hoofdmap van het bulkpakket GRA. Dit is het enige bestand in het bulkpakket dat door Composer wordt geëvalueerd.

## Inclusief modules van derden bij het GRA-bulkpakket

Voeg derdepakketten in toe vereiste sectie van composer.json bij de wortel van de stichting GRA om hen aan uw GRA toe te voegen. Op die manier worden de pakketten altijd in al uw instanties geïnstalleerd via composer.

## Uw code leveren

Er zijn twee paden om code aan de hoofdvertakking te leveren. Eerst de lokale modules, die aan de belangrijkste tak worden samengevoegd. Composer-update voor deze modules uitvoeren. Sta ontwikkelaars niet toe om composer.lock in hun kaarttakken bij te werken om conflicten te verminderen. Werk alleen het bestand composer.lock bij in afbouwings- en productietakken, waardoor het risico op conflicten afneemt.

In de tweede plaats de GRA-bulkpakketten, die worden samengevoegd tot de hoofdtak van de GRA-bulkopslagplaats. Vervolgens kunt u een tag Git aan de hoofdvertakking toevoegen en het Composer-pakket versieëren. Vereist uw nieuwe versie van het GRA bulkpakket in composer.json van de plaatsingsbewaarplaats om het te installeren.

## Vertakkingsstrategie

Dit GRA-patroon werkt met alle vertakkende strategieën zolang u de vertakkingsstrategie van de implementatieruimten in uw GRA bulkgegevensopslagruimte weerspiegelt. Voor versies maakt u een releasetak met dezelfde naam in beide opslagruimten. Voor ontwikkeling, creeer een kaarttak in beide bewaarplaatsen.

In kaartvertakkingen, zou u bijna nooit het composer.lock- dossier moeten bijwerken. Bekijk de juiste vertakkingen in uw ontwikkelomgeving voor zowel de opslag als de GRA-stichtingsopslagplaats met Git. De uitzondering is wanneer u vereisten in het GRA stichtingscomposer.json- dossier bijwerkt. De bevordering van de stichting GRA in de plaatsingsbewaarplaats wordt slechts gedaan wanneer het bouwen van de versie, of wanneer het bouwen van een tak QA.

## Codevoorbeelden

De codevoorbeelden van dit artikel zijn beschikbaar als een reeks bewaarplaatsen van de it, die u kunt gebruiken om het bewijs van concept te testen.

- Een voorbeeld van een productiearchief: <https://github.com/AntonEvers/gra-bulk-brand-x>
- De GRA-codeopslagplaats: <https://github.com/AntonEvers/gra-bulk-foundation>
- Een lokale voorbeeldmodule: <https://github.com/AntonEvers/module-example-local>

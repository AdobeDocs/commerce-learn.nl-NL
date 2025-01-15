---
title: Hoe kunt u gebruikmaken van wereldwijde referentiearchitectuur
description: Leer hoe u een wereldwijde referentiearchitectuur kunt gebruiken om een schaalbare en veerkrachtige handelservaring te creëren
landing-page-description: Meer informatie over Global Reference Architecture en hoe deze wordt gebruikt met Adobe Commerce
jira: KT-16728
doc-type: tutorial
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
badge: label="Bijgedragen door Tony Evers, Sr. Technical Architect, Adobe" type="Informative" url="https://www.linkedin.com/in/evers-tony/" tooltip="Bijgedragen door Tony Evers"
topic: Architecture, Commerce, Development
role: Architect, Developer, User, Leader
level: Intermediate, Advanced
source-git-commit: 7e7c22e994ac5be6eacbcd0084d8ec92666b2024
workflow-type: tm+mt
source-wordcount: '1385'
ht-degree: 0%

---


# Het globale referentiearchitecepatroon van Monorepo

In deze handleiding wordt uitgelegd hoe u Adobe Commerce instelt met het GRA-patroon (Monorepo Global Reference Architecture).

Het patroon van Monorepo GRA omvat één enkele bewaarplaats van de it om alle gemeenschappelijke aanpassingen te ontvangen. Deze afzonderlijke Git-opslagplaats wordt via Composer weergegeven als afzonderlijke composer-pakketten.

![ een diagram dat toont waar de code in een patroon van monorepo GRA ](/help/assets/global-reference-architecture/monorepo-gra-pattern-diagram.png){align="center"} wordt opgeslagen

## Voordelen en nadelen van dit patroon

Voordelen:

- Ideaal voor functionele tests
- Hergebruik van code via een gedeelde opslagplaats voor code
- Volledige flexibiliteit bij de installatie van pakketten. Elk GRA-pakket kan afzonderlijk worden bijgewerkt, gedowngradeerd of ondersteund
- Volledige ondersteuning voor semantische versioning
- Geen speciaal gereedschap, complexe infrastructuur of speciale vertakkingsstrategie vereist
- Ondersteuning voor alle pakkettypen die door Composer worden ondersteund
- Ideaal voor letterlijke omgevingen, die optioneel zijn, maar voor leveringsteams voor grote volumes zijn ze erg nuttig

Nadelen:

- Mogelijkheid om combinaties van pakketten in te voeren die niet in dezelfde configuratie zijn ontwikkeld, vereist strikte testprocedures
- Het monorepo GRA-patroon kan aan het begin complex zijn. Wijs een lood toe dat het team met het systeem helpt werken

## Adobe Commerce instellen met het GRA-patroon voor afzonderlijke pakketten

### De mappenstructuur

De uiteindelijke mapstructuur van een volledige Adobe Commerce-installatie met het GRA-patroon Aparte pakketten heeft de volgende directorystructuur:

```text
.
├── app/
│   └── etc/
│       └── config.php
├── packages/
│   └── ...
├── composer.json
└── composer.lock
```

Een opslagplaats van de productiegit heeft deze folderstructuur:

```text
.
├── app/
│   └── etc/
│       └── config.php
├── composer.json
└── composer.lock
```

Het verschil is dat de productie-instanties worden geïnstalleerd vanaf Composer, waar de monorepo zijn eigen kopie van elk pakket in de map packages bevat.

### Een productieopslagplaats voorbereiden

Maak een opslagplaats voor de eerste Adobe Commerce-instantie, die een webwinkel voor merk X vertegenwoordigt.

```bash
mkdir gra-monorepo-brand-x
cd gra-monorepo-brand-x
composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition .
git init
git remote add origin git@github.com:AntonEvers/gra-monorepo-brand-x.git 
git add composer.json composer.lock
git commit -m 'initialize Brand X repository'
git push -u origin main
```

Installeer Adobe Commerce met `bin/magento setup:install` . Leg de resulterende `app/etc/config.php` - en composer-bestanden vast. Composer beheert iets anders, dus niets anders zou in Git moeten zijn.

### De gegevensopslagplaats voor monorepo voorbereiden

De monorepo-opslagplaats begint met dezelfde stappen.

```bash
mkdir gra-monorepo 
cd gra-monorepo
composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition .
```

Installeer Adobe Commerce met `bin/magento setup:install` , wijs het toe en duw.

```bash
git init
git remote add origin git@github.com:AntonEvers/gra-monorepo.git 
git add composer.json composer.lock app/etc/config.php
git commit -m 'initialize monorepo GRA development repository'
git push -u origin main
```

### Voorbereiden op monorepo-ontwikkeling

Breng voor monorepo-ontwikkeling de volgende wijzigingen aan in het bestand composer.json:

1. Wijzig de naam en beschrijving van het pakket, zodat duidelijk is dat dit pakket uw monorepo-pakket is.
1. Verwijder het kenmerk version uit van composer.json, omdat de versie wordt beheerd met behulp van Git-tags voor deze opslagplaats.
1. Vervang de verplichte sectie door een metapakket dat later wordt gemaakt.
1. Minimale stabiliteit wijzigen in ontwikkelen.
1. Voeg een opslagplaats voor padtypen toe die naar `packages/*/*` wijst voor het hosten van monopakketten, inclusief vertakkingen voor elk pakket dat het bevat
1. Voeg een takalias voor het project zelf toe

In het volgende Git diff ziet u het verschil tussen een schone Adobe Commerce-installatie en de hierboven vermelde wijzigingen:

```diff
@@ -1,6 +1,6 @@
 {
-    "name": "magento/project-enterprise-edition",
-    "description": "eCommerce Platform for Growth (Enterprise Edition)",
+    "name": "antonevers/gra-monorepo",
+    "description": "Monorepo repository for Global Reference Architecture development",
     "type": "project",
     "license": [
         "proprietary"
@@ -15,11 +15,8 @@
         "preferred-install": "dist",
         "sort-packages": true
     },
-    "version": "2.4.7-p3",
     "require": {
-        "magento/product-enterprise-edition": "2.4.7-p3",
-        "magento/composer-dependency-version-audit-plugin": "~0.1",
-        "magento/composer-root-update-plugin": "^2.0.4"
+        "antonevers/gra-meta-brand-x": "self.version"
     },
     "autoload": {
         "exclude-from-classmap": [
@@ -69,16 +66,33 @@
             "Magento\\Tools\\Sanity\\": "dev/build/publication/sanity/Magento/Tools/Sanity/"
         }
     },
-    "minimum-stability": "stable",
+    "minimum-stability": "dev",
     "prefer-stable": true,
     "repositories": [
         {
+            "type": "path",
+            "url": "packages/*/*",
+            "options": {
+                "versions": {
+                    "antonevers/gra-meta-brand-x": "1.4.x-dev",
+                    "antonevers/gra-meta-foundation": "1.4.x-dev",
+                    "antonevers/gra-component-foundation": "1.4.x-dev",
+                    "antonevers/module-gra": "1.4.x-dev",
+                    "antonevers/module-3rdparty": "1.4.x-dev",
+                    "antonevers/module-local": "1.4.x-dev"
+                }
+            }
+        },
+        {
             "type": "composer",
             "url": "https://repo.magento.com/"
         }
     ],
     "extra": {
-        "magento-force": "override"
+        "magento-force": "override",
+        "branch-alias": {
+            "dev-main": "1.4.x-dev"
+        }
     }
 }
```

### Metapakketten gebruiken

Download de voorbeeldcode van [ AntonEvers/gra-meta-stichting ](https://github.com/AntonEvers/gra-meta-foundation) op GitHub om de metapakketten en de steekproefmodules te krijgen die in dit voorbeeld worden gebruikt.

Composer-metapakketten bundelen meerdere composer-pakketten in één pakket. Wanneer een metapakket wordt vereist, worden alle pakketten die het bundelt automatisch geïnstalleerd door Composer vereist sectie van de metapakket.

Voor dit voorbeeld zijn er twee metapakketten:

1. **antonevers/gra-meta-brand-x**: Een metapakket dat alles bevat dat omhoog &quot;Merk X&quot;maakt
1. **antonevers/gra-meta-stichting**: Een metapakket dat alles bevat die altijd in om het even welk merk geïnstalleerd is

Voor het merkenpakket is het basispakket voor metapakketten vereist. Wanneer het merk metapakket wordt vereist, wordt de stichting metapakket automatisch vereist. Zie de twee bestanden composer.json van de metapakketten voor de relatie tussen deze bestanden:

antonevers/gra-meta-brand-x:

```json
{
    "name": "antonevers/gra-meta-brand-x",
    "type": "metapackage",
    "license": [
        "OSL-3.0",
        "AFL-3.0"
    ],
    "require": {
        "antonevers/gra-meta-foundation": "^1.4",
        "antonevers/module-local": "^1.4"
    }
}
```

antonevers/gra-meta-foundation:

```json
{
    "name": "antonevers/gra-meta-foundation",
    "type": "metapackage",
    "license": [
        "OSL-3.0",
        "AFL-3.0"
    ],
    "require": {
        "antonevers/gra-component-foundation": "^1.4",
        "antonevers/module-gra": "^1.4",
        "antonevers/module-3rdparty": "^1.4",
        "magento/composer-dependency-version-audit-plugin": "~0.1",
        "magento/composer-root-update-plugin": "^2.0.4",
        "magento/product-enterprise-edition": "2.4.7-p3"
    }
}
```

Metapakketten zijn een goede manier om code samen te organiseren. Gebruik metapakketten om groepen pakketten te definiëren die regionaal, globaal, merkspecifiek zijn of elke groep die voor u zinvol is. Als u meerdere installaties van Adobe Commerce bijhoudt, biedt deze een veilige en flexibele manier om de context te definiëren waarin een pakket wordt verwacht.

Metapakketten staan in de monorepo in de map `packages` . In dit geval wordt de mapstructuur van de `vendor` gespiegeld:

```text
.
├── packages/
│   └── antonevers
│       ├── gra-meta-brand-x
│       │   └── composer.json
│       └── gra-meta-foundation
│           └── composer.json
├── composer.json
└── composer.lock
```

### Modules toevoegen en ontwikkelen

Modules in de monorepo staan in de map `packages` . Op deze manier kunnen Composer ze vinden via de opslagplaats voor padtypen.

Download de voorbeeldcode van [ AntonEvers/gra-meta-stichting ](https://github.com/AntonEvers/gra-meta-foundation) op GitHub om de metapakketten en de steekproefmodules te krijgen die in dit voorbeeld worden gebruikt.

```text
.
├── packages/
│   └── antonevers
│       ├── gra-meta-brand-x
│       ├── gra-meta-foundation
│       ├── module-3rdparty
│       ├── module-gra
│       └── module-local
├── composer.json
└── composer.lock
```

Indien nodig kunt u meerdere naamruimten in de map `packages` plaatsen.

De ontwikkeling vindt plaats in de map packages. Wanneer u `composer update` uitvoert, worden koppelingen naar de pakketten in de map `packages` gemaakt in de map `vendor` . Op deze manier wordt de code onderdeel van de Adobe Commerce-installatie.

Voer `bin/magento module:enable --all` uit of alleen voor specifieke modules om de toegevoegde modules in te schakelen.

Nu moet u een werkende Adobe Commerce-installatie hebben met de drie voorbeeldmodules geïnstalleerd en in gebruik. U kunt controleren of de modules zijn geïnstalleerd en werken door de opdrachten uit te voeren:

```bash
bin/magento test:gra
bin/magento test:3rdparty
bin/magento test:local
```

### Automatisch pakketten maken

Er zijn meerdere opties voor het automatisch maken van pakketten. Sommige opties zijn:

1. [ Privé Packagist ](https://packagist.com/)
1. [ Simplyfy Monorepo Builder ](https://github.com/symplify/monorepo-builder)
1. Bouw uw eigen oplossing

[ Privé Packagist ](https://packagist.com/) automatiseert het erkennen van pakketten in de monorepo van de Git en stelt hen door Composer bloot. Het is compatibel met Adobe Commerce, snel, laag onderhoud en foutgevoelig, en daarom richt deze gids zich op de optie Private Packagist.

Het is voorbij het werkingsgebied van deze gids om uit te leggen hoe te opstelling Privé Packagist, gelieve te zien [ docs ](https://packagist.com/docs).

U kunt een pakket veranderen in een monorepo nadat u de organisatie hebt gesynchroniseerd en uw Git-opslagplaatsen automatisch synchroniseren met Private Packagist.

Ga eerst naar het tabblad Pakketten en zoek de monorepo:

![ Privé het schermschot van het Pakket met het monorepo pakket zichtbaar in het pakkettenscherm ](/help/assets/global-reference-architecture/packagist-packages-before-multi-package.png){align="center"}

Klik op het monorepopakket en klik op &quot;Bewerken&quot; in het detailsscherm. Hiermee gaat u naar de volgende pagina:

![ Privé het schermschot van het Pakket met het monorepo pakket uitgeeft pagina ](/help/assets/global-reference-architecture/packagist-packages-edit.png)

Onder het eerste invoerveld bevindt zich een koppeling met de volgende tekst: Maak een opslagplaats voor meerdere pakketten. Klik op deze koppeling.

![ Privé het schermschot van het Pakket met de multi-pakketconfiguratie ](/help/assets/global-reference-architecture/packagist-packages-multi-package.png)

Definieer de locatie waar composerpakketten in uw monorepo kunnen worden gevonden. In het voorbeeld is de locatie `packages/**/composer.json` . Wijzig de locatie om te beperken of uit te breiden waar Private Packagist zoekt naar pakketten om te extraheren.

Op het tabblad Pakketten worden na het opslaan alle gevonden pakketten weergegeven. De monorepo zelf is dan niet meer zichtbaar als een Composer-pakket:

![ Privé het schermschot van het Pakket met alle monorepo pakketten zichtbaar in het pakketscherm ](/help/assets/global-reference-architecture/packagist-packages-after-multi-package.png)

Voor elk pakket in de monorepo wordt in Composer een versie gemaakt voor elke tag of vertakking die op de monorepo in Git wordt gemaakt.

## De pakketten installeren in de productieomgeving

Volg de instructies van Private Packagist om Private Packagist toe te voegen als een composer-opslagplaats. Private Packagist kan en moet worden gebruikt als spiegel voor al uw Composer-opslagplaatsen en Git-opslagplaatsen, inclusief packagist.org. Op die manier hoeven referenties niet te worden gedeeld met ontwikkelaars en hebt u volledige controle over elk pakket. In dit voorbeeld wordt deze beste praktijk niet gevolgd, omdat de Adobe Commerce-codebase dan openbaar wordt gemaakt.

Download [ GRA Monorepo Merk X ](https://github.com/AntonEvers/gra-monorepo-brand-x) van GitHub om een voorbeeld van een productieopslag te zien.

In de productieopslag is er geen map `packages` en worden alle pakketten geïnstalleerd via Composer. Het enige vereiste pakket is:

```json
    "require": {
        "antonevers/gra-meta-brand-x": "^1.0"
    },
```

Toch worden alle Adobe Commerce en de hele GRA geïnstalleerd via de vereisten van dit pakket.

## Versioning

Alle verpakkingen in de monorepo krijgen dezelfde versie als de monorepo zelf. Beschouw het als het publiceren van nieuwe versies van de volledige toepassing. Bij productie kunt u echter een pakket uit verschillende monorepo-versies installeren.

## Ephemerische omgevingen

Als je ephemelomgevingen gebruikt of ze wilt gebruiken, is de monorepo een uitstekende keuze. Elke versie en vertakking van de monorepo bevat alle bestanden van Adobe Commerce, derden en aangepaste modules. Met een volledige installatie in elke tak, is het mogelijk om elk type van test met inbegrip van functionele tests in werking te stellen. Bij andere GRA-sets, zoals de afzonderlijke pakketten of bulkpakketten GRA, moet u eerst een werkende Adobe Commerce-omgeving bouwen voordat u functionele tests kunt uitvoeren. Vanuit een DevOps-perspectief maakt monorepo het veel eenvoudiger.

## Codevoorbeelden

De codevoorbeelden van dit artikel zijn gecombineerd in een set Git-opslagplaatsen, die u kunt gebruiken om af te spelen met de concepttest.

- Een voorbeeld van een monorepo-opslagplaats: <https://github.com/AntonEvers/gra-monorepo>
- Een voorbeeld van een productiearchief: <https://github.com/AntonEvers/gra-monorepo-brand-x>

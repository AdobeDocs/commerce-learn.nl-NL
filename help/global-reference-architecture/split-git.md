---
title: Adobe Commerce instellen met de Split Git Global Reference Architecture
description: Leer hoe u Adobe Commerce instelt met behulp van de Split Git Global Reference Architecture voor efficiënt codebeheer en gestroomlijnde implementatie. ​
kt: 16725
doc-type: tutorial
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
badge: label="Bijgedragen door Tony Evers, Sr. Technical Architect, Adobe" type="Informative" url="https://www.linkedin.com/in/evers-tony/" tooltip="Bijgedragen door Tony Evers"
topic: Architecture, Commerce, Development
role: Architect, Developer, User, Leader
level: Beginner, Intermediate
exl-id: ac544f77-8f5f-4ad1-92b2-bdf323100c13
source-git-commit: dacd43ef84dcb2c2633221a90642a469b2ff5a30
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 0%

---

# Het globale referentiearchitectuurpatroon Splitsen Git

In deze handleiding wordt uitgelegd hoe u Adobe Commerce instelt met het GRA-patroon (Split Git Global Reference Architecture).

Het gesplitste Git GRA-patroon bestaat uit twee Git-opslagplaatsen voor ontwikkeling en één Git-opslagplaats per Adobe Commerce-instantie. In de voorbeelden wordt aangenomen dat elke instantie een uniek merk vertegenwoordigt.

![ een diagram dat toont waar de code in een gesplitst patroon GRA ](/help/assets/global-reference-architecture/split-git-gra-pattern-diagram.png){align="center"} wordt opgeslagen

## Voordelen en nadelen van dit patroon

Voordelen:

- Codehergebruik via een gedeelde gegevensopslagruimte
- Eenvoudig GRA-patroon, geschikt zelfs voor teams met beperkte Composer-kennis
- Naast Adobe Commerce-modules, -thema&#39;s en taalpakketten is het mogelijk om elk type Composer-pakket te installeren via dit model, inclusief composer-plugin, composer-metapack, magento2-component en patches
- Mogelijkheid om in fasen vrij te geven, planning versies aan gebieden in hun eigen onderhoudstijden
- Ondersteuning voor Git-tags voor beheerdoeleinden, niet voor implementatiecontrole
- Garandeert dat de combinatie van pakketten in een productieimplementatie in deze exacte configuratie wordt ontwikkeld en getest

Nadelen:

- Geen extra flexibiliteit in vergelijking met andere GRA-patronen
- Niet mogelijk om individuele modules per geval te bevorderen of te degraderen, altijd verbetering of downgrade GRA als geheel
- In de meeste gevallen is het patroon van bulkpakketten beter geschikt, omdat het even eenvoudig is, maar meer conventioneel

## Adobe Commerce instellen met het patroon Git splitsen

### De mappenstructuur

Het Git-GRA-patroon splitsen heeft twee typen opslagplaatsen: ontwikkelopslagplaatsen en installatierapporten. De ontwikkelingsopslagplaatsen bevatten slechts een deel van een volledige Adobe Commerce-installatie. De installatierapportages bevatten de volledige installatie van Adobe Commerce en worden gebruikt voor plaatsing, maar niet voor ontwikkeling.

De uiteindelijke mapstructuur van een volledige Adobe Commerce-installatie met het patroon Split Git GRA ziet er als volgt uit:

```text
.
├── .gitignore
├── app/
│   └── etc/
│       └── config.php
├── composer.json
├── composer.lock
└── packages/
    ├── 3rdparty/
    ├── gra/
    └── local/
```

De mappen `app/code`, `app/i18n` en `app/design` worden met opzet weggelaten, omdat Composer de code in deze mappen niet evalueert. Dientengevolge, worden de gebiedsdelen die in de pakketten worden verklaard niet automatisch geïnstalleerd. Het Git-GRA-patroon splitsen lost dit probleem op door alle aangepaste code in `packages/` te installeren en die map als een composeropslagplaats te behandelen. Composer symboliseert pakketten binnen `packages/` naar `vendor/` .

### De Git-opslagruimten voorbereiden

3 Git-opslagruimten maken voor:

1. Een Adobe Commerce-instantie
2. Code van derden die niet via Composer is geïnstalleerd
3. Uw aanpassingen in de vorm van modules, thema&#39;s, taalpakketten en dergelijke; uw GRA

In deze handleiding worden de volgende namen gebruikt voor deze opslagplaatsen:

1. gra-split-brand-x
2. gra-split-3rdparty
3. gra-split-gra

Alle opslagruimten in het Git-GRA-patroon splitsen worden samengevoegd tot één opslagplaats. Als Git het samenvoegen van meerdere opslagplaatsen mogelijk maakt, hebben alle drie opslagruimten een gedeelde geschiedenis nodig. Maak een Git-project met één commit en duw het naar alle remotes.

```bash
mkdir gra-split-brand-x
cd gra-split-brand-x
git init
git remote add origin git@github.com:AntonEvers/gra-split-brand-x.git
git remote add 3rdparty git@github.com:AntonEvers/gra-split-3rdparty.git
git remote add gra git@github.com:AntonEvers/gra-split-gra.git
touch .gitkeep
git add .gitkeep
git commit -m 'initialize repository'
git push -u origin main
git push 3rdparty main
git push gra main
```

Als u het tijdelijke bestand `.gitkeep` op alle externe items drukt, wordt voor het eerst dezelfde commit gedaan met dezelfde commit hash, waardoor een gedeelde geschiedenis ontstaat. Elke wijziging die in één externe server wordt gemaakt, kan worden samengevoegd met de andere wijzigingen.

Van hier lopen de opslagplaatsen uiteen. De gra-split-brand-x repository bevat merkspecifieke code. De gra-split-3rdparty gegevensopslagruimte bevat alleen code van derden. De gra-split-gra dataopslag bevat alleen uw globale stichting van de verwijzingsarchitectuur, die uit al uw douanecode bestaat.

Installeer Adobe Commerce in de gra-split-brand-x repository.

```bash
composer create-project --no-install --repository-url=https://repo.magento.com/ magento/project-enterprise-edition temp
mv temp/composer.json ./
rmdir temp
git add composer.json
git commit -m 'install Adobe Commerce'
git push origin main
```

Maak eerste vastleggingen in de gra-split-3rd-party en de gra-split-gra-repositories. De gemakkelijkste manier is door deze opslagplaatsen in afzonderlijke directory&#39;s uit te checken.

```bash
cd ..
git clone git@github.com:AntonEvers/gra-split-3rdparty.git
git clone git@github.com:AntonEvers/gra-split-gra.git
cd gra-split-3rdparty
mkdir -p packages/3rdparty
touch packages/3rdparty/.gitkeep
git add packages/3rdparty/.gitkeep
git commit -m 'initialize 3rd party package storage'
git push origin main
cd ../gra-split-gra
mkdir -p packages/gra
touch packages/gra/.gitkeep
git add packages/gra/.gitkeep
git commit -m 'initialize GRA package storage'
git push origin main
```

Deze twee opslagruimten slaan pakketten van derden en GRA-pakketten op. Er kan code zijn die exclusief is voor elke instantie van Adobe Commerce. Maak een plaats om deze lokale pakketten op te slaan in de opslagplaats van gra-split-brand-x.

```bash
cd ../gra-split-brand-x
mkdir -p packages/local
touch packages/local/.gitkeep
git add packages/local/.gitkeep
git commit -m 'initialize local package storage'
git push origin main
```

### Waar moet u verschillende typen code opslaan?

Adobe Commerce is een Composer-toepassing. De beste manier om te installeren is altijd via Composer-opslagruimten. Alleen als een leverancier van modules geen installatie aanbiedt via een Composer-opslagplaats, kunt u modules van derden opslaan in de opslagruimte van derden. De voorkeurslocatie voor aangepaste code is de GRA-opslagplaats. Wanneer een module slechts door één specifieke instantie wordt gebruikt, wordt het lokale code.

Samenvatten:

- **Adobe Commerce**: opgeslagen in een bewaarplaats Composer.
- **modules van de Derde**: opgeslagen in een bewaarplaats Composer.
- **de optie van de Derde van de modules van de Derde**: opgeslagen in de opslag van de groef-spleet-3dparty Git.
- **de stichtingscode van GRA**: opgeslagen in de bewaarplaats van de groef-spleet-groef van het Git.
- **Lokale code**: opgeslagen in de opslag van de groef-spleet-brandt-x van de it.

### Pakketopslag verbinden met Composer

Composer kan de pakketmap behandelen als een composer-opslagplaats. Informeer Composer over de locatie van pakketten in de pakketmap.

```json
"repositories": [
  {"type": "path", "url": "packages/local/*/*"},
  {"type": "path", "url": "packages/gra/*/*"},
  {"type": "path", "url": "packages/3rdparty/*/*"},
  {"type": "composer", "url": "https://repo.magento.com"}
]
```

Composer zoekt naar bestanden composer.json op twee niveaus diep in de drie opslagmappen. Maak submappen binnen de drie mappen voor codeopslag, precies zoals ze in de map `vendor/` worden weergegeven.

Bijvoorbeeld: als een pakket normaal in `vendor/example-corp/module-example/` wordt geïnstalleerd, slaat u het in `packages/3rdparty/example-corp/module-example/` op. Composer symboliseert het pakket aan `vendor/example-corp/module-example/` wanneer u het nodig hebt.

Gebruik de naamruimte en naam van het componentpakket als mapstructuur. Een module die traditioneel bestaat in `app/code/MyCorp/MyCustomization/` heeft bijvoorbeeld de naam `my-corp/module-my-customization` in composer.json. Sla dit pakket op in `packages/gra/my-corp/module-my-customization` .

### Nieuwe pakketten opnemen in de instantieopslagplaatsen

De pakketten van de fusie van de derde en GRA verwijderen zich in de gra-split-brand-x bewaarplaats.

```bash
cd gra-split-brand-x
git fetch - all
git merge gra/main 3rdparty/main
git push origin main
```

Het resultaat is de volgende mappenstructuur:

```text
.
├── composer.json
└── packages/
    ├── 3rdparty/
    ├── gra/
    └── local/
```

Wijzigingen in de gegevensopslagruimte van derden en GRA-stichtingen worden samengevoegd in de bewaarplaatsen van merkartikelen. Op die manier worden de code van derden en de GRA-code slechts op één plaats gehandhaafd. Verplaats de wijzigingen naar de merken met een Git-samenvoeging.

Adobe Commerce herkent nieuwe modules niet automatisch. Composer uitvoeren vereist om een nieuw pakket toe te voegen na het samenvoegen. Werk de composer telkens bij wanneer u een van uw pakketten bijwerkt na het samenvoegen.

### Voorbeeldmodules installeren

Als bewijs van concept, installeer voorbeeldmodules om te zien hoe het patroon GRA werkt.

Voer `composer install` en `bin/magento install` uit voordat u doorgaat.

Er zijn 3 testmodules voor op GitHub:

1. [ module-voorbeeld-lokaal ](https://github.com/AntonEvers/module-example-local)
2. [ module-voorbeeld-gra ](https://github.com/AntonEvers/module-example-gra)
3. [ module-voorbeeld-3rdparty ](https://github.com/AntonEvers/module-example-3rdparty)

### Een lokale module installeren

Het toevoegen van een module aan de lokale codepool is eenvoudig. Download en extraheer de module. Vereisen met Composer. Schakel deze in met `bin/magento` en wijs de bestanden toe in de merkenopslagplaats.

```bash
cd gra-split-brand-x
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

Als u de bovenstaande uitvoer ziet, kunt u deze veilig toewijzen aan de merkopslagplaats.

```bash
git add packages/local/antonevers/module-local app/etc/config.php composer.json composer.lock 
git commit -m 'add local module'
git push origin main
```

### Een GRA-stichtingsmodule installeren en ontwikkelen

Het toevoegen van een module aan de GRA-opslagplaats verschilt van het installeren van lokale modules. Standaard worden vastleggingen toegevoegd aan de oorspronkelijke opslagplaats/hoofdopslagplaats, de opslagplaats voor gra-split-brand-x. Wijzigingen in GRA-modules moeten naar de opslagplaats voor gra-split-gra worden geduwd en daarna in de opslagplaats voor gra-split-brand-x worden samengevoegd.

### Een ontwikkelomgeving maken

Maak een ontwikkelomgeving met een combinatie van alle codepools op één locatie. U kunt code aan lokale, GRA en derdebewaarplaats door symlinks individueel duwen. Begin door een nieuwe ontwikkelingsfolder naast uw merk, GRA en derderepo folders te creëren.

```text
.
├── gra-development    # <---
├── gra-split-3rdparty
├── gra-split-brand-x
└── gra-split-gra
```

```bash
cd ..
mkdir gra-development
cd gra-development
cp ../gra-split-brand-x/composer.json ../gra-split-brand-x/composer.lock .
mkdir packages
ln -s ../../gra-split-brand-x/packages/local/ packages/
ln -s ../../gra-split-3rdparty/packages/3rdparty/ packages/
ln -s ../../gra-split-gra/packages/gra/ packages/
```

Het resultaat is de volgende mappenstructuur:

```text
.
├── packages/
│ ├── 3rdparty -> ../../gra-split-3rdparty/packages/3rdparty/
│ ├── gra -> ../../gra-split-gra/packages/gra/
│ └── local -> ../../gra-split-brand-x/packages/local/
├── composer.lock
└── composer.json
```

Voer `composer install` en `bin/magento install` uit in de map voor rasterontwikkeling.

Het is nu mogelijk om wijzigingen rechtstreeks vast te leggen vanuit de mappen `packages/3rdparty` , `packages/gra` en `package/local` . Git legt de wijzigingen vast in de Git-opslagplaats waarnaar de directory&#39;s verwijzen. Het is belangrijk dat de opdracht it commit wordt uitgegeven in de map `packages/3rdparty` , `packages/gra` of `package/local` . Voer geen git uit bij de hoofdmap van het project.

### Voorbeeldmodules installeren

Installeer de modules van de derde en van het GRA- voorbeeld in de pakketfolders.

```bash
cd packages/gra
mkdir antonevers
cd antonevers
curl -OL https://github.com/AntonEvers/module-example-gra/archive/refs/heads/main.zip
unzip main.zip
rm main.zip
mv module-example-gra-main module-gra
git add module-gra
 
cd ../../3rdparty
mkdir antonevers
cd antonevers
curl -OL https://github.com/AntonEvers/module-example-3rdparty/archive/refs/heads/main.zip
unzip main.zip
rm main.zip
mv module-example-3rdparty-main module-3rdparty
git add module-3rdparty
 
cd ../../..
composer require antonevers/module-gra:@dev antonevers/module-3rdparty:@dev
bin/magento module:enable AntonEvers_Gra AntonEvers_ThirdParty
bin/magento test:gra
bin/magento test:3rdparty
```

Dat laatste bevel in de volgende output zou moeten resulteren om te bewijzen dat de module geïnstalleerd en werkend is:

```bash
GRA module is installed successfully and working!
3rd party module is installed successfully and working!
```

Als u de bovenstaande uitvoer ziet, kunt u deze veilig toewijzen aan de merkopslagplaats. Voer `git remote -v` uit om te controleren of u zich aan de rechterafstandsbediening vastlegt.

```bash
cd packages/gra
git remote -v 
origin git@github.com:AntonEvers/gra-split-gra.git (fetch)
origin git@github.com:AntonEvers/gra-split-gra.git (push)
git add antonevers/module-gra
git commit -m 'add GRA module'
git push origin main
 
cd ../3rdparty
git remote -v 
origin git@github.com:AntonEvers/gra-split-3rdparty.git (fetch)
origin git@github.com:AntonEvers/gra-split-3rdparty.git (push)
git add antonevers/module-3rdparty
git commit -m 'add third-party module'
git push origin main
```

### Code leveren aan de instanties

Voeg de GRA- en derdeopslagruimten samen tot de gra-split-brand-x-opslagplaats om de code aan een Adobe Commerce-instantie te leveren. Voer `composer require` , `bin/magento module:enable` uit en wijs het resultaat toe.

```bash
cd gra-split-brand-x
git fetch - all
git merge gra/main 3rdparty/main
composer require antonevers/module-gra:@dev antonevers/module-3rdparty:@dev
bin/magento module:enable AntonEvers_Gra AntonEvers_ThirdParty
git add app/etc/config.php composer.lock composer.json
git commit -m 'install GRA and third-party modules'
git push origin main
```

## Vertakkingsstrategie

Dit GRA-patroon werkt met alle vertakkingsstrategieën als u de vertakkingsstrategie van de opslagruimten in uw externe opslagruimten en GRA-opslagruimten weerspiegelt. Voor versies maakt u een releasetak met dezelfde naam in alle drie opslagruimten. De releasevertakkingen samenvoegen in de opslagplaats tijdens de voorbereiding van de release.

Soms hebt u een kaarttak die zowel lokale code als derdencode of GRA code vereist om worden veranderd. In dit geval moeten de vertakkingen van de tickets in alle verwante opslagplaatsen worden gecreëerd.

Voeg nooit derden en GRA toe aan de merkenopslagplaats binnen de loketvertakkingen. In plaats daarvan, controleer de juiste takken in uw ontwikkelomgeving voor elke codepool. Het samenvoegen in de merkenbewaarplaats wordt slechts gedaan wanneer het samenstellen van de versie, of wanneer het samenstellen van een tak QA.

## Codevoorbeelden

De codevoorbeelden van dit artikel zijn beschikbaar als een reeks bewaarplaatsen van de it, die u kunt gebruiken om het bewijs van concept te testen.

- Een voorbeeld van een productiearchief: <https://github.com/AntonEvers/gra-split-brand-x>
- De gegevensopslagruimte voor code van derden: <https://github.com/AntonEvers/gra-split-3rdparty>
- De GRA-codeopslagplaats: <https://github.com/AntonEvers/gra-split-gra>
- Een lokale voorbeeldmodule: <https://github.com/AntonEvers/module-example-local>
- Een voorbeeld-GRA-module: <https://github.com/AntonEvers/module-example-gra>
- Een voorbeeldmodule van derden: <https://github.com/AntonEvers/module-example-3rdparty>

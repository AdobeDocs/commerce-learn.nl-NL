---
title: IP-adressen detecteren
description: Leer hoe u IP-adressen kunt detecteren voor Adobe Commerce Cloud-omgevingen om de beveiliging te verbeteren en servercommunicatie te stroomlijnen
feature: Cloud, Configuration
topic: Commerce, Development, Integrations
role: Developer
level: Beginner
doc-type: Technical Video
duration: 0
last-substantial-update: 2025-04-07T00:00:00Z
jira: KT-17553
exl-id: beb0a6e1-e6b1-4ec0-976c-77a22a27e8a2
source-git-commit: b015b9c64be631b43ad63d180c003dda8fdd198a
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 0%

---

# Ontdek IP adressen voor verschillende milieu&#39;s

Leer hoe u IP-adressen kunt detecteren voor verschillende omgevingen in een Adobe Commerce Cloud-project. Door een reeks bevelen met inbegrip van Adobe Commerce CLI, gebruikt, xargs, graven, grep, en soort -u te gebruiken, kunnen de gebruikers IP adressen voor ontwikkeling, het opvoeren, en productiemilieu&#39;s identificeren.

## Voor wie is deze video?

* Ontwikkelaars: kijken hoe u de IP-adressen voor het Adobe Commerce Cloud-project kunt verzamelen.
* Ontwikkelaars en beveiligingsteams die de toegang tot systemen van derden of back-endsystemen moeten beperken

## Video-inhoud {#video-content}

* Leer hoe u het IP-adres voor een willekeurige omgeving in Adobe Commerce Cloud ontdekt.

>[!VIDEO](https://video.tv.adobe.com/v/3457493/?learn=on)

## Bevel om het IP adres te krijgen

Let op: u moet uw project-id en de naam van de omgeving gebruiken in plaats van de plaatsaanduidingsgegevens.  Het kan ook nodig zijn om de `{1..3}` aan te passen aan het aantal knooppunten in uw Adobe Commerce Cloud-cluster, maar 3 komt het meest voor.

```bash
magento-cloud environment:url -p InsertYourProjectID -e UseYourEnvironmentName --pipe -1 | sed 's/.\.c\.(.)/\1/;s/.$//' | xargs -I% dig +short {1..3}."%" | grep '^\d' | sort -u
```

## Adobe Commerce Cloud CLI

```bash
magento-cloud environment:url -p InsertYourProjectID -e UseYourEnvironmentName --pipe -1
```

Het hulpprogramma magento-cloud CLI is ontworpen om ontwikkelaars en systeembeheerders te helpen Adobe Commerce Cloud-projecten en -omgevingen efficiënt te beheren. De functionaliteit van de Cloud Console wordt uitgebreid, zodat gebruikers routinetaken kunnen uitvoeren en automatisering lokaal kunnen uitvoeren. Belangrijke functies zijn het beheren van integratieomgevingen, het uitchecken en samenvoegen van omgevingen, het weergeven van variabelen en het gebruik van SSH voor het maken van verbinding met externe omgevingen. Het hulpmiddel vereenvoudigt werkschema&#39;s door bevelen toe te staan om direct van het lokale werkstation worden uitgevoerd, die het algemene ontwikkeling en plaatsingsproces verbeteren.

In deze eerste sectie van de voorbeeldcode vraagt `magento-cloud environment:url -p InsertYourProjectID -e UseYourEnvironmentName --pipe -1` de URL voor de omgeving. De geretourneerde waarde ziet er ongeveer als volgt uit `http://integration-1ajmyuq-mk7xr7zmslfg.us-4.magentosite.cloud/` . Elke keer in een tijd ziet het er meer als volgt uit `http://mcprod.russell.dummycachetest.com.c.abcikdxbg789.ent.magento.cloud/` .  Dit eerste bevel is vrij eenvoudig, en nu is het tijd om zich naar het volgende bevel te bewegen.

Voor meer informatie, gelieve te lezen [&#x200B; CLI van de Wolk Overzicht &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview){target="_blank"}

## `sed` gebruiken voor zoeken en vervangen

```bash
sed 's/.\.c\.(.)/\1/;s/.$//'
```

De opdracht `sed` in UNIX®Linux® staat voor de Stream Editor. Het wordt gebruikt om basisteksttransformaties op een inputstroom (een dossier of input van een pijpleiding) uit te voeren. Vaak wordt tekst gezocht, zoeken en vervangen, ingevoegd en verwijderd. Met de opdracht `sed` wordt tekst regel voor regel verwerkt en worden opgegeven bewerkingen toegepast, waardoor deze een krachtig gereedschap is voor tekstmanipulatie en scripts.

Zoals eerder vermeld, zijn er doorgaans 2 typen URL&#39;s die door de `magento-cloud` -clip worden geretourneerd. Er is één variatie die `.com.c.c` in het midden bevat. Deze variant moet worden gemanipuleerd. Als deze structuur wordt gedetecteerd, moet alles worden verwijderd vanaf het begin van de URL tot en met `.com.c.c` .  Dan, wat wordt verlaten is slechts het laatste deel van URL. Een voorbeeld-URL ziet er als volgt uit: `http://mcprod.russell.dummycachetest.com.c.abcikdxbg789.ent.magento.cloud/` .  Wanneer dit patroon wordt gedetecteerd, is het doel om alles na `.c.` te houden.  In deze voorbeeldcode wordt `sed 's/.\.c\.(.)/\1/'` gebruikt om dit onderdeel vast te pakken en de rest van de oorspronkelijke geretourneerde waarde te negeren. Het resterende deel van de URL lijkt op iets als `abcikdxbg789.ent.magento.cloud/` .\
Er worden twee opdrachten uitgevoerd in `sed` . Ze worden gescheiden door een puntkomma. Het tweede deel van mijn `sed` opdracht `;s/.$//'` bestaat uit het verwijderen van eventuele volgslashes om die URL op te schonen zodat deze er zo uitziet als `abcikdxbg789.ent.magento.cloud` .  Op dit punt, is URL schoongemaakt en voor het volgende bevel klaar.

## Xargs met graven

```bash
xargs -I% dig +short {1..3}."%"
```

Het `xargs` bevel in UNIX®Linux® wordt gebruikt om bevellijnen van standaardinput te bouwen en uit te voeren. Het neemt input van een pijp of een dossier en zet het in argumenten voor een ander bevel om. Het is vooral handig voor het verwerken van grote aantallen argumenten die de shell-limiet overschrijden. De opdracht `xargs` kan worden gebruikt om bewerkingen uit te voeren zoals bestanden verplaatsen, kopiëren of verwijderen. Het staat voor efficiënte partijverwerking toe door veelvoudige argumenten tot bevelen in één enkele uitvoering over te gaan.

Het bevel `dig`, kort voor de Groper van de Informatie van het Domein, is een hulpmiddel van het netwerkbeleid dat wordt gebruikt om DNS (het Systeem van de Naam van het Domein) servers te vragen. Het helpt informatie over DNS verslagen, zoals A, AAA, MX, en CNAME verslagen terugwinnen. Het bevel `dig` wordt algemeen gebruikt om DNS kwesties problemen op te lossen, DNS configuraties te verifiëren, en gedetailleerde informatie over domeinnamen en hun bijbehorende IP adressen te verzamelen. Met behulp van verschillende opties en markeringen kunnen gebruikers de uitvoer aanpassen om specifieke details of een beknopt overzicht weer te geven.

Het gebruik van `xargs` met `dig` maakt het ingewikkeld, maar is noodzakelijk. Het doel is om die schoongemaakte URL te nemen en te bewaren.  Nadat de URL als variabele is opgeslagen, wordt deze ingevoegd in de opdracht `dig` .

De opdracht `dig` is gemaakt om DNS-informatie te verzamelen. Om de hoeveelheid gegevens te verminderen die wordt geretourneerd, wordt het argument `+short` gebruikt. Wanneer u `dig` gebruikt in combinatie met `+short` , worden IP-adressen en soms tekenreeksen geretourneerd.

In dat gedeelte van de opdracht slaat `xargs` die URL op `abcikdxbg789.ent.magento.cloud` en wordt deze ingevoegd in de volgende opdracht `dig` . De techniek om de URL in combinatie met herhaling op te slaan, maakt het gemakkelijker om deze met de opdracht `dig` te gebruiken. Houd in mening dat mijn steekproefcode één manier is om het doel te verwezenlijken, voel vrij om dingen te wijzigen om aan uw behoeften en verwachtingen te voldoen.

Op dit punt is de URL gereed. Daarna, zien wij hoe het mogelijk is om elke server in de cluster te controleren. Voor Adobe Commerce Cloud heeft elke server in de cluster een getal. De server-id is een voorvoegsel van de URL die zojuist is opgeschoond en klaar voor gebruik is gemaakt. Een snelle en eenvoudige manier om de servers uit te checken is met `{1..3}` . Door `{1..3}` te gebruiken die de opdracht `dig` drie keer meldt dat deze moet worden uitgevoerd. Hier volgt een weergave van wat er gebeurt als u de uitvoering in real-time wilt bekijken.

```bash
dig +short 1.<projectid>.ent.magento.cloud
dig +short 2.<projectid>.ent.magento.cloud
dig +short 3.<projectid>.ent.magento.cloud
```

Voor betere illustratiedoeleinden lijkt dit voorbeeld-URL die door `dig` wordt gebruikt op:

```bash
dig +short 1.aabcikdxbg789.ent.magento.cloud
dig +short 2.abcikdxbg789.ent.magento.cloud
dig +short 3.abcikdxbg789.ent.magento.cloud
```

Als `{1..3}` is gewijzigd om `{1..6}` te zijn, ziet het er als volgt uit:

```bash
dig +short 1.aabcikdxbg789.ent.magento.cloud
dig +short 2.abcikdxbg789.ent.magento.cloud
dig +short 3.abcikdxbg789.ent.magento.cloud
dig +short 4.aabcikdxbg789.ent.magento.cloud
dig +short 5.abcikdxbg789.ent.magento.cloud
dig +short 6.abcikdxbg789.ent.magento.cloud
```

## De opdracht `grep`

Er zijn momenten waarop een tekenreeks wordt geretourneerd als onderdeel van het resultaat van `dig` . Voor dit doel, is het doel slechts IP adressen en zij worden samengesteld uit aantallen met periodes. Als u er zeker van wilt zijn dat de uiteindelijke uitvoer alleen getallen bevat, kunt u de opdracht aanpassen. Na voltooiing is de uiteindelijke syntaxis ` grep '^\d'` .  Door `'^\d'` toe te voegen, houdt het bevel `grep` slechts aantallen en negeert om het even wat anders.

## De opdracht `sort`

Door `sort -u` te gebruiken, verwijdert het om het even welke duplicaten uit de lijst van IPs. Duplicaten gebeuren alleen wanneer wordt gekeken naar ontwikkelingsniveaus.

Deze lagere niveaumilieu&#39;s zijn multi-huurder en delen onderliggende servers met vele andere projecten. Ontwikkelomgevingen zijn afzonderlijke servers en nooit een cluster. Daarom wanneer het gravingsbevel over elke herhaling van een lus voorziet, keert het zelfde IP vaak terug. Zo, door het bevel `sort -u` te gebruiken, worden alle dubbele IPs verwijderd en slechts blijven de unieke IP adressen.



## Verwante documentatie

* [&#x200B; Regionale IP Adressen &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/regional-ip-addresses){target="_blank"}

---
title: Enkele gangbare Commerce Cloud-fouten opsporen en corrigeren
description: Los twee algemene Adobe Cloud-projectfouten op die voorkomen dat de site wordt geladen.
feature: Cloud, Site Management
topic: Commerce, Development
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
doc-type: Technical Video
duration: 260
last-substantial-update: 2024-10-30T00:00:00Z
jira: KT-16419
exl-id: 4c21b6a6-783a-422f-9071-3534ed68e8be
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Service controleren en repareren is niet beschikbaar en er is een fout opgetreden

Leer hoe u twee veelvoorkomende fouten in Adobe Commerce Cloud-projecten kunt bijsnijden en oplossen.  Begrijp hoe en waarom deze fouten gebeuren en wat zijn de aanbevolen stappen om deze op te lossen.

## Wie is deze video voor

- Ontwikkelaars en IT-professionals
- Systeembeheerders

## Video-inhoud

- Opslagproblemen onderzoeken en oplossen:
- Onderhoudsmodus beheren
- Tips voor efficiënte probleemoplossing

>[!VIDEO](https://video.tv.adobe.com/v/3447699?captions=dut&learn=on)


## Opdrachten die in de video worden gebruikt

Vind de laatste 5 lijnen van het uitzonderingslogboek dat in het antwoordbericht wordt vermeld.

```SHELL
 tail -n 5 ~/var/log/exception.log
```

Ruimte op vaste schijf controleren. Let op de regel dev/mapper/xxxx

```SHELL
df -h
```

Hier vindt u de 15 grootste bestanden

```SHELL
find -type f -exec du -Sh {} + | sort -rh | head -n 15
```

De status van de onderhoudsmodus weergeven

```SHELL
php bin/magento maintenance:status
```

De onderhoudsmodus uitschakelen

```SHELL
php bin/magento maintenance:disable 
```

---
title: Leer hoe Toolkit pt-vraag-samenvatting van Percona werkt en waarom het wordt gebruikt
description: Analyseer MySQL vragen van langzame, algemene, en binaire logboekdossiers. Het kan vragen van &grave; SHOW PROCESSLIST' en MySQL protocolgegevens van tcpdump ook analyseren.
kt: 13846
doc-type: video
activity: use
last-substantial-update: 2023-8-28
feature: Backend Development, Tools and External Services, Logs
topic: Commerce, Development
old-role: Architect, Developer
role: Developer
level: Intermediate
exl-id: 77e91f1b-b3ae-4c6d-bb6d-4fd7ebbb0baf
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Percona Toolkit pt-query-digest

Leer waarom u de pt-vraag-samenvatting en sommige echte voorbeelden gebruikt helpen het redeneren verdiepen.

## Voor wie is deze video?

- Architecten
- Ontwikkelaars
- DevOps

## Video-inhoud

- Meer informatie over het gebruik van pt-query-digest
- Meer informatie over de voordelen en tekortkomingen van deze Percona Toolkit-functie
- Begrijp de resultaten en leer welke mogelijke prestatiesstappen zouden moeten worden overwogen

>[!VIDEO](https://video.tv.adobe.com/v/3423480?learn=on)

## Codeverwijzingen

```MYSQL
Be sure to change to match your logs and time frame

$ pt-query-digest mysql-slow.log.7 > mysql-slow.log.7.DIGEST
```

## Nuttige bronnen

- [&#x200B; Toolkit Percona &#x200B;](https://docs.percona.com/percona-toolkit/pt-query-digest.html){target="_blank"}

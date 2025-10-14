---
title: Leer hoe te om langzame vragen in mysql langzame vraaglogboeken te vinden en waarom de Galera DB replicatieontwerpmethode de reden kan zijn
description: Galera DB heeft een ontwerpmethode die de replicatie van gegevens aan secundaire gegevensbestanden langer maakt dan primaire gegevensbestanden. Leer hoe te om deze gebeurtenissen in mysql langzaam vraaglogboek te vinden, en de onderliggende reden waarom u ingangen in de langzame vraaglogboeken ziet en misschien hoe te om hen in de toekomst te verhinderen.
kt: 13635
doc-type: video
activity: use
last-substantial-update: 2023-7-18
feature: Backend Development, Logs, Services
topic: Commerce, Development
role: Architect, Developer
level: Intermediate
exl-id: 4a8a2df1-8cac-4bd9-851f-0eaae011b76c
source-git-commit: 598bff1fd2cefdc449d5ae3431401aec1e796313
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Meer informatie over Galera DB-replicatie en verwante MySQL-trage query&#39;s

Galera-clusters helpen met prestaties en schaalbaarheid. Wanneer het overwegen van secundaire gegevensbestanden, is het belangrijk om te begrijpen hoe de gegevensreplicatie gebeurt verschillend is dan op primair. De primaire database kan bulkbewerkingen uitvoeren. Wanneer de replicatie voor alle secundaire gegevensbestanden gebeurt, doen zij acties één tegelijk. Bijvoorbeeld, als u 67.000.000 punten in schrapping hebt, op de secundaire gegevensbestanden elk één voor één gebeurt. Wanneer het herzien van de langzame vraaglogboeken van Mysql, vindt u deze actie kan lange tijd vergen. Omdat de secundaire gegevensbestanden dingen één voor één uitvoeren, is een reden voor dingen om niet synchroon te zijn en de prestatiesgevolgen kunnen worden ontdekt.

Als oplossing, indien mogelijk, batch uw grote verrichtingen om de secundaire gegevensbestanden te helpen synchroon houden met primaire. Door dingen in partij te doen, staat het toe dat de acties op een geschikte manier worden uitgevoerd en de prestatiesgevolgen tot een minimum worden beperkt.

## Voor wie is deze video?

- Architecten
- Ontwikkelaars
- DevOps

## Video-inhoud

- Galera-replicatie naar secundaire database
- Meer informatie over stroombeheer
- Het vinden van draadaantallen in mysql langzame vraaglogboeken
- Bulkexecuties vinden alleen plaats op de eerste plaats. Replicaties vinden één voor één plaats
- Batch uw grote inzet om de replicatie te helpen gelijke tred houden met de primaire

>[!VIDEO](https://video.tv.adobe.com/v/3432453?learn=on&captions=dut)

## Nuttige bronnen

- [&#x200B; Cluster Galera &#x200B;](https://galeracluster.com/)

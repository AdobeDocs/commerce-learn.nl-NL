---
title: Admin URI opnieuw instellen met CLI
description: Leer hoe u de beheer-URI opnieuw instelt in Adobe Commerce Cloud CLI. Deze methode is handig wanneer wijzigingen in admin-URL toegangsproblemen veroorzaken.
feature: Admin Workspace, Console
topic: Administration, Commerce
role: Developer, User
level: Beginner
doc-type: Technical Video
duration: 123
last-substantial-update: 2024-10-14T00:00:00Z
jira: KT-16338
exl-id: dbc155d7-8ce9-4622-abfb-1d8077c3a975
source-git-commit: 25ee35b730cc6265665a87c9c37d24e88c41b60e
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# De URI van de beheerder opnieuw instellen met behulp van cli

Leer hoe u de URI van de beheerder opnieuw instelt met de opdracht Adobe Commerce Cloud cli. Dit is handig als de admin-URL is gewijzigd ten opzichte van de beheerder, maar er een fout is gemaakt en u geen toegang meer hebt tot de admin.

>[!VIDEO](https://video.tv.adobe.com/v/3435066/?learn=on)

## Enkele opdrachten die in de zelfstudie worden gebruikt

Wijzig de configuratie zodat een aangepaste Admin-pad-URL naar 0 wordt verwacht:

`$ php bin/magento config:set admin/url/use_custom 0`

Wijzig de configuratie voor de aangepaste Admin-pad-URL in 0

`$ php bin/magento config:set admin/url/use_custom_path 0`

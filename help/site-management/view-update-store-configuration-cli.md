---
title: Leer hoe u beheerconfiguraties kunt weergeven en instellen met behulp van de opdrachtregel
description: Een demo voor om configuratiewaarden te bekijken en te plaatsen gebruikend de bevellijn
feature: Configuration,Console,System
topic: Administration,Commerce
role: Developer
level: Beginner
doc-type: Technical Video
duration: 462
last-substantial-update: 2024-01-31T00:00:00Z
jira: KT-14877
thumbnail: KT-14877.jpeg
source-git-commit: 9d4b01d383e5492ccc0cbd27636a49581e8ffb5b
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# Leer hoe te om admin configuraties te bekijken en te plaatsen gebruikend de bevellijn

Een demonstratie voor hoe te om, config waarden met de Handel CLI te bekijken te plaatsen en te vinden. Begrijp waar de waarden worden opgeslagen en ook waar de standaardwaarden vandaan komen.

## Voor wie is deze video?

- Adobe Commerce-ontwikkelaars

## Video-inhoud

>[!VIDEO](https://video.tv.adobe.com/v/3427123?&learn=on)

## Enkele opdrachten die in de zelfstudie worden gebruikt

Wijzig de beveiligingsinstelling voor het wachtwoord in aanbevolen:

`$ php bin/magento config:set admin/security/password_is_forced 0`

Het e-mailadres voor de functie voor automatisch kopiëren van de verkooporder weergeven

`$ php bin/magento config:show sales_email/order/copy_to`

Leeg resultaat weergeven voor een configuratie met een waarde in de beheerder

`php bin/magento config:show trans_email/ident_sales/email`

## In de zelfstudie gebruikte mysql-query&#39;s

```
SELECT * FROM core_config_data WHERE path = 'sales_email/order/copy_to';

SELECT * FROM core_config_data WHERE path = 'sales_email/order_comment/copy_to';

SELECT * FROM core_config_data WHERE path = 'trans_email/ident_sales/email';
```

## Locatie voor de standaard e-mail met verkopen

Hoe te om de configuratiewaarde te vinden die ergens in codebase wordt bepaald?
`grep -rnw vendor/magento/ -e 'sales@example.com'`

Een pagina in terminal weergeven en regelnummers weergeven `cat -n vendor/magento/module-email/etc/config.xml`

## Aanvullende bronnen

- [Opdrachtregel](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/config-cli.html){target="_blank"}
- [Beveiliging van beheerder configureren](https://experienceleague.adobe.com/docs/commerce-admin/systems/security/security-admin.html){target="_blank"}

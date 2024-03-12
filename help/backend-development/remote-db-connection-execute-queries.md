---
title: Verbinding maken en query's uitvoeren met de database
description: Leer verschillende methoden om verbinding te maken met een Adobe Commerce-cloud-project. Leer hoe u een tab weghaalt om offline te gebruiken. Leer enkele methoden om PII te maskeren en te verwijderen.
feature: Backend Development,Console,Cloud
topic: Commerce,Development
role: Developer
level: Intermediate, Experienced
doc-type: Technical Video
duration: 0
last-substantial-update: 2024-02-14T00:00:00Z
jira: KT-14910
thumbnail: KT-14910.jpeg
exl-id: e740bbd0-5ec7-4272-89cb-0bed776eb149
source-git-commit: a951f61ff71ad3777f8aebfa3c237b2ec1a4b1a5
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 0%

---

# Verbinding maken en query&#39;s uitvoeren met de Adobe Commerce-database

In deze zelfstudie leert u hoe u verbinding kunt maken met een Adobe Commerce-project in de cloud, een database kunt dumpen voor gebruik buiten de site en PII kunt maskeren en verwijderen.

U kunt Adobe Commerce-gegevens vanuit uw cloudproject op een van de volgende manieren benaderen:

* Een lokale DB-dump gebruiken
* Een DB-verbinding met uw externe cloud-omgeving met een toepassing zoals Mysql Workbench of Tables Plus
* Rechtstreeks verbinding maken met de cloud-omgeving met het hulpprogramma magento-cloud CLI en opdrachten uitvoeren op de externe server

De aangewezen methode moet een gegevensbestandstortplaats doen en het scrubben om het even welke klanteninformatie te verwijderen. Verwijder de klantgegevens volledig als de gegevens niet nodig zijn.

## Het Adobe Commerce Cloud CLI-gereedschap gebruiken

Voor het maken van een databasedumpel hebt u de [ADOBE COMMERCE CLOUD CLI](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli/cloud-cli-overview.html) geïnstalleerd. Ga op uw lokale laptop naar een directory en voer de volgende opdracht uit. Zorg ervoor dat u `your-project-id` met de project-id, vergelijkbaar met `asasdasd45q`. U moet ook vervangen `your-environment-name` met de naam van uw omgeving, zoals `master` of `staging`.

`magento-cloud db:dump -p your-project-id -e your-environment-name`

Als u niet zeker van projectidentiteitskaart of het milieu bent, kunt u deze in het bevel weglaten:

`magento-cloud db:dump`

CLI vraagt u om het correcte project en het milieu te specificeren. In het volgende voorbeeld wordt dat dialoogvenster weergegeven. In dit voorbeeld ziet u verschillende projecten die aan uw account zijn toegewezen, maar u hebt waarschijnlijk slechts één project beschikbaar.

Wijzigen in een map

```bash
cd ~/Downloads/db-tutorial 
```

Voer nu het bevel uit om de gegevensbestandstortplaats te creëren

```bash
magento-cloud db:dump
```

Omdat wij geen project of milieu specificeerden, zal CLI van Adobe Commerce een paar vragen stellen, hier is één of andere voorbeelddialoog

```bash
Enter a number to choose a project:
  [0] demo-ralbin (ral32nryq4123)
  [1] adobe-commerce-demo (abc123zzkipexnqo)
  [2] DX Tutorials - Commerce (abasrpikfw4123)
 > 2

Enter a number to choose an environment:
Default: master
  [0] master (type: production)
  [1] remote-db (type: development)
 > 1

Creating SQL dump file: /Users/<username>/Downloads/db-tutorial/abasrpikfw4123--remote-db-ecpefky--mysql--main--dump.sql
```

## De Adobe Commerce ECE-gereedschappen gebruiken

Als u het Adobe Commerce CLI-gereedschap niet hebt, kunt u `ssh` in uw project en voer de `ece` command `vendor/bin/ece-tools db-dump`: Monsterreactie:

```bash
ssh abasrpikfw4123-remote-db-ecpefky--mymagento@ssh.us-4.magento.cloud

 __  __                   _          ___ _             _ 
|  \/  |__ _ __ _ ___ _ _| |_ ___   / __| |___ _  _ __| |
| |\/| / _` / _` / -_) ' \  _/ _ \ | (__| / _ \ || / _` |
|_|  |_\__,_\__, \___|_||_\__\___/  \___|_\___/\_,_\__,_|
            |___/                                        

 Welcome to Magento Cloud.

 This is environment remote-db-ecpefky
 of project abasrpikfw4123.

web@mymagento.0:~$ vendor/bin/ece-tools db-dump
The db-dump operation switches the site to maintenance mode, stops all active cron jobs and consumer queue processes, and disables cron jobs before starting the dump process.
Your site will not receive any traffic until the operation completes.
Do you wish to proceed with this process? (y/N)?y
[2024-02-13T19:01:45.130999+00:00] INFO: Starting backup.
[2024-02-13T19:01:45.155039+00:00] NOTICE: Enabling Maintenance mode
[2024-02-13T19:01:46.404427+00:00] INFO: Trying to kill running cron jobs and consumers processes
[2024-02-13T19:01:46.420149+00:00] INFO: Running Magento cron and consumers processes were not found.
[2024-02-13T19:01:46.420434+00:00] INFO: Waiting for lock on db dump.
[2024-02-13T19:01:46.420499+00:00] INFO: Start creation DB dump for main database...
[2024-02-13T19:01:50.697886+00:00] INFO: Finished DB dump for main database, it can be found here: /app/var/dump-main-1707850906.sql.gz
[2024-02-13T19:01:51.628328+00:00] NOTICE: Maintenance mode is disabled.
[2024-02-13T19:01:51.628419+00:00] INFO: Backup completed.
web@mymagento.0:~$ exit
logout
Connection to ssh.us-4.magento.cloud closed.
```

Gebruiken `SFTP` of `rsync` om de gegevensbestandstortplaats aan uw lokale milieu te trekken.

In het volgende voorbeeld wordt `rsync` om het bestand aan de `~/Downloads/db-tutorial` map.

```bash
rsync -avrp -e ssh abasrpikfw4123-remote-db-ecpefky--mymagento@ssh.us-4.magento.cloud:/app/var/dump-main-1707850906.sql.gz ~/Downloads/db-tutorial
```

Het eindvenster zal sommige informatie uitvoeren, hier is één of andere voorbeeldoutput

```bash
rsync -avrp -e ssh abasrpikfw4123-remote-db-ecpefky--mymagento@ssh.us-4.magento.cloud:/app/var/dump-main-1707850906.sql.gz ~/Downloads/db-tutorial
receiving file list ... done
dump-main-1707850906.sql.gz

sent 38 bytes  received 2691041 bytes  358810.53 bytes/sec
total size is 2690241  speedup is 1.00
```

Bekijk de inhoud van het bestand om te controleren of het bestand is gedownload.

```bash
ls -lah
total 29840
drwxr-xr-x    4 <ussername>  staff   128B Feb 13 13:02 .
drwx------@ 103 <ussername>   staff   3.2K Feb 13 12:52 ..
-rw-r--r--    1 <ussername>   staff    11M Feb 13 12:53 abasrpikfw4123--remote-db-ecpefky--mysql--main--dump.sql
-rw-r--r--    1 <ussername>   staff   2.6M Feb 13 13:01 dump-main-1707850906.sql.gz
```

Zodra u de gegevens hebt, moet u deze opschonen door de gegevens van de klant te verwijderen of te maskeren. Het volgende voorbeeldscript helpt u aan de slag te gaan.

In dit voorbeeld worden klantgegevens omgezet in willekeurige tekenreeksen, maar blijven alle items behouden. Dit voorbeeld bevat een paar extra lijsten om aan te tonen dat klant PII in derdetabellen evenals kernlijsten kan worden gevonden. Controleer zorgvuldig gegevens in elke tabel en maskeer of verwijder klantgegevens.

Doorgaans is de architect of de lead developer de enige die verantwoordelijk is voor het maskeren en ontsmetten van databasedumps. Een speciale ontsmettingsfunctie vermindert de blootstelling van de onbewerkte gegevens, waardoor de kans op overtreding van de regels en voorschriften wordt verkleind.

```sql
SET FOREIGN_KEY_CHECKS=0;
UPDATE customer_entity SET email = REPLACE(email, SUBSTRING(email, LOCATE('@', email) +1), CONCAT(UUID(), '.com'));
UPDATE email_contact SET email = REPLACE(email, SUBSTRING(email, LOCATE('@', email) +1), CONCAT(UUID(), '.com'));
UPDATE sales_invoice_grid SET customer_email = 'customer@example.com', customer_name  = 'Jack Smith';
UPDATE sales_order SET customer_email = 'customer@example.com', customer_firstname = 'Sally', customer_lastname = 'Smith', remote_ip = '127.0.0.1';
UPDATE sales_order_address SET region = 'Ohio', postcode = '12345-1234', lastname = 'Smith', street = '123 Main street', region_id = 44, city = 'Phoenix', telephone = NULL, firstname = 'Jane', company = NULL;
UPDATE sales_order_grid SET customer_email = 'customer@example.com', shipping_name = 'Jack', billing_name = 'Jack Smith', billing_address = '123 Main Street', shipping_address = '321 Pine Street', customer_name = 'Jane Smith';
UPDATE sales_shipment_grid SET customer_email = 'customer@example.com', customer_name = 'Jane Smith', billing_address = '123 Main street', billing_name = 'Jack Doe', shipping_name = 'Susie Smith';
UPDATE quote SET customer_email = 'customer@example.com', customer_firstname = 'Sally', customer_lastname = 'Jones', customer_dob = NULL, remote_ip = '127.0.0.1';
UPDATE quote_address SET email = 'customer@example.com', firstname = 'Jack', lastname = 'Smith', company = NULL, street = '123 Main st', city = 'AnyCity', region = 'Some State', region_id = 44, postcode = '12345-1234', telephone = NULL;
UPDATE magento_rma SET customer_custom_email = 'customer@example.com' WHERE customer_custom_email IS NOT NULL;
UPDATE customer_address_entity SET firstname = 'Jack', lastname = 'Smith', telephone = '909-555-1212', postcode = NULL,  region = NULL, street = '123 Main street', city = 'Anycity', company = NULL;
UPDATE customer_grid_flat SET name = 'Jane Doe', email = 'customer@example.com', dob = NULL, gender = NULL, taxvat = NULL, shipping_full = '', billing_full = '', billing_firstname = 'Jack', billing_lastname = 'Smith', billing_telephone = NULL, billing_postcode = NULL, billing_country_id = NULL, billing_region = NULL, billing_street = '123 Main street', billing_city = 'Anycity', billing_fax = NULL, billing_vat_id = NULL, billing_company = NULL;
UPDATE sales_creditmemo_grid SET billing_name = 'Sally', billing_address = '123 Main Street', customer_name = 'Jack Smith', customer_email = 'customer@example.com';
UPDATE magento_rma_grid SET customer_name = 'Jack Smith';
UPDATE newsletter_subscriber SET subscriber_email = 'customer@example.com';
UPDATE core_config_data SET value = '' WHERE path = 'orderexport/general/serial';
UPDATE core_config_data SET value = '' WHERE path = 'productexport/general/serial';
UPDATE core_config_data SET value = '' WHERE path = 'trackingimport/general/serial';
UPDATE core_config_data SET value = '' WHERE path = 'stockimport/general/serial';
UPDATE core_config_data SET value = '' WHERE path = 'remarketing/onescript/merchant_id';
UPDATE core_config_data SET value = '' WHERE path = 'remarketing/onescript/merchant_id';
UPDATE core_config_data SET value = '' WHERE path = 'algoliasearch_credentials/credentials/application_id';
UPDATE core_config_data SET value = '' WHERE path = 'algoliasearch_credentials/credentials/search_only_api_key';
UPDATE core_config_data SET value = '' WHERE path = 'tax/avatax/production_account_number';
UPDATE core_config_data SET value = '' WHERE path = 'tax/avatax/production_license_key';
UPDATE core_config_data SET value = '' WHERE path = 'design/head/includes';
UPDATE core_config_data SET value = '' WHERE path = 'payment/braintree/merchant_id';
UPDATE core_config_data SET value = '' WHERE path = 'payment/braintree/public_key';     
UPDATE core_config_data SET value = '' WHERE path = 'payment/braintree/private_key';
UPDATE core_config_data SET value = '' WHERE path = 'system/full_page_cache/fastly/fastly_service_id';
UPDATE core_config_data SET value = '' WHERE path = 'system/full_page_cache/fastly/fastly_api_key';
UPDATE core_config_data SET value = '' WHERE path = 'google/analytics/container_id';  
UPDATE core_config_data SET value = '' WHERE path = 'analytics/general/token';
UPDATE vault_payment_token SET public_hash = UUID(), details = '{"type":"VI","maskedCC":"1111","expirationDate":"01\/2019"}';
TRUNCATE customer_log; 
TRUNCATE customer_visitor; 
TRUNCATE magento_logging_event;
TRUNCATE oauth_consumer;
TRUNCATE oauth_nonce;
TRUNCATE oauth_token;
TRUNCATE password_reset_request_event;
TRUNCATE acknowledgement;
TRUNCATE acknowledgement_report;
TRUNCATE avatax_log;
TRUNCATE avatax_queue;
TRUNCATE cron_schedule;
SET FOREIGN_KEY_CHECKS=1;
```

U kunt ook de records verwijderen in plaats van de gegevens te maskeren, waardoor ook de nieuwe DB kleiner wordt. Zodra PII wordt gemaskeerd of verwijderd, kunnen de gegevens veilig aan teamgenoot voor gebruik op hun lokale milieu worden verstrekt.

## Externe DB-verbinding met een Adobe Commerce Cloud-project

Met deze methode kunnen echte gegevens per ongeluk worden bewerkt en verwijderd. Deze aanpak moet met voorzichtigheid worden toegepast. Het gebruik van een databaseback-up en het offline evalueren van de gegevens is de voorkeursaanpak. Er zijn momenten dat er behoefte is aan rechtstreekse toegang tot de gegevens op de Adobe Commerce Cloud, maar dat brengt wel risico&#39;s met zich mee. Er is geen &quot;ben je zeker?&quot; gestelde vragen, zodat het mogelijk is om gegevens onbedoeld te veranderen of te verwijderen.

Super belangrijk! Een externe DB-verbinding maken is handig en met behulp van live-gegevens, maar brengt risico&#39;s met zich mee. Persoonlijk en als Opdrachtgever Technisch Architect voor Adobe Commerce adviseer ik dit niet. Het is te gemakkelijk om te vergeten u op verre OB bent en gegevens per ongeluk schrapt of wijzigt. Er is een optie om verbinding te maken met de alleen-lezen replica, maar die enige invloed heeft op de site, afhankelijk van hoe zwaar de SQL-activiteiten zijn. Aangezien het echter mogelijk is, zijn dit de stappen om het te verwezenlijken.

Een SSH-tunnel tot stand brengen:

```bash
magento-cloud tunnel:open
```

Nadat het project wordt gekozen en het milieu wordt gekozen, is er output van het bevel dat in de montages voor de mysql grafische interface wordt gebruikt.

```bash
magento-cloud tunnel:open

Enter a number to choose a project:
  [0] demo-ralbin (ral32nryq4123)
  [1] adobe-commerce-demo (abc123zzkipexnqo)
  [2] DX Tutorials - Commerce (abasrpikfw4123)
 > 2

Enter a number to choose an environment:
Default: master
  [0] master (type: production)
  [1] remote-db (type: development)
 > 1

SSH tunnel opened to database at: mysql://user:@127.0.0.1:30000/main
SSH tunnel opened to redis at: redis://127.0.0.1:30001
SSH tunnel opened to opensearch at: http://127.0.0.1:30002
SSH tunnel opened to rabbitmq at: amqp://guest:guest@127.0.0.1:30003

Logs are written to: /Users/<user>/.magento-cloud/tunnels.log

List tunnels with: magento-cloud tunnels
View tunnel details with: magento-cloud tunnel:info
Close tunnels with: magento-cloud tunnel:close

Save encoded tunnel details to the MAGENTO_CLOUD_RELATIONSHIPS variable using:
  export MAGENTO_CLOUD_RELATIONSHIPS="$(magento-cloud tunnel:info --encode)"
```

Vestig een verbinding gebruikend een grafische interface MySQL door te gebruiken `SSH tunnel opened to database at` gebruiken.

```bash
SSH tunnel opened to database at: mysql://user:@127.0.0.1:30000/main
```

Nu u de juiste informatie hebt, kunt u deze waarden blijven invoegen in de Cloud Console.

U vindt de hostnaam en gebruikersnaam van SSH via de aanmeldingsgegevens voor de cloud in de Cloud Console.

![logo - Adobe Commerce Cloud Console](./assets/cloud-ui-screenshot.png "Adobe Commerce Cloud Console")

Hier volgt een voorbeeld: `ssh abasrpikfw4123-remote-db-ecpefky--mymagento@ssh.us-4.magento.cloud`
De SSH hostname is alles na @ teken: `ssh.us-4.magento.cloud` in dit voorbeeld.
De gebruikersnaam SSH is alles vóór het @-teken:  `abasrpikfw4123-remote-db-ecpefky—mymagento`

## Waarden zoeken voor verbinding met de database

Als u rechtstreeks toegang wilt krijgen tot de MariaDB-database, moet u SSH gebruiken om u aan te melden bij de externe cloud-omgeving en verbinding te maken met de database.

1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Haal de MySQL aanmeldingsgegevens op van het `database` en `type` eigenschappen in de [$MAGENTO_CLOUD_RELATIONSHIPS](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/properties/properties.html?lang=en#relationships) variabele.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   of

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   In de reactie, vind de informatie MySQL. Bijvoorbeeld:

   ```json
   "database" : [
      {
         "password" : "",
         "rel" : "mysql",
         "hostname" : "nnnnnnnn.mysql.service._.magentosite.cloud",
         "service" : "mysql",
         "host" : "database.internal",
         "ip" : "###.###.###.###",
         "port" : 3306,
         "path" : "main",
         "cluster" : "projectid-integration-id",
         "query" : {
            "is_master" : true
         },
         "type" : "mysql:10.3",
         "username" : "user",
         "scheme" : "mysql"
      }
   ],
   ```

Dan gebruik de configuratiewaarden in uw MySQL GUI. In het volgende voorbeeld wordt MySQL Workbench gebruikt, maar elke toepassing die MySQL-verbindingen ondersteunt, heeft vergelijkbare velden.

![logo - Mysql GUI-voorbeeld met Mysql Workbench](./assets/mysql-workbench-after-connecting.png " Mysql GUI-voorbeeld met Mysql Workbench")

![logo - Mysql GUI-voorbeeld met TablesPlus](./assets/tablesPlus-db-connection.png " Mysql GUI-voorbeeld met TablesPlus")

Nadat alles opstelling is, is het mogelijk om MySQL GUI te gebruiken om vragen op een ver project van Adobe Commerce Cloud in werking te stellen.

## Direct verbinding maken met de database van het cloudproject om SQL uit te voeren

De volgende methode gebruikt de `magento-cloud` om rechtstreeks verbinding te maken met de mysql-database en SQL uit te voeren, waardoor database sneller kan worden opgezocht. Als u deze database moet kopiëren, raadpleegt u een van de alternatieve methoden om [een databasedumpdump maken](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud.html).

```bash
magento-cloud db:sql    

Enter a number to choose a project:
  [0] demo-ralbin (ral32nryq4123)
  [1] adobe-commerce-demo (abc123zzkipexnqo)
  [2] DX Tutorials - Commerce (abasrpikfw4123)
 > 2

Enter a number to choose an environment:
Default: master
  [0] master (type: production)
  [1] remote-db (type: development)
 > 1

Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 273454
Server version: 10.6.15-MariaDB-1:10.6.15+maria~deb10-log mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

U kunt bijvoorbeeld alle records zoeken in het dialoogvenster `core_config_data` tabel die het woord bevat `secure` als onderdeel van de kolom `path`:

```sql
MariaDB [main]> SELECT * FROM core_config_data WHERE path LIKE '%secure%' \G;
*************************** 1. row ***************************
 config_id: 5
     scope: default
  scope_id: 0
      path: web/unsecure/base_url
     value: http://remote-db-ecpefky-abasrpikfw4123.us-4.magentosite.cloud/
updated_at: 2024-02-02 18:03:17
*************************** 2. row ***************************
 config_id: 6
     scope: default
  scope_id: 0
      path: web/secure/base_url
     value: https://remote-db-ecpefky-abasrpikfw4123.us-4.magentosite.cloud/
updated_at: 2024-02-02 18:03:17
*************************** 3. row ***************************
 config_id: 8
     scope: default
  scope_id: 0
      path: web/secure/use_in_adminhtml
     value: 1
updated_at: 2023-04-26 19:43:58
3 rows in set (0.001 sec)

ERROR: No query specified

MariaDB [main]> 
```

## Aanvullende bronnen

[ADOBE COMMERCE CLOUD CLI](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli/cloud-cli-overview.html)
[MySQL-service instellen](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/mysql.html)
[Een externe MySQL-databaseverbinding instellen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/database-server/mysql-remote.html)
[Database-dump maken op Adobe Commerce op cloudinfrastructuur](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud.html)

---
title: Checklist Adobe Commerce Cloud voorafgaand aan de introductie
description: Meer informatie over de checklist Adobe Commerce Cloud voor het starten.
feature: Cloud
topic: Commerce, Architecture, Development
role: Architect, Developer
level: Intermediate
doc-type: Tutorial
duration: 0
last-substantial-update: 2024-04-17T00:00:00Z
jira: KT-15180
kt: 15180
exl-id: c6adb2c2-f194-4a3d-9290-e0837ef062ae
source-git-commit: 00a8d6883473de796abc79ef2e9be34f56429a17
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 0%

---

# Controlelijst vóór starten Commerce Cloud

Het volgende is een synopsis van de Adobe Commerce [Site-startdocumentatie](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/overview){target="_blank"}.

Deze controlelijst is bedoeld als hulp bij het plannen en uitvoeren van een geslaagde start van de Adobe Commerce Cloud-site. Werk samen met uw systeemintegrator voor Adobe Commerce Cloud om ervoor te zorgen dat alle configuratietaken en controlelijstitems worden voltooid en geverifieerd. Als u problemen ondervindt met checklist-items of vragen hebt, neemt u contact op met de aangewezen technisch adviseur van de klant of met de succesvolle technicus van de klant. Als uw rekening geen toegewezen CTA/CSE heeft, kunt u een steunkaartje voor hulp tot stand brengen.

Als u een CTA/CSE aan de rekening toegewezen hebt, contacteer hen en de Manager van de Rekening minstens 4 weken voorafgaand aan het lanceren van de nieuwe plaats van Adobe Commerce Cloud om hen van uw op de hoogte te brengen **intentie** om te starten.

- Sommige controles zijn gemarkeerd met [!BADGE Blocker]{type=caution tooltip="Potentiële blokkering"}
- Zorg ervoor dat u met uw ontwikkelaar- of systeemintegratiepartner samenwerkt om deze uit te lijnen met uw implementatiebenadering.

>[!IMPORTANT]
> U accepteert [verantwoordelijkheid](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility){target="_blank"} voor eventuele negatieve effecten en bijbehorende risico&#39;s voor het startprogramma voor de productie en de aanhoudende stabiliteit van de site, als u deze checklist niet gebruikt en aanvult.

## 1. Pre-Go Live

1. Documentatie over testen en live gaan [Site-startdocumentatie](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/overview){target="_blank"}

   >[!NOTE]
   >Zorgen voor _&quot;kies voor een live-klaar plan&quot;_ volledig is voorbereid met uw partner of systeemintegrator, die alle noodzakelijke actiepunten omvat. Onthoud dat in de checklist voorafgaand aan de introductie de beste praktijken van de Adobe worden benadrukt, maar dat _**niet**_ vervang de behoefte aan uw eigen go-live klaar plan.

2. [!BADGE Blocker]{type=caution tooltip="Potentiële blokkering"}[Handboek](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/intro){target="_blank"})
3. Eindgebruiker/handelaar voerde UAT (het Testen van de Erkenning van de Gebruiker), met inbegrip van backendverrichtingen uit.
4. Het team van de systeemintegrator heeft UAT van begin tot eind op het opvoeren en de productie uitgevoerd. Zie de [Documentatie Experience League](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/staging-and-production){target="_blank"}.
5. Implementatie en testen van code bevestigen in testomgevingen en productieomgevingen ([Meer informatie](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/staging-and-production){target="_blank"}).
6. De productiecluster is permanent vergroot tot de contractueel vastgelegde dagelijkse basislijn. Spreek aan toegewezen CTA/CSE voor meer details, of breng een steunkaartje op.

## 2. Huidige configuraties

1. Upgrade uitvoeren van Adobe Commerce en verwante pakketten/services naar de [nieuwste versie](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview){target="_blank"}
2. Herzie de huidige configuraties en de diensten met uw SI/Partner, en [de beste praktijken volgen](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/catalog-management){target="_blank"}.
3. Controleer MySQL/Shared-Files [schijfgebruik](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space){target="_blank"}

## 3. Snelle configuraties

1. [!BADGE Blocker]{type=caution tooltip="Potentiële blokkering"}[Cache van volledige pagina](https://developer.adobe.com/commerce/frontend-core/guide/caching/){target="_blank"} of [GraphQL caching](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/){target="_blank"}). Lees de [Gids snel instellen](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly){target="_blank"}.
2. Gebruik, indien van toepassing, de methode GET voor GraphQL-query&#39;s op PWA/Headless-websites.

   >[!NOTE]
   > Alleen de query&#39;s die met een HTTP-GET worden verzonden, kunnen in de cache worden geplaatst (indien van toepassing). [POST query&#39;s kunnen niet in cache worden geplaatst](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/){target="_blank"}.

3. Zorg ervoor dat Fastly Image Optimization is ingeschakeld ([Zie Snelle optimalisatie van afbeeldingen](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly-image-optimization){target="_blank"})
4. Controleer of de juiste schermlocatie is geconfigureerd ([Cachegeheugen, achtergronden en oorsprongsbeveiliging configureren](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration){target="_blank"}).
5. Webtoepassingsfirewall (**WAF**) werkt. (Zie [Problemen met geblokkeerde aanvragen oplossen](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly-waf-service){target="_blank"}, indien van toepassing, en beperkingen)
6. De sneltoets bijwerken [&quot;Genegeerde URL-parameters&quot;](https://github.com/iancassidyweb/magento2/commit/68fdecfcd26c957382b8d68b64887e0a83298524){target="_blank"} in het deelvenster Beheer om de prestaties van de cache te verbeteren.

   >[!NOTE]
   > In de snelconfiguratie onder _Beheer > Opslag > Configuraties > Systeem > Volledige paginacache > Snelle configuratie > Geavanceerde configuratie > Genegeerde URL-parameters (wereldwijd)_ kunt u een lijst met door komma&#39;s gescheiden parameters vinden die u bij het zoeken naar pagina&#39;s in de cache snel moet negeren. Zorg ervoor dat u de VCL opnieuw uploadt nadat u deze lijst hebt gewijzigd

## 4. DNS en SSL

1. [!BADGE Blocker]{type=caution tooltip="Potentiële blokkering"}_(Een ondersteuningsticket vooraf verzenden voor toegevoegde of gewijzigde domeinen)_
2. [!BADGE Blocker]{type=caution tooltip="Potentiële blokkering"}[dit artikel](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/ssl-tls-certificates-for-magento-commerce-cloud-faq){target="_blank"} voor meer informatie .
3. DNS bijwerken [TTL (Tijd om te leven)](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist#to-update-dns-configuration-for-site-launch){target="_blank"} waarde tot het minimum dat mogelijk is, voor onderweg.
4. Sendgrid SPF en DKIM inschakelen

   >[!NOTE]
   > Voeg de verslagen SendGrid CNAME voor elk domein aan de DNS configuratie toe. Lezen [E-mailservice SendGrid](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/sendgrid){target="_blank"} om te zien hoe u de afzenderdomeinen en meer wijzigt.

## 5. Databaseconfiguraties

Adobe Commerce Cloud gebruikt een MariaDB Galera-cluster als database voor zowel de testomgeving als de productieomgeving. Galera-clusters zijn van essentieel belang voor het verbeteren van prestaties en schaalbaarheid. Raadpleeg de volgende artikelen voor meer informatie over de optimale werkwijzen en beperkingen van Galera-clusterreplicaties.

- [Best practices voor MySQL-configuraties](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration){target="_blank"}
- Beheerde waarschuwingen op Adobe Commerce: [MariaDB-waarschuwingen](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-mariadb-alerts){target="_blank"}
- Aanbevolen procedures voor [databaseconfiguratie](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud){target="_blank"}
- Diepe analyse naar [Clusterreplicaties en stroombeheer in Galera.](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/backend-development/galera-db-slow-replication){target="_blank"}

1. [MYSQL Slave-verbinding](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration#slave-connections){target="_blank"} wordt aanbevolen voor betere prestaties bij het laden van een hoge database.
2. Zorg ervoor dat de rijindeling voor alle databasetabellen is ingesteld op [DYNAMISCH in plaats van COMPACT](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/maintenance/mariadb-upgrade#convert-database-table-storage-format){target="_blank"} (Dit geldt met name voor migratie van on-prem naar cloud.)
3. De database-opslagengine wijzigen vanuit [MyISAM naar InnoDB](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud#convert-all-myisam-tables-to-innodb){target="_blank"} voor alle tabellen.
4. Beoordeel en optimaliseer databasetabellen van meer dan 1 GB van tevoren.
5. De gegevens over het databaseschema zijn actueel en bijgewerkt. (Zie [deze handleiding](https://mariadb.com/kb/en/engine-independent-table-statistics/#collecting-statistics-with-the-analyze-table-statement){target="_blank"}).

## 6. Inzetposten

1. Herzie de Static Content Deployment (SCD) ideale staat om onderhoudstijd tijdens plaatsingen op het productiemilieu te verminderen. Controleren [SCD-strategieën (Static Content Deployment)](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/static-content){target="_blank"} en [Beheer van winkelconfiguratie](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/store-settings){target="_blank"} hulplijn.
2. Controleer minificatie-instellingen voor HTML, JavaScript en CSS. (Dit geldt niet voor websites zonder PWA/koptekst).
3. Bevestig dat het gebruik van de volgende wolkenvariabelen op hun voorgenomen doeleinden richt. ([SCD_MATRIX](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-build#scd_matrix){target="_blank"}, [SCD_ON_DEMAND](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global#scd_on_demand){target="_blank"} en [SKIP_SCD](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy#skip_scd){target="_blank"})

## 7. Testen en problemen oplossen

1. Test de uitgaande e-mails over transacties. Meer informatie over [Adobe Commerce Cloud - Functionaliteit SendGrid Mail](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/sendgrid){target="_blank"}.
2. [!BADGE Blocker]{type=caution tooltip="Potentiële blokkering"}
3. [!BADGE Blocker]{type=caution tooltip="Potentiële blokkering"}

   >[!NOTE]
   > A [belasting- en stresstests dienen voor het doel](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/guidance#:~:text=A%20load%20test%20can%20help,Scan%20Tool%20for%20your%20sites.){target="_blank"} het opsporen van knelpunten en het opsporen van prestatieproblemen binnen de toepassing. Het speelt een cruciale rol bij het beheren van verwachtingen ten aanzien van clustergrootte en het bepalen van de noodzakelijke schaalaanpassingen om effectief aan de bedrijfsvereisten te voldoen.

   >[!IMPORTANT]
   > **_WAARSCHUWING:_** Bij het voorbereiden van een belastingtest: **_niet_** e-mails met live-transacties verzenden (zelfs naar dummyadressen). Het verzenden van e-mails tijdens het testen kan ertoe leiden dat het project de standaard verzendlimiet (12k) bereikt die voor SendGrid is geconfigureerd voordat het wordt gestart.
   > 
   > - E-mailcommunicatie uitschakelen:
   >   Ga naar _Store > Configuration > Advanced > System > Email Sending Settings_.

4. Voer de veiligheidspenetratietests op de productie-instantie uit als onderdeel van de [beveiligingsmodel gedeelde verantwoordelijkheid](https://business.adobe.com/products/magento/secure-ecommerce.html){target="_blank"}. Voor compatibiliteit met PCI (Payment Card Industry) vereist de aangepaste site een penetratietest.

## 8. Overige configuraties

1. Indexeren wijzigen in _&quot;update volgens schema_&quot;, behalve de **_customer_grid_** die op &quot;SAVE&quot; blijft staan (zie [Indexeringsmodi](https://developer.adobe.com/commerce/php/development/components/indexing/#indexing-modes){target="_blank"}).
2. Gebruikt u zoekprogramma&#39;s of extensies van derden?
3. Bevestig dat [SEO-configuraties (Search Engine Optimization, optimalisatie van zoekprogramma&#39;s) worden correct ingesteld](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/seo-overview){target="_blank"} om indexeerders/kruiplers in staat te stellen de website te scannen, indien van toepassing.
4. Omleiding en routes toevoegen (zie [Verbindingen vormen](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/routes/routes-yaml){target="_blank"})

   >[!NOTE]
   >Voeg omleidingen en routes aan het routes.yaml- dossier in het milieu van de Integratie toe en verifieer de configuratie in dit milieu alvorens aan het Opvoeren en de Productie op te stellen.

       &quot;http://{all}/&quot;:
       tekst: upstream
       upstream: &quot;mymagento:http&quot;
       
       &quot;http://{all}/&quot;:
       tekst: upstream
       upstream: &quot;mymagento:http&quot;
   
5. Zorg ervoor dat XDebug is uitgeschakeld als deze tijdens de ontwikkeling is ingeschakeld (zie [Xdebug configureren](https://developer.adobe.com/commerce/cloud-tools/docker/test/configure-xdebug/){target="_blank"}).
6. Controleer of de op-cache en andere configuraties correct zijn bijgewerkt in het bestand php.ini ([verwijzen naar dit voorbeeld](https://github.com/magento/magento-cloud/blob/master/php.ini#L41){target="_blank"}).
7. Abonneren op de [**Adobe Commerce-statuspagina**](https://status.adobe.com/cloud/experience_cloud#/){target="_blank"}.
8. Je abonneren op New Relic &quot;[Beheerde waarschuwingen voor Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce){target="_blank"}&quot; communicatiekanalen om de gegeven prestatiesmetriek te controleren ([meer lezen](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/monitor/new-relic/new-relic-service){target="_blank"}).

## 9. Veiligheid

1. De Adobe Commerce Security Scan instellen

   >[!NOTE]
   > [Adobe Commerce Security Scan is een handig hulpmiddel](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-scan){target="_blank"} dat helpt verouderde softwareversies, onjuiste configuratie, en potentiële malware op de plaats ontdekken. Meld u aan, plant de presentatie zodat deze vaak wordt uitgevoerd en zorg ervoor dat e-mails naar de juiste contactpersoon voor technische beveiliging worden verzonden.
   > 
   > Voltooi deze taak tijdens UAT. Als u de optie voor periodiek scannen gebruikt, moet u scans plannen op momenten van lage vraag. Zie de [Beveiligingsscan](https://account.magento.com/scanner/index/dashboard/){target="_blank"} in de Adobe Commerce-account. U moet zich aanmelden bij een Adobe Commerce-account om toegang te krijgen tot de beveiligingsscan.

2. Wijzig de standaardinstellingen voor Adobe Commerce Admin.
3. Het beheerderswachtwoord wijzigen (zie [Beveiliging van beheerder configureren](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-admin){target="_blank"}).
4. De URL van de beheerder wijzigen (zie [Een aangepaste Admin URL gebruiken](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-urls#use-a-custom-admin-url){target="_blank"}).
5. Verwijder om het even welke gebruikers niet meer op het project (zie [Gebruikers maken en beheren](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/user-access){target="_blank"}).
6. Wachtwoorden voor beheerders zijn geconfigureerd (zie [Wachtwoordvereisten voor beheerders](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-admin){target="_blank"}).
7. Vorm twee-factor authentificatie (zie [Verificatie met twee factoren](https://developer.adobe.com/commerce/testing/functional-testing-framework/two-factor-authentication/){target="_blank"}).

## 10. Ga live

Wanneer het tijd is om over te slaan, gelieve de volgende stappen uit te voeren (voor meer informatie zie [DNS-configuraties](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist){target="_blank"}):

1. Heb toegang tot uw DNS dienst en werk A en CNAME verslagen voor elk van uw domeinen en hostnames bij:
   1. Een CNAME-record toevoegen voor _&lt;&lt;www.yourdomain.com>>_, onder verwijzing naar **prod.magentocloud.map.fastly.net**
   2. Vier A-records instellen voor _&lt;&lt;yourdomain.com>>_, onder verwijzing naar:\
      15.10.1.124\
      151 101 65 124\
      15.10.129.124\
      15.10.193.124
2. De Adobe Commerce Base-URL wijzigen in _&lt;&lt;www.yourdomain.com>>_
3. Wacht op de tijd van TTL om over te gaan, dan herstart Webbrowser.
4. Test de website.

### Als u een probleem hebt dat go-live blokkeert:

Als u om het even welke problemen tegenkomt die u verhinderen te lanceren tijdens de cutover, de snelste methode om juiste geschikte geschikte geschikte steun te krijgen is de helpdesk te gebruiken en een kaartje met de reden &quot;Onbekwaam te openen mijn opslag&quot; te openen, en een hotline steunaantal te roepen (zie [de lijst van Adobe Commerce P1 (Prioriteit 1)-meldnummers](https://support.magento.com/hc/en-us/articles/360042536151){target="_blank"}):

- US gratis: (+1) 877 282 7436 (direct naar Adobe Commerce P1-hotline)
- US Gratis: (+1) 800 685 3620 (druk in het eerste menu op 7 voor de Adobe Commerce P1-hotline)
- US Lokaal: (+1) 408 537 8777

## 11. Na introductie

Zodra de site live is, stuurt u een e-mail naar de toegewezen technische advies (Customer Technical Advisory), CSE (Customer Success Engineer) en AM (Account Manager). Nochtans, als u geen rekeningsmanager hebt die aan het project wordt toegewezen, kunt u een steunkaartje tot stand brengen vragend om de controle van Hoge SLA wordt toegelaten zodra de plaats live is gegaan. De CTA/CSE voert de volgende taken uit zodra de plaats wordt geverifieerd om met Fastly wordt toegelaten en caching:

- Label de cluster als live en maak een ondersteuningsticket om High SLA (Service Level Agreements)-controle te activeren.
- Activeer New Relic Synthetics voor uptime controle.

>[!MORELIKETHIS]
> 
> - [Gereedheidsoverzicht starten - Implementatie afspeelboek](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/launch/overview){target="_blank"}
> - [Checklist starten - Gebruikershandleiding](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist){target="_blank"}
> - [Checklist vooraf starten - Handleiding voor sitebeheer/Commerce-beheer](https://experienceleague.adobe.com/en/docs/commerce-admin/start/setup/prelaunch-checklist){target="_blank"}
> - [Beveiligingsmodel voor gedeelde verantwoordelijkheid](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility){target="_blank"}

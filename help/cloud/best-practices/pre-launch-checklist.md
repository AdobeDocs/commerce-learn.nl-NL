---
title: Controlelijst voor het starten van Adobe Commerce Cloud
description: Meer informatie over de checklist voor het vooraf starten van Adobe Commerce Cloud.
feature: Cloud
topic: Commerce, Architecture, Development
old-role: Architect, Developer
role: Developer
level: Intermediate
doc-type: Tutorial
duration: 0
last-substantial-update: 2024-04-17T00:00:00Z
jira: KT-15180
kt: 15180
exl-id: c6adb2c2-f194-4a3d-9290-e0837ef062ae
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 0%

---

# Commerce Cloud Pre-Launch Checklist

Het volgende is een synopsis van de Adobe Commerce [&#x200B; documentatie van de lancering van de Plaats &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/overview){target="_blank"}.

Deze controlelijst is bedoeld als hulp bij het plannen en uitvoeren van een geslaagde start van de Adobe Commerce Cloud-site. Werk samen met uw systeemintegrator voor Adobe Commerce Cloud om ervoor te zorgen dat alle configuratietaken en controlelijstitems worden voltooid en geverifieerd. Als u problemen ondervindt met checklist-items of vragen hebt, neemt u contact op met de aangewezen technisch adviseur van de klant of met de succesvolle technicus van de klant. Als uw account geen toegewezen CTA/CSE heeft, kunt u een ondersteuningsticket voor hulp maken.

Als u een CTA/CSE hebt die aan de rekening wordt toegewezen, contacteer hen en de Manager van de Rekening minstens 4 weken voorafgaand aan het lanceren van de nieuwe plaats van de Wolk van de Handel van Adobe om hen van uw **te informeren bedoeling** om te lanceren.

- Sommige controles worden benadrukt met [!BADGE &#x200B; Blocker &#x200B;]{type=caution tooltip="Potentiële blokkering"} aangezien zij uw gaan-levende kunnen blokkeren als niet zorgvuldig herzien.
- Zorg ervoor dat u met uw ontwikkelaar- of systeemintegratiepartner samenwerkt om deze uit te lijnen met uw implementatiebenadering.

>[!IMPORTANT]
> U keurt [&#x200B; verantwoordelijkheid &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility){target="_blank"} voor om het even welke negatieve gevolgen en bijbehorende risico&#39;s aan het programma van de productielanctie en aan de gang zijnde plaatsstabiliteit goed, als u er niet in slaagt om deze controlelijst te gebruiken en te voltooien.

## 1. Pre-Go Live

1. Herzie de documentatie over het testen en het gaan van levende [&#x200B; documentatie van de lancering van de Plaats &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/overview){target="_blank"}

   >[!NOTE]
   >Verzeker een uitvoerige _&quot;ga live klaar plan&quot;_ volledig met uw partner of systeemintegrator wordt voorbereid, die alle noodzakelijke actiepunten omvat. Herinner me, terwijl de pre-lanceringschecklist de beste praktijken van Adobe benadrukt, vervangt het _&#x200B;**niet**&#x200B;_ de behoefte aan uw eigen go-live opstellingsplan.

2. [!BADGE &#x200B; Blocker &#x200B;]{type=caution tooltip="Potentiële blokkering"} herzie de Aanbevelingen en Informatie van de Gegevens van de Steun (SWAT) ([&#x200B; Gids van de Gebruiker &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/intro){target="_blank"})
3. Eindgebruiker/handelaar voerde UAT (het Testen van de Erkenning van de Gebruiker), met inbegrip van backendverrichtingen uit.
4. Het team van de systeemintegrator heeft UAT van begin tot eind op het opvoeren en de productie uitgevoerd. Verwijs naar de [&#x200B; Documentatie van Experience League &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/staging-and-production){target="_blank"}.
5. Bevestig codeplaatsing en het testen in het opvoeren en productiemilieu&#39;s ([&#x200B; las meer &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/staging-and-production){target="_blank"}).
6. De productiecluster is permanent vergroot tot de contractueel vastgelegde dagelijkse basislijn. Spreek naar de toegewezen CTA/CSE voor meer informatie of geef een ondersteuningsticket op.

## &#x200B;2. Huidige configuraties

1. Verbetering Adobe Commerce en verwante pakketten/de diensten aan de [&#x200B; recentste versie &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview){target="_blank"}
2. Herzie de huidige configuraties en de diensten met uw SI/Partner, en [&#x200B; volg de beste praktijken &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/catalog-management){target="_blank"}.
3. Herzie het MySQL/Shared-Files [&#x200B; schijfgebruik &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space){target="_blank"}

## &#x200B;3. Snelle configuraties

1. [!BADGE &#x200B; Blocker &#x200B;]{type=caution tooltip="Potentiële blokkering"} zorg ervoor dat het caching werkt ([&#x200B; het Geheime voorgeheugen van de volledig-Pagina &#x200B;](https://developer.adobe.com/commerce/frontend-core/guide/caching/){target="_blank"} of [&#x200B; GraphQL caching &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/){target="_blank"}). Lees de [&#x200B; Snelle opstellingsgids &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly){target="_blank"}.
2. Gebruik indien van toepassing de GET-methode voor GraphQL-query&#39;s op PWA/Headless-websites.

   >[!NOTE]
   > Alleen de query&#39;s die met een HTTP GET-bewerking worden verzonden, kunnen in de cache worden geplaatst (indien van toepassing). [&#x200B; POST vragen kunnen niet in het voorgeheugen ondergebracht worden &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/){target="_blank"}.

3. Zorg ervoor dat de Snelle Optimalisering van het Beeld wordt toegelaten ([&#x200B; zie de Snelle Optimalisering van het Beeld &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly-image-optimization){target="_blank"})
4. Verifieer dat de correcte schildplaats wordt gevormd ([&#x200B; vormt geheim voorgeheugen, achtergronden en oorsprongsbescherming &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration){target="_blank"}).
5. De Firewall van de Toepassing van het Web (**WAF**) werkt. (Zie [&#x200B; het Oplossen van problemen geblokkeerde verzoeken &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly-waf-service){target="_blank"}, als om het even welk, en beperkingen)
6. Werk de Snelle [&#x200B; &quot;Genegeerde Parameters URL&quot;](https://github.com/iancassidyweb/magento2/commit/68fdecfcd26c957382b8d68b64887e0a83298524){target="_blank"} lijst in het admin paneel bij om geheim voorgeheugenprestaties te verbeteren.

   >[!NOTE]
   > In de snelste configuratie onder _Admin > Opslag > Configuraties > Systeem > het Volledige Geheime voorgeheugen van de Pagina > de Snelle Configuratie > Geavanceerde Configuratie > Genegeerde Parameters URL (Globaal)_, kunt u een komma-gescheiden lijst van parameters vinden die snel zouden moeten negeren wanneer het zoeken naar caching pagina&#39;s. Zorg ervoor dat u de VCL opnieuw uploadt nadat u deze lijst hebt gewijzigd

## &#x200B;4. DNS en SSL

1. [!BADGE &#x200B; Blocker &#x200B;]{type=caution tooltip="Potentiële blokkering"} bevestigt alle vereiste domeinnamen worden gevraagd. _(Verzend vooraf een steunkaartje voor om het even welke toegevoegde of veranderde domeinen)_
2. [!BADGE &#x200B; SSL (TLS) certificaat van 0&rbrace; Blocker &lbrace;is van toepassing geweest op domein(en). &#x200B;]{type=caution tooltip="Potentiële blokkering"} Lees [&#x200B; dit artikel &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/ssl-tls-certificates-for-magento-commerce-cloud-faq){target="_blank"} voor meer informatie.
3. DNS van de update [&#x200B; TTL (Tijd aan Levend) &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist#to-update-dns-configuration-for-site-launch){target="_blank"} waarde aan het minimum mogelijk, voor gaat live.
4. Sendgrid SPF en DKIM inschakelen

   >[!NOTE]
   > Voeg de verslagen SendGrid CNAME voor elk domein aan de DNS configuratie toe. Lees [&#x200B; SendGrid e-maildienst &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/sendgrid){target="_blank"} om te zien hoe te om de afzenderdomeinen en meer te veranderen.

## &#x200B;5. Databaseconfiguraties

Adobe Commerce Cloud gebruikt een MariaDB Galera-cluster als de database voor zowel de testomgeving als de productieomgeving. Galera-clusters zijn van essentieel belang voor het verbeteren van prestaties en schaalbaarheid. Raadpleeg de volgende artikelen voor meer informatie over de optimale werkwijzen en beperkingen van Galera-clusterreplicaties.

- [&#x200B; MySQL de beste praktijken van Configuraties &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration){target="_blank"}
- Beheerde Alarm op Adobe Commerce: [&#x200B; MariaDB alarm &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-mariadb-alerts){target="_blank"}
- Beste praktijken voor [&#x200B; gegevensbestandconfiguratie &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud){target="_blank"}
- Diepe analyse aan [&#x200B; de clusterreplicaties van Galera en stroom-controle.](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/backend-development/galera-db-slow-replication){target="_blank"}

1. [&#x200B; de verbinding van de Slave MYSQL &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration#slave-connections){target="_blank"} wordt geadviseerd voor betere prestaties tijdens hoge gegevensbestandladingen.
2. Zorg ervoor dat het rijformaat voor alle gegevensbestandlijsten aan [&#x200B; DYNAMIC in plaats van COMPACT &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/maintenance/mariadb-upgrade#convert-database-table-storage-format){target="_blank"} wordt geplaatst (Dit is vooral waar voor op-prem aan wolkenmigraties).
3. Verander de motor van de gegevensbestandopslag van [&#x200B; MyISAM in InnoDB &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud#convert-all-myisam-tables-to-innodb){target="_blank"} voor alle lijsten.
4. Beoordeel en optimaliseer databasetabellen van meer dan 1 GB van tevoren.
5. De gegevens over het databaseschema zijn actueel en bijgewerkt. (Verwijs naar [&#x200B; deze gids &#x200B;](https://mariadb.com/kb/en/engine-independent-table-statistics/#collecting-statistics-with-the-analyze-table-statement){target="_blank"}).

## &#x200B;6. Inzetposten

1. Herzie de Static Content Deployment (SCD) ideale staat om onderhoudstijd tijdens plaatsingen op het productiemilieu te verminderen. De Strategieën van de Plaatsing van de Inhoud van het overzicht [&#x200B; Statische (SCD) van de Inhoud &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/static-content){target="_blank"} en [&#x200B; gids van het de configuratiebeheer van de Opslag &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/store-settings){target="_blank"}.
2. Controleer minificatiemontages voor HTML, JavaScript, en CSS. (Dit geldt niet voor PWA/Headless-websites).
3. Bevestig dat het gebruik van de volgende wolkenvariabelen op hun voorgenomen doeleinden richt. ([&#x200B; SCD_MATRIX &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-build#scd_matrix){target="_blank"}, [&#x200B; SCD_ON_DEMAND &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global#scd_on_demand){target="_blank"} en [&#x200B; SKIP_SCD &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy#skip_scd){target="_blank"})

## &#x200B;7. Testen en problemen oplossen

1. Test de uitgaande e-mails over transacties. Lees meer over [&#x200B; de Wolk van de Handel van Adobe - functionaliteit SendGrid Post &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/sendgrid){target="_blank"}.
2. [!BADGE &#x200B; Blocker &#x200B;]{type=caution tooltip="Potentiële blokkering"} Om het even welke blokkers met Adobe?
3. [!BADGE &#x200B; Blocker &#x200B;]{type=caution tooltip="Potentiële blokkering"} voert lading en stress het testen op de instantie van de Productie uit alvorens levend te gaan en resultaten met toegewezen CTA/CSE te delen.

   >[!NOTE]
   > A [&#x200B; lading en de stresstest dienen het doel &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/guidance#:~:text=A%20load%20test%20can%20help,Scan%20Tool%20for%20your%20sites.){target="_blank"} om knelpunten te identificeren en prestatieskwesties binnen de toepassing te ontdekken. Het speelt een cruciale rol bij het beheren van verwachtingen ten aanzien van clustergrootte en het bepalen van de noodzakelijke schaalaanpassingen om effectief aan de bedrijfsvereisten te voldoen.

   >[!IMPORTANT]
   > **_WARNING:_** wanneer het voorbereiden van een ladingstest gelieve_2 **_verzendt geen levende transactie e-mails (zelfs naar dummyadressen)._** Het verzenden van e-mails tijdens het testen kan ertoe leiden dat het project de standaard verzendlimiet (12k) bereikt die voor SendGrid is geconfigureerd voordat het wordt gestart.
   > 
   > - E-mailcommunicatie uitschakelen:
   >   Ga naar _Opslag > Configuratie > Geavanceerd > Systeem > het Verzenden van Montages E-mail_.

4. Het testen van de veiligheidspenetratie van de uitvoering op de productiemilitie als deel van het [&#x200B; gedeelde model van de verantwoordelijkheidsveiligheid &#x200B;](https://business.adobe.com/products/magento/secure-ecommerce.html){target="_blank"}. Voor compatibiliteit met PCI (Payment Card Industry) vereist de aangepaste site een penetratietest.

## &#x200B;8. Overige configuraties

1. De schakelaar indexerend aan _&quot;update op programma_&quot;, behalve **_customer_grid_** die op &quot;SAVE&quot;blijft (zie [&#x200B; Indexerende wijzen &#x200B;](https://developer.adobe.com/commerce/php/development/components/indexing/#indexing-modes){target="_blank"}).
2. Gebruikt u zoekprogramma&#39;s of extensies van derden?
3. Bevestig dat [&#x200B; (de Optimalisering van de Motor van het Onderzoek) configuraties SEO behoorlijk opstelling &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/seo-overview){target="_blank"} zijn om indexeerders/kruiplers toe te laten om de website af te tasten, indien relevant.
4. Voeg opnieuw richt en routes toe (zie [&#x200B; routes &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/routes/routes-yaml){target="_blank"} vormen)

   >[!NOTE]
   >Voeg omleidingen en routes aan het routes.yaml- dossier in het milieu van de Integratie toe en verifieer de configuratie in dit milieu alvorens aan het Opvoeren en de Productie op te stellen.

        &quot;http://{all}/&quot;:
        type: upstream 
        stroomopwaarts: &quot;mymagento:http&quot;
       
        &quot;http://{all}/&quot;:
        type: stroomopwaarts 
        stroomopwaarts: &quot;mymagento:http&quot;
   
5. Verzeker XDebug wordt onbruikbaar gemaakt als toegelaten tijdens ontwikkeling (zie [&#x200B; Xdebug &#x200B;](https://developer.adobe.com/commerce/cloud-tools/docker/test/configure-xdebug/){target="_blank"} vormen).
6. Verifieer dat op-geheime voorgeheugen en andere configuraties nauwkeurig in het php.ini- dossier zijn bijgewerkt ([&#x200B; verwijs naar deze steekproef &#x200B;](https://github.com/magento/magento-cloud/blob/master/php.ini#L41){target="_blank"}).
7. Abonneren aan de [**de statuspagina van Adobe Commerce** &#x200B;](https://status.adobe.com/cloud/experience_cloud#/){target="_blank"}.
8. Abonneer aan New Relic &quot;[&#x200B; Beheerde Alarm voor Adobe Commerce &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce){target="_blank"}&quot;berichtkanalen om de bepaalde prestatiesmetriek te controleren ([&#x200B; lees meer &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/monitor/new-relic/new-relic-service){target="_blank"}).

## &#x200B;9. Veiligheid

1. De Adobe Commerce Security Scan instellen

   >[!NOTE]
   > [&#x200B; het Scannen van de Veiligheid van Adobe Commerce is een nuttig hulpmiddel &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-scan){target="_blank"} dat de hulp verouderde softwareversies, onjuiste configuratie, en potentiële malware op de plaats ontdekt. Meld u aan, plant de presentatie zodat deze vaak wordt uitgevoerd en zorg ervoor dat e-mails naar de juiste contactpersoon voor technische beveiliging worden verzonden.
   > 
   > Voltooi deze taak tijdens UAT. Als u de optie voor periodiek scannen gebruikt, moet u scans plannen op momenten van lage vraag. Zie de [&#x200B; pagina van het Scannen van de Veiligheid &#x200B;](https://account.magento.com/scanner/index/dashboard/){target="_blank"} in de Rekening van Adobe Commerce. U moet zich aanmelden bij een Adobe Commerce-account om toegang te krijgen tot de beveiligingsscan.

2. Wijzig de standaardinstellingen voor Adobe Commerce Admin.
3. Verander het admin wachtwoord (zie [&#x200B; Vormend Veiligheid Admin &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-admin){target="_blank"}).
4. Verander admin URL (zie [&#x200B; Gebruikend een douane Admin URL &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-urls#use-a-custom-admin-url){target="_blank"}).
5. Verwijder om het even welke gebruikers niet meer op het project (zie [&#x200B; tot gebruikers &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/user-access){target="_blank"} leiden en leiden).
6. De wachtwoorden voor beheerders worden gevormd (zie {de Vereisten van het Wachtwoord van 0} Admin [).](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-admin){target="_blank"}
7. Vorm twee-factor authentificatie (zie [&#x200B; two-Factor Authentificatie &#x200B;](https://developer.adobe.com/commerce/testing/functional-testing-framework/two-factor-authentication/){target="_blank"}).

## &#x200B;10. Ga live

Wanneer het tijd is om te bedekken, gelieve de volgende stappen (voor meer informatie, zie [&#x200B; DNS Configuraties &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist){target="_blank"}) uit te voeren:

1. Heb toegang tot uw DNS dienst en werk A en CNAME verslagen voor elk van uw domeinen en hostnames bij:
   1. Voeg een verslag CNAME voor _&lt;&lt;www.yourdomain.com>>_ toe, richtend bij **prod.magentocloud.map.faals.net**
   2. Plaats vier A verslagen voor _&lt;&lt;yourdomain.com>>_, richtend bij:\
      151.101.1.124\
      151.101.65.124\
      151.101.129.124\
      151.101.193.124
2. Wijzig de Adobe Commerce Base-URL in _&lt;&lt;www.yourdomain.com>>_
3. Wacht op de tijd van TTL om over te gaan, dan herstart Webbrowser.
4. Test de website.

### Als u een probleem hebt dat go-live blokkeert:

Als u om het even welke problemen ontmoet die u verhinderen tijdens de cutover te lanceren, de snelste methode om juiste geschikte geschikte steun te krijgen is de helpdesk te gebruiken en een kaartje met de reden &quot;Onbekwaam te openen mijn opslag&quot;te openen, en een hotline steunaantal (zie [&#x200B; de lijst van Adobe Commerce P1 (Prioriteit 1) te roepen hotline aantallen &#x200B;](https://support.magento.com/hc/en-us/articles/360042536151){target="_blank"}):

- US gratis: (+1) 877 282 7436 (direct naar Adobe Commerce P1-hotline)
- US Gratis: (+1) 800 685 3620 (druk in het eerste menu op 7 voor de Adobe Commerce P1-hotline)
- US Lokaal: (+1) 408 537 8777

## &#x200B;11. Na introductie

Zodra de site live is, stuurt u een e-mail naar de toegewezen CTA (Customer Technical Advisory), CSE (Customer Success Engineer) en AM (Account Manager). Als u echter geen accountmanager hebt toegewezen aan het project, kunt u een ondersteuningsticket maken waarin u wordt gevraagd om High SLA-bewaking in te schakelen zodra de site live is gegaan. De CTA/CSE voert de volgende taken uit zodra is geverifieerd dat de site is gestart met Snelingeschakeld en in cache plaatsen:

- Label de cluster als live en maak een ondersteuningsticket om de controle op hoog SLA (Service Level Agreements) te activeren.
- Activeer New Relic Synthetics voor uptime controle.

>[!MORELIKETHIS]
> 
> - [&#x200B; Overzicht van de Gereedheid van de Lancering van de Lancering - Playbook van de Implementatie &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/launch/overview){target="_blank"}
> - [&#x200B; Checklist van de Lancering - de Gids van de Gebruiker &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist){target="_blank"}
> - [&#x200B; Prelaunch Checklist - de Gids van Admin van de Manager van de Plaats/Commerce &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/start/setup/prelaunch-checklist){target="_blank"}
> - [&#x200B; Gedeeld model van de verantwoordelijkheidsveiligheid &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility){target="_blank"}

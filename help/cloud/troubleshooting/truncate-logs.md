---
title: Staafstammen afkappen
description: Leer hoe u een mislukte implementatie kunt triggeren vanwege een volledige harde schijf door grote logbestanden af te kappen.
feature: Cloud, Site Management
topic: Commerce, Development
role: Architect, Developer
level: Beginner, Intermediate
doc-type: Technical Video
duration: 206
last-substantial-update: 2025-3-25
jira: KT-17595
source-git-commit: b90aa9eb8759391a16dfb29ca25b0d2d271956ed
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Staafstammen afkappen

Leer hoe u kunt triggeren en een mislukte implementatie vanwege een volledige harde schijf. Leer hoe u kunt zoeken en welke opdrachten u kunt uitvoeren om ruimte vrij te maken in uw Adobe Commerce Cloud-omgeving.

Als u denkt dat u deze logbestanden nodig hebt, kunt u deze `rsync` gebruiken of andere methoden gebruiken om een kopie van de server beschikbaar te maken voordat u deze afkapt.

## Wie is deze video voor

- Ontwikkelaars en IT-professionals
- Systeembeheerders

## Video-inhoud

- Diagnose en los een ontbroken plaatsing op
- Waar enkele veelvoorkomende grote logbestanden worden gevonden
- Snelle methode om een logbestand af te kappen

>[!VIDEO](https://video.tv.adobe.com/v/3454572?learn=on)


## Opdrachten die in de video worden gebruikt

De ruimte op de vaste schijf controleren `df -h` . Let op de regel dev/mapper/xxxx

```SHELL
df -h

Filesystem                              Size  Used Avail Use% Mounted on
/dev/loop217                           1016M 1016M     0 100% /
none                                    492K  4.0K  488K   1% /dev
fake-sysfs                              120G     0  120G   0% /sys
tmpfs                                   120G     0  120G   0% /sys/fs/cgroup
tmpfs                                   384M     0  384M   0% /dev/shm
tmpfs                                    50M  460K   50M   1% /run
tmpfs                                   5.0M     0  5.0M   0% /run/lock
/dev/loop236                            144M  144M     0 100% /app
/dev/mapper/hyjh5nlaoabqtxxnh4opgjqzpu  4.9G  4.9G     0 100% /mnt
/dev/loop14                             8.0G  403M  7.6G   5% /tmp
/dev/mapper/platform-lxc                5.0T   69G  4.7T   2% /run/shared
```


De bestanden en hun grootte met de opdracht weergeven in een leesbare indeling, zoals kb, mb en gb `ls -lah`

```SHELL
ls -lah

total 4.7G
drwxr-xr-x 2 web web 4.0K Jul 16  2024 .
drwxr-xr-x 6 web web 4.0K Jan 10  2024 ..
-rw-rw-r-- 1 web web 487K Jul  5  2024 cache.log
-rw-r--r-- 1 web web 1.2K Jul 16  2024 cloud.error.log
-rw-r--r-- 1 web web 328K Mar 25 14:09 cloud.log
-rw-rw-r-- 1 web web 2.4G Jul  5  2024 cron.log
-rw-rw-r-- 1 web web  363 Dec  6  2023 debug.log
-rw-rw-r-- 1 web web  15K Jan 10  2024 indexation.log
-rw-r--r-- 1 web web 229K Jan 10  2024 install_upgrade.log
-rw-r--r-- 1 web web 2.9K Jul 16  2024 patch.log
-rw-rw-r-- 1 web web 2.4G Mar 25 15:36 support_report.log
-rw-rw-r-- 1 web web  516 Dec  6  2023 system.log
```

## Voorbeelden voor afbreeklogboek

Wijzig de map `var/log` nadat u het juiste project en de juiste omgeving hebt ingestuurd. Vervolgens kunt u een bestand afkappen, vergelijkbaar met `> some-log-file.log`

```BASH
> support_report.log 
> cron.log 
```

## Gerelateerde documentatie

- [ de berichten van de Gezondheid ](https://experienceleague.adobe.com/nl/docs/commerce-on-cloud/user-guide/dev-tools/integrations/health-notifications){target="_blank"} 

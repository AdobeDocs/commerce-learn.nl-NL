---
title: Gebruik Snel om toegang tot een gehele website te weigeren
description: Toegang tot Adobe Commerce-site beperken met snel Edge ACL's en een aangepaste VCL
feature: Cloud, Configuration, Site Management, System
topic: Administration,Commerce,Development, Security
role: Admin, Developer, User
level: Intermediate, Experienced
doc-type: Technical Video
duration: 200
last-substantial-update: 2025-07-11T00:00:00Z
jira: KT-18494
source-git-commit: 810d1a17e9fe564e8450b091bbeb5574d7d76075
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Gebruik Snel om toegang voor een gehele website te weigeren

Leer hoe u de toegang tot uw Adobe Commerce Cloud-site beperkt met snelwerkende Edge ACL&#39;s en aangepaste VCL-fragmenten. Deze geleidelijke gids helpt u uw pre-lanceringsmilieu beveiligen door slechts specifieke IP adressen toe te staan, die uw ontwikkelingsplaats privé blijven.

## Wat u gaat leren

Toegang tot Adobe Commerce-sites beperken met snel Edge ACL&#39;s en aangepaste VCL | Beveiligde pre-startomgevingen

## Voor wie is deze video?

* DevOps-engineer
* Adobe Commerce Developer
* Site Reliability Engineer

>[!VIDEO](https://video.tv.adobe.com/v/3464785/?learn=on&enablevpops&captions=dut)

## Codevoorbeeld

Dit is een voorbeeld van het gebruikte VCL

```BASH
if ( !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 "Forbidden";}
```

## Verwante documentatie

* [ ontdekt kwaadwillig IP adres ](https://experienceleague.adobe.com/nl/docs/commerce-learn/tutorials/tools/new-relic/malicious-ip)
* [ Douane VCL voor het toestaan van verzoeken ](https://experienceleague.adobe.com/nl/docs/commerce-on-cloud/user-guide/cdn/custom-vcl-snippets/fastly-vcl-allowlist)
* [ Douane VCL voor het blokkeren van verzoeken ](https://experienceleague.adobe.com/nl/docs/commerce-on-cloud/user-guide/cdn/custom-vcl-snippets/fastly-vcl-blocking)
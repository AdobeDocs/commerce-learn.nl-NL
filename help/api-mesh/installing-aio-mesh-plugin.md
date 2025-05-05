---
title: Adobe I/O Runtime-opdrachtregelinterface en API Mesh-insteekmodule installeren
description: Ontdek hoe u de Adobe I/O Runtime opdrachtregelinterface en de API Mesh-plug-in installeert
landing-page-description: Ontdek hoe u Adobe App Builder kunt gebruiken en de Adobe I/O Runtime met de API Mesh-plug-in kunt installeren.
short-description: Ontdek hoe u Adobe App Builder kunt gebruiken en de Adobe I/O Runtime met de API Mesh-plug-in kunt installeren.
kt: 11801
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 898a0918-0362-4fa4-9204-d770ff1a7e6f
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Adobe I/O Runtime CLI- en netplug-in installeren

Voordat u begint met het gebruik van API Mesh voor Adobe Developer App Builder, moet u de insteekmodule `aio` CLI en API Mesh installeren.
Voor installatieinstructies en eerste vereisten, bezoek het API Netwerk [ Begonnen het worden ](https://developer.adobe.com/graphql-mesh-gateway/gateway/getting-started/){target="_blank"}  pagina.

## Voor wie is deze video?

* De ontwikkelaars nieuw aan het Net van API of [!DNL Adobe Commerce] met beperkte ervaring die [ Adobe I/O Runtime ](https://developer.adobe.com/runtime/docs/guides/overview/){target="_blank"} gebruiken  en het Net van API.

## Video-inhoud

* Inleiding tot API-net
* Adobe I/O Runtime CLI installeren (opdrachtregelinterface)
* De API Mesh-insteekmodule installeren

>[!VIDEO](https://video.tv.adobe.com/v/3414122?quality=12&learn=on)

## De plug-in `aio` CLI en API Mesh installeren

Nadat u `node` en `npm` hebt geïnstalleerd, voert u de volgende opdracht uit om de `aio` CLI te installeren:

```bash
npm install -g @adobe/aio-cli
```

Nadat de Adobe I/O Runtime CLI is geïnstalleerd, gebruikt u de volgende opdracht om de API Mesh-insteekmodule te installeren:

```bash
aio plugins:install @adobe/aio-cli-plugin-api-mesh
```

{{$include /help/_includes/api-mesh-related-links.md}}

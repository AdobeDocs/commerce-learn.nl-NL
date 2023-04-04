---
title: Adobe I/O Runtime-opdrachtregelinterface en API Mesh-insteekmodule installeren
description: Ontdek hoe u de Adobe I/O Runtime opdrachtregelinterface en de API Mesh-plug-in installeert
landing-page-description: Ontdek hoe u Adobe App Builder kunt gebruiken en de Adobe I/O Runtime met de API Mesh-plug-in kunt installeren.
short-description: Discover how to use Adobe App Builder and install the Adobe I/O Runtime with API Mesh plugin.
kt: 11801
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
source-git-commit: d85426bcf3ae0412a433414d70c874964905dda0
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---


# Adobe I/O Runtime CLI- en netplug-in installeren

Voordat u begint met het gebruik van API Mesh voor Adobe Developer App Builder, moet u de `aio` CLI en de API-netplug-in.
Ga voor installatie-instructies en -voorwaarden naar het API-net [Aan de slag](https://developer.adobe.com/graphql-mesh-gateway/gateway/getting-started/){target="_blank"} pagina.

## Voor wie is deze video?

* Ontwikkelaars die nog niet bekend zijn met API Mesh of [!DNL Adobe Commerce] met beperkte ervaring [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/guides/overview/){target="_blank"} en API-net.

## Video-inhoud

* Inleiding tot API-net
* Adobe I/O Runtime CLI installeren (opdrachtregelinterface)
* De API Mesh-insteekmodule installeren

>[!VIDEO](https://video.tv.adobe.com/v/3414122?quality=12&learn=on)

## De installatie van de `aio` CLI- en API-netplug-in

Na installatie `node` en `npm`voert u de volgende opdracht uit om de `aio` CLI:

```bash
npm install -g @adobe/aio-cli
```

Nadat de Adobe I/O Runtime CLI is geïnstalleerd, gebruikt u de volgende opdracht om de API-netplug-in te installeren:

```bash
aio plugins:install @adobe/aio-cli-plugin-api-mesh
```

{{$include /help/_includes/api-mesh-related-links.md}}

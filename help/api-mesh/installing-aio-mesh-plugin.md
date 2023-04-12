---
title: Adobe I/O Runtime-opdrachtregelinterface en API Mesh-insteekmodule installeren
description: Ontdek hoe u de Adobe I/O Runtime opdrachtregelinterface en de API Mesh-plug-in installeert
landing-page-description: Ontdek hoe u Adobe App Builder kunt gebruiken en de Adobe I/O Runtime met de API Mesh-plug-in kunt installeren.
short-description: Ontdek hoe u Adobe App Builder kunt gebruiken en de Adobe I/O Runtime met de API Mesh-plug-in kunt installeren.
kt: 11801
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
exl-id: 898a0918-0362-4fa4-9204-d770ff1a7e6f
source-git-commit: edb98cf6544954d741c43beb39f4056326c7d26b
workflow-type: tm+mt
source-wordcount: '195'
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

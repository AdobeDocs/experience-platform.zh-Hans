---
keywords: Experience Platform；首頁；熱門主題；資料收集；launch；web sdk
solution: Experience Platform
title: 数据收集概述
description: 瞭解在Adobe Experience Platform中收集客戶體驗資料的相關各種技術。
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 13c02dd5930905e3851ff147c0ea4d914e3dc6c7
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 7%

---

# 数据收集概述

Adobe Experience Platform提供了一套技術，可讓您從使用者端來源收集客戶體驗資料，並將其傳送至Adobe Experience Platform Edge Network，在那裡可以快速擴充和轉換資料，並將其分發到Adobe或非Adobe目的地。

下列使用者端來源支援資料收集：

* 網頁型應用程式
* 原生行動應用程式
* 過頂式(OTT)應用程式

資料收集著重於所擷取資料集的可發現性和可存取性，包括以下內容：

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [标记](../tags/home.md)
* [数据流](../edge/datastreams/overview.md)
* [事件轉送](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../edge/home.md)
* [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [體驗資料模型(XDM)](../xdm/home.md)
* [Adobe Experience Platform Identity Service](../identity-service/home.md)

本指南提供資料收集的高層級簡介，並說明如何透過Platform Edge Network將資料傳送至Adobe Experience Cloud產品和非Adobe應用程式。

## 標籤、Web SDK和行動SDK

Platform Web SDK和Platform Mobile SDK可分別收合所有Adobe產品程式庫，並將其壓縮為適用於Web和行動平台的單一開發套件。 這些可使用原始程式碼或以下方式實作： [標籤](../tags/home.md) 透過Data Collection UI或Adobe Experience Platform UI。

壓縮這些程式庫可加快資料收集速度，並將從使用者端裝置到Platform Edge Network的操作整合為單一資料流。

![標籤， Web SDK， Mobile SDK](./images/home/tags-sdks.png)

## Platform Edge Network和資料串流 {#edge}

Platform Edge Network是分散於全球且快速可靠的伺服器網路，可接收及處理超大規模資料。 使用標籤，您可以設定 [資料串流](../edge/datastreams/overview.md) 適用於Adobe Target、Adobe Audience Manager和Adobe Analytics等產品，可讓您在伺服器端啟用這些產品，而不需變更使用者端代碼。

此外，資料串流還與數項平台功能整合，有助於確保您傳送的任何敏感資料都會根據組織政策和法規受到適當處理。 請參閱以下小節： [處理敏感資料](../edge/datastreams/overview.md#sensitive) 如需詳細資訊，請參閱資料串流檔案。

![資料串流和Adobe解決方案](./images/home/adobe-solutions.png)

>[!NOTE]
>
>如需Platform Edge Network的高層級簡介，請參閱下列內容 [互動式產品導覽](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## 事件轉送

[事件轉送](../tags/ui/event-forwarding/overview.md) 可以挖掘任何Experience Platform資料串流，讓您以極低的延遲將資料轉換、擴充及傳送至任何非Adobe目的地，而不需將任何協力廠商程式碼新增至使用者端裝置。

![事件轉送](./images/home/event-forwarding.png)

>[!NOTE]
>
>事件轉送是一項付費功能，屬於Adobe Real-time Customer Data Platform Connections、Prime或Ultimate方案的一部分。

## 后续步骤

本檔案提供資料收集如何運作的高層級概觀，以自動化將收集的客戶體驗資料傳送至Adobe產品和第三方目的地的程式。

![資料收集架構](./images/home/collection.png)

如需透過Edge Network傳送事件資料所需的一般工作流程詳細資訊，請參閱 [端對端總覽](./e2e.md).

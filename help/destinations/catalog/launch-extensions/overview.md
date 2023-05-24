---
keywords: 標籤擴充功能；標籤擴充功能；Launch目的地；Platform標籤擴充功能；Platform標籤擴充功能；platform launch目的地
title: Adobe Experience Platform中的標籤擴充功能
description: Adobe Experience Platform提供Adobe新一代的標籤管理功能。 Platform可讓您透過簡單的方式部署及管理所有必要的分析、行銷及廣告標籤功能，以便支援相關客戶體驗。
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: fe71294cb73a25c2c4708b0a6ebe04fc2b97afdf
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# Adobe Experience Platform中的標籤擴充功能

Adobe Experience Platform提供新一代Adobe標籤管理功能。 Platform可讓您透過簡單的方式部署及管理所有必要的分析、行銷及廣告標籤功能，以便支援相關客戶體驗。 標籤是以隨附的加值功能形式提供給Adobe Experience Cloud客戶。

如需標籤的簡介，請參閱下列資源：

- [标记概述](../../../tags/home.md)
- [快速入门指南](../../../tags/quick-start/quick-start.md)

## 如何在Platform介面中尋找標籤擴充功能 {#how-to-find-extensions-in-interface}

若要在Platform介面中尋找擴充功能，請瀏覽 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]** 並選取 **[!UICONTROL 擴充功能]** 在 **[!UICONTROL 型別]** 篩選。

![介面中的擴充功能篩選器](../../assets/catalog/launch-extensions/filter.png)

## 標籤擴充功能的運作方式 {#how-extensions-work}

A [標籤延伸模組](../../../tags/home.md#extensions) 是程式碼套件，可增強網站或行動應用程式的功能。 這可能包括傳送原始事件資料到目的地，例如 [Google Analytics](/help/destinations/catalog/analytics/google-universal-analytics.md) 但它們也可用於其他功能。

請務必區分標籤和事件轉送擴充功能。 Platform目的地使用者介面中浮現的擴充功能包括 *標籤延伸模組*. 如需詳細資訊，請參閱事件轉送概觀。 [標籤和事件轉送之間的差異](/help/tags/ui/event-forwarding/overview.md#differences-between-event-forwarding-and-tags).



<!--

Extensions forward raw event data to several types of destinations. Think of extensions as an **Event Forwarding** type of destination. This is a simpler type of integration with destination platforms, which only forwards raw event data. Examples of those are the [Gainsight personalization extension](../personalization/gainsight.md) or the [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Profile/Segment Export** destinations in Adobe Experience Platform capture event data, combine it with other data sources, apply segmentation, and export segments and qualified profiles to destinations. Examples of those are the [Amazon S3 cloud storage destination](../cloud-storage/amazon-s3.md) or the [Google Display & Video 360 advertising destination](../advertising/google-dv360.md).

![Tag extensions compared to other destinations](../../assets/common/launch-and-other-destinations.png)

-->

## 使用標籤擴充功能的好處 {#extensions-benefits}

現有的Experience Cloud客戶可免費使用Platform的標籤功能。 透過您可安裝、設定、更新和刪除的簡單易用擴充功能，此系統可簡化網站上的標籤部署作業。 標籤在您的網站上留下很小的空間，並可讓您保持頁面快速載入。

雖然您無法啟用區段來標籤擴充功能，但您可以設定規則，只在某些情況下轉送事件資料。 這項強大的功能可讓您只在某些情況下轉送事件資料，而不是每次互動時都傳送事件資料。 如需詳細資訊，請閱讀 [標籤檔案](../../../tags/ui/managing-resources/rules.md).

## 擴充功能的範例使用案例 {#extensions-use-cases}

擴充功能可讓您滿足各種客戶使用案例。 使用擴充功能的一些範例使用案例包括：

- 您可以透過Facebook畫素擴充功能，將網站或原生應用程式資料傳送至Facebook。 facebook Pixel指出訪客導覽至您網站或應用程式的哪些部分、將該資訊轉送至Facebook，而且您可以透過Facebook重新鎖定訪客。
- 您可以將網站和應用程式的事件資料轉送至Google Analytics，以便根據該資料進行分析並做出決策。
- 您可以根據使用者與頁面互動的方式，根據您設定的規則，在適當的時間開啟使用者端聊天箱應用程式。

## 擴充功能類別 {#extension-categories}

擴充功能在Platform中可能屬於下列類別：

- [Advertising](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [資料管理平台](../data-management/overview.md)
- [電子郵件行銷目的地](../email-marketing/overview.md)
- [个性化](../personalization/overview.md)
- [调查](../survey/overview.md)
- [客戶的心聲](../voice/overview.md)

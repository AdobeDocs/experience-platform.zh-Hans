---
keywords: Awin廣告商轉換標籤擴充功能；轉換標籤；Awin；AWIN
title: Awin廣告商轉換標籤擴充功能
description: Awin廣告商轉換標籤擴充功能是Adobe Experience Platform中的廣告目的地。 如需擴充功能的相關詳細資訊，請參閱Adobe交換上的擴充功能頁面。
exl-id: 99feb169-acf3-4e68-8785-3f4cf565e5a9
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 3%

---

# Awin廣告商轉換標籤擴充功能 {#awin-conversiontag-extension}

## 概述 {#overview}

轉換標籤是AWIN.Tracking.Sale JavaScript物件的宣告，會在確認頁面上完成，以指示Mastertag已發生轉換。 之後，它會執行必要的追蹤要求。

Awin Advertiser Conversion Tag是Adobe Experience Platform中的廣告擴充功能。 如需擴充功能的相關詳細資訊，請參閱擴充功能頁面，網址為 [Adobe交換](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html).

此目的地是標籤延伸模組。 如需標籤擴充功能在Platform中如何運作的詳細資訊，請參閱 [標籤擴充功能概觀](../launch-extensions/overview.md).

![UI中的Awin Advertiser Conversiontag擴充功能](../../assets/catalog/advertising/awin-conversion-tag/catalog.png)

## 先决条件 {#prerequisites}

所有已購買Platform的客戶都可在Destinations目錄中找到此擴充功能。

若要使用此擴充功能，您需要存取Platform中的標籤。 標籤是以隨附的加值功能形式提供給Adobe Experience Cloud客戶。 請聯絡您的組織管理員，以取得UI中資料收集功能的存取權，並要求他們授予您 **[!UICONTROL manage_properties]** 許可權，方便您安裝擴充功能。

## 安裝擴充功能 {#install-extension}

若要安裝 [!DNL Awin Advertiser Conversion Tag] 副檔名：

在 [平台介面](https://platform.adobe.com/)，前往 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**.

從目錄選取擴充功能或使用搜尋列。

按一下目的地以反白顯示，然後選取 **[!UICONTROL 設定]** 在右側邊欄中。 如果 **[!UICONTROL 設定]** 控制項呈現灰色，表示您遺漏 **[!UICONTROL manage_properties]** 許可權。 另請參閱 [必要條件](#prerequisites).

選取您要安裝擴充功能的標籤屬性。 您也可以選擇建立新屬性。 资产是规则、数据元素、配置的扩展、环境和库的集合。瞭解中的屬性 [標籤檔案](../../../tags/ui/administration/companies-and-properties.md).

工作流程會將您帶到資料收集UI以完成安裝。

如需擴充功能組態選項和安裝支援的詳細資訊，請參閱 [Adobe交換上的Awin廣告商轉換標籤頁面](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html).

您也可以直接在中安裝擴充功能 [資料彙集UI](https://experience.adobe.com/#/data-collection/). 請參閱指南： [新增擴充功能](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 以取得詳細資訊。


## 如何使用擴充功能 {#how-to-use}

安裝擴充功能後，您就可以開始設定規則。 在資料收集UI中，您可以為已安裝的擴充功能設定規則，以只在某些情況下將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱以下主題的概觀： [規則](../../../tags/ui/managing-resources/rules.md) 標籤檔案中。

## 設定、升級和刪除擴充功能 {#configure-upgrade-delete}

您可以在資料收集UI中設定、升級和刪除擴充功能。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，UI仍會顯示 **[!UICONTROL 安裝]** 用於擴充功能。 依照中的說明開始安裝工作流程 [安裝擴充功能](#install-extension) 以設定或刪除您的擴充功能。

若要升級您的擴充功能，請參閱 [擴充功能升級程式](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 標籤檔案中。

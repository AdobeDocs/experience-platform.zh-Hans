---
keywords: Invoca；Invoca
title: Invoca標籤擴充功能
description: Invoca標籤擴充功能是Adobe Experience Platform中客戶目的地的聲音。 如需擴充功能的相關詳細資訊，請參閱Adobe交換上的擴充功能頁面。
exl-id: f66a2e74-8d94-4b3a-9627-083ca875fad7
source-git-commit: b4e869f9bc29122db4fc66ccda752a50c7db729f
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 3%

---

# [!DNL Invoca Tags] 扩展 {#invoca-extension}

## 概述 {#overview}

[!DNL Invoca] 將通話資料和語音深入解析帶入數位客戶歷程。 替換為 [!DNL Invoca’s] 通話情報平台，行銷人員終於能透過分析來測量通話結果，並將離線轉換次數與數位支出聯絡起來。

[!DNL Invoca Tags] 是Adobe Experience Platform中客戶擴充功能的聲音。 如需擴充功能的相關詳細資訊，請參閱擴充功能頁面，網址為 [Adobe交換](https://exchange.adobe.com/experiencecloud.details.100067.invoca.html).

此目的地是標籤延伸模組。 如需標籤擴充功能在Platform中如何運作的詳細資訊，請參閱 [標籤擴充功能概觀](../launch-extensions/overview.md).

![Invoca擴充功能](../../assets/catalog/voice/invoca/catalog.png)

## 先决条件 {#prerequisites}

此擴充功能適用於 [!DNL Destinations] 已購買Platform之所有客戶的目錄。

若要使用此擴充功能，您需要存取Adobe Experience Platform中的標籤。 標籤是以隨附的加值功能形式提供給Adobe Experience Cloud客戶。 請聯絡您的組織管理員以取得標籤的存取權，並要求他們授予您 **[!UICONTROL manage_properties]** 許可權，方便您安裝擴充功能。

## 安裝擴充功能 {#install-extension}

若要安裝 [!DNL Invoca Tags] 副檔名：

在 [平台介面](https://platform.adobe.com/)，前往 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**.

從目錄選取擴充功能或使用搜尋列。

按一下目的地以反白顯示，然後選取 **[!UICONTROL 設定]** 在右側邊欄中。 如果 **[!UICONTROL 設定]** 控制項呈現灰色，表示您遺漏 **[!UICONTROL manage_properties]** 許可權。 另請參閱 [必要條件](#prerequisites).

選取您要安裝擴充功能的屬性。 您也可以選擇建立新屬性。 资产是规则、数据元素、配置的扩展、环境和库的集合。瞭解中的屬性 [「屬性」頁面段落](../../../tags/ui/administration/companies-and-properties.md#properties-page) 標籤檔案中的。

工作流程會逐步引導您完成安裝步驟。

如需擴充功能組態選項和安裝支援的詳細資訊，請參閱 [在Adobe交換上叫用標籤頁面](https://exchange.adobe.com/experiencecloud.details.100067.invoca.html).

您也可以直接在中安裝擴充功能 [資料彙集UI](https://experience.adobe.com/#/data-collection/). 如需詳細資訊，請參閱以下章節： [新增擴充功能](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 標籤檔案中。

## 如何使用擴充功能 {#how-to-use}

安裝擴充功能後，您就可以開始設定規則。

您可以為已安裝的擴充功能設定規則，以只在特定情況下將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱 [標籤檔案](../../../tags/ui/managing-resources/rules.md).

## 設定、升級和刪除擴充功能 {#configure-upgrade-delete}

您可以在資料收集UI中設定、升級和刪除擴充功能。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，Platform UI仍會顯示 **[!UICONTROL 安裝]** 用於擴充功能。 依照中的說明開始安裝工作流程 [安裝擴充功能](#install-extension) 以設定或刪除您的擴充功能。

若要升級您的擴充功能，請參閱 [擴充功能升級程式](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 標籤檔案中。

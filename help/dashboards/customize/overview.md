---
keywords: Experience Platform；使用者介面；UI；儀表板；儀表板；設定檔；區段；目的地
title: 儀表板自訂概觀
description: 進一步瞭解您可以如何自訂Adobe Experience Platform儀表板中顯示的資料。
exl-id: efabdb61-4148-4b0e-b7a1-6e788b5e43a8
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# 儀表板自訂概觀

Adobe Experience Platform中可用的設定檔、區段和目的地儀表板可以透過多種方式自訂。 本指南提供可用自訂的概觀，其中包含逐步指示的連結，引導您瞭解如何個人化控制面板中顯示的介面工具以及這些介面工具的大小、形狀和位置。

>[!NOTE]
>
>Widget會顯示在 [!UICONTROL 授權使用情況] 無法自訂儀表板。 若要深入瞭解此獨特控制面板，請閱讀 [授權使用情況儀表板檔案](../guides/license-usage.md).

## 修改儀表板

選取 **[!UICONTROL 修改儀表板]** 您可從「設定檔」、「區段」或「目的地」儀表板調整目前顯示在儀表板中Widget的大小、順序和位置。 如需如何修改控制面板中Widget外觀的詳細資訊，請參閱 [修改儀表板指南](modify.md).

## Widget程式庫

Experience Platform內的Widget程式庫可讓您檢視所有 [標準](#standard-widgets) 和 [自訂](#custom-widgets) 您的組織可以使用的Widget。 從您的儀表板（例如，設定檔儀表板）中，您可以選取 **[!UICONTROL 修改儀表板]** 以顯示 **[!UICONTROL Widget資料庫]** 按鈕。

![會反白顯示「修改」圖示板的「輪廓」圖示板。](../images/customization/modify-dashboard.png)

選取 **[!UICONTROL Widget資料庫]** 開啟Widget資料庫並檢視所有可用的標準量度，或開始建立自訂Widget。

![會反白顯示Widget資料庫的「設定檔」儀表板。](../images/customization/widget-library-button.png)

### 標準Widget {#standard-widgets}

標準Widget是指Adobe提供用於儀表板的Widget。 這些Widget是唯讀的，您的組織無法編輯。

在Widget程式庫中， **[!UICONTROL 標準]** tab包含Adobe提供的所有可用標準widget。 您可以使用任何這些標準量度來更新您的儀表板。 若要進一步瞭解如何新增標準Widget至您的儀表板，請參閱指南，瞭解 [在儀表板中使用標準Widget](standard-widgets.md).

### 自訂Widget {#custom-widgets}

自訂Widget是指由您組織的成員建立和共用的Widget。 這些Widget是透過 **[!UICONTROL 自訂]** 標籤，並要求您的組織透過使用 [綱要](#edit-schema)

如需建立您自己的Widget的完整步驟，請參閱 [控制面板的自訂Widget指南](custom-widgets.md).

![反白顯示「標準」和「自訂」的Widget程式庫工作區。](../images/customization/widget-library.png)

#### 编辑架构 {#edit-schema}

為了建立 [自訂Widget](#custom-widgets) 對於儀表板，您必須先識別Widget將依據的Real-Time Customer Profile屬性。

如需編輯您組織結構以建立自訂儀表板Widget的逐步指示，請瀏覽指南 [編輯您的儀表板結構](edit-schema.md).

## 后续步骤

閱讀本檔案後，您可以修改現有Widget的大小、形狀和順序、新增Adobe提供的標準Widget，或建立自訂Widget並與您的組織共用，開始自訂Experience Platform儀表板。

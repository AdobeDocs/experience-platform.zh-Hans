---
title: 應用程式內傳訊檢視
description: 本指南詳細說明Adobe Experience Platform Assurance中應用程式內傳訊檢視的相關資訊。
exl-id: 6131289a-aebb-4b3a-9045-4b2cf23415f8
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Assurance中的應用程式內傳訊檢視

Adobe Experience Platform保證中的應用程式內傳訊檢視可讓您驗證應用程式、監視傳遞到裝置的應用程式內訊息，以及模擬傳送到裝置的訊息。

## 裝置上的訊息

在頂端 **[!UICONTROL 裝置上的訊息]** 索引標籤是 **[!UICONTROL 訊息]** 下拉式清單。 這將包括已在Assurance工作階段接收的所有訊息。 如果訊息不在此清單中，表示應用程式從未收到該訊息。

![消息](./images/in-app-messaging/message.png)

選取訊息時，將會顯示許多有關該訊息的資訊，如下節所述。

### 訊息預覽

在右側面板中為 **[!UICONTROL 訊息預覽]** 窗格，顯示訊息的預覽。 選取 **[!UICONTROL 在裝置上模擬]** 會將該訊息傳送至目前連線至工作階段的任何裝置。

![预览](./images/in-app-messaging/preview.png)

### 訊息行為

在 **[!UICONTROL 訊息預覽]** 窗格是 **[!UICONTROL 訊息行為]** 標籤。 此部分包含訊息顯示方式的所有詳細資料。 此資訊包括定位資訊、動畫、撥動手勢和外觀設定。

![行为](./images/in-app-messaging/gestures.png)

### 資訊標籤

在左側區段中，有四個標籤會顯示訊息的詳細資訊。 此 **[!UICONTROL 資訊]** 索引標籤顯示從Adobe Journey Optimizer (AJO)載入的訊息行銷活動相關資訊。

您也可以選取 **[!UICONTROL 檢視行銷活動]** 在AJO中開啟訊息以進行檢查或編輯。

![信息](./images/in-app-messaging/info.png)

### 規則標籤

此 **[!UICONTROL 規則]** 索引標籤會顯示需要發生什麼才會顯示此訊息。 這可提供觸發訊息顯示的確切專案分析。 檢視此範例：

![规则](./images/in-app-messaging/rules.png)

此範例顯示規則的三個不同條件。 如果您選取事件（從事件清單、「分析」標籤或時間軸中），則會根據這些規則評估該事件。 如果事件符合條件，則會顯示綠色核取記號：

![規則相符](./images/in-app-messaging/rule-match.png)

如果事件不符，則會顯示紅色圖示：

![規則不符](./images/in-app-messaging/rule-mismatch.png)

如果這三個條件都符合目前的事件，則會顯示訊息。

### 分析標籤

此 **[!UICONTROL 分析]** 索引標籤提供規則的額外深入分析。 在此，我們會根據訊息規則與事件的符合程度來篩選工作階段中的每個事件。

![分析](./images/in-app-messaging/analyze.png)

在以下範例中： **[!UICONTROL 規則標籤]** 區段，規則中有三個條件。 此索引標籤會顯示每個事件符合的規則百分比。 大多數事件符合33% （三個條件之一），其餘符合100%。

因此，您可以找到接近相符但不完全相符規則的事件。

![臨界值](./images/in-app-messaging/threshold.png)

此 **[!UICONTROL 符合臨界值]** 滑桿可讓您篩選應顯示哪些事件。 例如，這可以設為50% - 90%，以取得完全符合三個條件中兩個之事件的清單。

### 互動標籤

此 **[!UICONTROL 互動]** 索引標籤會顯示傳送至Edge以供追蹤的互動事件清單。

![互動](./images/in-app-messaging/interactions.png)

每次顯示訊息時，通常都會有四個互動事件：

```
trigger > display > interact > dismiss
```

「interact」互動具有與其相關聯的額外「action」值。 可能的值包括「已點按」或「取消」。

驗證欄會顯示互動事件是否已由Edge正確接收及處理。

## 验证

此 **[!UICONTROL 驗證]** tab會針對您目前的工作階段執行驗證，檢查應用程式是否已正確設定應用程式內傳訊：

![验证](./images/in-app-messaging/validation.png)

如果發現任何錯誤，將會提供如何修正這些錯誤的詳細資訊。

## 事件清單

![验证](./images/in-app-messaging/event-list.png)

此 **[!UICONTROL 事件清單]** 索引標籤可讓您快速檢視與應用程式內傳訊相關的保證工作階段中的所有事件。 您可能會在這裡看到的部分活動包括：

* 擷取訊息的要求和回應
* 顯示訊息事件
* 互動追蹤事件

在此檢視中，您可以使用許多標準事件清單功能，包括套用搜尋、套用篩選器、新增或移除欄，以及匯出資料。

在右側面板中選取事件，以檢視該事件的原始詳細資訊。

從右邊的詳細資料面板中，可以標籤所選的事件，這對於標籤應由其他人檢閱的內容很有幫助。

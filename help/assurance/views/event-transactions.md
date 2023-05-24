---
title: 事件交易檢視
description: 本指南詳細說明了Adobe Experience Platform Assurance中事件交易檢視的相關資訊。
exl-id: ad97f2c1-5bbc-49e2-8378-edcb8af149a3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# 事件交易檢視

Adobe Experience Platform Assurance中的「事件交易」檢視可讓您驗證和偵錯Edge Network使用者端實作，並近乎即時地檢視上游驗證結果。

## 設定Edge Network工作流程的保證

晚於 [設定Assurance](../tutorials/implement-assurance.md)，確定您已在應用程式中實作最新版本的Assurance和Edge Network擴充功能。

若要檢視您的事件，請從左側功能表選取 **[!UICONTROL 事件交易]** 在 **[!UICONTROL Adobe Experience Platform Edge]** 區段。

如果沒有看見此選項，請選取 **[!UICONTROL 設定]** 在視窗左下方，新增 **[!UICONTROL 事件交易]** 檢視並選取 **[!UICONTROL 儲存]**.

## 開始使用事件交易檢視

在本節中，請熟悉「事件交易」檢視，並瞭解如何在Edge Network工作流程上有效率地使用它進行端對端驗證。

### 事件處理流程

![事件交易檢視](./images/event-transactions/event-transactions-view.png)

「事件異動」檢視會依事件處理流程的順序顯示三個欄位：

- **[!UICONTROL 使用者端]**：此欄顯示使用者端已處理或已接收的事件，可供Mobile SDK存取。 這包括使用API呼叫建立的事件，例如 `Edge.sendEvent`，以及使用者端從Edge Network伺服器收到的回應事件處理常式（如有）。 使用者端事件範例：
   - AEP請求事件是透過Edge擴充功能傳送的事件，並包含XDM和選用的自由格式資料。
   - AEP Response Event Handle是從Edge Network收到的事件控制代碼，以回應AEP要求事件。 請求事件可能未收到任何、一個或多個回應事件控制代碼。
   - 發生錯誤時，例如無法處理XDM裝載，或其中一個上游服務傳回錯誤或警告時，可能會看到AEP錯誤回應。
- **[!UICONTROL 邊緣網路]**：此欄顯示Edge Network透過網路要求從伺服器端收到的事件，以及該事件包含的資料和中繼資料。
- **[!UICONTROL 上游]**：此欄顯示已設定的上游服務所接收的事件，包括傳入事件的處理和/或驗證結果的詳細資訊。
請注意，此欄是動態的，可能會根據兩個主要因素顯示不同型別的資訊：
   - 資料串流設定和在其上啟用的服務。
   - 傳送至Edge Network的事件型別。

### Inspect事件

「事件交易」檢視中顯示的事件會提供每個狀態所處理資料之格式和內容的相關資訊，以及在上游處理資料時所遇到之任何警告或錯誤的深入詳細資訊。 此檢視有助於縮小事件/請求層級的偵錯資訊，並在開發週期的初期識別錯誤。

#### 展開事件詳細資料

若要檢查事件，請從檢視中選取所需的事件。 此動作會展開 **[!UICONTROL 事件詳細資料]** 在熒幕右側檢視。
巢狀資料會以樹狀結構格式顯示。 您可以透過選取 **+** 鍵名稱左側的（加號）按鈕。

![事件詳細資料](./images/event-transactions/event-details.png)

#### Inspect警告或錯誤

每個事件名稱都會加上一個圖示，指出該事件處理的高層級狀態：

- 如果事件已成功處理，則會顯示綠色勾號。
- 如果偵測到警告或錯誤，則會顯示警告符號。 選取相關事件，以進一步瞭解「 」中警告或錯誤的原因 **[!UICONTROL 事件詳細資料]** 檢視。

### 組態設定

您可以選取「 」旁邊的「資訊工具提示」，以檢查目前使用的資料流識別碼。 **[!UICONTROL 邊緣網路]** 欄標題。

![顯示資料串流ID](./images/event-transactions/show-datastream-id.png)

>[!INFO]
>
>當多個使用者端連線至相同的保證工作階段，並使用不同的資料流ID時，您會看到所有這些ID都顯示在這裡。 但這並不表示您目前的實作使用多個資料串流。 應用程式只會使用在標籤（行動屬性）中設定的目前資料串流ID，來處理來自該使用者端的新事件。 在測試具有不同組態設定且連線多個使用者端的更複雜使用案例時，使用個別保證工作階段來簡化驗證程式可能會有所幫助。

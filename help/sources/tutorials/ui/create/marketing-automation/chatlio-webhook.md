---
title: 在UI中建立Chatlio來源連線
description: 瞭解如何使用Adobe Experience Platform UI建立Chatlio來源連線。
badge: Beta
exl-id: 55c10bcb-0332-45ff-970b-272d375b591d
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 1%

---

# 建立 [!DNL Chatlio] ui中的來源連線

>[!NOTE]
>
>此 [!DNL Chatlio] 來源為測試版。 請閱讀 [來源概觀](../../../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

本教學課程提供建立 [!DNL Chatlio] 使用Adobe Experience Platform使用者介面的來源連線。

## 快速入门 {#getting-started}

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

## 先决条件 {#prerequisites}

下節提供建立前必須完成的必要條件相關資訊 [!DNL Chatlio] 來源連線。

### 定義來源結構描述的JSON範例 [!DNL Chatlio] {#prerequisites-json-schema}

建立之前 [!DNL Chatlio] 來源連線，您需要提供來源結構描述。 您可以使用下方的JSON。

```
{
  "visitor": {
    "email": "test@example.com",
    "UUID": "2d3f4260-2235-903b-0a82-a23d326cc257"
  },
   "message": "Hi",
  "channelId": "C04J7M7LCMQ",
  "slackChannelName": "aep",
  "slackChannelId": "C04JVR71WKS"
}
```

### 建立平台結構描述 [!DNL Chatlio] {#create-platform-schema}

您也必須確保建立平台結構描述以用於您的來源。 閱讀教學課程日期： [建立平台結構描述](../../../../../xdm/schema/composition.md) 有關如何建立方案的完整步驟。

![顯示Chatlio範例結構描述的平台UI](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/schema.png)

## 連線您的 [!DNL Chatlio] 帳戶 {#connect-account}

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 並檢視Experience Platform中可用的來源目錄。

使用 *[!UICONTROL 類別]* 功能表，依類別篩選來源。 或者，在搜尋列中輸入來源名稱，從目錄中尋找特定來源。

前往 [!UICONTROL 行銷自動化] 類別以檢視 [!DNL Chatlio] 來源卡。 若要開始，請選取 **[!UICONTROL 新增資料]**.

![具有Chatlio卡的Platform UI目錄](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/catalog.png)

## 选择数据 {#select-data}

此 **[!UICONTROL 選取資料]** 步驟隨即顯示，提供介面供您選取要帶至Platform的資料。

* 介面的左側是瀏覽器，可讓您檢視帳戶內的可用資料流；
* 介面的右側部分可讓您預覽來自JSON檔案的最多100列資料。

選取 **[!UICONTROL 上傳檔案]** 以從您的本機系統上傳JSON檔案。 或者，您也可以將要上傳的JSON檔案拖放至 [!UICONTROL 拖放檔案] 面板。

![來源工作流程的新增資料步驟。](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/add-data.png)

上傳檔案後，預覽介面會更新，以顯示您上傳的結構描述預覽。 預覽介面可讓您檢查檔案的內容和結構。 您也可以使用 [!UICONTROL 搜尋欄位] 用於從結構描述中存取特定專案的公用程式。

完成後，選取 **[!UICONTROL 下一個]**.

![來源工作流程的預覽步驟。](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/preview.png)

## 数据流详细信息 {#dataflow-detail}

此 **資料流詳細資料** 步驟隨即顯示，為您提供使用現有資料集或為資料流建立新資料集的選項，以及提供資料流名稱和說明的機會。 在此步驟中，您還可以配置設定檔擷取、錯誤診斷、部分擷取和警示的設定。

完成後，選取 **[!UICONTROL 下一個]**.

![來源工作流程的資料流詳細資料步驟。](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/dataflow-detail.png)

## 映射 {#mapping}

此 [!UICONTROL 對應] 步驟隨即顯示，為您提供介面，用於將來源結構描述中的來源欄位對應到目標結構描述中適當的目標XDM欄位。

Platform會根據您選取的目標結構描述或資料集，為自動對應的欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。 您可以視需要選擇直接對應欄位，或使用資料準備函式來轉換來源資料，以衍生計算值或計算值。 如需使用對應程式介面和計算欄位的完整步驟，請參閱 [資料準備UI指南](../../../../../data-prep/ui/mapping.md).

下列對應是強制性的，在繼續前應先設定 [!UICONTROL 檢閱] 階段。

| 目標欄位 | 描述 |
| --- | --- |
| `UUID` | 此 [!DNL Chatlio] 事件的識別碼。 |

成功對應來源資料後，請選取 **[!UICONTROL 下一個]**.

![來源工作流程的對應步驟。](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/mapping.png)

## 请查看 {#review}

此 **[!UICONTROL 檢閱]** 步驟隨即顯示，可讓您在建立新資料流之前對其進行檢閱。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **[!UICONTROL 指派資料集和對應欄位]**：顯示要將來源資料擷取到哪個資料集中，包括資料集所堅持的結構描述。

檢閱資料流後，選取 **[!UICONTROL 完成]** 並留出一些時間來建立資料流。

![來源工作流程的稽核步驟。](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/review.png)

## 取得您的串流端點URL {#get-streaming-endpoint-url}

建立串流資料流後，您現在可以擷取串流端點URL。 此端點將用於訂閱您的webhook，允許您的串流來源與Experience Platform通訊。

為了建構用來設定webhook的URL [!DNL Chatlio] 您必須擷取下列專案：

* **[!UICONTROL 資料流ID]**
* **[!UICONTROL 串流端點]**

擷取您的 **[!UICONTROL 資料流ID]** 和 **[!UICONTROL 串流端點]**，前往 [!UICONTROL 資料流活動] 您剛建立之資料流的頁面，並從 [!UICONTROL 屬性] 面板。

![資料流活動中的串流端點。](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/endpoint-test.png)

擷取串流端點和資料流ID後，請根據以下模式建立URL： ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. 例如，建構的webhook URL可能如下所示： ``https://dcs.adobedc.net/collection/d56b47ee3985104beaf724efcd78a3e1a863d720471a482bebac0acc1ab95983``

## 在中設定webhook [!DNL Chatlio] {#set-up-webhook}

建立webhook URL後，您現在可以使用以下工具設定webhook [!DNL Chatlio] 使用者介面。

登入您的 [[!DNL Chatlio]](https://chatlio.com/) 帳戶和關注 [安裝指南](https://chatlio.com/docs/setup/) 以建立Widget。

建立Widget後，請導覽至Widget的設定頁面，將您的webhook URL新增至該Widget。

![Chatlio上的webhook設定頁面。](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/widget-settings.png)

接下來，選取 **[!DNL Behavior]** 標籤並將webhook URL新增至 *[!DNL Webhook when a new conversation starts]* 欄位以及您要訂閱的任何其他webhook事件欄位。

![顯示webhook端點欄位的Chatlio UI。](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/webhook.png)

>[!TIP]
>
>您可以為您的訂閱各種不同的事件 [!DNL Chatlio] webhook。 如需不同事件的詳細資訊，請參閱 [[!DNL Chatlio] 事件檔案](https://chatlio.com/docs/webhooks/).

## 后续步骤 {#next-steps}

依照本教學課程，您已成功設定串流資料流，將 [!DNL Chatlio] 要Experience Platform的資料。 若要監視正在擷取的資料，請參閱上的指南 [使用Platform UI監控串流資料流](../../monitor-streaming.md).

## 其他资源 {#additional-resources}

以下各節提供其他資源，您可在使用時參照 [!DNL Chatlio] 來源。

### 验证 {#validation}

驗證您是否已正確設定來源及 [!DNL Chatlio] 正在內嵌訊息，請遵循下列步驟：

* 您可以檢查 [!DNL Chatlio] **[!UICONTROL 報表]** > **[!UICONTROL 聊天記錄]** 識別所擷取事件的頁面 [!DNL Chatlio].

![顯示聊天記錄的聊天室使用者介面熒幕擷圖](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/chatlio-chat-history.png)

* 在Platform UI中選取 **[!UICONTROL 檢視資料流]** 旁邊 [!DNL Chatlio] 來源目錄上的卡片功能表。 接下來，選取 **[!UICONTROL 預覽資料集]** 驗證您所設定Webhook內擷取的資料 [!DNL Chatlio].

![顯示已擷取事件的平台UI熒幕擷圖](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/platform-dataset.png)

如需更多資訊，請參閱 [!DNL Chatlio]，請造訪 [[!DNL Chatlio] 檔案](https://chatlio.com/docs/) 和 [常見問題集](https://chatlio.com/pricing/#FAQ).

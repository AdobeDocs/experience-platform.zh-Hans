---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
title: （測試版）在UI中建立Mixpanel來源連線
description: 瞭解如何使用Adobe Experience Platform UI建立Mixpanel來源連線。
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: 6b9e5da9e552d93ff174d1d65dabb0ffd3128c1a
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 10%

---

# (Beta)建立 [!DNL Mixpanel] ui中的來源連線

>[!NOTE]
>
>此 [!DNL Mixpanel] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

本教學課程提供建立 [!DNL Mixpanel] 使用Adobe Experience Platform平台使用者介面的來源連線。

## 快速入门

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

### 收集必要的認證

為了連線 [!DNL Mixpanel] 至Platform，您必須提供下列連線屬性的值：

| 認證 | 描述 | 示例 |
| --- | --- | --- |
| 用户名 | 與您對應的服務帳戶使用者名稱 [!DNL Mixpanel] 帳戶。 請參閱 [[!DNL Mixpanel] 服務帳戶檔案](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) 以取得詳細資訊。 | `Test8.6d4ee7.mp-service-account` |
| 密码 | 與您對應的服務帳戶密碼 [!DNL Mixpanel] 帳戶。 | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| 项目ID | 您的 [!DNL Mixpanel] 專案ID。 建立來源連線時需要此ID。 請參閱 [[!DNL Mixpanel] 專案設定檔案](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) 和 [[!DNL Mixpanel] 建立和管理專案指南](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) 以取得詳細資訊。 | `2384945` |
| 时区 | 與您的時區對應的時區 [!DNL Mixpanel] 專案。 需要時區才能建立來源連線。 請參閱 [Mixpanel專案設定檔案](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) 以取得詳細資訊。 | `Pacific Standard Time` |

如需驗證您的憑證的詳細資訊 [!DNL Mixpanel] 來源，請參閱 [[!DNL Mixpanel] 來源概觀](../../../../connectors/analytics/mixpanel.md).

## 連線您的 [!DNL Mixpanel] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 以存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 *分析* 類別，選取 [!DNL Mixpanel]，然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

此 **[!UICONTROL 連線Mixpanel帳戶]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Mixpanel] 要用來建立新資料流的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![現有](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選擇性說明和您的認證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![新](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## 選取您的專案ID和時區 {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="为 Mixpanel 提取设置时区"
>abstract="时区必须与您的 Mixpanel 配置文件时区设置相同，因为 Platform 使用指定的项目时区来从 Mixpanel 提取相关数据。在将事件记录到 Mixpanel 数据存储之前，Mixpanel 将调整其时区以与您的项目时区协调。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html?lang=zh-Hans#project-id-and-timezone" text="请参阅文档以了解详情"

來源通過驗證後，請提供您的專案ID和時區，然後選取 **[!UICONTROL 選取]**.

您在擷取之前指定的時區 [!DNL Mixpanel] 資料傳送至Platform時，必須與您的 [!DNL Mixpanel] 設定檔時區設定。 資料時區的任何變更只會套用至新事件，而舊事件將保留在您先前指定的時區內。 [!DNL Mixpanel] 因應日光節約時間，並適當調整您的擷取時間戳記。 如需時區如何影響資料的詳細資訊，請參閱 [!DNL Mixpanel] 指南： [管理專案的時區](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel).

過了一會兒，正確的介面會更新為預覽面板，讓您在建立資料流之前先檢查結構。 完成後，選取 **[!UICONTROL 下一個]**.

![設定](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## 后续步骤

依照本教學課程，您已建立與的連線， [!DNL Mixpanel] 帳戶。 您現在可以繼續下一節教學課程和 [設定資料流以將分析資料匯入Platform](../../dataflow/analytics.md).

## 其他资源 {#additional-resources}

以下各節提供您在使用時，可參考的其他資源 [!DNL Mixpanel] 來源。

### 验证 {#validation}

以下概述驗證您已成功連線至您的主機時可採取的步驟。 [!DNL Mixpanel] 來源及 [!DNL Mixpanel] 事件正在內嵌至Platform。

在Platform UI中選取 **[!UICONTROL 資料集]** 以存取 [!UICONTROL 資料集] 工作區。 此 [!UICONTROL 資料集活動] 畫面會顯示執行的詳細資訊。

![資料集 — 活動](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

接著，選取您要檢視之資料流的資料流執行ID，以檢視有關該資料流執行的特定詳細資訊。

![資料流監視](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

最後，選取 **[!UICONTROL 預覽資料集]** 以顯示所擷取的資料。

![預覽資料集](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

您可以根據 [!DNL Mixpanel] > [!DNL Events] 頁面。 請參閱 [[!DNL Mixpanel] 事件相關檔案](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-) 以取得詳細資訊。

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Mixpanel結構描述

下表列出必須為設定的支援對應 [!DNL Mixpanel].

>[!TIP]
>
>另請參閱 [事件匯出API >下載](https://developer.mixpanel.com/reference/raw-event-export) 以取得有關API的詳細資訊。


| 来源 | 类型 |
|---|---|
| `distinct_id` | 字符串 |
| `event_name` | 字符串 |
| `import` | 布尔 |
| `insert_id` | 字符串 |
| `item_id` | 字符串 |
| `item_name` | 字符串 |
| `item_price` | 字符串 |
| `mp_api_endpoint` | 字符串 |
| `mp_api_timestamp_ms` | 整数 |
| `mp_processing_time_ms` | 整数 |
| `time` | 整数 |

### 限制 {#limits}

* 您每小時最多有100個並行查詢和60個查詢，如所示 [匯出API速率限制](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints).

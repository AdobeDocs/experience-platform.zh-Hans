---
keywords: Experience Platform；首頁；熱門主題；批次擷取；批次擷取；部分擷取；擷取錯誤；擷取錯誤；部分批次擷取；部分批次擷取；部分；擷取；
solution: Experience Platform
title: 部分批次擷取概觀
description: 本檔案提供管理部分批次擷取的教學課程。
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---

# 部分批次擷取

部分批次擷取是擷取包含錯誤的資料的能力，上限為特定臨界值。 透過此功能，使用者可以成功將其所有正確的資料擷取到Adobe Experience Platform，同時將其所有不正確的資料單獨分批處理，以及其無效原因的詳細資訊。

本檔案提供管理部分批次擷取的教學課程。

## 快速入门

本教學課程需要具備與部分批次擷取相關的各種Adobe Experience Platform服務的運作知識。 在開始本教學課程之前，請檢閱下列服務的檔案：

- [批次擷取](./overview.md)：方法： [!DNL Platform] 從資料檔案擷取及儲存資料，例如CSV和Parquet。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Platform] 組織客戶體驗資料。

以下小節提供您需瞭解的其他資訊，才能成功對進行呼叫 [!DNL Platform] API。

### 讀取範例API呼叫

本指南提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：持有人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

## 在API中啟用批次進行部分批次擷取 {#enable-api}

>[!NOTE]
>
>本節說明如何使用API為部分批次擷取啟用批次。 如需使用UI的說明，請閱讀 [在UI中啟用批次進行部分批次擷取](#enable-ui) 步驟。

您可以建立已啟用部分擷取的新批次。

若要建立新批次，請依照 [批次擷取開發人員指南](./api-overview.md). 一旦您到達 **[!UICONTROL 建立批次]** 步驟，在請求內文中新增下列欄位：

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `enableErrorDiagnostics` | 允許此功能的標幟 [!DNL Platform] 產生有關批次的詳細錯誤訊息。 |
| `partialIngestionPercent` | 整個批次失敗之前的可接受錯誤百分比。 因此，在此範例中，最多5%的批次可能是錯誤，然後才會失敗。 |


## 在UI中啟用批次進行部分批次擷取 {#enable-ui}

>[!NOTE]
>
>本節說明如何使用UI為部分批次擷取啟用批次。 如果您已使用API為部分批次擷取啟用批次，則可以跳至下一節。

若要透過啟用批次進行部分擷取 [!DNL Platform] UI後，您可以透過來源連線建立新批次、在現有資料集中建立新批次，或透過「 」建立新批次[!UICONTROL 將CSV對應至XDM流程]「。

### 建立新的來源連線 {#new-source}

若要建立新的來源連線，請依照 [來源概觀](../../sources/home.md). 一旦您到達 **[!UICONTROL 資料流詳細資料]** 步驟，記下 **[!UICONTROL 部分擷取]** 和 **[!UICONTROL 錯誤診斷]** 欄位。

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

此 **[!UICONTROL 部分擷取]** 切換可讓您啟用或停用部分批次擷取。

此 **[!UICONTROL 錯誤診斷]** 切換僅在 **[!UICONTROL 部分擷取]** 切換功能已關閉。 此功能允許 [!DNL Platform] 產生您所擷取批次的詳細錯誤訊息。 如果 **[!UICONTROL 部分擷取]** 切換功能已開啟，自動執行增強的錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

此 **[!UICONTROL 錯誤臨界值]** 可讓您設定整個批次失敗之前可接受的錯誤百分比。 預設情況下，此值會設為5%。

### 使用現有的資料集 {#existing-dataset}

若要使用現有資料集，請從選取資料集開始。 右側邊欄會填入資料集的相關資訊。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

此 **[!UICONTROL 部分擷取]** 切換可讓您啟用或停用部分批次擷取。

此 **[!UICONTROL 錯誤診斷]** 切換僅在 **[!UICONTROL 部分擷取]** 切換功能已關閉。 此功能允許 [!DNL Platform] 產生您所擷取批次的詳細錯誤訊息。 如果 **[!UICONTROL 部分擷取]** 切換功能已開啟，自動執行增強的錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

此 **[!UICONTROL 錯誤臨界值]** 可讓您設定整個批次失敗之前可接受的錯誤百分比。 預設情況下，此值會設為5%。

現在，您可以使用上傳資料 **新增資料** 按鈕，則會使用部分擷取來擷取。

### 使用&quot;[!UICONTROL 將CSV對應至XDM結構描述]&quot;流量 {#map-flow}

若要使用「[!UICONTROL 將CSV對應至XDM結構描述]&quot;流程，請依照 [對應CSV檔案教學課程](../tutorials/map-csv/overview.md). 一旦您到達 **[!UICONTROL 新增資料]** 步驟，記下 **[!UICONTROL 部分擷取]** 和 **[!UICONTROL 錯誤診斷]** 欄位。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

此 **[!UICONTROL 部分擷取]** 切換可讓您啟用或停用部分批次擷取。

此 **[!UICONTROL 錯誤診斷]** 切換僅在 **[!UICONTROL 部分擷取]** 切換功能已關閉。 此功能允許 [!DNL Platform] 產生您所擷取批次的詳細錯誤訊息。 如果 **[!UICONTROL 部分擷取]** 切換功能已開啟，自動執行增強的錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL 錯誤臨界值]** 可讓您設定整個批次失敗之前可接受的錯誤百分比。 預設情況下，此值會設為5%。

## 后续步骤 {#next-steps}

本教學課程說明如何建立或修改資料集，以啟用部分批次擷取。 如需批次擷取的詳細資訊，請閱讀 [批次擷取開發人員指南](./api-overview.md).

如需有關監控部分擷取錯誤的資訊，請參閱 [批次擷取錯誤診斷指南](../quality/error-diagnostics.md).

---
keywords: Experience Platform；首頁；熱門主題；流量服務；
title: （Beta版）使用流量服務API建立隨選擷取的流量執行
description: 本教學課程涵蓋使用流量服務API建立隨選擷取之流量執行的步驟
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: 795b1af6421c713f580829588f954856e0a88277
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 1%

---

# （測試版）使用建立隨選擷取的流程執行 [!DNL Flow Service] API

>[!IMPORTANT]
>
>隨選擷取目前為測試版，貴組織可能尚未提供存取許可權。 本檔案中說明的功能可能會有所變更。

流程執行代表流程執行的例項。 例如，如果流程排定在早上9:00、上午10:00及上午11:00每小時執行，則您會有三個流程執行例項。 流程執行是您的特定組織所專屬。

隨選擷取可讓您針對指定的資料流建立資料流執行。 這可讓您的使用者根據指定的引數建立流程執行，並建立擷取週期，而不需要服務權杖。 僅批次來源支援隨選擷取。

本教學課程涵蓋如何使用隨選擷取及使用建立流程執行的步驟。 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

>[!NOTE]
>
>為了建立資料流執行，您必須先擁有排程為一次擷取的資料流的資料流ID。

本教學課程需要您實際瞭解Adobe Experience Platform的下列元件：

* [來源](../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../landing/api-guide.md).

## 為以表格為基礎的來源建立流程執行

若要建立以表格為基礎的來源的流程，請向以下網站發出POST請求： [!DNL Flow Service] API，並提供您要對其建立執行的流量ID，以及開始時間、結束時間和差異欄的值。

>[!TIP]
>
>以表格為基礎的來源包括以下來源類別：廣告、分析、同意和偏好設定、CRM、客戶成功、資料庫、行銷自動化、付款和通訊協定。

**API格式**

```http
POST /runs/
```

**请求**

下列請求會建立流程ID的流程執行 `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>您只需提供 `deltaColumn` 建立您的第一個資料流執行時。 之後， `deltaColumn` 將修補為的一部分 `copy` 和中的轉換，將被視為真實來源。 任何變更 `deltaColumn` 流執行引數的值會產生錯誤。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567",
          "deltaColumn": {
              "name": "DOB"
          }
      }
  }'
```

| 参数 | 描述 |
| --- | --- |
| `flowId` | 要針對其建立您的流程執行的流程ID。 |
| `params.startTime` | 定義執行開始時間的整數。 值以unix epoch時間表示。 |
| `params.windowStartTime` | 整數，定義提取資料期間的視窗開始時間。 值以Unix時間表示。 |
| `params.windowEndTime` | 整數，定義提取資料期間的視窗結束時間。 值以Unix時間表示。 |
| `params.deltaColumn` | 必須有delta欄才能分割資料，並將新擷取的資料與歷史資料分開。 **注意**：此 `deltaColumn` 只有在建立您的第一個流程執行時才需要。 |
| `params.deltaColumn.name` | 差異資料行的名稱。 |

**响应**

成功的回應會傳回新建立的流程執行的詳細資訊，包括其唯一執行 `id`.

```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 新建立之流量執行的ID。 請參閱指南： [正在擷取流程規格](../api/collect/database-nosql.md#specs) 以取得以表格為基礎的執行規格的詳細資訊。 |
| `etag` | 流程執行的資源版本。 |
<!-- 
| `createdAt` | The unix timestamp that designates when the flow run was created. |
| `updatedAt` | The unix timestamp that designates when the flow run was last updated. |
| `createdBy` | The organization ID of the user who created the flow run. |
| `updatedBy` | The organization ID of the user who last updated the flow run. |
| `createdClient` | The application client that created the flow run. |
| `updatedClient` | The application client that last updated the flow run. |
| `sandboxId` | The ID of the sandbox that contains the flow run. |
| `sandboxName` | The name of the sandbox that contains the flow run. |
| `imsOrgId` | The organization ID. |
| `flowId` | The ID of the flow in which the flow run is created against. |
| `params.windowStartTime` | An integer that defines the start time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.windowEndTime` | An integer that defines the end time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.deltaColumn` | The delta column is required to partition the data and separate newly ingested data from historic data. **Note**: The `deltaColumn` is only needed when creating your firs flow run. |
| `params.deltaColumn.name` | The name of the delta column. |
| `etag` | The resource version of the flow run. |
| `metrics` | This property displays a status summary for the flow run. | -->

## 為檔案型來源建立流程執行

若要建立檔案型來源的流程，請向以下發出POST請求： [!DNL Flow Service] API，同時提供您要針對其建立執行的流程ID，以及開始時間和結束時間的值。

>[!TIP]
>
>檔案型來源包含所有雲端儲存空間來源。

**API格式**

```http
POST /runs/
```

**请求**

下列請求會建立流程ID的流程執行 `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| 参数 | 描述 |
| --- | --- |
| `flowId` | 要針對其建立您的流程執行的流程ID。 |
| `params.startTime` | 定義執行開始時間的整數。 值以unix epoch時間表示。 |
| `params.windowStartTime` | 整數，定義提取資料期間的視窗開始時間。 值以Unix時間表示。 |
| `params.windowEndTime` | 整數，定義提取資料期間的視窗結束時間。 值以Unix時間表示。 |

**响应**

成功的回應會傳回新建立的流程執行的詳細資訊，包括其唯一執行 `id`.


```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 新建立之流量執行的ID。 請參閱指南： [正在擷取流程規格](../api/collect/database-nosql.md#specs) 以取得以表格為基礎的執行規格的詳細資訊。 |
| `etag` | 流程執行的資源版本。 |

## 監視您的流量執行

建立流程執行後，您可以監視透過它擷取的資料，以檢視有關流程執行、完成狀態和錯誤的資訊。 若要使用API監控您的流量執行，請參閱以下主題上的教學課程： [監視API中的資料流 ](./monitor.md). 若要使用Platform UI監控您的流量執行，請參閱以下指南： [使用監視儀表板監視來源資料流](../../../dataflows/ui/monitor-sources.md).

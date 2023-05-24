---
keywords: Experience Platform；首頁；熱門主題；監控資料流；流程服務api；流程服務
solution: Experience Platform
title: 使用流量服務API監控資料流
type: Tutorial
description: 本教學課程涵蓋使用流量服務API監控流量執行資料的完整性、錯誤和量度的步驟。
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# 使用流量服務API監控資料流

Adobe Experience Platform可從外部來源擷取資料，同時讓您能夠使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。 此外，Experience Platform可讓外部合作夥伴啟用資料。

[!DNL Flow Service] 用於收集及集中Adobe Experience Platform內各種不同來源的客戶資料。 此服務提供可連線所有支援來源和目的地的使用者介面和RESTful API。

本教學課程涵蓋監控流程執行資料的步驟，瞭解資料的完整性、錯誤及使用下列專案的量度： [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本教學課程要求您具備有效資料流的ID值。 如果您沒有有效的資料流ID，請從「 」中選擇您選擇的聯結器 [來源概觀](../../sources/home.md) 或 [目的地概觀](../../destinations/catalog/overview.md) 並依照在嘗試本教學課程之前概述的步驟進行。

本教學課程也要求您實際瞭解Adobe Experience Platform的下列元件：

- [目的地](../../destinations/home.md)：目的地是預先建立的與常用應用程式的整合，可讓您順暢地從Platform啟用資料，用於跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例。
- [來源](../../sources/home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供您需要瞭解的其他資訊，才能使用成功監視流量執行 [!DNL Flow Service] API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括屬於 [!DNL Flow Service]，會隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

- `Content-Type: application/json`

## 監視流量執行

GET建立資料流後，請對 [!DNL Flow Service] API。

**API格式**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 唯一 `id` 您要監控之資料流的值。 |

**请求**

以下請求會擷取現有資料流的規格。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功回應會傳回有關您資料流執行的詳細資訊，包括其建立日期、來源和目標連線以及資料流執行的唯一識別碼(`id`)。

```json
{
    "items": [
        {
            "id": "65b7cfcc-6b2e-47c8-8194-13005b792752",
            "createdAt": 1607520228894,
            "updatedAt": 1607520276948,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "prod",
            "imsOrgId": "{ORG_ID}",
            "flowId": "f00c8762-df2f-432b-a7d7-38999fef5e8e",
            "etag": "\"560266dc-0000-0200-0000-5fd0d0140000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1607520205922,
                    "completedAtUTC": 1607520262413
                },
                "sizeSummary": {
                    "inputBytes": 87885,
                    "outputBytes": 56730
                },
                "recordSummary": {
                    "inputRecordCount": 26758,
                    "outputRecordCount": 26758,
                    "failedRecordCount": 0
                },
                "fileSummary": {
                    "inputFileCount": 11,
                    "outputFileCount": 11,
                    "activityRefs": [
                        "37b34f84-1ada-11eb-adc1-0242ac120002"
                    ]
                },
                "statusSummary": {
                    "status": "success"
                }
            },
            "activities": [
                {
                    "id": "4f008a00-3a04-11eb-adc1-0242ac120002",
                    "name": "Copy Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520205922,
                        "completedAtUTC": 1607520236968
                    },
                    "sizeSummary": {
                        "inputBytes": 87885,
                        "outputBytes": 87885
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 11
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                },
                {
                    "id": "37b34f84-1ada-11eb-adc1-0242ac120002",
                    "name": "Promotion Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520244985,
                        "completedAtUTC": 1607520262413
                    },
                    "sizeSummary": {
                        "inputBytes": 26758,
                        "outputBytes": 56730
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758,
                        "failedRecordCount": 0
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 2,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01ES3TRN69E9W2DZ770XCGYAH1/meta?path=input_files",
                                "pathPrefix": "bucket1/csv_test/"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                }
            ]
        }
    ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `items` | 包含與您特定流程執行相關聯的單一中繼資料裝載。 |
| `metrics` | 資料流執行中的資料特徵。 |
| `activities` | 顯示資料的轉換方式。 |
| `durationSummary` | 流程執行的開始和結束時間。 |
| `sizeSummary` | 以位元組為單位的資料量。 |
| `recordSummary` | 資料的記錄計數。 |
| `fileSummary` | 資料的檔案計數。 |
| `fileSummary.extensions` | 包含活動專屬的資訊。 例如， `manifest` 只是「促銷活動」的一部分，因此也包含在 `extensions` 物件。 |
| `statusSummary` | 顯示流程執行是成功還是失敗。 |

## 后续步骤

依照本教學課程，您已使用擷取資料流中的量度和錯誤資訊 [!DNL Flow Service] API。 您現在可以繼續根據擷取排程監控資料流，以追蹤其狀態和擷取率。 如需如何監控來源資料流的詳細資訊，請參閱 [使用使用者介面監控來源的資料流](../ui/monitor-sources.md) 教學課程。 如需如何監控目的地的資料流的詳細資訊，請參閱 [使用使用者介面監控目的地的資料流](../ui/monitor-destinations.md) 教學課程。

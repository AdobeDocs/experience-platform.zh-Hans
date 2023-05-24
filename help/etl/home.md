---
keywords: Experience Platform；首頁；熱門主題；ETL；etl；ETL整合；ETL整合
solution: Experience Platform
title: 為Adobe Experience Platform開發ETL整合
description: ETL整合指南概述建立高效能、安全聯結器以進行Experience Platform並將資料擷取到Platform的一般步驟。
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '4081'
ht-degree: 1%

---

# 為Adobe Experience Platform開發ETL整合

ETL整合指南概述了為建立高效能、安全聯結器的一般步驟。 [!DNL Experience Platform] 並將資料擷取到 [!DNL Platform].


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Batch Ingestion]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [[!DNL Streaming Ingestion]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Experience Platform API的驗證和授權](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

本指南也包含設計ETL聯結器時要使用的範例API呼叫，以及概述每個呼叫的說明檔案連結 [!DNL Experience Platform] 以及其API的使用提供詳細資訊。

範例整合可在以下網址取得： [!DNL GitHub] 透過 [ETL生態系統整合參考代碼](https://github.com/adobe/acp-data-services-etl-reference) 在 [!DNL Apache] 授權版本2.0。

## 工作流

下列工作流程圖表提供Adobe Experience Platform元件與ETL應用程式和聯結器整合的整體概觀。

![](images/etl.png)

## Adobe Experience Platform元件

ETL聯結器整合涉及多個Experience Platform元件。 下列清單概述數個主要元件和功能：

- **AdobeIdentity Management系統(IMS)**  — 提供Adobe服務驗證的架構。
- **IMS組織**  — 可擁有或授權產品及服務並允許存取其成員的企業實體。
- **IMS使用者** - IMS組織的成員。 組織與使用者的關係是多對多。
- **[!DNL Sandbox]**  — 單一虛擬磁碟分割 [!DNL Platform] 執行個體，協助開發及改進數位體驗應用程式。
- **資料探索**  — 在中記錄所擷取和轉換資料的中繼資料 [!DNL Experience Platform].
- **[!DNL Data Access]**  — 為使用者提供存取其資料的介面，位於 [!DNL Experience Platform].
- **[!DNL Data Ingestion]**  — 推送資料至 [!DNL Experience Platform] 替換為 [!DNL Data Ingestion] API。
- **[!DNL Schema Registry]**  — 定義並儲存描述要用於下列專案的資料結構的結構描述： [!DNL Experience Platform].

## 開始使用 [!DNL Experience Platform] API

以下小節提供您需瞭解或掌握的其他資訊，才能成功對進行呼叫 [!DNL Experience Platform] API。

### 讀取範例API呼叫

本指南提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：持有人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../sandboxes/home.md).

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的標頭：

- Content-Type： application/json

## 一般使用者流程

若要開始，ETL使用者需登入 [!DNL Experience Platform] 使用者介面(UI)並建立資料集，以使用標準聯結器或推送服務聯結器擷取。

在UI中，使用者透過選取資料集結構描述來建立輸出資料集。 結構描述的選擇取決於要擷取的資料型別（記錄或時間序列） [!DNL Platform]. 按一下UI內的「結構描述」索引標籤，使用者就可以檢視所有可用的結構描述，包括結構描述支援的行為型別。

在ETL工具中，使用者將在設定適當的連線（使用其憑證）後，開始設計其對應轉換。 假設ETL工具已經具有 [!DNL Experience Platform] 聯結器已安裝（本整合指南中未定義程式）。

範例ETL工具和工作流程的模型已提供在 [ETL工作流程](./workflow.md). 雖然ETL工具在格式上可能有所不同，但大多數工具都會公開類似的功能。

>[!NOTE]
>
>ETL聯結器必須指定時間戳記篩選條件，以標示擷取資料和位移的日期(即要讀取其資料的視窗)。 ETL工具應支援在這個或其他相關UI中取得這兩個引數。 在Adobe Experience Platform中，這些引數將會對應至可用日期（如果存在）或資料集批次物件中的擷取日期。

### 檢視資料集清單

使用對應資料來源，即可使用擷取所有可用資料集的清單。 [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

您可以發出單一API請求來檢視所有可用的資料集(例如 `GET /dataSets`)，最佳作法是加入查詢引數，以限制回應大小。

在請求完整資料集資訊的情況下，回應裝載的大小可能超過3GB，這可能會降低整體效能。 因此，使用查詢引數來篩選所需的資訊將會 [!DNL Catalog] 查詢更有效率。

#### 清單篩選

篩選回應時，您可以使用&amp;符號(`&`)。 有些查詢引數會接受逗號分隔的值清單，例如以下範例請求中的「屬性」篩選器。

[!DNL Catalog] 回應會根據設定的限制自動計量，但「limit」查詢引數可用於自訂限制並限制傳回的物件數。 預先設定的 [!DNL Catalog] 回應限製為：

- 如果未指定限制引數，則每個回應裝載的物件數目上限為20。
- 所有其他專案的全域限制 [!DNL Catalog] 查詢是100個物件。
- 對於資料集查詢，如果使用properties查詢引數請求observableSchema，則傳回的資料集數量上限為20。
- 無效的限制引數(包括 `limit=0`)會發生HTTP 400錯誤，此錯誤會概述適當的範圍。
- 如果限制或位移是以查詢引數的形式傳遞，則優先於以標頭傳遞的限制或位移。

如需查詢引數的詳細資訊，請參閱 [目錄服務概觀](../catalog/home.md).

**API格式**

```http
GET /catalog/dataSets
GET /catalog/dataSets?{filter1}={value1},{value2}&{filter2}={value3}
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3&properties=name,description,schemaRef" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

請參閱 [目錄服務概觀](../catalog/home.md) 以取得如何呼叫 [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

**响应**

回應包括三項(`limit=3`)資料集顯示的「name」、「description」和「schemaRef」，如 `properties` 查詢引數。

```json
{
    "5b95b155419ec801e6eee780": {
        "name": "Store Transactions",
        "description": "Retails Store Transactions",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c351fa2f5fee300000fa9e8": {
        "name": "Loyalty Members",
        "description": "Loyalty Program Members",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c1823b19e6f400000993885": {
        "name": "Web Traffic",
        "description": "Retail Web Traffic",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2025a705890c6d4a4a06b16f8cf6f4ca",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

### 檢視資料集結構描述

資料集的「schemaRef」屬性包含參照資料集所依據的XDM架構的URI。 XDM結構描述(「schemaRef」)代表資料集可以使用的所有潛在欄位，不一定是正在使用的欄位（請參閱下面的「observableSchema」）。

XDM結構描述是您需要向使用者呈現所有可寫入可用欄位清單時使用的結構描述。

上一個回應物件中的第一個「schemaRef.id」值(`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`)是URI，指向 [!DNL Schema Registry]. 您可以向以下專案提出查詢(GET)請求，以擷取結構描述： [!DNL Schema Registry] API。

>[!NOTE]
>
>「schemaRef」屬性會取代現已被取代的「schema」屬性。 如果資料集中不存在&quot;schemaRef&quot;或不包含值，您將需要檢查&quot;schema&quot;屬性是否存在。 可透過在中將「schemaRef」取代為「schema」來完成 `properties` 上一個呼叫中的查詢引數。 有關「schema」屬性的詳細資訊，請參閱 [資料集「結構描述」屬性](#dataset-schema-property-deprecated---eol-2019-05-30) 下一節。

**API格式**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**请求**

請求會使用編碼的URL `id` 結構描述的URI （「schemaRef.id」屬性的值），並需要Accept標頭。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

回應格式取決於請求中傳送的Accept標頭型別。 查詢請求還需要 `version` 包含在Accept標頭中。 下表概述可用於查閱的Accept標頭：

| Accept | 描述 |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | 清單(GET)請求、標題、ID和版本 |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs和allOf已解決，有標題和說明 |
| `application/vnd.adobe.xed+json; version={major version}` | 以$ref和allOf為原始，提供標題和說明 |
| `application/vnd.adobe.xed-notext+json; version={major version}` | 含$ref和allOf的原始，無標題或說明 |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs和allOf已解決，無標題或說明 |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs和allOf已解決，包括描述元 |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` 和 `application/vnd.adobe.xed-full+json; version={major version}` 是最常用的Accept標頭。 `application/vnd.adobe.xed-id+json` 建議在下列位置列出資源： [!DNL Schema Registry] 因為它只會傳回「title」、「id」和「version」。 `application/vnd.adobe.xed-full+json; version={major version}` 偏好使用它來檢視特定資源（依其「id」），因為它會傳回所有欄位（巢狀於「屬性」下方），以及標題和說明。

**响应**

傳回的JSON結構描述描述了結構和欄位層級資訊（「型別」、「格式」、「最小值」、「最大值」等） 的資料中，已序列化為JSON。 如果內嵌使用JSON以外的序列化格式（例如Parquet或Scala），則 [結構描述登入指南](../xdm/tutorials/create-schema-api.md) 包含一個表格，顯示所需的JSON型別(&quot;meta：xdmType&quot;)及其在其他格式中的對應表示法。

連同此表格， [!DNL Schema Registry] 開發人員指南包含可使用進行的所有可能呼叫的深入範例。 [!DNL Schema Registry] API。

### 資料集「schema」屬性（已棄用 — EOL 2019-05-30）

資料集可能包含「結構描述」屬性，該屬性現在已被取代，並暫時可用於回溯相容性。 例如，與先前請求相似的清單(GET)請求，其中「schema」取代了 `properties` 查詢引數可能會傳回以下內容：

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

如果填入資料集的「schema」屬性，表示該結構描述已過時 `/xdms` 綱要，並且在支援的情況下，ETL聯結器應使用&quot;schema&quot;屬性中的值搭配 `/xdms` 端點(以下位置中已被取代的端點： [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/))以擷取舊版結構描述。

**API格式**

```http
GET /catalog/{"schema" property without the "@"}
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE]
>
>選用的查詢引數， `expansion=xdm`，會告知API完全展開並內嵌任何參考的結構描述。 在向使用者展示所有潛在欄位清單時，您可能想要這麼做。

**响应**

與的步驟類似 [檢視資料集結構](#view-dataset-schema)，回應會包含JSON結構描述，說明序列化為JSON之資料的結構和欄位層級資訊。

>[!NOTE]
>
>當「schema」欄位空白或完全不存在時，聯結器應讀取「schemaRef」欄位並使用 [結構描述登入API](https://www.adobe.io/experience-platform-apis/references/schema-registry/) 如先前步驟所示， [檢視資料集結構](#view-dataset-schema).

### &quot;observableSchema&quot;屬性

資料集的「observableSchema」屬性的JSON結構與XDM結構描述JSON的結構相符。 「observableSchema」包含傳入輸入檔案中存在的欄位。 將資料寫入時 [!DNL Experience Platform]，使用者不需要使用目標結構描述中的每個欄位。 相反地，他們應該只提供正在使用的欄位。

可觀察結構描述是您在讀取資料或顯示可讀取/對應之欄位清單時，所使用的結構描述。

```json
{
    "598d6e81b2745f000015edcb": {
        "observableSchema": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "name": {
                    "type": "string",
                },
                "age": {
                    "type": "string",
                }
            }
        }
    }
}
```

### 预览数据

ETL應用程式可提供預覽資料的功能([ETL工作流程中的「圖8」](./workflow.md))。 資料存取API提供數個選項來預覽資料。

其他資訊，包括使用資料存取API預覽資料的逐步指南，請參閱 [資料存取教學課程](../data-access/tutorials/dataset-data.md).

### 使用「屬性」查詢引數取得資料集詳細資訊

如上述步驟所示，將目標設定為 [檢視資料集清單](#view-list-of-datasets)，您可使用「properties」查詢引數來請求「files」。

您可參閱 [目錄服務概觀](../catalog/home.md) 以取得關於查詢資料集和可用回應篩選器的詳細資訊。

**API格式**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**响应**

回應將包含一個資料集(`limit=1`)顯示「檔案」屬性。

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### 使用「檔案」屬性列出資料集檔案

您也可以使用GET請求，以使用「檔案」屬性來擷取檔案詳細資訊。

**API格式**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**响应**

回應會將資料集檔案ID納入頂層屬性，且檔案詳細資料包含在資料集檔案ID物件中。

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542749145828,
        "updated": 1542749145828
    },
    "14d5758c107443e1a83c714e56ca79d0-1": {
        "batchId": "14d5758c107443e1a83c714e56ca79d0",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542752699111,
        "updated": 1542752699111
    },
    "ea40946ac03140ec8ac4f25da360620a-1": {
        "batchId": "ea40946ac03140ec8ac4f25da360620a",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542756935535,
        "updated": 1542756935535
    }
}
```

### 擷取檔案詳細資料

先前回應中傳回的資料集檔案ID可用於GET請求，以透過 [!DNL Data Access] API。

此 [資料存取總覽](../data-access/home.md) 包含有關如何使用 [!DNL Data Access] API。

**API格式**

```http
GET /export/files/{DATASET_FILE_ID}
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**响应**

```json
[
    {
    "name": "{FILE_NAME}.parquet",
    "length": 2576,
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet"
            }
        }
    }
]
```

### 預覽檔案資料

「href」屬性可用來透過擷取預覽資料 [[!DNL Data Access API]](../data-access/home.md).

**API格式**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

對上述要求的回應將包含檔案內容的預覽。

有關以下專案的更多資訊： [!DNL Data Access] API （包括詳細的請求和回應）可在 [資料存取總覽](../data-access/home.md).

### 從資料集取得「fileDescription」

作為轉換後資料輸出的目標元件，資料工程師將選擇輸出資料集([ETL工作流程中的「圖12」](workflow.md))。 XDM結構描述與輸出資料集相關聯。 要寫入的資料將由資料集API中資料集實體的「fileDescription」屬性識別。 這項資訊可使用資料集ID (`{DATASET_ID}`)。 JSON回應中的「fileDescription」屬性將提供要求的資訊。

**API格式**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{DATASET_ID}` | 此 `id` 您嘗試存取之資料集的值。 |

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
```

**响应**

```JSON
{
  "59c93f3da7d0c00000798f68": {
    "version": "1.0.4",
    "fileDescription": {
        "persisted": false,
        "format": "parquet"
    }
  }
}
```

資料將寫入 [!DNL Experience Platform] 使用 [批次擷取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).  寫入資料是一個非同步過程。 將資料寫入Adobe Experience Platform時，只有在資料完全寫入後，才會建立批次並標籤為成功。

資料輸入 [!DNL Experience Platform] 應該以Parquet檔案的形式撰寫。

## 執行階段

執行開始時，聯結器（如來源元件中所定義）會從讀取資料 [!DNL Experience Platform] 使用 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/). 轉換程式會讀取特定時間範圍內的資料。 在內部，它會查詢批次的來源資料集。 進行查詢時，它會使用引數化（針對時間序列資料或增量資料滾動）開始日期，並列出這些批次的資料集檔案，並開始為這些資料集檔案提出資料請求。

### 轉換範例

此 [範例ETL轉換](./transformations.md) 檔案包含許多轉換範例，包括身分處理和資料型別對應。 請參考這些轉換。

### 讀取資料來源 [!DNL Experience Platform]

使用 [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)中，您可以擷取指定開始時間和結束時間之間的所有批次，並依照其建立順序排序。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

有關篩選批次的詳細資訊，請參閱 [資料存取教學課程](../data-access/tutorials/dataset-data.md).

### 從批次中取得檔案

當您擁有要尋找之批次的ID後(`{BATCH_ID}`)，則可能透過以下動作擷取屬於特定批次的檔案清單： [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/).  欲知詳情，請參閱 [[!DNL Data Access] 教學課程](../data-access/tutorials/dataset-data.md).

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### 使用檔案ID存取檔案

使用檔案的唯一ID (`{FILE_ID`)， [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 可用來存取檔案的特定詳細資料，包括其名稱、大小（位元組）及下載連結。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

回應可能指向單一檔案或目錄。 如需各個專案的詳細資訊，請參閱 [[!DNL Data Access] 教學課程](../data-access/tutorials/dataset-data.md).

### 存取檔案內容

此 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 可用來存取特定檔案的內容。 若要擷取內容，會使用傳回的值發出GET請求 `_links.self.href` 使用檔案ID存取檔案時。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

此要求的回應包含檔案內容。 如需詳細資訊，包括回應分頁的詳細資訊，請參閱 [如何透過資料存取API查詢資料](../data-access/tutorials/dataset-data.md) 教學課程。

### 驗證記錄以符合結構描述

寫入資料時，使用者可以選擇根據XDM結構描述中定義的驗證規則來驗證資料。 有關結構描述驗證的更多資訊可在以下網址找到： [上的ETL生態系統整合參考代碼 [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

如果您使用的參考實作位於 [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md)，您可使用系統屬性在此實作中開啟結構描述驗證 `-DenableSchemaValidation=true`.

可以使用屬性（例如）對邏輯XDM型別執行驗證 `minLength` 和 `maxlength` 對於字串， `minimum` 和 `maximum` 用於整數等。 此 [Schema Registry API開發人員指南](../xdm/api/getting-started.md) 包含一個表格，其中概述XDM型別以及可用於驗證的屬性。

>[!NOTE]
>
>為各種專案提供的最小值和最大值 `integer` 型別是該型別可以支援的MIN和MAX值，但這些值可以進一步限製為您選擇的最小值和最大值。

### 建立批次

處理完資料後，ETL工具會將資料寫回 [!DNL Experience Platform] 使用 [批次擷取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). 在將資料新增到資料集之前，必須將其連結到批次，該批次稍後將上傳到特定資料集中。

**请求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

建立批次的詳細資訊，包括範例請求和回應，請參見 [批次擷取概觀](../ingestion/batch-ingestion/overview.md).

### 寫入資料集

成功建立新批次後，檔案可以上傳到特定資料集。 可以在批次中張貼多個檔案，直到升級為止。 您可以使用小型檔案上傳API上傳檔案；但是，如果您的檔案太大，並且已超過閘道限制，則可以使用大型檔案上傳API。 有關同時使用大型和小型檔案上傳的詳細資訊，請參閱 [批次擷取概觀](../ingestion/batch-ingestion/overview.md).

**请求**

資料輸入 [!DNL Experience Platform] 應該以Parquet檔案的形式撰寫。

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{ORG_ID}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### 標籤批次上傳完成

將所有檔案上傳至批次後，可以發出完成批次的訊號。 藉由執行此動作， [!DNL Catalog] 系統會為完成的檔案建立「DataSetFile」專案，並與產生批次相關聯。 此 [!DNL Catalog] 然後批次會標籤為成功，這會觸發下游資料流擷取可用資料。

資料會先在Adobe Experience Platform上的測試位置著陸，然後在編目和驗證後，移至最終位置。 當所有資料移至永久位置後，批次將被標籤為成功。

**请求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

如果成功，回應會傳回HTTP Status 200 OK，且回應本文會是空的。

ETL工具會確保在讀取資料時記下來源資料集的時間戳記。

在下一次轉換執行中（可能透過排程或事件引發），ETL將開始從先前儲存的時間戳記及所有後續資料請求資料。

### 取得上一個批次狀態

在ETL工具中執行新工作之前，您必須確定上一個批次已成功完成。 此 [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) 提供批次特定選項，可提供相關批次的詳細資訊。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**响应**

如果前一個批次「狀態」值為「成功」，則可排程新任務，如下所示：

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "CLIENT_USER_ID@AdobeID",
    "updatedUser": "CLIENT_USER_ID@AdobeID",
    "updated": 1494349963467,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

### 依ID取得上一個批次狀態

個別批次狀態可透過以下方式擷取： [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) 透過發出GET請求，使用 `{BATCH_ID}`. 此 `{BATCH_ID}` 會與建立批次時傳回的ID相同。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**回應 — 成功**

下列回應顯示「成功」：

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

**回應 — 失敗**

如果失敗，「錯誤」可以從回應中擷取，並出現在ETL工具上作為錯誤訊息。

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "failure",
    "errors": [
        {
            "code": "200",
            "description": "Error in validating schema for file: 'adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv' with errorMessage=adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv is not a Parquet file. expected magic number at tail [80, 65, 82, 49] but found [57, 98, 55, 10] and errorType=java.lang.RuntimeException",
            "rows": []
        }
    ],
    "version": "1.0.1",
    "availableDates": {}
}
```

## 增量與快照資料，事件與設定檔

資料可以二乘二的矩陣來表示，如下所示：

| 增量事件 | 增量設定檔 |
|-------------------------------|----------------------|
| 快照事件（不太可能發生） | 快照集設定檔 |

事件資料通常是在每列中有索引時間戳記欄時。

設定檔資料通常會在資料中沒有時間戳記時，而且每一列都可由主要/複合索引鍵識別。

增量資料是指只有新增/更新資料才會進入系統，並附加至資料集中目前資料的位置。

快照資料是指所有資料都進入系統，並取代資料集中部分或所有先前資料的時間。

若是增量事件，ETL工具應使用批次實體的可用日期/建立日期。 若是推送服務，則不會出現可用日期，因此工具會使用批次建立/更新日期來標示增量。 每批次的增量事件都需要處理。

對於增量設定檔，ETL工具將使用批次實體的建立/更新日期。 通常需要處理每個增量設定檔資料批次。

由於資料規模龐大，發生快照事件的可能性極低。 但是，如果必須這樣做，則ETL工具必須僅挑選最後一個批次進行處理。

使用快照設定檔時，ETL工具必須挑選到達系統的最後一批資料。 但如果需要追蹤變更的版本，則需要處理所有批次。 ETL程式中的重複資料刪除處理有助於控制儲存成本。

## 批次重播和資料重新處理

當使用者端發現過去「n」天內，ETL處理的資料未如預期發生，或來源資料本身可能不正確，此時可能需要批次重播和重新處理資料。

若要這麼做，使用者端的資料管理員將使用 [!DNL Platform] 用於移除包含損壞資料的批次的UI。 之後，可能需要重新執行ETL，因此會使用正確的資料重新填入。 如果來源本身有損壞的資料，資料工程師/管理員將需要更正來源批次，並重新內嵌資料(或是透過Adobe Experience Platform或ETL聯結器)。

根據產生的資料型別，資料工程師會選擇從特定資料集中移除單一批次或所有批次。 資料將移除/封存為 [!DNL Experience Platform] 准則。

在某些情況下，清除資料的ETL功能可能會很重要。

清除完成後，使用者端管理員必須重新設定Adobe Experience Platform，從批次刪除時起重新開始處理核心服務。

## 並行批次處理

根據使用者端的決定，資料管理員/工程師可能會決定依序或並行方式擷取、轉換和載入資料，端視特定資料集的特性而定。 這也將根據使用者端使用轉換後的資料定位的使用案例。

例如，如果使用者端持續儲存至可更新的持續性存放區，並且事件的順序或順序很重要，則使用者端可能需要嚴格處理具有循序ETL轉換的工作。

在其他情況下，使用指定時間戳記在內部排序的下游應用程式/程式可以處理順序錯亂的資料。 在這些情況下，平行ETL轉換對於改善處理時間可能是可行的。

對於來源批次，它將再次取決於使用者端偏好設定和使用者限制。 如果來源資料可以並行擷取，而不考慮資料列的區域/順序，則轉換程式可以建立平行程度較高的處理批次（根據順序錯的處理進行最佳化）。 但是，如果轉換必須遵循時間戳記或變更優先順序，資料存取API或ETL工具排程器/呼叫必須儘可能確保批次處理不會順序混亂。

## 遞延

延遲是輸入資料尚未完成到無法傳送給下遊程式，但日後可能可以使用的程式。 客戶將決定其未來比對資料視窗的個別容忍度與處理成本，以告知其決定擱置資料並在下一次轉換執行中重新處理，希望可以在保留視窗內的某個未來時間擴充及協調/彙整。 此週期會持續進行，直到資料列處理足夠或被視為過時而無法繼續投資為止。 每個反複專案都會產生延遲資料，這是先前反複專案中所有延遲資料的超集。

Adobe Experience Platform目前無法識別延期的資料，因此使用者端實作必須依賴ETL和資料集手動設定，才能在中建立另一個資料集 [!DNL Platform] 映象可用於保留延遲資料的來源資料集。 在這種情況下，延期的資料將會類似於快照集資料。 每次執行ETL轉換時，來源資料都會與延遲的資料合併，然後傳送以進行處理。

## Changelog

| 日期 | 操作 | 描述 |
| ---- | ------ | ----------- |
| 2019-01-19 | 已從資料集中移除「欄位」屬性 | 資料集之前包含的「欄位」屬性包含結構描述的副本。 此功能不應再使用。 如果找到「fields」屬性，則應忽略該屬性，並改用「observedSchema」或「schemaRef」。 |
| 2019-03-15 | 「schemaRef」屬性已新增至資料集 | 資料集的「schemaRef」屬性包含參照資料集所依據的XDM架構的URI，並代表資料集可使用的所有潛在欄位。 |
| 2019-03-15 | 所有一般使用者識別碼都會對應至「identityMap」屬性 | 「identityMap」是主體所有唯一識別碼（例如CRM ID、ECID或忠誠度計畫ID）的封裝。 此地圖使用者： [[!DNL Identity Service]](../identity-service/home.md) 解析主體所有已知和匿名的身分識別，為每位使用者形成一個身分圖表。 |
| 2019-05-30 | EOL並從資料集中移除「結構描述」屬性 | 資料集「schema」屬性提供使用已棄用之結構描述的參考連結 `/xdms` 中的端點 [!DNL Catalog] API。 這已由「schemaRef」取代，提供「id」、「version」和「contentType」的結構描述，如新結構描述中所參照 [!DNL Schema Registry] API。 |

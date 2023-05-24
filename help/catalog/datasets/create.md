---
keywords: Experience Platform；首頁；熱門主題；資料集；資料集；建立資料集；建立資料集
solution: Experience Platform
title: 使用API建立資料集
description: 本檔案提供使用Adobe Experience Platform API建立資料集以及使用檔案填入資料集的一般步驟。
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 1%

---

# 使用API建立資料集

本檔案提供使用Adobe Experience Platform API建立資料集以及使用檔案填入資料集的一般步驟。

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [批次擷取](../../ingestion/batch-ingestion/overview.md)： [!DNL Experience Platform] 可讓您將資料內嵌為批次檔案。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供您需瞭解的其他資訊，才能成功對 [!DNL Platform] API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的標頭：

* Content-Type： application/json

## 教程

若要建立資料集，必須先定義結構描述。 結構是一組規則，可協助表示資料。 除了說明資料結構外，結構描述還提供可以套用和用來驗證在系統之間行動資料的限制和期望。

這些標準定義可讓資料以一致的方式解譯，無論其來源為何，並移除跨應用程式翻譯的需求。 如需撰寫結構描述的詳細資訊，請參閱 [結構描述組合基本概念](../../xdm/schema/composition.md)

## 查詢資料集結構描述

本教學課程的開頭為 [結構描述登入API教學課程](../../xdm/tutorials/create-schema-api.md) 結束，並利用在該教學課程中建立的熟客會員結構。

如果您尚未完成 [!DNL Schema Registry] 教學課程，請從這裡開始，並在您撰寫了必要的結構描述後，再繼續此資料集教學課程。

以下呼叫可用於檢視您在 [!DNL Schema Registry] API教學課程：

**API格式**

```HTTP
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

回應物件的格式取決於請求中傳送的Accept標頭。 此回應中的個別屬性已最小化空間。

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {},
        "repositoryLastModifiedBy": {},
        "createdByBatchID": {},
        "modifiedByBatchID": {},
        "_repo": {},
        "identityMap": {},
        "_id": {},
        "timeSeriesEvents": {},
        "person": {},
        "homeAddress": {},
        "personalEmail": {},
        "homePhone": {},
        "mobilePhone": {},
        "faxPhone": {},
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "title": "Loyalty",
                    "description": "Loyalty Info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## 建立資料集

備妥忠誠度會員方案後，您現在可以建立參考該方案的資料集。

**API格式**

```HTTP
POST /dataSets
```

**请求**

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| 属性 | 描述 |
| --- | --- |
| `schemaRef.id` | URI `$id` 資料集將依據的XDM結構描述值。 |
| `schemaRef.contentType` | 表示結構描述的格式和版本。 請參閱以下小節： [結構描述版本設定](../../xdm/api/getting-started.md#versioning) XDM API指南中取得更多資訊。 |

>[!NOTE]
>
>本教學課程使用 [Apache Parquet](https://parquet.apache.org/docs/) 檔案格式的所有範例。 以下是使用JSON檔案格式的範例： [批次擷取開發人員指南](../../ingestion/batch-ingestion/api-overview.md)

**响应**

成功的回應會傳回HTTP Status 201 （已建立）和一個回應物件，該回應物件包含一個陣列，其中包含以格式建立的新資料集的ID `"@/datasets/{DATASET_ID}"`. 資料集ID是系統產生的唯讀字串，用來參考API呼叫中的資料集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## 建立批次

您必須先建立連結至資料集的批次，才能將資料新增至資料集。 然後，該批次將用於上傳。

**API格式**

```HTTP
POST /batches
```

**请求**

請求內文包含「datasetId」欄位，其值為 `{DATASET_ID}` 產生於上一個步驟。

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**响应**

成功的回應會傳回HTTP狀態201 （已建立）以及包含新建立批次詳細資訊的回應物件，包括其 `id`，系統產生的唯讀字串。

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```

## 將檔案上傳至批次

成功建立要上傳的新批次後，您現在可以將檔案上傳到特定資料集。 請務必記住，定義資料集時，已將檔案格式指定為Parquet。 因此，您上傳的檔案必須使用該格式。

>[!NOTE]
>
>支援的最大資料上傳檔案為512 MB。 如果您的資料檔案大於此值，則需要將其分成不大於512 MB的區塊，以便一次上傳一個。 您可以使用相同的批次ID對每個檔案重複此步驟，將每個檔案上傳到相同的批次中。 如果檔案可作為批次的一部分上傳，則數量沒有限制。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{BATCH_ID}` | 此 `id` 您上傳到的批次的。 |
| `{DATASET_ID}` | 此 `id` 批次將保留在的資料集內。 |
| `{FILE_NAME}` | 您正在上傳的檔案名稱。 |

**请求**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**响应**

成功上傳的檔案會傳回空白的回應內文和HTTP狀態200 （確定）。

## 訊號批次完成

將所有資料檔案上傳至批次後，您可以發出完成批次的訊號。 訊號完成導致服務建立 [!DNL Catalog] `DataSetFile` 上傳檔案的專案，並將其與先前產生的批次建立關聯。 此 [!DNL Catalog] 批次標籤為成功，這會觸發任何下游流程，這些流程隨後可以使用現在可用的資料。

**API格式**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 参数 | 描述 |
| --- | --- |
| `{BATCH_ID}` | 此 `id` 標示為完成的批次。 |

**请求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**响应**

成功完成的批次會傳回空白的回應本文和HTTP狀態200 （確定）。

## 監視內嵌

根據資料的大小，批次擷取的時間長度各不相同。 您可以藉由附加 `batch` 將包含批次ID的請求引數新增至 `GET /batches` 要求。 API會輪詢資料集從擷取到批次的狀態，直到 `status` 回應中會指出已完成（「成功」或「失敗」）。

**API格式**

```HTTP
GET /batches?batch={BATCH_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{BATCH_ID}` | 此 `id` 您想要監控的批次的。 |

**请求**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**响应**

正面回應會傳回物件及其 `status` 屬性值為的屬性 `success`：

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{ORG_ID}",
        "created": 1534142888068,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1534142955152,
        "replay": {},
        "status": "success",
        "errors": [],
        "version": "1.0.3",
        "availableDates": {},
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "metrics": {
            "startTime": 1534142943819,
            "endTime": 1534142951760,
            "recordsRead": 108,
            "recordsWritten": 108
        }
    }
}
```

負回應會傳回物件，其值為 `"failed"` 在其中 `"status"` 屬性，並包含任何相關的錯誤訊息：

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{ORG_ID}",
        "status": "failed",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "replay": {},
        "availableDates": {},
        "metrics": {
            "startTime": 1536610322329,
            "endTime": 1536610438083,
            "recordsRead": 4004,
            "recordsWritten": 4004,
            "failureReason": "Job aborted due to stage failure: Task 0 in stage 1.0 failed 4 times,:"
        },
        "errors": [
            {
                "code": "0070000017",
                "description": "Unknown error occurred."
            },
            {
                "code": "unknown",
                "description": "Job aborted."
            }
        ],
        "created": 1536609893629,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1536610442814,
        "version": "1.0.5"
    }
}
```

>[!NOTE]
>
>建議的輪詢間隔為兩分鐘。

## 從資料集中讀取資料

使用批次ID時，您可以使用資料存取API來讀取及驗證上傳至批次的所有檔案。 回應會傳回包含檔案ID清單的陣列，每個檔案ID都參照批次中的檔案。

您也可以使用資料存取API來傳回名稱、大小（位元組），以及下載檔案或資料夾的連結。

有關使用資料存取API的詳細步驟，請參閱 [Data Access開發人員指南](../../data-access/home.md).

## 更新資料集結構

您可以新增欄位，並將其他資料擷取到您已建立的資料集中。 要執行此操作，您首先需要透過新增定義新資料的其他屬性來更新結構。 這可以使用PATCH和/或PUT操作來更新現有結構描述來完成。

如需更新結構的詳細資訊，請參閱 [Schema Registry API開發人員指南](../../xdm/api/getting-started.md).

更新結構描述後，您可以依照本教學課程中的步驟重新進行，以擷取符合修訂後結構描述的新資料。

請務必記住，結構描述演化是純粹的加總，這表示一旦結構描述儲存至登入並用於資料擷取，您就無法對其引入重大變更。 若要進一步瞭解撰寫結構描述以與Adobe Experience Platform搭配使用的最佳實務，請參閱以下指南中的 [結構描述組合基本概念](../../xdm/schema/composition.md).

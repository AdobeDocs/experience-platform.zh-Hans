---
keywords: Experience Platform；首頁；熱門主題；串流擷取；擷取；記錄資料；串流記錄資料；
solution: Experience Platform
title: 使用串流擷取API串流記錄資料
type: Tutorial
description: 本教學課程將幫助您開始使用串流獲取API，這是Adobe Experience Platform資料獲取服務API的一部分。
exl-id: 097dfd5a-4e74-430d-8a12-cac11b1603aa
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 2%

---


# 使用串流獲取API串流記錄資料

本教學課程將幫助您開始使用串流獲取API (屬於Adobe Experience Platform的一部分) [!DNL Data Ingestion Service] API。

## 快速入门

本教學課程需要各種Adobe Experience Platform服務的實際操作知識。 在開始本教學課程之前，請檢閱下列服務的檔案：

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Platform] 組織體驗資料。
   - [Schema Registry開發人員指南](../../xdm/api/getting-started.md)：涵蓋每個可用端點的完整指南 [!DNL Schema Registry] API以及如何對其發出呼叫。 這包括瞭解您的 `{TENANT_ID}`，會在本教學課程中的呼叫中顯示，並且瞭解如何建立結構（用於建立資料集以供擷取）。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的消費者設定檔。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../landing/api-guide.md).

## 根據以下專案撰寫結構描述： [!DNL XDM Individual Profile] 類別

若要建立資料集，您首先需要建立實作的新結構描述 [!DNL XDM Individual Profile] 類別。 如需如何建立結構描述的詳細資訊，請參閱 [Schema Registry API開發人員指南](../../xdm/api/getting-started.md).

**API格式**

```http
POST /schemaregistry/tenant/schemas
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:immutableTags": [
        "union"
    ]
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `title` | 您要用於結構描述的名稱。 此名稱必須是唯一的。 |
| `description` | 對您正在建立的結構描述進行有意義的說明。 |
| `meta:immutableTags` | 在此範例中， `union` 標籤用於將您的資料儲存到 [[!DNL Real-Time Customer Profile]](../../profile/home.md). |

**响应**

成功的回應會傳回HTTP狀態201，其中包含您新建立的結構描述詳細資料。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/cpmtext/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:immutableTags": [
        "union"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createDate": 1551376506996,
        "repo:lastModifiedDate": 1551376506996,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{TENANT_ID}` | 此ID可用來確保您建立的資源能正確建立名稱空間，並包含在您的組織內。 如需租使用者ID的詳細資訊，請參閱 [結構描述登入指南](../../xdm/api/getting-started.md#know-your-tenant-id). |

請記下 `$id` 以及 `version` 屬性，因為建立資料集時將同時使用這兩個屬性。

## 設定結構描述的主要身分描述項

接下來，新增 [身分描述項](../../xdm/api/descriptors.md) 以上建立的結構描述，使用工作電子郵件地址屬性作為主要識別碼。 這樣做會導致兩個變更：

1. 工作電子郵件地址將成為必填欄位。 這表示在沒有此欄位的情況下傳送的訊息將無法通過驗證，且不會被擷取。

2. [!DNL Real-Time Customer Profile] 將使用工作電子郵件地址作為識別碼，以協助彙整該個人的更多資訊。

### 请求

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "@type":"xdm:descriptorIdentity",
    "xdm:sourceProperty":"/workEmail/address",
    "xdm:property":"xdm:code",
    "xdm:isPrimary":true,
    "xdm:namespace":"Email",
    "xdm:sourceSchema":"{SCHEMA_REF_ID}",
    "xdm:sourceVersion":1
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEMA_REF_ID}` | 此 `$id` 撰寫結構描述時先前收到的內容。 它應該看起來像這樣： `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B;&#x200B;**身分名稱空間程式碼**
>
> 請確定程式碼有效 — 上述範例使用「email」，這是標準身分名稱空間。 其他常用的標準身分名稱空間可在以下網址找到： [Identity Service常見問題集](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> 如果您想要建立自訂名稱空間，請依照 [身分名稱空間總覽](../../identity-service/home.md).

**响应**

成功的回應會傳回HTTP狀態201，其中包含有關結構描述新建立的主要身分描述項的資訊。

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/workEmail/address",
    "@id": "17aaebfa382ce8fc0a40d3e43870b6470aab894e1c368d16",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{ORG_ID}"
}
```

## 建立記錄資料的資料集

建立結構描述後，您需要建立資料集以擷取記錄資料。

>[!NOTE]
>
>此資料集將啟用 **[!DNL Real-Time Customer Profile]** 和 **[!DNL Identity Service]**.

**API格式**

```http
POST /catalog/dataSets
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' {
    "name": "Dataset name",
    "description": "Dataset description",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID},
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**响应**

成功的回應會傳回HTTP狀態201和陣列，其中包含以格式建立的新資料集的ID `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## 建立串流連線

建立結構描述和資料集後，您可以建立串流連線

如需建立串流連線的詳細資訊，請參閱 [建立串流連線教學課程](./create-streaming-connection.md).

## 將記錄資料擷取至串流連線 {#ingest-data}

資料集和串流連線就緒後，您就可以內嵌XDM格式的JSON記錄，將記錄資料內嵌至 [!DNL Platform].

**API格式**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 此 `inletId` 先前建立的串流連線的值。 |
| `syncValidation` | 供開發使用的選用查詢引數。 若設為 `true`，可用來立即提供意見回饋，以判斷要求是否已成功傳送。 預設情況下，此值設定為 `false`. 請注意，如果您將此查詢引數設為 `true` 此請求的速率限製為每分鐘最多60次/ `CONNECTION_ID`. |

**请求**

可以在使用或不使用來源名稱的情況下，將記錄資料擷取到串流連線。

以下範例請求會將缺少來源名稱的記錄擷取到Platform。 如果記錄缺少來源名稱，則會從串流連線定義新增來源ID。

>[!NOTE]
>
>以下API呼叫會 **not** 需要任何驗證標頭。

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "flowId": "{FLOW_ID}",
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                },
                "birthDate": "1969-03-14",
                "gender": "female"
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "type": "work",
                "status": "active"
            }
        }
    }
}'
```

如果要包含來源名稱，以下範例顯示如何包含它。

```json
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含新串流的詳細資訊 [!DNL Profile].

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "syncValidation": {
        "status": "pass"
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 先前建立的串流連線的ID。 |
| `xactionId` | 伺服器端為您剛傳送的記錄產生的唯一識別碼。 此ID有助於Adobe透過各種系統和偵錯追蹤此記錄的生命週期。 |
| `receivedTimeMs` | 顯示收到要求的時間戳記（紀元，以毫秒為單位）。 |
| `syncValidation.status` | 由於查詢引數 `syncValidation=true` 「 」已新增，則會顯示此值。 如果驗證成功，狀態將為 `pass`. |

## 擷取新擷取的記錄資料

若要驗證先前擷取的記錄，您可以使用 [[!DNL Profile Access API]](../../profile/api/entities.md) 以擷取記錄資料。

>[!NOTE]
>
>如果未定義合併原則ID，且 `schema.name` 或 `relatedSchema.name` 是 `_xdm.context.profile`， [!DNL Profile Access] 將擷取 **全部** 相關身分。

**API格式**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| 参数 | 描述 |
| --------- | ----------- |
| `schema.name` | **必需。** 您正在存取的結構描述名稱。 |
| `entityId` | 實體的識別碼。 如果提供，您也必須提供實體名稱空間。 |
| `entityIdNS` | 您嘗試擷取的ID名稱空間。 |

**请求**

您可以使用以下GET請求來檢閱先前擷取的記錄資料。

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含請求實體的詳細資訊。 如您所見，這是先前成功擷取的相同記錄。

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "mergePolicy": {
            "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56"
        },
        "sources": [
            "5e30d7986c0cc218a85cee65"
        ],
        "tags": [
            "1580346827274:2478:215"
        ],
        "identityGraph": [
            "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA"
        ],
        "entity": {
            "person": {
                "name": {
                    "lastName": "Doe",
                    "middleName": "F",
                    "firstName": "Jane"
                },
                "gender": "female",
                "birthDate": "1969-03-14"
            },
            "workEmail": {
                "type": "work",
                "address": "janedoe@example.com",
                "status": "active",
                "primary": true
            },
            "identityMap": {
                "email": [
                    {
                        "id": "janedoe@example.com"
                    }
                ]
            }
        },
        "lastModifiedAt": "2020-01-30T01:13:59Z"
    }
}
```

## 后续步骤

閱讀本檔案後，您現在瞭解如何將記錄資料擷取至 [!DNL Platform] 使用串流連線。 您可以嘗試使用不同的值執行更多呼叫，並擷取更新的值。 此外，您也可以透過以下方式開始監控您擷取的資料： [!DNL Platform] UI。 如需詳細資訊，請閱讀 [監控資料擷取](../quality/monitor-data-ingestion.md) 指南。

如需串流擷取的詳細資訊，請閱讀 [串流擷取概觀](../streaming-ingestion/overview.md).

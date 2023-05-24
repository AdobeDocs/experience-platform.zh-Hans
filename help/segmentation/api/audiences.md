---
keywords: Experience Platform；首頁；熱門主題；細分；細分；細分服務；對象；對象；API；API；
title: Audiences API端點
description: Adobe Experience Platform Segmentation Service API中的受眾端點可讓您以程式設計方式管理組織的受眾。
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
hide: true
hidefromtoc: true
source-git-commit: 9aba3384b320b8c7d61a875ffd75217a5af04815
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 4%

---

# 受眾端點

>[!IMPORTANT]
>
>對象端點目前為測試版，並非所有使用者都可使用。 文档和功能可能会发生变化。

對象是具有相同類似行為和/或特徵的人集合。 這些人員集合可以使用Adobe Experience Platform或從外部來源產生。 您可以使用 `/audiences` 區段API中的端點，可讓您以程式設計方式擷取、建立、更新和刪除對象。

## 快速入门

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API。 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需成功呼叫API所需的重要資訊，包括必要的標頭及如何讀取範例API呼叫。

## 擷取對象清單 {#list}

您可以透過向以下網站發出GET請求，擷取貴組織的所有對象清單： `/audiences` 端點。

**API格式**

此 `/audiences` 端點支援數個查詢引數，以協助篩選結果。 雖然這些引數是選用的，但強烈建議使用這些引數，以幫助在列出資源時減少昂貴的額外負荷。 如果您在不使用引數的情況下呼叫此端點，則會擷取貴組織可用的所有對象。 可包含多個引數，以&amp;符號(`&`)。

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

擷取對象清單時，可使用下列查詢引數：

| 查询参数 | 描述 | 示例 |
| --------------- | ----------- | ------- |
| `start` | 指定傳回對象的開始位移。 | `start=5` |
| `limit` | 指定每頁傳回的最大對象數。 | `limit=10` |
| `sort` | 指定排序結果的順序。 這會以格式撰寫 `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | 可讓您指定受眾的篩選器 **完全符合** 符合屬性的值。 這會以格式撰寫 `property=` | `property=audienceId==test-audience-id` |
| `name` | 可讓您指定名稱為的對象的篩選器 **contain** 提供的值。 此值不區分大小寫。 | `name=Sample` |
| `description` | 可讓您指定其說明的對象的篩選器 **contain** 提供的值。 此值不區分大小寫。 | `description=Test Description` |
| `withMetrics` | 除了傳回對象外，還傳回量度的篩選器。 | `property=withMetrics==true` |

>[!IMPORTANT]
>
>針對對象，量度會傳回至 `metrics` 屬性，並包含設定檔計數、建立和更新時間戳記的資訊。

**無量度**

下列請求/回應配對用於 `withMetrics` 查詢引數不存在。

**请求**

以下請求會擷取貴組織中建立的最後5個對象。

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=5 \
 -H 'Authorization:  Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id:  {IMS_ORG}' \
 -H 'x-api-key:  {API_KEY}' \
 -H 'x-sandbox-name:  {SANDBOX_NAME}'
```

**响应** {#no-metrics}

成功的回應會傳回HTTP狀態200，其中包含您的組織中建立為JSON的對象清單。

>[!NOTE]
>
>下列回應已截斷空格，且僅顯示傳回的第一個對象。

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "isSystem": false,
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
    ]
}
```

| 属性 | 對象型別 | 描述 |
| -------- | ------------- | ----------- | 
| `id` | 兩者 | 系統產生的對象唯讀識別碼。 |
| `audienceId` | 兩者 | 如果對象是平台產生的對象，則此值與的值相同。 `id`. 如果對象是外部產生的，此值由使用者端提供。 |
| `schema` | 兩者 | 對象的Experience Data Model (XDM)結構描述。 |
| `imsOrgId` | 兩者 | 對象所屬組織的ID。 |
| `sandbox` | 兩者 | 受眾所屬沙箱的相關資訊。 有關沙箱的更多資訊可在以下網址找到： [沙箱總覽](../../sandboxes/home.md). |
| `name` | 兩者 | 受众的名称。 |
| `description` | 兩者 | 對象說明。 |
| `expression` | 平台產生 | 對象的設定檔查詢語言(PQL)運算式。 如需PQL運算式的詳細資訊，請參閱 [PQL運算式指南](../pql/overview.md). |
| `mergePolicyId` | 平台產生 | 與對象相關聯的合併原則ID。 有關合併原則的更多資訊可在以下網址找到： [合併原則指南](../../profile/api/merge-policies.md). |
| `evaluationInfo` | 平台產生 | 顯示評估對象的方式。 可能的評估方法包括批次、串流或邊緣。 有關評估方法的詳細資訊，請參閱 [區段概述](../home.md) |
| `dependents` | 兩者 | 相依於目前受眾的受眾ID陣列。 如果您建立的對象是區段的區段，則會使用此屬性。 |
| `dependencies` | 兩者 | 受眾相依的受眾ID陣列。 如果您建立的對象是區段的區段，則會使用此屬性。 |
| `type` | 兩者 | 系統產生的欄位，顯示對象是平台產生的還是外部產生的對象。 可能的值包括 `SegmentDefinition` 和 `ExternalAudience`. A `SegmentDefinition` 指在Platform中產生的對象，而 `ExternalAudience` 指不是在Platform中產生的對象。 |
| `createdBy` | 兩者 | 建立受眾之使用者的ID。 |
| `labels` | 兩者 | 與對象相關的物件層級資料使用情況和屬性型存取控制標籤。 |
| `namespace` | 兩者 | 對象所屬的名稱空間。 可能的值包括 `AAM`， `AAMSegments`， `AAMTraits`、和 `AEPSegments`. |
| `audienceMeta` | 外部 | 從外部建立的對象中從外部建立的中繼資料。 |

**使用量度**

下列請求/回應配對用於 `withMetrics` 出現查詢引數。

**请求**

以下請求會擷取您組織中建立的最後5個對象（含量度）。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?propoerty=withMetrics==true&limit=5&sort=totalProfiles:desc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功回應會傳回HTTP狀態200，其中包含指定組織的對象清單及量度，格式為JSON。

>[!NOTE]
>
>下列回應已截斷空格，且僅顯示傳回的第一個對象。

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "metrics": {
                "type": "export",
                "jobId": "test-job-id",
                "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
                "data": {
                    "totalProfiles": 11200769,
                    "totalProfilesByNamespace": {
                        "crmid": 11400769
                    },
                    "totalProfilesByStatus": {
                        "realized": 11400769
                    }
                },
                "createEpoch": 1653583927,
                "updateEpoch": 1653583927
            },
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
   ],
   "_page": {
      "totalCount": 111,
      "pageSize": 5,
      "next": "1"
   },
   "_links": {
      "next": {
         "href": "@/audiences?start=1&limit=5&totalCount=111"
      }
   }
}
```

以下列出屬性 **獨佔** 至 `withMetrics` 回應。 如果您想知道標準對象屬性，請閱讀 [上一節](#no-metrics).

| 属性 | 描述 |
| -------- | ----------- |
| `metrics.imsOrgId` | 對象的組織ID。 |
| `metrics.sandbox` | 和受眾相關的沙箱資訊。 |
| `metrics.jobId` | 處理對象的區段作業ID。 |
| `metrics.type` | 區段作業型別。 這可以是 `export` 或 `batch_segmentation`. |
| `metrics.id` | 對象的ID。 |
| `metrics.data` | 與對象相關的量度。 這包括對象中包含的設定檔總數、依每個名稱空間的設定檔總數，以及依每個狀態的設定檔總數。 |
| `metrics.createEpoch` | 顯示對象建立時間的時間戳記。 |
| `metrics.updateEpoch` | 顯示上次更新對象時間的時間戳記。 |

## 创建新受众 {#create}

您可以透過向以下傳送POST請求來建立新受眾： `/audiences` 端點。

**API格式**

```http
POST /audiences
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "type": "SegmentDefinition",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "labels": [
          "core/C1"
        ]
    }'
```

| 属性 | 描述 |
| -------- | ----------- | 
| `name` | 受众的名称。 |
| `description` | 對象說明。 |
| `type` | 此欄位會顯示對象是平台產生的受眾，還是外部產生的受眾。 可能的值包括 `SegmentDefinition` 和 `ExternalAudience`. A `SegmentDefinition` 指在Platform中產生的對象，而 `ExternalAudience` 指不是在Platform中產生的對象。 |
| `expression` | 對象的設定檔查詢語言(PQL)運算式。 如需PQL運算式的詳細資訊，請參閱 [PQL運算式指南](../pql/overview.md). |
| `schema` | 對象的Experience Data Model (XDM)結構描述。 |
| `labels` | 與對象相關的物件層級資料使用情況和屬性型存取控制標籤。 |

**响应**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,     
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## 查詢指定的對象 {#get}

您可以透過向以下網站發出GET要求，查詢有關特定對象的詳細資訊： `/audiences` 端點，並提供您想要在請求路徑中擷取之對象的ID。

**API格式**

```http
GET /audiences/{AUDIENCE_ID}
GET /audiences/{AUDIENCE_ID}?property=withmetrics==true
```

| 参数 | 描述 |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | 您嘗試擷取的對象ID。 |
| `property=withmetrics==true` | 選擇性查詢引數，如果要使用對象量度擷取指定的對象，可使用此引數。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含指定對象的資訊。 回應將因對象是使用Adobe Experience Platform還是外部來源產生而異。

**平台產生**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

**外部產生**

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "externalSegment1",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "active",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ],
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## 更新對象中的欄位 {#update-field}

您可以透過向以下連結發出PATCH請求，更新特定對象的欄位： `/audiences` 端點，並在請求路徑中提供您要更新的對象ID。

**API格式**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 您要更新的對象ID。 |

**请求**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
     [
        {
            "op": "add",
            "path": "/expression",
            "value": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"CA\""
            }
        }
      ]'
```

| 属性 | 描述 |
| -------- | ----------- |
| `op` | 若要更新對象，此值一律為 `add`. |
| `path` | 您要更新的欄位路徑。 |
| `value` | 您要更新欄位的值。 |

**响应**

成功回應會傳回HTTP狀態200，其中包含您新更新對象的資訊。

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## 更新對象 {#put}

您可以透過向以下專案發出PUT請求，更新（覆寫）特定對象： `/audiences` 端點，並在請求路徑中提供您要更新的對象ID。

**API格式**

```http
PUT /audiences/{AUDIENCE_ID}
```

**请求**

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId":"test-external-audience-id",
    "name":"new externalSegment",
    "namespace":"aam",
    "description":"Last 30 days",
    "type":"ExternalSegment",
    "lifecycle":"published",
    "datasetId":"6254cf3c97f8e31b639fb14d",
    "labels":[
        "core/C1"
    ]
}' 
```

| 属性 | 描述 |
| -------- | ----------- | 
| `audienceId` | 對象的ID。 外部對象會使用此專案 |
| `name` | 受众的名称。 |
| `namespace` |  |
| `description` | 對象說明。 |
| `type` | 系統產生的欄位，顯示對象是平台產生的還是外部產生的對象。 可能的值包括 `SegmentDefinition` 和 `ExternalAudience`. A `SegmentDefinition` 指在Platform中產生的對象，而 `ExternalAudience` 指不是在Platform中產生的對象。 |
| `lifecycle` | 對象的狀態。 可能的值包括 `draft`， `published`， `inactive`、和 `archived`. `draft` 代表建立對象的時間， `published` 發佈對象時， `inactive` 對象不再作用中時，以及 `archived` 是否刪除對象。 |
| `datasetId` | 可找到對象資料的資料集ID。 |
| `labels` | 與對象相關的物件層級資料使用情況和屬性型存取控制標籤。 |

**响应**

成功回應會傳回HTTP狀態200以及您新更新對象的詳細資料。 請注意，您的對象詳細資訊會因平台產生的對象或外部產生的對象而有所不同。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "new externalSegment",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## 刪除對象 {#delete}

您可以透過向以下專案發出DELETE請求來刪除特定對象： `/audiences` 端點並在請求路徑中提供您要刪除之對象的ID。

**API格式**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 您要刪除的對象ID。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態204，但無訊息。

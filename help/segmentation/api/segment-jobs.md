---
keywords: Experience Platform；首頁；熱門主題；細分；細分；細分服務；細分工作；細分工作；API；API；
solution: Experience Platform
title: 區段作業API端點
description: Adobe Experience Platform Segmentation Service API中的區段作業端點可讓您以程式設計方式管理組織的區段作業。
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 2%

---

# 區段作業端點

區段作業為非同步程式，可依需求建立對象區段。 它參照 [區段定義](./segment-definitions.md)，以及任何 [合併原則](../../profile/api/merge-policies.md) 控制方式 [!DNL Real-Time Customer Profile] 合併您的設定檔片段中的重疊屬性。 當區段工作成功完成時，您可以收集關於區段的各種資訊，例如處理期間可能發生的任何錯誤以及您的對象的最終規模。

本指南提供的資訊可協助您更清楚瞭解區段作業，並包含使用API執行基本動作的範例API呼叫。

## 快速入门

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API。 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需成功呼叫API所需的重要資訊，包括必要的標頭及如何讀取範例API呼叫。

## 擷取區段作業清單 {#retrieve-list}

您可以透過向以下專案發出GET請求，擷取組織的所有區段作業清單： `/segment/jobs` 端點。

**API格式**

此 `/segment/jobs` 端點支援數個查詢引數，以協助篩選結果。 雖然這些引數是選用的，但強烈建議使用它們來協助減少昂貴的額外負荷。 在不使用引數的情況下呼叫此端點將擷取可用於您的組織的所有匯出作業。 可包含多個引數，以&amp;符號(`&`)。

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**查詢引數**

| 参数 | 描述 | 示例 |
| --------- | ----------- | ------- |
| `start` | 指定傳回之區段作業的起始位移。 | `start=1` |
| `limit` | 指定每頁傳回的區段作業數。 | `limit=20` |
| `status` | 根據狀態篩選結果。 支援的值為NEW、QUEUED、PROCESSING、SUCCEEDED、FAILED、CANCELING、CANCELLED | `status=NEW` |
| `sort` | 區段作業傳回的訂單。 以格式撰寫 `[attributeName]:[desc|asc]`. | `sort=creationTime:desc` |
| `property` | 篩選區段作業，並取得指定篩選器的完全相符專案。 可採用下列任一格式撰寫： <ul><li>`[jsonObjectPath]==[value]`  — 篩選物件索引鍵</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]`  — 在陣列中篩選</li></ul> | `property=segments~segmentId==workInUS` |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功回應會傳回HTTP狀態200，其中包含指定組織的區段作業清單(JSON)。 不過，回應會因區段作業內的區段數而異。

**區段作業中的區段數量少於或等於1500個**

如果您的區段作業中執行的區段少於1500個，則所有區段的完整清單將顯示在 `children.segments` 屬性。

>[!NOTE]
>
>下列回應已截斷空格，且僅會顯示第一個傳回的工作。

```json
{
    "_page": {
        "totalCount": 14,
        "pageSize": 14
    },
    "children": [
        {
            "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "profileInstanceId": "ups",
            "source": "scheduler",
            "status": "SUCCEEDED",
            "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
            "computeJobId": 8811,
            "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                        "mergePolicy": {
                            "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                            "version": 1
                        }
                    }
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1573203617195,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 778460
                },
                "profileSegmentationTime": {
                    "startTimeInMs": 1573204266727,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 128928
                },
                "totalProfiles":13146432,
                "segmentedProfileCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":1033
                },
                "segmentedProfileByNamespaceCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "tenantiduserobjid":1033,
                        "campaign_profile_mscom_mkt_prod2":1033
                    }
                },
                "segmentedProfileByStatusCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "exited":144646,
                        "realized":2056
                    }
                },
                "totalProfilesByMergePolicy":{
                    "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
                }
            },
            "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "properties": {
                "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
                "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
            },
            "_links": {
                "cancel": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "DELETE"
                },
                "checkStatus": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "GET"
                }
            },
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    ],
    "_links": {
        "next": {}
    }
}
```

**超過1500個區段**

如果您的區段作業中執行的區段超過1500個，則 `children.segments` 屬性將會顯示 `*`，表示正在評估所有區段。

>[!NOTE]
>
>下列回應已截斷空格，且僅會顯示第一個傳回的工作。

```json
{
    "_page": {
        "totalCount": 14,
        "pageSize": 14
    },
    "children": [
        {
            "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "profileInstanceId": "ups",
            "source": "scheduler",
            "status": "SUCCEEDED",
            "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
            "computeJobId": 8811,
            "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
            "segments": [
                {
                    "segmentId": "*",
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1573203617195,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 778460
                },
                "profileSegmentationTime": {
                    "startTimeInMs": 1573204266727,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 128928
                },
                "totalProfiles": 13146432,
                "segmentedProfileCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":1033
                },
                "segmentedProfileByNamespaceCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "tenantiduserobjid":1033,
                        "campaign_profile_mscom_mkt_prod2":1033
                    }
                },
                "segmentedProfileByStatusCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "exited":144646,
                        "realized":2056
                    }
                },
                "totalProfilesByMergePolicy":{
                    "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
                }
            },
            "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "properties": {
                "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
                "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
            },
            "_links": {
                "cancel": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "DELETE"
                },
                "checkStatus": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "GET"
                }
            },
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 區段作業的系統產生唯讀識別碼。 |
| `status` | 區段作業的目前狀態。 狀態的潛在值包括「NEW」、「PROCESSING」、「CANCELING」、「CANCELLED」、「FAILED」和「SUCCEEDED」。 |
| `segments` | 此物件包含區段作業中傳回之區段定義的相關資訊。 |
| `segments.segment.id` | 區段定義的ID。 |
| `segments.segment.expression` | 一個物件，包含有關以PQL寫入的區段定義運算式的資訊。 |
| `metrics` | 包含區段作業之診斷資訊的物件。 |
| `metrics.totalTime` | 一個物件，包含分段工作開始和結束的時間以及花費的總時間的相關資訊。 |
| `metrics.profileSegmentationTime` | 一個物件，包含區段評估開始和結束的時間以及花費的總時間的相關資訊。 |
| `metrics.segmentProfileCounter` | 每個區段符合資格的設定檔數。 |
| `metrics.segmentedProfileByNamespaceCounter` | 每個區段符合每個身分名稱空間資格的設定檔數。 |
| `metrics.segmentProfileByStatusCounter` | 每個狀態的設定檔計數。 支援下列三種狀態： <ul><li>「已實現」 — 符合區段資格的設定檔數。</li><li>「已退出」 — 區段中不再存在的設定檔區段數。</li></ul> |
| `metrics.totalProfilesByMergePolicy` | 根據合併原則，合併的設定檔總數。 |

## 建立新的區段工作 {#create}

您可以透過向以下專案發出POST請求，以建立新的區段作業： `/segment/jobs` 端點，並在內文中包含您要建立新對象之區段定義的ID。

**API格式**

```http
POST /segment/jobs
```

建立新區段作業時，請求和回應會因區段作業內的區段數而異。

**區段作業中的區段數量少於或等於1500個**

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e"
    }
 ]'
```

| 属性 | 描述 |
| -------- | ----------- |
| `segmentId` | 您要為其建立區段作業的區段定義ID。 這些區段定義可屬於不同的合併原則。 如需區段定義的詳細資訊，請參閱 [區段定義端點指南](./segment-definitions.md). |

**响应**

成功的回應會傳回HTTP狀態200，其中包含新建立區段工作的相關資訊。

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "scheduler",
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1573203617195,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 778460
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1573204266727,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 128928
        },
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
        }
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "properties": {
        "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
        "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "GET"
        }
    },
    "updateTime": 1573204395000,
    "creationTime": 1573203600535,
    "updateEpoch": 1573204395
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 系統產生的唯讀識別碼，用於新建立的區段作業。 |
| `status` | 區段作業的目前狀態。 由於區段作業是新建立的，因此狀態將一律為「新」。 |
| `segments` | 一個物件，其中包含執行此區段工作的區段定義相關資訊。 |
| `segments.segment.id` | 您提供的區段定義ID。 |
| `segments.segment.expression` | 一個物件，包含有關以PQL寫入的區段定義運算式的資訊。 |

**超過1500個區段**

**请求**

>[!NOTE]
>
>雖然您可以建立包含超過1500個區段的區段作業，但這會 **強烈不建議**.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "segments": [
        {
            "segmentId": "*"
        }
    ]
 }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `schema.name` | 區段的結構描述名稱。 |
| `segments.segmentId` | 執行含有超過1500個區段的區段工作時，您需要通過 `*` 作為區段ID，表示您要使用所有區段執行分段作業。 |

**响应**

成功的回應會傳回HTTP狀態200以及您新建立的區段工作的詳細資訊。

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "scheduler",
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "*"
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1573203617195,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 778460
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1573204266727,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 128928
        },
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
        }
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "properties": {
        "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
        "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "GET"
        }
    },
    "updateTime": 1573204395000,
    "creationTime": 1573203600535,
    "updateEpoch": 1573204395
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 系統產生的唯讀識別碼，用於新建立的區段作業。 |
| `status` | 區段作業的目前狀態。 由於區段作業是新建立的，因此狀態將一律為 `NEW`. |
| `segments` | 一個物件，其中包含執行此區段工作的區段定義相關資訊。 |
| `segments.segment.id` | 此 `*` 表示此區段工作正在組織內的所有區段執行。 |

## 擷取特定區段工作 {#get}

您可以透過向以下專案發出GET請求，擷取有關特定區段作業的詳細資訊： `/segment/jobs` 端點，並提供您要在請求路徑中擷取的區段作業ID。

**API格式**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| 属性 | 描述 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 此 `id` 您要擷取之區段工作的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含指定區段工作的詳細資訊。  不過，回應會因區段作業內的區段數而異。

**區段作業中的區段數量少於或等於1500個**

如果您的區段作業中執行的區段少於1500個，則所有區段的完整清單將顯示在 `children.segments` 屬性。

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "SUCCEEDED",
    "batchId": "651fc109-3963-48d2-aa98-9e3cc2003bac",
    "computeJobId": 39312,
    "computeGatewayJobId": "a0099ab6-11ab-4c2b-a0ea-6162e16806bd",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1579304313411
        },
        "profileSegmentationTime": {}
    },
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304339000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304339
}
```

**超過1500個區段**

如果您的區段作業中執行的區段超過1500個，則 `children.segments` 屬性將會顯示 `*`，表示正在評估所有區段。

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "scheduler",
    "status": "SUCCEEDED",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "*"
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1573203617195,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 778460
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1573204266727,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 128928
        },
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
        }
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "properties": {
        "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
        "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "GET"
        }
    },
    "updateTime": 1573204395000,
    "creationTime": 1573203600535,
    "updateEpoch": 1573204395
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 區段作業的系統產生唯讀識別碼。 |
| `status` | 區段作業的目前狀態。 狀態的潛在值包括「NEW」、「PROCESSING」、「CANCELING」、「CANCELLED」、「FAILED」和「SUCCEEDED」。 |
| `segments` | 此物件包含區段作業中傳回之區段定義的相關資訊。 |
| `segments.segment.id` | 區段定義的ID。 |
| `segments.segment.expression` | 一個物件，包含有關以PQL寫入的區段定義運算式的資訊。 |
| `metrics` | 包含區段作業之診斷資訊的物件。 |

## 大量擷取區段作業 {#bulk-get}

您可以透過向以下專案發出POST請求，擷取多個區段作業的詳細資訊： `/segment/jobs/bulk-get` 端點，並提供  `id` 請求內文中的區段作業值。

**API格式**

```http
POST /segment/jobs/bulk-get
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "cc3419d3-0389-47f1-b174-fead6b3c830d"
            },
            {
                "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8"
            }
        ]
    }'
```

**响应**

成功的回應會傳回HTTP狀態207以及請求的區段作業。 然而，此 `children.segments` 屬性會因區段作業的執行是否超過1500個區段而有所不同。

>[!NOTE]
>
>以下回應已截斷空間，僅顯示每個區段工作的部分詳細資訊。 完整回應將列出請求區段作業的完整詳細資料。

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{ORG_ID}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        },
        "c527dc3f-07fe-4b96-be4e-23f38e734ff8": {
            "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8",
            "imsOrgId": "{ORG_ID}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "*"
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 區段作業的系統產生唯讀識別碼。 |
| `status` | 區段作業的目前狀態。 狀態的潛在值包括「NEW」、「PROCESSING」、「CANCELING」、「CANCELLED」、「FAILED」和「SUCCEEDED」。 |
| `segments` | 此物件包含區段作業中傳回之區段定義的相關資訊。 |
| `segments.segment.id` | 區段定義的ID。 |
| `segments.segment.expression` | 一個物件，包含有關以PQL寫入的區段定義運算式的資訊。 |

## 取消或刪除特定區段工作 {#delete}

您可以透過向以下專案發出DELETE請求來刪除特定區段作業： `/segment/jobs` 端點，並在請求路徑中提供您要刪除之區段作業的ID。

>[!NOTE]
>
>對刪除請求的API回應是立即的。 不過，實際刪除區段作業為非同步。 換句話說，對區段工作提出刪除請求的時間與套用請求的時間之間會存在時間差異。

**API格式**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| 属性 | 描述 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 此 `id` 您要刪除之區段工作的值。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態204，並提供下列資訊。

```json
{
    "status": true,
    "message": "Segment job with id 'd3b4a50d-dfea-43eb-9fca-557ea53771fd' has been marked for cancelling"
}
```

## 后续步骤

閱讀本指南後，您現在已能更清楚瞭解區段工作的運作方式。

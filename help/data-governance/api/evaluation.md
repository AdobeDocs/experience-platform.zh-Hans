---
keywords: Experience Platform；首頁；熱門主題；原則執行；自動執行；API型執行；資料控管
solution: Experience Platform
title: 原則評估API端點
description: 建立行銷動作並定義原則後，您就可以使用原則服務API來評估某些動作是否違反了任何原則。 傳回的限制會採取一組原則的形式，嘗試對包含資料使用標籤的指定資料執行行銷動作時，違反這些原則。
exl-id: f9903939-268b-492c-aca7-63200bfe4179
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 1%

---

# 原則評估端點

建立行銷動作並定義資料使用原則後，您可以使用 [!DNL Policy Service] 用於評估特定動作是否違反任何原則的API。 傳回的限制會採取一組原則的形式，嘗試對包含資料使用標籤的指定資料執行行銷動作時，違反這些原則。

依預設，只有狀態設定為的原則 `ENABLED` 參與評估。 不過，您可以使用查詢引數 `?includeDraft=true` 要包含 `DRAFT` 評估中的原則。

您可以透過下列三種方式之一提出評估請求：

1. 指定某個行銷動作和一組資料使用標籤，該動作是否會違反任何原則？
1. 指定行銷動作和一個或多個資料集，該動作是否違反任何政策？
1. 指定行銷動作、一個或多個資料集，以及這些資料集中一個或多個欄位的子集，該動作是否違反任何原則？

## 快速入门

本指南中使用的API端點屬於 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功對任一檔案發出呼叫所需必要標題的重要資訊 [!DNL Experience Platform] API。

## 使用資料使用標籤評估原則違規 {#labels}

您可以根據特定資料使用標籤集是否存在，評估原則違規，方法是使用 `duleLabels` GET請求中的查詢引數。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 根據一組資料使用標籤進行測試的行銷動作名稱。 您可以透過建立「 」 [行銷動作端點的GET請求](./marketing-actions.md#list). |
| `{LABELS_LIST}` | 以逗號分隔的資料使用標簽名稱清單，可針對此清單測試行銷動作。 例如： `duleLabels=C1,C2,C3`<br><br>請注意，標簽名稱會區分大小寫。 確保您在下列專案中使用正確的大小寫： `duleLabels` 引數。 |

**请求**

以下範例請求會針對標籤C1和C3評估行銷動作。

>[!IMPORTANT]
>
>請注意 `AND` 和 `OR` 原則運算式中的運運算元。 在以下範例中，如果任一標籤(`C1` 或 `C3`)單獨出現在要求中，行銷動作不會違反此原則。 需要兩個標籤(`C1` 和 `C3`)以傳回違反的原則。 請務必謹慎評估原則，並謹慎定義原則運算式。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應包括 `violatedPolicies` 陣列，包含對提供的標籤執行行銷動作而違反之原則的詳細資訊。 如果沒有違反任何原則， `violatedPolicies` 陣列將是空的。

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform.adobe.io/marketingActions/custom/sampleMarketingAction",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
            ],
            "description": "NEW content for description.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "OR",
                        "operands": [
                            {
                                "label": "C3"
                            },
                            {
                                "label": "C7"
                            }
                        ]
                    }
                ]
            },
            "imsOrg": "{ORG_ID}",
            "created": 1550703519823,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714340335,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb9f5c404513dc2dc454"
                }
            },
            "id": "5c6ddb9f5c404513dc2dc454"
        }
    ]
}
```

## 使用資料集評估原則違規 {#datasets}

您可以根據可從中收集資料使用標籤的一或多個資料集集合來評估原則違規。 這是透過對「 」執行POST請求來完成 `/constraints` 端點的特定行銷動作，並在請求內文中提供資料集ID的清單。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 針對一或多個資料集進行測試的行銷動作名稱。 您可以透過建立「 」 [行銷動作端點的GET請求](./marketing-actions.md#list). |

**请求**

以下請求會執行 `crossSiteTargeting` 針對一組三個資料集執行行銷動作，以評估任何原則違規。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319"
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e"
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f"
        }
      ]'
```

| 属性 | 描述 |
| --- | --- |
| `entityType` | 同級中指出其ID的實體型別 `entityId` 屬性。 目前唯一接受的值是 `dataSet`. |
| `entityId` | 要用來測試行銷動作的資料集ID。 您可以向以下專案發出GET要求，以取得資料集清單及其對應的ID： `/dataSets` 中的端點 [!DNL Catalog Service] API。 請參閱指南： [清單 [!DNL Catalog] 物件](../../catalog/api/list-objects.md) 以取得詳細資訊。 |

**响应**

成功的回應包括 `violatedPolicies` 陣列，其中包含對提供的資料集執行行銷動作而違反原則的詳細資訊。 如果沒有違反任何原則， `violatedPolicies` 陣列將是空的。

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C1",
        "C2",
        "C4",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C4",
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/identityMap"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/journeyAI"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C1"
                        ],
                        "path": "/properties/identityMap"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": [
        {
            "name": "Targeting Ads or Content",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
            ],
            "description": "Data cannot be used for targeting any ads or content, either on-site or cross-site.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C4"
                    },
                    {
                        "label": "C6"
                    }
                ]
            },
            "imsOrg": "{ORG_ID}",
            "created": 1551141210463,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1551146178603,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/policies/custom/5c74895a74744d13dc2d87cc"
                }
            },
            "id": "5c74895a74744d13dc2d87cc"
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `duleLabels` | 回應物件包含 `duleLabels` 陣列，包含在指定資料集中找到之所有標籤的整合清單。 此清單包含資料集內所有欄位上的資料集和欄位層級標籤。 |
| `discoveredLabels` | 回應也包含 `discoveredLabels` 包含每個資料集之物件的陣列，顯示 `datasetLabels` 細分為資料集和欄位層級標籤。 每個欄位層級標籤都會顯示該標籤特定欄位的路徑。 |

## 使用特定資料集欄位評估原則違規 {#fields}

您可以根據一或多個資料集中的欄位子集來評估原則違規，以便只評估套用這些欄位的資料使用標籤。

使用資料集欄位評估原則時，請記住以下事項：

* **欄位名稱區分大小寫**：提供欄位時，必須完全依照資料集中顯示的樣式來撰寫(例如， `firstName` 與 `firstname`)。
* **資料集標籤繼承**：資料集中的個別欄位會繼承已在資料集層級套用的任何標籤。 如果您的原則評估未如預期傳回，除了在欄位層級套用的標籤之外，請務必檢查是否任何標籤已從資料集層級向下繼承至欄位。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 根據資料集欄位子集進行測試的行銷動作名稱。 您可以透過建立「 」 [行銷動作端點的GET請求](./marketing-actions.md#list). |

**请求**

以下請求會測試行銷動作 `crossSiteTargeting` 屬於三個資料集的特定欄位集上。 裝載類似於 [僅涉及資料集的評估請求](#datasets)，為每個要從中收集標籤的資料集新增特定欄位。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/faxPhone"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/geoUnit"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "entityMeta": {
                "fields": [
                    "/properties/faxPhone"
                ]
            }
        }
      ]'
```

| 属性 | 描述 |
| --- | --- |
| `entityType` | 同級中指出其ID的實體型別 `entityId` 屬性。 目前唯一接受的值是 `dataSet`. |
| `entityId` | 資料集的ID，其欄位將根據行銷動作進行評估。 您可以向以下專案發出GET要求，以取得資料集清單及其對應的ID： `/dataSets` 中的端點 [!DNL Catalog Service] API。 請參閱指南： [清單 [!DNL Catalog] 物件](../../catalog/api/list-objects.md) 以取得詳細資訊。 |
| `entityMeta.fields` | 資料集結構描述中特定欄位的路徑陣列，以JSON指標字串形式提供。 請參閱以下小節： [JSON指標](../../landing/api-fundamentals.md#json-pointer) API基礎指南中，瞭解這些字串可接受語法的詳細資訊。 |

**响应**

成功的回應包括 `violatedPolicies` 陣列，包含對提供的資料集欄位執行行銷動作而違反原則的詳細資訊。 如果沒有違反任何原則， `violatedPolicies` 陣列將是空的。

將下列範例回應與 [僅涉及資料集的回應](#datasets)，請注意，收集到的標籤清單較短。 此 `discoveredLabels` 也減少了每個資料集的數量，因為它們僅包含請求內文中指定的欄位。 此外，先前違反的原則 `Targeting Ads or Content` 需要兩者 `C4 AND C6` 標籤顯示，因此不再違反，如空白所示 `violatedPolicies` 陣列。

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C2",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": []
}
```

## 大量評估原則 {#bulk}

此 `/bulk-eval` 端點可讓您在單一API呼叫中執行多個評估工作。

**API格式**

```http
POST /bulk-eval
```

**请求**

大量評估請求的裝載應為物件陣列；每個要執行的評估工作各一個。 對於根據資料集和欄位進行評估的工作，請 `entityList` 必須提供陣列。 對於根據資料使用標籤進行評估的工作， `labels` 必須提供陣列。

>[!WARNING]
>
>如果列出的任何評估工作同時包含 `entityList` 和 `labels` 陣列，則會導致錯誤。 如果您想要根據資料集和標籤評估相同的行銷動作，則必須為該行銷動作納入個別評估工作。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "labels": [
            "C1",
            "C2",
            "C3"
          ]
        },
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "entityList": [
            {
              "entityType": "dataSet",
              "entityId": "5b67f4dd9f6e710000ea9da4",
              "entityMeta": {
                "fields": [
                  "address"
                ]
              }
            }
          ]
        }
      ]'
```

| 属性 | 描述 |
| --- | --- |
| `evalRef` | 根據原則違規的標籤或資料集進行測試的行銷動作URI。 |
| `includeDraft` | 依預設，只有啟用的原則會參與評估。 若 `includeDraft` 設為 `true`，中的原則 `DRAFT` 狀態也會參與。 |
| `labels` | 用來測試行銷動作的一系列資料使用標籤。<br><br>**重要**：使用此屬性時， `entityList` 屬性不得包含在相同物件中。 若要使用資料集和/或欄位評估相同的行銷動作，您必須在請求裝載中包含個別的物件， `entityList` 陣列。 |
| `entityList` | 資料集陣列，以及這些資料集內用來測試行銷動作的特定欄位（選擇性）。<br><br>**重要**：使用此屬性時， `labels` 屬性不得包含在相同物件中。 若要使用特定資料使用標籤來評估相同的行銷動作，您必須在請求裝載中包含一個單獨的物件， `labels` 陣列。 |
| `entityType` | 要測試行銷動作的實體型別。 目前，僅限 `dataSet` 支援。 |
| `entityId` | 要用來測試行銷動作的資料集ID。 |
| `entityMeta.fields` | （選用）資料集中要用來測試行銷動作的特定欄位清單。 |

**响应**

成功的回應會傳回評估結果的陣列；請求中傳送的每個原則評估工作各一個。

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{ORG_ID}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2",
        "C3"
      ],
      "violatedPolicies": []
    }
  },
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{ORG_ID}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2"
      ],
      "discoveredLabels": [
        {
          "entityType": "dataset",
          "entityId": "5b67f4dd9f6e710000ea9da4",
          "dataSetLabels": {
            "connection": {
              "labels": [

              ]
            },
            "dataset": {
              "labels": [
                "C1",
                "C2"
              ]
            },
            "fields": []
          }
        }
      ],
      "violatedPolicies": [
        {
          "name": "Email Policy",
          "status": "DRAFT",
          "marketingActionRefs": [
            "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting"
          ],
          "description": "Conditions under which we won't send marketing-based email",
          "deny": {
            "label": "C1",
            "operator": "AND",
            "operands": [
              {
                "label": "C1"
              },
              {
                "label": "C3"
              }
            ]
          },
          "id": "76131228-7654-11e8-adc0-fa7ae01bbebc",
          "imsOrg": "{ORG_ID}",
          "created": 1529696681413,
          "createdClient": "{CLIENT_ID}",
          "createdUser": "{USER_ID}",
          "updated": 1529697651972,
          "updatedClient": "{CLIENT_ID}",
          "updatedUser": "{USER_ID}",
          "_links": {
            "self": {
              "href": "./76131228-7654-11e8-adc0-fa7ae01bbebc"
            }
          }
        }
      ]
    }
  }
]
```

## 的原則評估 [!DNL Real-Time Customer Profile]

此 [!DNL Policy Service] API也可用來檢查涉及使用的原則違規 [!DNL Real-Time Customer Profile] 區段。 請參閱教學課程，位置如下： [強制對象區段的資料使用合規性](../../segmentation/tutorials/governance.md) 以取得詳細資訊。

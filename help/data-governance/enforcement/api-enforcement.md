---
keywords: Experience Platform；首頁；熱門主題；原則執行；自動執行；API型執行；資料控管；測試
solution: Experience Platform
title: 使用原則服務API強制執行資料使用原則
type: Tutorial
description: 一旦您為資料建立了資料使用標籤，並針對這些標籤建立了行銷動作的使用原則，您就可以使用原則服務API來評估對資料集或任意一組標籤執行的行銷動作是否構成原則違規。 然後，您可以設定自己的內部通訊協定，以根據API回應處理原則違規。
exl-id: 093db807-c49d-4086-a676-1426426b43fd
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 1%

---

# 使用強制執行資料使用原則 [!DNL Policy Service] API

一旦您建立了資料的資料使用標籤，並針對這些標籤建立了行銷動作的使用原則，您就可以使用 [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) 評估在資料集或任意一組標籤上執行的行銷動作是否構成原則違規。 然後，您可以設定自己的內部通訊協定，以根據API回應處理原則違規。

>[!NOTE]
>
>依預設，只有狀態設定為的原則 `ENABLED` 可以參與評估。 允許 `DRAFT` 要參與評估的原則，您必須包括查詢引數 `includeDraft=true` 在請求路徑中。

本檔案提供如何使用 [!DNL Policy Service] API可檢查不同情境中的原則違規。

## 快速入门

本教學課程需要您深入瞭解下列實施資料使用原則的重要概念：

* [資料控管](../home.md)：作為依據的框架 [!DNL Platform] 強制資料使用規範。
   * [資料使用標籤](../labels/overview.md)：資料使用標籤會套用至資料集（和/或這些資料集中的個別欄位），並指定該資料使用方式的限制。
   * [資料使用原則](../policies/overview.md)：資料使用原則是描述允許或限制某些資料使用標籤集的行銷動作型別的規則。
* [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

在開始本教學課程之前，請檢閱 [開發人員指南](../api/getting-started.md) 如需您成功對 [!DNL Policy Service] API，包括必要的標頭以及如何讀取範例API呼叫。

## 使用標籤和行銷動作進行評估

您可以根據一組假設會出現在資料集中的資料使用標籤來測試行銷動作，以評估原則。 這是透過使用 `duleLabels` 查詢引數，其中標籤是以逗號分隔的值清單提供，如以下範例所示。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 與您正在評估的資料使用原則相關聯的行銷動作名稱。 |
| `{LABEL_1}` | 用來測試行銷動作的資料使用標籤。 至少必須提供一個標籤。 提供多個標籤時，必須以逗號分隔。 |

**请求**

以下請求會測試 `exportToThirdParty` 針對標籤的行銷動作 `C1` 和 `C3`. 由於您先前在本教學課程中建立的資料使用原則會定義 `C1` 標籤為其中一項 `deny` 條件的原則運算式中，行銷動作應觸發原則違規。

>[!NOTE]
>
>資料使用標籤區分大小寫。 只有當原則運算式中定義的標籤完全相符時，才會發生原則違規。 在此範例中， `C1` 標籤會觸發違規，而 `c1` 標籤不會。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功回應會傳回行銷動作的URL、測試該動作時所用的使用標籤，以及針對這些標籤測試該動作所違反的任何原則清單。 在此範例中，「將資料匯出至第三方」原則顯示在 `violatedPolicies` 陣列，指出行銷動作觸發了預期的原則違規。

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "AND",
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
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `violatedPolicies` | 陣列會列出測試行銷動作所違反的任何原則(指定於 `marketingActionRef`)與提供的 `duleLabels`. |

## 使用資料集進行評估

您可以針對可收集標籤的一或多個資料集測試行銷動作，以評估資料使用原則。 這可透過向發出POST請求來完成 `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` 並在請求內文中提供資料集ID，如下列範例所示。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 與您正在評估之原則相關聯的行銷動作名稱。 |

**请求**

以下請求會測試 `exportToThirdParty` 針對三個不同資料集執行行銷動作。 資料集由承載中提供的陣列中的型別和ID引用。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
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
      "entityId": "5cc1fb685410ef14b748c55f",
      "entityMeta": {
          "fields": [
              "/properties/personalEmail/properties/address",
              "/properties/person/properties/name/properties/fullName"
          ]
      }
    }
  ]'
```

| 属性 | 描述 |
| --- | --- |
| `entityType` | 承載陣列中的每個專案都必須指出所定義的實體型別。 對於此使用案例，值將一律為「dataSet」。 |
| `entityId` | 承載陣列中的每個專案都必須提供資料集的唯一ID。 |
| `entityMeta.fields` | （選用）一系列 [JSON指標](../../landing/api-fundamentals.md#json-pointer) 字串，參照資料集結構描述中的特定欄位。 如果包含此陣列，則只有陣列中包含的欄位會參與評估。 陣列中未包含的任何結構描述欄位都不會參與評估。<br><br>如果未包含此欄位，則資料集結構描述中的所有欄位都將包含在評估中。 |

**响应**

成功的回應會傳回行銷動作的URL、從提供的資料集收集的使用情況標籤，以及針對這些標籤測試動作所違反的任何原則清單。 在此範例中，「將資料匯出至第三方」原則顯示在 `violatedPolicies` 陣列，指出行銷動作觸發了預期的原則違規。

```json
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
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
                        "path": "/properties/personalEmail/properties/address",
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/person/properties/name/properties/fullName"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "AND",
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
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `duleLabels` | 從要求裝載中提供的資料集擷取的資料使用標籤清單。 |
| `discoveredLabels` | 請求承載中提供的資料集清單，顯示可在每個資料集中找到之資料集層級和欄位層級標籤。 |
| `violatedPolicies` | 陣列會列出測試行銷動作所違反的任何原則(指定於 `marketingActionRef`)與提供的 `duleLabels`. |

## 后续步骤

透過閱讀本檔案，您在對資料集或一組資料使用標籤執行行銷動作時，已成功檢查原則違規。 您可以使用API回應中傳回的資料，在體驗應用程式中設定通訊協定，以便在發生原則違規時適當地強制執行。

如需Platform如何自動為已啟用的區段提供原則執行的資訊，請參閱以下指南： [自動執行](./auto-enforcement.md).

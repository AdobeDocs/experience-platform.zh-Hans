---
keywords: Experience Platform；首頁；熱門主題；原則執行；API型執行；資料控管
solution: Experience Platform
title: 資料控管原則API端點
description: 資料控管原則是貴組織採用的規則，用於說明允許或限制您對Experience Platform內的資料執行的行銷動作型別。 /policies端點用於與檢視、建立、更新或刪除資料治理原則相關的所有API呼叫。
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 2%

---

# 資料治理原則端點

資料控管原則是描述允許或限制您對內資料執行何種行銷動作的規則 [!DNL Experience Platform]. 此 `/policies` 中的端點 [!DNL Policy Service API] 可讓您以程式設計方式管理組織的資料控管原則。

>[!IMPORTANT]
>
>治理原則不應與存取控制原則混淆，存取控制原則會決定組織中特定Platform使用者可存取的特定資料屬性。 請參閱 `/policies` 的端點指南 [存取控制API](../../access-control/abac/api/policies.md) 有關如何以程式設計方式管理存取控制原則的詳細資訊。

## 快速入门

本指南中使用的API端點是 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). 在繼續之前，請檢閱 [快速入門手冊](getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功對任一檔案發出呼叫所需必要標題的重要資訊 [!DNL Experience Platform] API。

## 擷取原則清單 {#list}

您可以列出所有 `core` 或 `custom` 向發出GET請求以制定原則 `/policies/core` 或 `/policies/custom`（分別）。

**API格式**

```http
GET /policies/core
GET /policies/custom
```

**请求**

以下請求會擷取貴組織定義的自訂原則清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應包括 `children` 列出每個擷取原則的詳細資訊的陣列，包括其 `id` 值。 您可以使用 `id` 要執行的特定原則的欄位 [查詢](#lookup)， [更新](#update)、和 [刪除](#delete) 該原則的要求。

```JSON
{
    "_page": {
        "start": "5c6dacdf685a4913dc48937c",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/policies/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "Export Data to Third Party",
            "status": "DRAFT",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
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
            "created": 1550691551888,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550701472910,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
                }
            },
            "id": "5c6dacdf685a4913dc48937c"
        },
        {
            "name": "Combine Data",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
            ],
            "description": "Data that meets these conditions cannot be combined.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "I1"
                    }
                ]
            },
            "imsOrg": "{ORG_ID}",
            "created": 1550703519823,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550714340335,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
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

| 属性 | 描述 |
| --- | --- |
| `_page.count` | 已擷取的原則總數。 |
| `name` | 原則的顯示名稱。 |
| `status` | 原則的目前狀態。 可能的狀態有三種： `DRAFT`， `ENABLED`，或 `DISABLED`. 依預設，僅限 `ENABLED` 原則會參與評估。 請參閱以下文章的概觀： [原則評估](../enforcement/overview.md) 以取得詳細資訊。 |
| `marketingActionRefs` | 列出原則所有適用行銷動作的URI的陣列。 |
| `description` | 選擇性說明，提供原則使用案例的進一步內容。 |
| `deny` | 描述原則的相關行銷動作限制執行的特定資料使用標籤的物件。 請參閱以下小節： [建立原則](#create-policy) 以取得此屬性的詳細資訊。 |

## 查詢原則 {#look-up}

您可以包含特定原則，以查詢該原則 `id` GET要求路徑中的屬性。

**API格式**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 此 `id` 您想要查閱的原則的URL。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回原則的詳細資訊。

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
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
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550714340335,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

| 属性 | 描述 |
| --- | --- |
| `name` | 原則的顯示名稱。 |
| `status` | 原則的目前狀態。 可能的狀態有三種： `DRAFT`， `ENABLED`，或 `DISABLED`. 依預設，僅限 `ENABLED` 原則會參與評估。 請參閱以下文章的概觀： [原則評估](../enforcement/overview.md) 以取得詳細資訊。 |
| `marketingActionRefs` | 列出原則所有適用行銷動作的URI的陣列。 |
| `description` | 選擇性說明，提供原則使用案例的進一步內容。 |
| `deny` | 說明原則的相關行銷動作限制執行的特定資料使用標籤的物件。 請參閱以下小節： [建立原則](#create-policy) 以取得此屬性的詳細資訊。 |

## 建立自訂原則 {#create-policy}

在 [!DNL Policy Service] API中，原則由以下專案定義：

* 特定行銷動作的參考
* 描述行銷動作被限制執行的資料使用標籤的運算式

為了滿足後一種要求，原則定義必須包括關於資料使用標籤存在的布林運算式。 此運算式稱為原則運算式。

提供原則運算式的形式為 `deny` 屬性（在每個原則定義中）。 簡單範例 `deny` 僅檢查單一標籤是否存在的物件如下所示：

```json
"deny": {
    "label": "C1"
}
```

不過，許多原則會針對資料使用標籤的存在指定更複雜的條件。 若要支援這些使用案例，您也可以包含布林運算來說明您的原則運算式。 原則運算式物件必須包含標籤或運運算元和運算元，但不能同時包含兩者。 反過來，每個運算元也是原則運算式物件。

例如，為了定義禁止對資料執行行銷動作的原則， `C1 OR (C3 AND C7)` 標籤存在，原則的 `deny` 屬性將指定為：

```JSON
"deny": {
  "operator": "OR",
  "operands": [
    {"label": "C1"},
    {
      "operator": "AND",
      "operands": [
        {"label": "C3"},
        {"label": "C7"}
      ]
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `operator` | 表示同層級中提供的標籤之間的條件關係 `operands` 陣列。 接受的值包括： <ul><li>`OR`：如果中的任何標籤，運算式會解析為true `operands` 陣列存在。</li><li>`AND`：只有在 `operands` 陣列存在。</li></ul> |
| `operands` | 一個物件陣列，每個物件分別代表一個標籤或另外一對標籤 `operator` 和 `operands` 屬性。 標籤和/或作業是否存在 `operands` 陣列會根據其同層級的值解析為true或false `operator` 屬性。 |
| `label` | 套用至原則的單一資料使用標籤的名稱。 |

您可以透過向以下專案發出POST請求，以建立新的自訂原則： `/policies/custom` 端點。

**API格式**

```http
POST /policies/custom
```

**请求**

以下請求會建立限制行銷動作的新原則 `exportToThirdParty` 不在包含標籤的資料上執行 `C1 OR (C3 AND C7)`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "OR",
          "operands": [
            {"label": "C1"},
            {
              "operator": "AND",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 原則的顯示名稱。 |
| `status` | 原則的目前狀態。 可能的狀態有三種： `DRAFT`， `ENABLED`，或 `DISABLED`. 依預設，僅限 `ENABLED` 原則會參與評估。 請參閱以下文章的概觀： [原則評估](../enforcement/overview.md) 以取得詳細資訊。 |
| `marketingActionRefs` | 列出原則所有適用行銷動作的URI的陣列。 行銷動作的URI提供於 `_links.self.href` 在的回應中 [查詢行銷動作](./marketing-actions.md#look-up). |
| `description` | 選擇性說明，提供原則使用案例的進一步內容。 |
| `deny` | 說明特定資料使用標籤的原則運算式，限制執行原則的相關行銷動作。 |

**响应**

成功的回應會傳回新建立原則的詳細資訊，包括其 `id`. 此值是唯讀的，會在建立原則時自動指派。

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550691551888,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 更新自訂原則 {#update}

>[!IMPORTANT]
>
>您只能更新自訂原則。 如果您想要啟用或停用核心原則，請參閱以下章節： [更新已啟用的核心原則清單](#update-enabled-core).

您可以透過在PUT請求的路徑中提供其ID來更新現有的自訂原則，其裝載包含整個原則的更新形式。 換言之，PUT要求基本上會重寫原則。

>[!NOTE]
>
>請參閱以下小節： [更新部分自訂原則](#patch) 如果您只想更新原則的一或多個欄位，而不是覆寫原則。

**API格式**

```http
PUT /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 此 `id` 要更新的原則。 |

**请求**

在此範例中，將資料匯出至協力廠商的條件已變更，現在您需要建立的原則來拒絕此行銷動作，如果 `C1 AND C5` 出現資料標籤。

以下請求會更新現有原則以包含新的原則運算式。 請注意，由於此請求基本上會重寫原則，因此所有欄位都必須包含在裝載中，即使其某些值未更新。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "../marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "AND",
          "operands": [
            {"label": "C1"},
            {"label": "C5"}
          ]
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 原則的顯示名稱。 |
| `status` | 原則的目前狀態。 可能的狀態有三種： `DRAFT`， `ENABLED`，或 `DISABLED`. 依預設，僅限 `ENABLED` 原則會參與評估。 請參閱以下文章的概觀： [原則評估](../enforcement/overview.md) 以取得詳細資訊。 |
| `marketingActionRefs` | 列出原則所有適用行銷動作的URI的陣列。 行銷動作的URI提供於 `_links.self.href` 在的回應中 [查詢行銷動作](./marketing-actions.md#look-up). |
| `description` | 選擇性說明，提供原則使用案例的進一步內容。 |
| `deny` | 說明特定資料使用標籤的原則運算式，限制執行原則的相關行銷動作。 請參閱以下小節： [建立原則](#create-policy) 以取得此屬性的詳細資訊。 |

**响应**

成功的回應會傳回更新原則的詳細資訊。

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/core/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "label": "C5"
            }
        ]
    },
    "imsOrg": "{ORG_ID}",
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550701472910,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 更新部分自訂原則 {#patch}

>[!IMPORTANT]
>
>您只能更新自訂原則。 如果您想要啟用或停用核心原則，請參閱以下章節： [更新已啟用的核心原則清單](#update-enabled-core).

可以使用PATCH請求更新原則的特定部分。 不同於重寫原則的PUT要求，PATCH要求僅更新要求內文中指定的屬性。 當您想要啟用或停用原則時，此功能特別有用，因為您只需要提供適當屬性的路徑(`/status`)及其值(`ENABLED` 或 `DISABLED`)。

>[!NOTE]
>
>PATCH請求的裝載遵循JSON修補程式格式。 請參閱 [API基礎指南](../../landing/api-fundamentals.md) 以取得接受語法的詳細資訊。

此 [!DNL Policy Service] API支援JSON修補程式操作 `add`， `remove`、和 `replace`，並可讓您將數個更新一起合併為單一呼叫，如下列範例所示。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 此 `id` 要更新其屬性的原則的。 |

**请求**

以下請求使用兩個 `replace` 變更原則狀態的作業 `DRAFT` 至 `ENABLED`，並更新 `description` 欄位及新的說明。

>[!IMPORTANT]
>
>在單一請求中傳送多個PATCH作業時，將會依照作業在陣列中出現的順序進行處理。 確保您在必要時以正確的順序傳送請求。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' [
          {
            "op": "replace",
            "path": "/status",
            "value": "ENABLED"
          },
          {
            "op": "replace",
            "path": "/description",
            "value": "New policy description."
          }
        ]'
```

**响应**

成功的回應會傳回更新原則的詳細資訊。


```JSON
{
    "name": "Export Data to Third Party",
    "status": "ENABLED",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "New policy description.",
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
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550712163182,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 刪除自訂原則 {#delete}

您可以包含自訂原則，將其刪除 `id` 在DELETE請求的路徑中。

>[!WARNING]
>
>一旦刪除，原則就無法復原。 最佳實務是 [執行查詢(GET)請求](#lookup) 首先檢視原則，並確認它是您要移除的正確原則。

**API格式**

```http
DELETE /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 您要刪除之原則的ID。 |

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態200 （確定），並出現空白內文。

您可以再次嘗試查詢(GET)原則以確認刪除。 如果原則已成功刪除，您應該會收到HTTP 404 （找不到）錯誤。

## 擷取已啟用的核心原則清單 {#list-enabled-core}

依預設，只有已啟用的資料治理原則會參與評估。 您可以透過向以下網站發出GET要求，擷取貴組織目前啟用的核心原則清單： `/enabledCorePolicies` 端點。

**API格式**

```http
GET /enabledCorePolicies
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回底下啟用的核心原則清單 `policyIds` 陣列。

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0003",
    "corepolicy_0004",
    "corepolicy_0005",
    "corepolicy_0006",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{ORG_ID}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## 更新已啟用的核心原則清單 {#update-enabled-core}

依預設，只有已啟用的資料治理原則會參與評估。 藉由向發出PUT請求 `/enabledCorePolicies` 端點，您可使用單一呼叫來更新貴組織的已啟用核心原則清單。

>[!NOTE]
>
>此端點只能啟用或停用核心原則。 若要啟用或停用自訂原則，請參閱以下章節： [更新原則的一部分](#patch).

**API格式**

```http
PUT /enabledCorePolicies
```

**请求**

以下請求會根據承載中提供的ID更新已啟用的核心原則清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "policyIds": [
          "corepolicy_0001",
          "corepolicy_0002",
          "corepolicy_0007",
          "corepolicy_0008"
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `policyIds` | 要啟用的核心原則ID清單。 任何未包含的核心原則都會設為 `DISABLED` 狀態，且不會參與評估。 |

**响应**

成功的回應會傳回底下啟用的核心原則更新清單 `policyIds` 陣列。

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{ORG_ID}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1595876052649,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## 后续步骤

定義新原則或更新現有原則後，您可以使用 [!DNL Policy Service] API可針對特定標籤或資料集測試行銷動作，並檢視您的原則是否如預期般引發違規。 請參閱 [原則評估端點](./evaluation.md) 以取得詳細資訊。

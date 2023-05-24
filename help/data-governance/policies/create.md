---
keywords: Experience Platform；首頁；熱門主題；資料控管；資料使用原則
solution: Experience Platform
title: 在API中建立資料控管原則
type: Tutorial
description: 瞭解如何使用原則服務API建立資料治理原則。
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 2%

---

# 在API中建立資料治理原則

此 [原則服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 可讓您建立和管理資料控管原則，以決定可以對包含特定資料使用標籤的資料採取哪些行銷動作。

本檔案提供逐步教學課程，說明如何使用建立治理原則。 [!DNL Policy Service] API。

>[!NOTE]
>
>如需如何建立存取控制原則的步驟，請參閱 `/policies` 的端點指南 [存取控制API](../../access-control/abac/api/policies.md). 若要瞭解如何建立同意原則，請參閱 [原則UI指南](./user-guide.md#consent-policy).

## 快速入门

本教學課程需要深入瞭解建立與評估原則相關的下列重要概念：

* [Adobe Experience Platform資料控管](../home.md)：作為依據的框架 [!DNL Platform] 強制資料使用規範。
   * [資料使用標籤](../labels/overview.md)：資料使用標籤會套用至XDM資料欄位，並指定存取該資料方式的限制。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Platform] 組織客戶體驗資料。
* [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

在開始本教學課程之前，請檢閱 [開發人員指南](../api/getting-started.md) 如需您成功對 [!DNL Policy Service] API，包括必要的標頭以及如何讀取範例API呼叫。

## 定義行銷動作 {#define-action}

在資料控管框架中，行銷動作是指要 [!DNL Experience Platform] 資料取用者需要檢查資料使用原則是否違規。

建立資料使用原則的第一步，是決定該原則將評估哪些行銷動作。 您可使用下列其中一個選項來達成此目的：

* [查詢現有的行銷動作](#look-up)
* [建立新的行銷動作](#create-new)

### 查詢現有的行銷動作 {#look-up}

您可以透過向以下其中一項發出GET要求，查詢現有行銷動作，以由您的原則進行評估： `/marketingActions` 端點。

**API格式**

視您是否要查詢提供的行銷動作而定 [!DNL Experience Platform] 或您的組織建立的自訂行銷動作，使用 `marketingActions/core` 或 `marketingActions/custom` 端點。

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**请求**

以下請求使用 `marketingActions/custom` 端點會擷取貴組織定義的所有行銷動作清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回找到的行銷動作總數(`count`)，並列出 `children` 陣列。

```json
{
    "_page": {
        "start": "sampleMarketingAction",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{ORG_ID}",
            "created": 1550714012088,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714012088,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{ORG_ID}",
            "created": 1550793833224,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550793833224,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `_links.self.href` | 內的每個專案 `children` 陣列包含所列行銷動作的URI ID。 |

當您找到要使用的行銷動作時，請記錄其值 `href` 屬性。 此值會在的下一個步驟中使用 [建立原則](#create-policy).

### 建立新的行銷動作 {#create-new}

您可以透過向以下傳送PUT請求，建立新的行銷動作： `/marketingActions/custom/` 端點並在請求路徑結尾提供行銷動作的名稱。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 您要建立的新行銷動作名稱。 此名稱會作為行銷動作的主要識別碼，因此必須是唯一的。 最佳實務是為行銷動作提供描述性但簡潔的名稱。 |

**请求**

以下請求會建立名為「exportToThirdParty」的新自訂行銷動作。 請注意 `name` 請求裝載中的名稱與請求路徑中提供的名稱相同。

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "exportToThirdParty",
      "description": "Export data to a third party"
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 您要建立的行銷動作名稱。 此名稱必須符合請求路徑中提供的名稱，否則會發生400 （錯誤請求）錯誤。 |
| `description` | 人類看得懂的行銷動作說明。 |

**响应**

成功的回應會傳回HTTP狀態201 （已建立）和新建立行銷動作的詳細資訊。

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{ORG_ID}",
    "created": 1550713341915,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1550713856390,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        }
    }
}
```

| 属性 | 描述 |
| --- | --- |
| `_links.self.href` | 行銷動作的URI ID。 |

記錄新建立之行銷動作的URI ID，因為它將用於建立原則的下一個步驟。

## 创建策略 {#create-policy}

建立新原則需要您提供行銷動作的URI ID，以及禁止該行銷動作的使用標籤運算式。

此運算式稱為原則運算式，是包含(A)標籤或(B)運運算元和運算元的物件，但不能同時包含兩者。 反過來，每個運算元也是原則運算式物件。 例如，在下列情況下，可能會禁止將資料匯出至協力廠商 `C1 OR (C3 AND C7)` 標籤已存在。 此運算式將指定為：

```json
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
}
```

>[!NOTE]
>
>僅支援OR和AND運運算元。

設定原則運算式後，您可以透過向以下專案發出POST請求來建立新原則： `/policies/custom` 端點。

**API格式**

```http
POST /policies/custom
```

**请求**

下列請求會建立名為「將資料匯出至第三方」的原則，方法是在請求承載中提供行銷動作和原則運算式。

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
      "../marketingActions/custom/exportToThirdParty"
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
| `marketingActionRefs` | 一個包含 `href` 行銷動作的值，取得於 [上一步](#define-action). 雖然上述範例僅列出一個行銷動作，但也可以提供多個動作。 |
| `deny` | 原則運算式物件。 定義會使得原則拒絕中參考之行銷動作的使用標籤和條件 `marketingActionRefs`. |

**响应**

成功的回應會傳回HTTP狀態201 （已建立）和新建立原則的詳細資訊。

```json
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
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
    "updated": 1565651746693,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 唯讀、系統產生的值，可唯一識別原則。 |

記錄新建立之原則的URI ID，因為它用於下一個步驟以啟用原則。

## 啟用原則

>[!NOTE]
>
>如果您想要將原則保留在 `DRAFT` 狀態，請注意，原則預設必須將其狀態設定為 `ENABLED` 以參與評估。 請參閱指南： [原則執行](../enforcement/api-enforcement.md) 有關如何為中的原則制定例外的資訊 `DRAFT` 狀態。

依預設，具備以下條件的原則： `status` 屬性設定為 `DRAFT` 不要參與評估。 您可以透過向以下網站發出PATCH請求，以啟用評估原則： `/policies/custom/` 端點並在要求路徑結尾提供原則的唯一識別碼。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 此 `id` 要啟用的原則值。 |

**请求**

PATCH以下請求會對 `status` 原則的屬性，將其值從 `DRAFT` 至 `ENABLED`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    {
      "op": "replace",
      "path": "/status",
      "value": "ENABLED"
    }
  ]'
```

| 属性 | 描述 |
| --- | --- |
| `op` | 要執行的PATCH作業型別。 此請求會執行「取代」操作。 |
| `path` | 要更新之欄位的路徑。 啟用原則時，值必須設定為「/status」。 |
| `value` | 要指派給中指定的屬性的新值 `path`. 此請求會設定原則的 `status` 屬性重新命名為「ENABLED」。 |

**响应**

成功的回應會傳回HTTP狀態200 （確定）和已更新原則的詳細資訊，以及其 `status` 現在設定為 `ENABLED`.

```json
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
    "createdUser": "{CREATED_USER}",
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
```

## 后续步骤

依照本教學課程，您已成功建立行銷動作的資料使用原則。 您現在可以繼續上的教學課程 [強制資料使用原則](../enforcement/api-enforcement.md) 瞭解如何檢查原則違規，並在您的體驗應用程式中處理這些違規。

如需中不同可用操作的詳細資訊， [!DNL Policy Service] API，請參閱 [原則服務開發人員指南](../api/getting-started.md). 如需如何強制執行原則的詳細資訊， [!DNL Real-Time Customer Profile] 資料，請參閱以下主題上的教學課程： [強制對象區段的資料使用合規性](../../segmentation/tutorials/governance.md).

若要瞭解如何在中管理使用原則 [!DNL Experience Platform] 使用者介面，請參閱 [原則使用手冊](user-guide.md).

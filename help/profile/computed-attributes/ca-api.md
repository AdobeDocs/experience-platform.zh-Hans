---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 計算屬性API端點
type: Documentation
description: 在Adobe Experience Platform中，計算屬性是用於彙總事件層級資料至設定檔層級屬性的函式。 這些函式會自動計算，以便用於區段、啟用和個人化。 本指南說明如何使用即時客戶設定檔API建立、檢視、更新和刪除計算屬性。
exl-id: 6b35ff63-590b-4ef5-ab39-c36c39ab1d58
hide: true
hidefromtoc: true
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2274'
ht-degree: 2%

---

# (Alpha)計算屬性API端點

>[!IMPORTANT]
>
>本檔案中概述的計算屬性功能目前為Alpha版，並非所有使用者都可使用。 文档和功能可能会发生变化。

計算屬性是用來將事件層級資料彙總到設定檔層級屬性的函式。 這些函式會自動計算，以便用於區段、啟用和個人化。 本指南包含使用執行基本CRUD作業的API呼叫範例 `/computedAttributes` 端點。

若要進一步瞭解運算屬性，請先閱讀 [計算屬性概觀](overview.md).

## 快速入门

本指南中使用的API端點是 [即時客戶設定檔API](https://www.adobe.com/go/profile-apis-en).

在繼續之前，請檢閱 [設定檔API快速入門手冊](../api/getting-started.md) 如需建議檔案的連結、閱讀本檔案中所顯示範例API呼叫的指南，以及有關成功呼叫任何Experience PlatformAPI所需標題的重要資訊。

## 設定計算屬性欄位

若要建立計算屬性，您首先需要識別將儲存計算屬性值的結構描述中的欄位。

請參閱以下說明檔案： [設定計算屬性](configure-api.md) 以取得在結構描述中建立計算屬性欄位的完整端對端指南。

>[!WARNING]
>
>為了繼續進行API指南，您必須設定計算屬性欄位。

## 建立計算屬性 {#create-a-computed-attribute}

在啟用設定檔的結構描述中定義運算屬性欄位後，您現在可以設定運算屬性。 如果您尚未執行此動作，請依照以下說明的工作流程： [設定計算屬性](configure-api.md) 說明檔案。

POST若要建立計算屬性，請從對 `/config/computedAttributes` 端點，要求內文包含您要建立之計算屬性的詳細資料。

**API格式**

```http
POST /config/computedAttributes
```

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "birthdayCurrentMonth",
        "path": "_{TENANT_ID}",
        "description": "Computed attribute to capture if the customer birthday is in the current month.",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| 属性 | 描述 |
|---|---|
| `name` | 計算屬性欄位的名稱，以字串表示。 |
| `path` | 包含計算屬性的欄位路徑。 此路徑可在 `properties` 結構描述的屬性，且不應在路徑中包含欄位名稱。 寫入路徑時，省略以下多個層級 `properties` 屬性。 |
| `{TENANT_ID}` | 如果您不熟悉租使用者ID，請參考以下步驟來尋找您的租使用者ID： [Schema Registry開發人員指南](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | 計算屬性的說明。 定義多個計算屬性後，這項功能會特別有用，因為可協助組織內的其他人決定要使用的正確計算屬性。 |
| `expression.value` | 有效的 [!DNL Profile Query Language] (PQL)運算式。 計算屬性目前支援下列函式：sum、count、min、max和boolean。 如需範例運算式的清單，請參閱 [PQL運算式範例](expressions.md) 說明檔案。 |
| `schema.name` | 包含計算屬性欄位的結構描述所依據的類別。 範例： `_xdm.context.experienceevent` 適用於以XDM ExperienceEvent類別為基礎的結構描述。 |

**响应**

成功建立的計算屬性會傳回HTTP狀態200 （確定）以及包含新建立計算屬性之詳細資訊的回應內文。 這些詳細資料包括系統產生的唯一、唯讀 `id` 可用於在其他API作業期間參照計算屬性的屬性。

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

| 属性 | 描述 |
|---|---|
| `id` | 唯一、唯讀、系統產生的ID，可用於在其他API作業期間參照運算屬性。 |
| `imsOrgId` | 與計算屬性相關的IMS組織應符合請求中傳送的值。 |
| `sandbox` | 沙箱物件包含設定運算屬性的沙箱詳細資訊。 此資訊是從請求中傳送的沙箱標頭中擷取的。 如需詳細資訊，請參閱 [沙箱總覽](../../sandboxes/home.md). |
| `positionPath` | 包含已解構的陣列 `path` 至要求中傳送的欄位。 |
| `returnSchema.meta:xdmType` | 將儲存計算屬性的欄位型別。 |
| `definedOn` | 顯示已定義計算屬性的聯合結構描述的陣列。 每個聯合結構描述包含一個物件，這表示如果計算屬性已根據不同類別新增至多個結構描述，則陣列中可能會有多個物件。 |
| `active` | 顯示運算屬性目前是否有效的布林值。 默认情况下，该值为 `true`。 |
| `type` | 已建立的資源型別，在此例中，「ComputedAttribute」是預設值。 |
| `createEpoch` 和 `updateEpoch` | 分別建立及上次更新計算屬性的時間。 |

## 建立參照現有計算屬性的計算屬性

您也可以建立參照現有計算屬性的計算屬性。 若要這麼做，請先向發出POST要求 `/config/computedAttributes` 端點。 要求內文將包含對下列專案中所計算屬性的參考： `expression.value` 欄位，如下列範例所示。

**API格式**

```http
POST /config/computedAttributes
```

**请求**

在此範例中，已建立兩個計算屬性，並將用來定義第三個屬性。 現有的計算屬性包括：

* **`totalSpend`：** 擷取客戶已花費的總金額。
* **`countPurchases`：** 計算客戶已購買的次數。

以下請求會參考兩個現有的計算屬性，使用有效的PQL進行除以計算新的 `averageSpend` 計算屬性。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "averageSpend",
        "path": "_{TENANT_ID}.purchaseSummary",
        "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| 属性 | 描述 |
|---|---|
| `name` | 計算屬性欄位的名稱，以字串表示。 |
| `path` | 包含計算屬性的欄位路徑。 此路徑可在 `properties` 結構描述的屬性，且不應在路徑中包含欄位名稱。 寫入路徑時，省略以下多個層級 `properties` 屬性。 |
| `{TENANT_ID}` | 如果您不熟悉租使用者ID，請參考以下步驟來尋找您的租使用者ID： [Schema Registry開發人員指南](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | 計算屬性的說明。 定義多個計算屬性後，此功能會特別有用，因為此功能可協助您IMS組織內的其他人決定要使用的正確計算屬性。 |
| `expression.value` | 有效的PQL運算式。 計算屬性目前支援下列函式：sum、count、min、max和boolean。 如需範例運算式的清單，請參閱 [PQL運算式範例](expressions.md) 說明檔案。<br/><br/>在此範例中，運算式會參考兩個現有的計算屬性。 屬性是使用 `path` 和 `name` 運算屬性的ID值，因為它們出現在定義運算屬性的結構描述中。 例如， `path` 第一個參照的計算屬性為 `_{TENANT_ID}.purchaseSummary` 和 `name` 是 `totalSpend`. |
| `schema.name` | 包含計算屬性欄位的結構描述所依據的類別。 範例： `_xdm.context.experienceevent` 適用於以XDM ExperienceEvent類別為基礎的結構描述。 |

**响应**

成功建立的計算屬性會傳回HTTP狀態200 （確定）以及包含新建立計算屬性之詳細資訊的回應內文。 這些詳細資料包括系統產生的唯一、唯讀 `id` 可用於在其他API作業期間參照計算屬性的屬性。

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "averageSpend",
    "path": "_{TENANT_ID}.purchaseSummary",
    "positionPath": [
        "_{TENANT_ID}",
        "purchaseSummary"
    ],
    "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
    "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "number"
    },
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"\bVR)JMSR())(+KLOJKկHO+I(/(OI/S8{E:",
    "dependencies": [
        "c08a92f3-2418-4a3d-89d0-96f15fda3e5d",
        "4ed9e3aa-57ae-4705-9e8a-7fba9a6a7010"
    ],
    "dependents": [],
    "active": true,
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
    "type": "ComputedAttribute",
    "createEpoch": 1613696592,
    "updateEpoch": 1613696593
}
```

| 属性 | 描述 |
|---|---|
| `id` | 唯一、唯讀、系統產生的ID，可用於在其他API作業期間參照運算屬性。 |
| `imsOrgId` | 與計算屬性相關的IMS組織應符合請求中傳送的值。 |
| `sandbox` | 沙箱物件包含設定運算屬性的沙箱詳細資訊。 此資訊是從請求中傳送的沙箱標頭中擷取的。 如需詳細資訊，請參閱 [沙箱總覽](../../sandboxes/home.md). |
| `positionPath` | 包含已解構的陣列 `path` 至要求中傳送的欄位。 |
| `returnSchema.meta:xdmType` | 將儲存計算屬性的欄位型別。 |
| `definedOn` | 顯示已定義計算屬性的聯合結構描述的陣列。 每個聯合結構描述包含一個物件，這表示如果計算屬性已根據不同類別新增至多個結構描述，則陣列中可能會有多個物件。 |
| `active` | 顯示運算屬性目前是否有效的布林值。 默认情况下，该值为 `true`。 |
| `type` | 已建立的資源型別，在此例中，「ComputedAttribute」是預設值。 |
| `createEpoch` 和 `updateEpoch` | 分別建立及上次更新計算屬性的時間。 |

## 存取計算屬性

使用API使用計算屬性時，有兩個選項可用於存取您的組織已定義的計算屬性。 第一個是列出所有計算屬性，第二個是檢視特定計算屬性（依其唯一性） `id`.

本檔案概述了這兩種存取模式的步驟。 選取下列其中一個專案以開始：

* **[列出所有現有的計算屬性](#list-all-computed-attributes)：** 傳回貴組織已建立的所有現有計算屬性清單。
* **[檢視特定的計算屬性](#view-a-computed-attribute)：** 在要求期間指定單一計算屬性的ID，以傳回其詳細資訊。

### 列出所有計算屬性 {#list-all-computed-attributes}

GET您的IMS組織可以建立多個計算屬性，並對 `/config/computedAttributes` 端點可讓您列出組織的所有現有計算屬性。

**API格式**

```http
GET /config/computedAttributes
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的回應包括 `_page` 屬性提供計算屬性的總數(`totalCount`)和頁面上的計算屬性數目(`pageSize`)。

回應也包含 `children` 陣列由一或多個物件組成，每個物件都包含一個計算屬性的詳細資訊。 如果您的組織沒有任何計算屬性， `totalCount` 和 `pageSize` 將為0 （零）且 `children` 陣列將是空的。

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "birthdayCurrentMonth",
            "path": "person._{TENANT_ID}",
            "positionPath": [
                "person",
                "_{TENANT_ID}"
            ],
            "description": "Computed attribute to capture if the customer birthday is in the current month.",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "person.birthDate.getMonth() = currentMonth()"
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1572555223,
            "updateEpoch": 1572555225
        },
        {
            "id": "ae0c6552-cf49-4725-8979-116366e8e8d3",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "productDownloads",
            "path": "_{TENANT_ID}",
            "positionPath": [
                "_{TENANT_ID}"
            ],
            "description": "Calculate total product downloads.",
            "expression": {
                "type": "PQL", 
                "format": "pql/text", 
                "value":  "let Y = xEvent[_coresvc.event.subType = \"DOWNLOAD\"].groupBy(_coresvc.attributes[name = \"product\"].value).map({
                  \"downloaded\": this.head()._coresvc.attributes[name = \"product\"].head().value,
                  \"downloadsSum\": this.count(),
                  \"downloadsToday\": this[timestamp occurs today].count(),
                  \"downloadsPast30Days\": this[timestamp occurs < 30 days before now].count(),
                  \"downloadsPast60Days\": this[timestamp occurs < 60 days before now].count(),
                  \"downloadsPast90Days\": this[timestamp occurs < 90 days before now].count() }) in { \"uniqueProductDownloadSum\": Y.count(), \"products\": Y }"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "schema": {
                "name": "_xdm.context.profile"
            },
            "encodedDefinedOn": "\u001f?\b\u0000\u0000\u0000\u0000\u0000\u0000\u0000?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?\u0005\u00008{?E:\u0000\u0000\u0000",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1571945277,
            "updateEpoch": 1571945280
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| 属性 | 描述 |
|---|---|
| `_page.totalCount` | 您的IMS組織定義的計算屬性總數。 |
| `_page.pageSize` | 在此結果頁面上傳回的計算屬性數目。 若 `pageSize` 等於 `totalCount`，這表示結果只有一頁，且已傳回所有計算屬性。 如果兩者不相等，則有其他可存取的結果頁面。 另請參閱 `_links.next` 以取得詳細資訊。 |
| `children` | 由一或多個物件組成的陣列，每個物件都包含單一計算屬性的詳細資訊。 如果尚未定義計算屬性，則 `children` 陣列是空的。 |
| `id` | 建立計算屬性時，系統自動指派的唯一唯讀值。 如需計算屬性物件之元件的詳細資訊，請參閱以下章節： [建立計算屬性](#create-a-computed-attribute) 在本教學課程的前面部分。 |
| `_links.next` | 如果傳回單一頁面的計算屬性， `_links.next` 為空白物件，如上述範例回應所示。 如果您的組織有許多計算屬性，系統會在多個頁面上傳回這些屬性，您可以透過向發出GET請求來存取這些屬性。 `_links.next` 值。 |

### 檢視計算屬性 {#view-a-computed-attribute}

您可以透過向以下專案發出GET要求來檢視特定的計算屬性： `/config/computedAttributes` 端點並在要求路徑中包含運算屬性ID。

**API格式**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| 参数 | 描述 |
|---|---|
| `{ATTRIBUTE_ID}` | 您要檢視的計算屬性ID。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

## 更新計算屬性

如果您發現需要更新現有的計算屬性，可透過向發出PATCH要求來完成 `/config/computedAttributes` 端點，並包含您要在請求路徑中更新的計算屬性的ID。

**API格式**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| 参数 | 描述 |
|---|---|
| `{ATTRIBUTE_ID}` | 您要更新的計算屬性ID。 |

**请求**

此請求使用 [JSON修補程式格式](https://datatracker.ietf.org/doc/html/rfc6902) 更新「運算式」欄位的「值」。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type": "PQL", 
            "format": "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| 属性 | 描述 |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | 有效的 [!DNL Profile Query Language] (PQL)運算式。 計算屬性目前支援下列函式：sum、count、min、max和boolean。 如需範例運算式的清單，請參閱 [PQL運算式範例](expressions.md) 說明檔案。 |

**响应**

成功的更新會傳回HTTP狀態204 （無內容）和空白的回應內文。 如果您希望確認更新成功，可以執行GET要求，以依據其ID檢視計算屬性。

## 刪除計算屬性

您也可以使用API刪除計算屬性。 這是透過向發出DELETE請求來完成 `/config/computedAttributes` 端點，並包含您想要在要求路徑中刪除的計算屬性ID。

>[!NOTE]
>
>刪除計算屬性時請務必小心，因為它可能用於多個結構描述，且DELETE操作無法復原。

**API格式**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| 参数 | 描述 |
|---|---|
| `{ATTRIBUTE_ID}` | 要刪除的計算屬性的ID。 |

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**响应**

成功的刪除請求會傳回HTTP狀態200 （確定）和空白的回應內文。 若要確認刪除成功，您可以執行GET要求，依其ID查詢運算屬性。 如果屬性已刪除，您會收到HTTP狀態404 （找不到）錯誤。

## 建立參考計算屬性的區段定義

Adobe Experience Platform可讓您建立區段，從一組設定檔中定義一組特定屬性或行為。 區段定義包含運算式，該運算式封裝以PQL撰寫的查詢。 這些運算式也可以參考計算屬性。

下列範例會建立參考現有計算屬性的區段定義。 若要進一步瞭解區段定義，以及如何在Segmentation Service API中使用這些定義，請參閱 [區段定義API端點指南](../../segmentation/api/segment-definitions.md).

若要開始，請向發出POST要求 `/segment/definitions` 端點，在要求內文中提供計算屬性。

**API格式**

```http
POST /segment/definitions
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "downloadedInLast7Days",
        "description": "Has product been downloaded in last 7 days?",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "ttlInDays": 30,
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "_{TENANT_ID}.downloadsLast7Days > 0",
            "meta": "m"
        },
        "dataGovernancePolicy": {
            "excludeOptOut": true
        },
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
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 區段的唯一名稱（字串）。 |
| `description` | 可讀取的定義說明。 |
| `schema.name` | 與區段中的實體相關聯的結構描述。 包含 `id` 或 `name` 欄位。 |
| `expression` | 一個物件，其中包含具有區段定義相關資訊的欄位。 |
| `expression.type` | 指定運算式型別。 目前僅支援「PQL」。 |
| `expression.format` | 指示值中運算式的結構。 目前，僅限 `pql/text` 支援。 |
| `expression.value` | 有效的PQL運算式，在此範例中，它包含現有計算屬性的參照。 |

如需結構描述定義屬性的詳細資訊，請參閱 [區段定義API端點指南](../../segmentation/api/segment-definitions.md).

**响应**

成功的回應會傳回HTTP狀態200以及您新建立的區段定義的詳細資訊。 若要深入瞭解區段定義回應物件，請參閱 [區段定義API端點指南](../../segmentation/api/segment-definitions.md).

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "segment-downloadedInLast7Days",
    "description": "Has product been downloaded in last 7 days?",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "_{TENANT_ID}.downloadsLast7Days > 0",
        "meta": "m"
    },
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
    "creationTime": 1602016581000,
    "updateEpoch": 1610609459,
    "updateTime": 1610609459000,
    "createEpoch": 1602016554,
    "_etag": "\"8b01611a-0000-0200-0000-5ffff3330000\"",
    "dependents": [
        "023d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [
    "103d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "type": "SegmentDefinition"
}
```

## 后续步骤

現在您已瞭解計算屬性的基本知識，可以開始為組織定義這些屬性了。

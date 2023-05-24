---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 合併原則API端點
type: Documentation
description: Adobe Experience Platform可讓您將多個來源的資料片段集合在一起，並加以合併，以便檢視每個個別客戶的完整檢視。 彙總此資料時，合併原則是Platform用來判斷資料優先順序的方式以及將合併哪些資料以建立統一檢視的規則。
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2468'
ht-degree: 1%

---

# 合併原則端點

Adobe Experience Platform可讓您將多個來源的資料片段集合在一起，並加以合併，以便檢視每個個別客戶的完整檢視。 彙總此資料時，合併原則是指 [!DNL Platform] 使用來決定資料的優先順序以及將合併哪些資料以建立統一的檢視。

例如，如果客戶跨多個管道與您的品牌互動，您的組織將有多個與該單一客戶相關的設定檔片段出現在多個資料集中。 將這些片段內嵌至Platform時，會合併在一起，以便為該客戶建立單一設定檔。 當來自多個來源的資料衝突時（例如，一個片段將客戶列為「單身」，而另一個片段將客戶列為「已婚」），合併原則會決定要包含在個人設定檔中的資訊。

使用RESTful API或使用者介面，您可以建立新的合併原則、管理現有原則，並為您的組織設定預設合併原則。 本指南提供使用API處理合併原則的步驟。

若要使用UI使用合併原則，請參閱 [合併原則UI指南](../merge-policies/ui-guide.md). 若要進一步瞭解一般合併原則及其在Experience Platform中的角色，請先閱讀 [合併原則概觀](../merge-policies/overview.md).

## 快速入门

本指南中使用的API端點是 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). 在繼續之前，請檢閱 [快速入門手冊](getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功對任一檔案發出呼叫所需必要標題的重要資訊 [!DNL Experience Platform] API。

## 合併原則的元件 {#components-of-merge-policies}

合併原則是您組織專屬的原則，可讓您建立不同的原則，以所需的特定方式合併方案。 任何API存取 [!DNL Profile] 資料需要合併原則，但若未明確提供合併原則，則會使用預設值。 [!DNL Platform] 為組織提供預設的合併原則，或者您可以為特定Experience Data Model (XDM)結構描述類別建立合併原則，並將其標籤為組織的預設值。

雖然每個組織在每個結構描述類別中可能都有多個合併原則，但每個類別只能有一個預設合併原則。 在提供結構描述類別名稱且需要合併原則但未提供合併原則的情況下，將使用任何設定為預設的合併原則。

>[!NOTE]
>
>當您設定新的合併原則為預設值時，先前設為預設值的任何現有合併原則會自動更新為不再使用作為預設值。

為確保所有設定檔消費者在邊緣上使用相同的檢視，可將合併原則標籤為邊緣上的作用中。 為了在邊緣上啟用區段（標籤為邊緣區段），該區段必須繫結至在邊緣上標籤為有效的合併原則。 如果區段為 **not** 繫結至在edge上標示為「作用中」的合併原則，該區段不會在edge上標示為「作用中」，而會標示為串流區段。

此外，每個組織只能擁有 **一** 在edge上作用中的合併原則。 如果合併原則在Edge上為作用中，則可將其用於Edge上的其他系統，例如Edge Profile、Edge Segmentation和Destinations on Edge。

### 完成合併原則物件

完整的合併原則物件代表一組偏好設定，可控制合併設定檔片段的各個層面。

**合併原則物件**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{ORG_ID}",
        "schema": {
            "name": "{SCHEMA_CLASS_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "isActiveOnEdge": "{BOOLEAN}",
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| 属性 | 描述 |
|---|---|
| `id` | 系統會在建立時產生指派的唯一識別碼 |
| `name` | 可在清單檢視中識別合併原則的易記名稱。 |
| `imsOrgId` | 此合併原則所屬的組織ID |
| `schema.name` | 的一部分 [`schema`](#schema) 物件， `name` 欄位包含與合併原則相關的XDM結構描述類別。 如需結構描述和類別的詳細資訊，請參閱 [XDM檔案](../../xdm/home.md). |
| `version` | [!DNL Platform] 維護版本的合併原則。 此唯讀值會在合併原則更新時遞增。 |
| `identityGraph` | [身分圖表](#identity-graph) 表示將從其中取得相關身分的身分圖表物件。 將合併找到的所有相關身分的設定檔片段。 |
| `attributeMerge` | [屬性合併](#attribute-merge) 物件，指明當資料衝突時，合併原則優先處理設定檔屬性的方式。 |
| `isActiveOnEdge` | 表示此合併原則是否可用於Edge的布林值。 根據預設，此值為 `false`. |
| `default` | 表示此合併原則是否為指定之結構描述的預設值的布林值。 |
| `updateEpoch` | 合併原則的上次更新日期。 |

**合併原則範例**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{ORG_ID}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "timestampOrdered"
        },
        "isActiveOnEdge": false,
        "default": true,
        "updateEpoch": 1551660639
    }
```

### 身份图 {#identity-graph}

[Adobe Experience Platform Identity Service](../../identity-service/home.md) 管理全域使用的身分圖表，以及每個組織在 [!DNL Experience Platform]. 此 `identityGraph` 合併原則的屬性定義如何確定使用者的相關身分。

**identitygraph物件**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

位置 `{IDENTITY_GRAPH_TYPE}` 為下列其中一項：

* **&quot;none&quot;：** 不執行身分拼接。
* **&quot;pdg&quot;：** 根據您的私人身分圖表執行身分拼接。

**示例`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### 屬性合併 {#attribute-merge}

個人資料片段是存在於特定使用者身分識別清單中，只有一個身分識別的個人資料資訊。 當使用的身分圖表型別導致多個身分時，可能會發生衝突的設定檔屬性，必須指定優先順序。 使用 `attributeMerge`，您可以指定在索引鍵值（記錄資料）型別資料集之間發生合併衝突時，要優先處理哪些設定檔屬性。

**attributeMerge物件**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

位置 `{ATTRIBUTE_MERGE_TYPE}` 為下列其中一項：

* **`timestampOrdered`**：（預設）為上次更新的設定檔指定優先順序。 使用此合併型別， `data` 屬性不是必要專案。
* **`dataSetPrecedence`**：根據設定檔片段來自的資料集為其賦予優先權。 當某個資料集中存在的資訊比另一個資料集中的資料更受偏好或信任時，可以使用此功能。 使用此合併型別時， `order` 屬性是必要的，因為它會依優先順序列出資料集。
   * **`order`**：使用「dataSetPrecedence」時，會 `order` 陣列必須隨資料集清單提供。 不會合併清單中未包含的任何資料集。 換言之，資料集必須明確列出，才能合併至設定檔中。 此 `order` array會依優先順序列出資料集的ID。

#### 範例 `attributeMerge` 物件，使用 `dataSetPrecedence` type

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

#### 範例 `attributeMerge` 物件，使用 `timestampOrdered` type

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### 架构 {#schema}

結構描述物件會指定為其建立此合併原則的Experience Data Model (XDM)結構描述類別。

**`schema`物件**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

其中值 `name` 是與合併原則相關聯之結構描述所根據的XDM類別名稱。

**示例`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

若要進一步瞭解XDM以及使用Experience Platform中的結構描述，請從閱讀 [XDM系統總覽](../../xdm/home.md).

## 存取合併原則 {#access-merge-policies}

使用 [!DNL Real-Time Customer Profile] API， `/config/mergePolicies` 端點可讓您執行查詢請求，以依據其ID檢視特定合併原則，或存取組織中按特定條件篩選的所有合併原則。 您也可以使用 `/config/mergePolicies/bulk-get` 端點，以依據其ID擷取多個合併原則。 以下各節將概述執行上述每個呼叫的步驟。

### 依ID存取單一合併原則

您可以透過單一合併原則的ID，向以下網站發出GET請求來存取該原則： `/config/mergePolicies` 端點，並包含 `mergePolicyId` 在請求路徑中。

**API格式**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| 参数 | 描述 |
|---|---|
| `{mergePolicyId}` | 您要刪除的合併原則識別碼。 |

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**响应**

成功的回應會傳回合併原則的詳細資訊。

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{ORG_ID}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "pdg"
    },
    "attributeMerge": {
        "type": "timestampOrdered"
    },
    "isActiveOnEdge": "false",
    "default": false,
    "updateEpoch": 1551127597
}
```

請參閱 [合併原則的元件](#components-of-merge-policies) 區段，以取得組成合併原則的個別元素的詳細資訊。

### 依其ID擷取多個合併原則

您可以透過向以下專案發出POST請求來擷取多個合併原則： `/config/mergePolicies/bulk-get` 端點，並包含您想要在請求內文中擷取的合併原則ID。

**API格式**

```http
POST /config/mergePolicies/bulk-get
```

**请求**

請求內文包含「ids」陣列，其中包含您要擷取詳細資料的每個合併原則之個別物件，其中包含「id」。

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "ids": [
          {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b"
          },
          {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130"
          }
        ]
      }'
```

**响应**

成功的回應會傳回HTTP狀態207 （多重狀態）以及POST要求中提供ID的合併原則詳細資訊。

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "isActiveOnEdge": false,
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

請參閱 [合併原則的元件](#components-of-merge-policies) 區段，以取得組成合併原則的個別元素的詳細資訊。

### 依條件列出多個合併原則

您可以透過向以下發出GET請求，列出組織內的多個合併原則： `/config/mergePolicies` 端點，並使用選用的查詢引數來篩選、排序及分頁回應。 可包含多個引數，以&amp;分隔。 在不使用引數的情況下呼叫此端點將會擷取您的組織可用的所有合併原則。

**API格式**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| 参数 | 描述 |
|---|---|
| `default` | 布林值，會依據合併原則是否為結構描述類別的預設值來篩選結果。 |
| `limit` | 指定頁面大小限制，以控制頁面中包含的結果數量。 預設值： 20 |
| `orderBy` | 指定排序結果依據的欄位，如下所示 `orderBy=name` 或 `orderBy=+name` 若要依名稱遞增順序排序，或 `orderBy=-name`，以遞減順序排序。 省略此值會導致預設排序 `name` 以遞增順序排列。 |
| `isActiveOnEdge` | 布林值，會依據合併原則在Edge上是否有效來篩選結果。 |
| `schema.name` | 要擷取其可用合併原則的結構描述名稱。 |
| `identityGraph.type` | 依身分圖表型別篩選結果。 可能的值包括「none」和「pdg」（私密圖表）。 |
| `attributeMerge.type` | 依使用的屬性合併型別篩選結果。 可能的值包括「timestampOrdered」和「dataSetPrecedence」。 |
| `start` | 頁面位移 — 指定要擷取之資料的起始ID。 預設值： 0 |
| `version` | 如果您想要使用特定版本的合併原則，請指定此專案。 依預設，將會使用最新版本。 |

如需有關的詳細資訊 `schema.name`， `identityGraph.type`、和 `attributeMerge.type`，請參閱 [合併原則的元件](#components-of-merge-policies) 本章節先前提供。


**请求**

下列要求列出特定結構描述的所有合併原則：

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**响应**

成功的回應會傳回符合由請求中傳送的查詢引數所指定之條件的合併原則分頁清單。

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "isActiveOnEdge": false,
            "default": false,
            "updateEpoch": 1576099719
        }
    ],
    "_links": {
        "next": {
            "href": "@/mergePolicies?start=K1JJRDpFaWc5QUpZWHY1c2JBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQldBQkVBQVBnaFFQLzM4VUIvL2tKQi8rLysvMUpBLzMrMi8wRkFmLzR4UUwvL0VrRC85em4zRTBEcmNmYi92Kzh4UUwvL05rQVgzRi8rMStqNS80WHQwN2NhUUVzQUFBUUFleGpLQ1JnVXRVcEFCQUFFQVBBRA==&orderBy=&limit=2"
        }
    }
}
```

| 属性 | 描述 |
|---|---|
| `_links.next.href` | 下一頁結果的URI位址。 使用此URI作為另一個API呼叫的要求引數，以檢視頁面。 如果下一頁不存在，則此值將為空字串。 |

## 建立合併原則

您可以透過向以下網站發出POST請求，為您的組織建立新的合併原則： `/config/mergePolicies` 端點。

**API格式**

```http
POST /config/mergePolicies
```

**請求**
以下請求會建立新的合併原則，此原則由承載中提供的屬性值設定：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "isActiveOnEdge": true,
    "default": true
}'
```

| 属性 | 描述 |
|---|---|
| `name` | 人類易記的名稱，透過此名稱，可在清單檢視中識別合併原則。 |
| `identityGraph.type` | 從中取得要合併之相關身分的身分圖表型別。 可能的值： 「無」或「pdg」（私密圖表）。 |
| `attributeMerge` | 當資料衝突時，設定檔屬性值的優先順序方式。 |
| `schema` | 與合併原則關聯的XDM結構描述類別。 |
| `isActiveOnEdge` | 指定此合併原則在Edge上是否有效。 |
| `default` | 指定此合併原則是否為結構描述的預設值。 |

請參閱 [合併原則的元件](#components-of-merge-policies) 區段以取得詳細資訊。

**响应**

成功的回應會傳回新建立的合併原則的詳細資料。

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

請參閱 [合併原則的元件](#components-of-merge-policies) 區段，以取得組成合併原則的個別元素的詳細資訊。

## 更新合併原則 {#update}

您可以編輯個別屬性(PATCH)或使用新屬性(PUT)覆寫整個合併原則，以修改現有的合併原則。 每種的範例如下所示。

### 編輯個別合併原則欄位

您可以透過向以下專案發出PATCH請求，編輯合併原則的個別欄位： `/config/mergePolicies/{mergePolicyId}` 端點：

**API格式**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| 参数 | 描述 |
|---|---|
| `{mergePolicyId}` | 您要刪除的合併原則識別碼。 |

**请求**

以下請求會透過變更其值來更新指定的合併原則 `default` 屬性至 `true`：

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "op": "add",
    "path": "/default",
    "value": "true"
  }'
```

| 属性 | 描述 |
|---|---|
| `op` | 指定要執行的作業。 其他PATCH操作的範例可在以下網址找到： [JSON修補程式檔案](https://datatracker.ietf.org/doc/html/rfc6902) |
| `path` | 要更新的欄位路徑。 接受的值為：「/name」、「/identityGraph.type」、「/attributeMerge.type」、「/schema.name」、「/version」、「/default」、「/isActiveOnEdge」 |
| `value` | 要設定指定欄位的值。 |

請參閱 [合併原則的元件](#components-of-merge-policies) 區段以取得詳細資訊。


**响应**

成功的回應會傳回新更新的合併原則的詳細資料。

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

### 覆寫合併原則

修改合併原則的另一種方法是使用PUT請求，這會覆寫整個合併原則。

**API格式**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| 参数 | 描述 |
|---|---|
| `{mergePolicyId}` | 您要覆寫之合併原則的識別碼。 |

**请求**

以下請求會覆寫指定的合併原則，將其屬性值取代為承載中提供的屬性值。 由於此請求會完全取代現有的合併原則，因此您必須提供原始定義合併原則時所需的所有相同欄位。 不過，這次您是要為要變更的欄位提供更新的值。

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{ORG_ID}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "dataSetPrecedence",
            "order": [
                "5b76f86b85d0e00000be5c8b",
                "5b76f8d787a6af01e2ceda18"
            ]
        },
        "isActiveOnEdge": true,
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| 属性 | 描述 |
|---|---|
| `name` | 人類易記的名稱，透過此名稱，可在清單檢視中識別合併原則。 |
| `identityGraph` | 從中取得要合併之相關身分的身分圖表。 |
| `attributeMerge` | 當資料衝突時，設定檔屬性值的優先順序方式。 |
| `schema` | 與合併原則關聯的XDM結構描述類別。 |
| `isActiveOnEdge` | 指定此合併原則在Edge上是否有效。 |
| `default` | 指定此合併原則是否為結構描述的預設值。 |

請參閱 [合併原則的元件](#components-of-merge-policies) 區段以取得詳細資訊。

**响应**

成功的回應會傳回已更新合併原則的詳細資料。

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

## 刪除合併原則

您可以透過向以下專案發出DELETE請求來刪除合併原則： `/config/mergePolicies` 端點，並在請求路徑中包含您要刪除的合併原則ID。

>[!NOTE]
>
>如果合併原則具有 `isActiveOnEdge` 設為true，則合併原則 **無法** 被刪除。 使用 [PATCH](#edit-individual-merge-policy-fields) 或 [PUT](#overwrite-a-merge-policy) 端點以在刪除合併原則之前更新它。

**API格式**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| 参数 | 描述 |
|---|---|
| `{mergePolicyId}` | 您要刪除的合併原則識別碼。 |

**请求**

以下請求會刪除合併原則。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的刪除請求會傳回HTTP狀態200 （確定）和空白的回應內文。 若要確認刪除成功，您可以執行GET要求，依合併原則的ID檢視合併原則。 如果刪除合併原則，您會收到HTTP狀態404 （找不到）錯誤。

## 后续步骤

現在您知道如何為組織建立和設定合併原則，就可以使用它們來調整Platform中客戶設定檔的檢視，以及從建立受眾區段 [!DNL Real-Time Customer Profile] 資料。

請參閱 [Adobe Experience Platform Segmentation Service檔案](../../segmentation/home.md) 以開始定義和使用區段。

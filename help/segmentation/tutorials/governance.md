---
keywords: Experience Platform；首頁；熱門主題；資料使用規範；強制執行；強制執行資料使用規範；細分服務；細分；細分；
solution: Experience Platform
title: 使用API強制執行受眾區段的資料使用合規性
type: Tutorial
description: 本教學課程涵蓋使用API對「即時客戶個人檔案」對象區段強制執行資料使用合規性的步驟。
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 1%

---

# 使用API對受眾區段強制執行資料使用合規性

本教學課程涵蓋強制資料使用法規遵循的步驟 [!DNL Real-Time Customer Profile] 使用API的對象區段。

## 快速入门

本教學課程需要您深入瞭解下列元件 [!DNL Adobe Experience Platform]：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)： [!DNL Real-Time Customer Profile] 是一般查詢實體存放區，用於管理 [!DNL Experience Data Model (XDM)] 資料範圍 [!DNL Platform]. 設定檔可合併各種企業資料資產中的資料，並在統一的簡報中提供該資料的存取權。
   - [合併原則](../../profile/api/merge-policies.md)：使用的規則 [!DNL Real-Time Customer Profile] 以判斷在特定條件下可以將哪些資料合併到統一檢視中。 可針對資料控管目的設定合併原則。
- [[!DNL Segmentation]](../home.md)：如何 [!DNL Real-Time Customer Profile] 會將設定檔存放區中包含的大量個人群組劃分為具有類似特徵且對行銷策略有類似回應的較小群組。
- [資料控管](../../data-governance/home.md)：資料控管使用下列元件，為資料使用標籤和強制執行提供基礎架構：
   - [資料使用標籤](../../data-governance/labels/user-guide.md)：用來根據處理資料集和欄位各自資料的敏感度層級描述資料集和欄位的標籤。
   - [資料使用原則](../../data-governance/policies/overview.md)：指出對依特定資料使用標籤分類的資料允許哪些行銷動作的設定。
   - [原則執行](../../data-governance/enforcement/overview.md)：可讓您強制執行資料使用原則，並防止構成原則違規的資料作業。
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供您需瞭解的其他資訊，才能成功對 [!DNL Platform] API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：持有人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的標頭：

- Content-Type： application/json

## 查詢區段定義的合併原則 {#merge-policy}

此工作流程從存取已知受眾區段開始。 已啟用以用於中的區段 [!DNL Real-Time Customer Profile] 在其區段定義中包含合併原則ID。 此合併原則包含要將哪些資料集納入區段的相關資訊，而這些資料集又包含任何適用的資料使用標籤。

使用 [!DNL Segmentation] API的相關資訊，您可以透過區段的ID來查詢區段定義，以尋找與其關聯的合併原則。

**API格式**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | 您要查閱的區段定義ID。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/24379cae-726a-4987-b7b9-79c32cddb5c1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回區段定義的詳細資料。

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{ORG_ID}",
    "name": "Cart abandons in CA",
    "description": "",
    "expression": {
        "type": "PQL", 
        "format": "pql/text", 
        "value": "homeAddress.countryISO = 'US'"
    },
    "mergePolicyId": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1556094486000,
    "updateEpoch": 1556094486000,
    "updateTime": 1556094486000
  }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `mergePolicyId` | 用於區段定義的合併原則ID。 這將在下一個步驟中使用。 |

## 從合併原則尋找來源資料集 {#datasets}

合併原則包含其來源資料集的相關資訊，而這些資料集又包含資料使用標籤。 您可以在GET要求中提供合併原則ID，查詢合併原則的詳細資料 [!DNL Profile] API。 有關合併原則的更多資訊可在以下網址找到： [合併原則端點指南](../../profile/api/merge-policies.md).

**API格式**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | 在中取得的合併原則ID [上一步](#merge-policy). |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回合併原則的詳細資訊。

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{ORG_ID}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence", 
        "data": {
            "order": ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `schema.name` | 與合併原則關聯的結構描述名稱。 |
| `attributeMerge.type` | 合併原則的資料優先順序設定型別。 如果值為 `dataSetPrecedence`，與此合併原則關聯的資料集會列在 `attributeMerge > data > order`. 如果值為 `timestampOrdered`，然後是與中參考的結構描述相關聯的所有資料集 `schema.name` 由合併原則使用。 |
| `attributeMerge.data.order` | 如果 `attributeMerge.type` 是 `dataSetPrecedence`，此屬性會是陣列，包含此合併原則所使用的資料集ID。 這些ID會用於下一個步驟。 |

## 評估原則違規的資料集

>[!NOTE]
>
> 此步驟假設您至少有一個有效資料使用原則，可防止對包含特定標籤的資料執行特定行銷動作。 如果您沒有任何適用的使用原則適用於正在評估的資料集，請遵循 [原則建立教學課程](../../data-governance/policies/create.md) 以建立一個，然後再繼續此步驟。

取得合併原則的來源資料集的ID後，您可以使用 [原則服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 根據特定行銷動作評估這些資料集，以檢查資料使用原則違規。

若要評估資料集，您必須在POST請求的路徑中提供行銷動作的名稱，同時在請求內文中提供資料集ID，如下列範例所示。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 與您評估資料集的資料使用原則相關聯的行銷動作名稱。 視原則是由Adobe定義還是您的組織定義而定，您必須使用 `/marketingActions/core` 或 `/marketingActions/custom`（分別）。 |

**请求**

以下請求會測試 `exportToThirdParty` 針對中取得的資料集採取行銷動作 [上一步](#datasets). 請求承載是包含每個資料集ID的陣列。

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
      "entityId": "5b95b155419ec801e6eee780"
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df"
    }
  ]'
```

| 属性 | 描述 |
| --- | --- |
| `entityType` | 承載陣列中的每個專案都必須指出所定義的實體型別。 對於此使用案例，值將一律為「dataSet」。 |
| `entityID` | 承載陣列中的每個專案都必須提供資料集的唯一ID。 |

**响应**

成功回應會傳回行銷動作的URI、從所提供資料集收集的資料使用標籤，以及針對這些標籤測試動作所違反的任何資料使用原則清單。 在此範例中，「將資料匯出至第三方」原則顯示在 `violatedPolicies` 陣列，指出行銷動作已觸發原則違規。

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
    "C5"
  ],
  "discoveredLabels": [
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780",
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
      "entityId": "5b7c86968f7b6501e21ba9df",
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
| `duleLabels` | 從提供的資料集中擷取的資料使用標籤清單。 |
| `discoveredLabels` | 請求承載中提供的資料集清單，顯示可在每個資料集中找到之資料集層級和欄位層級標籤。 |
| `violatedPolicies` | 陣列會列出測試行銷動作所違反的任何資料使用原則(指定於 `marketingActionRef`)與提供的 `duleLabels`. |

您可以使用API回應中傳回的資料，在體驗應用程式中設定通訊協定，以便在發生原則違規時適當地強制執行。

## 篩選資料欄位

如果您的受眾區段沒有通過評估，您可以透過下列兩種方法之一調整區段中包含的資料。

### 更新區段定義的合併原則

更新區段定義的合併原則將會調整資料集和執行區段作業時要包含的欄位。 請參閱以下小節： [更新現有的合併原則](../../profile/api/merge-policies.md#update) 在API合併原則教學課程中取得更多資訊。

### 匯出區段時限制特定資料欄位

使用將區段匯出至資料集時 [!DNL Segmentation] API時，您可以使用 `fields` 引數。 新增至此引數的任何資料欄位都將包含在匯出中，而所有其他資料欄位則會被排除。

假設區段有名為「A」、「B」和「C」的資料欄位。 如果您只想匯出欄位「C」，則 `fields` 引數只會包含&quot;C&quot;欄位。 如此，匯出區段時就會排除「A」和「B」欄位。

請參閱以下小節： [匯出區段](./evaluate-a-segment.md#export) 如需詳細資訊，請參閱區段教學課程。

## 后续步骤

依照本教學課程，您已查詢與對象區段相關聯的資料使用標籤，並測試這些標籤是否違反特定行銷動作的原則。 如需中資料控管的詳細資訊 [!DNL Experience Platform]，請閱讀 [資料控管](../../data-governance/home.md).

---
title: 加速查詢端點
description: 瞭解如何以無狀態方式存取查詢加速存放區，以根據彙總資料快速傳回結果。 本檔案提供查詢服務加速查詢端點的範例HTTP請求和回應。
exl-id: 29ea4d25-9c46-4b29-a6d7-45ac33dcb0fb
source-git-commit: aa209dce9268a15a91db6e3afa7b6066683d76ea
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 1%

---

# 加速的查詢端點

在Data Distiller SKU中， [查詢服務API](https://developer.adobe.com/experience-platform-apis/references/query-service/) 可讓您對加速存放區進行無狀態查詢。 傳回的結果會根據彙總的資料。 減少結果的延遲可讓您以更具互動性的方式交換資訊。 加速查詢API也用於提供動力 [使用者定義儀表板](../../dashboards/user-defined-dashboards.md).

在繼續使用本指南之前，請確定您已閱讀並瞭解 [查詢服務API指南](./getting-started.md) 才能成功使用查詢服務API。

## 快速入门

需要Data Distiller SKU才能使用查詢加速存放區。 請參閱 [封裝](../packages.md) 和 [護欄](../guardrails.md#query-accelerated-store) 與資料Distiller SKU相關的檔案。 如果您沒有Data Distiller SKU，請聯絡您的Adobe客戶服務代表以取得更多資訊。

<!-- Document is hidden temporarily
Please see the [packaging](../packages.md), [guardrails](../guardrails.md#query-accelerated-store), and [licensing](../data-distiller/license-usage.md) documentation that relates to the Data Distiller SKU. 
-->

以下各節將詳細介紹透過查詢服務API以無狀態方式存取查詢加速存放區所需的API呼叫。 每個呼叫都包含一般API格式、顯示必要標題的範例要求以及範例回應。

## 執行加速查詢 {#run-accelerated-query}

向發出POST請求 `/accelerated-queries` 端點以執行加速查詢。 查詢直接包含在請求承載中，或使用範本ID參照。

**API格式**

```shell
POST /accelerated-queries
```

### 请求

>[!IMPORTANT]
>
>向以下專案的請求： `/accelerated-queries` 端點需要SQL陳述式或範本ID，但不是兩者都需要。 在請求中提交兩者會導致錯誤。

下列請求會將請求內文中的SQL查詢提交至加速存放區。

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/acceleated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "sql": "SELECT * FROM accounts;",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

此替代請求會將請求內文中的範本ID提交至加速存放區。 使用對應範本中的SQL來查詢加速存放區。

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/acceleated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "templateId": "5d8228e7-4200-e3de-11e9-7f27416c5f0d",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

| 属性 | 描述 |
|---|---|
| `dbName` | 您向其提出加速查詢的資料庫名稱。 的值 `dbName` 應採用以下格式 `{SANDBOX_NAME}:{ACCELERATED_STORE_DATABASE}.{ACCELERATED_STORE_SCHEMA}`. 提供的資料庫必須存在於加速存放區中，否則請求會導致錯誤。 您也必須確保 `x-sandbox-name` 中的標題和沙箱名稱 `dbName` 請參閱相同的沙箱。 |
| `sql` | SQL陳述式字串。 允許的大小上限為1000000個字元。 |
| `templateId` | 向發出POST請求時建立並儲存為範本的查詢的唯一識別碼 `/templates` 端點。 |
| `name` | 加速查詢的可選人性化描述性名稱。 |
| `description` | 有關查詢意圖的可選評論，可幫助其他使用者瞭解其目的。 允許的大小上限為1000個位元組。 |

**响应**

成功的回應會傳回HTTP狀態200及查詢建立的隨選結構描述。

>[!NOTE]
>
>為簡短起見，下列回應已截斷。

```json
{
  "queryId": "315a0a66-0fbb-4810-bc30-484cea5e0f1e",
  "resultsMeta": {
    "_adhoc": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
                "Units": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_name_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_code": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_name": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_aggregation_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Value": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Year": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_category": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_ANZSIC06": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                }
            }
        }
    },
  "results": [
     {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H26",
            "Variable_name": "Fixed tangible assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "282",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H27",
            "Variable_name": "Additions to fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "35",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H28",
            "Variable_name": "Disposals of fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "9",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        ...
    ],
  "request": {
    "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
    "sql": "SELECT * FROM accounts;",
    "name": "Sample Accelerated Query",
    "description": "A sample of an accelerated query."
  }
}
```

| 属性 | 描述 |
|---|---|
| `queryId` | 已建立查詢的ID值。 |
| `resultsMeta` | 此物件包含結果中傳回之每個欄的中繼資料，讓使用者知道每個欄的名稱和型別。 |
| `resultsMeta._adhoc` | 臨機Experience Data Model (XDM)結構描述，其欄位已命名為僅供單一資料集使用。 |
| `resultsMeta._adhoc.type` | 臨時結構描述的資料型別。 |
| `resultsMeta._adhoc.meta:xdmType` | 這是系統為XDM欄位型別產生的值。 如需可用型別的詳細資訊，請參閱以下檔案： [可用的XDM型別](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/custom-fields-api.html). |
| `resultsMeta._adhoc.properties` | 這些是查詢資料集的欄名稱。 |
| `resultsMeta._adhoc.results` | 這些是查詢資料集的列名稱。 它們會反映每個傳回的欄。 |

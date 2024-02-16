---
title: 加速查询端点
description: 了解如何以无状态方式访问查询加速存储区，以根据聚合数据快速返回结果。 本文档提供了查询服务加速查询端点的示例HTTP请求和响应。
exl-id: 29ea4d25-9c46-4b29-a6d7-45ac33dcb0fb
source-git-commit: ea2a1cddf299bec750875c4a9125cdd065f18d8b
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# 加速查询端点

作为Data Distiller SKU的一部分， [查询服务API](https://developer.adobe.com/experience-platform-apis/references/query-service/) 允许您对accelerated store进行无状态查询。 返回的结果基于聚合的数据。 减少结果的延迟有助于进行更具互动性的信息交换。 加速查询API也用于增强 [用户定义的仪表板](../../dashboards/user-defined-dashboards.md).

在继续本指南之前，请确保您已阅读并理解 [查询服务API指南](./getting-started.md) 以成功使用查询服务API。

## 快速入门

需要Data Distiller SKU才能使用查询加速存储。 请参阅 [封装](../packaging.md) 和 [护栏](../guardrails.md#query-accelerated-store)、和 [许可](../data-distiller/license-usage.md) 与数据Distiller SKU相关的文档。 如果您没有Data Distiller SKU，请联系您的Adobe客户服务代表以了解更多信息。

以下部分详细介绍了通过查询服务API以无状态方式访问查询加速存储区所需的API调用。 每个调用包括常规API格式、显示所需标头的示例请求以及示例响应。

## 运行加速查询 {#run-accelerated-query}

向发出POST请求 `/accelerated-queries` 端点运行加速查询。 查询直接包含在请求有效负载中或用模板ID引用。

**API格式**

```shell
POST /accelerated-queries
```

### 请求

>[!IMPORTANT]
>
>请求 `/accelerated-queries` 端点需要SQL语句或模板ID，但不能同时需要。 在请求中提交这两个请求会导致错误。

以下请求将请求正文中的SQL查询提交到加速存储。

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/accelerated-queries
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

此备用请求将请求正文中的模板ID提交到加速商店。 使用相应模板中的SQL来查询加速存储。

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/accelerated-queries
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
| `dbName` | 要向其进行加速查询的数据库名称。 的值 `dbName` 应采用以下格式 `{SANDBOX_NAME}:{ACCELERATED_STORE_DATABASE}.{ACCELERATED_STORE_SCHEMA}`. 提供的数据库必须存在于加速存储中，否则请求将导致错误。 您还必须确保 `x-sandbox-name` 中的标题和沙盒名称 `dbName` 引用同一沙盒。 |
| `sql` | SQL语句字符串。 允许的最大大小为1000000个字符。 |
| `templateId` | 向发出POST请求时创建并另存为模板的查询的唯一标识符 `/templates` 端点。 |
| `name` | 加速查询的可选的人类易记描述性名称。 |
| `description` | 有关查询意图的可选评论，可帮助其他用户了解其用途。 允许的最大大小为1000字节。 |

**响应**

成功的响应会返回具有由查询创建的临时架构的HTTP状态200。

>[!NOTE]
>
>为简短起见，以下响应已截断。

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
| `queryId` | 创建的查询的ID值。 |
| `resultsMeta` | 此对象包含结果中返回的每个列的元数据，以便用户了解每个列的名称和类型。 |
| `resultsMeta._adhoc` | 临时体验数据模型(XDM)架构，其字段已命名为仅供单个数据集使用。 |
| `resultsMeta._adhoc.type` | 临时架构的数据类型。 |
| `resultsMeta._adhoc.meta:xdmType` | 这是XDM字段类型的系统生成的值。 有关可用类型的更多信息，请参阅 [可用的XDM类型](../../xdm/tutorials/custom-fields-api.md). |
| `resultsMeta._adhoc.properties` | 这些是查询的数据集的列名称。 |
| `resultsMeta._adhoc.results` | 这些是查询的数据集的行名称。 它们反映每个返回的列。 |

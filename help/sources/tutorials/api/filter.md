---
keywords: Experience Platform；主页；热门主题；流服务；流服务API；源；源
title: 使用流服务API筛选Source的行级数据
description: 本教程介绍了有关如何使用流服务API在源级别过滤数据的步骤
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: b0e2fc4767fb6fbc90bcdd3350b3add965988f8f
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API筛选源的行级数据

>[!IMPORTANT]
>
>目前，仅对以下源支持筛选行级数据：
>
>* [Google BigQuery](../../connectors/databases/bigquery.md)
>* [Microsoft Dynamics](../../connectors/crm/ms-dynamics.md)
>* [Salesforce](../../connectors/crm/salesforce.md)
>* [Snowflake](../../connectors/databases/snowflake.md)

本教程提供了有关如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)筛选源的行级数据的步骤。

## 快速入门

本教程要求您实际了解Adobe Experience Platform的以下组件：

* [源](../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用平台API

有关如何成功调用平台API的信息，请参阅[平台API快速入门](../../../landing/api-guide.md)指南。

## 筛选源数据

下面概述了为筛选源的行级数据而采取的步骤。

### 查找连接规范

在使用API筛选源的行级数据之前，必须首先检索源的连接规范详细信息，以确定特定源支持的运算符和语言。

要检索给定源的连接规范，请向[!DNL Flow Service] API的`/connectionSpecs`端点发出GET请求，同时提供源的属性名称作为查询参数的一部分。

**API格式**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{QUERY_PARAMS}` | 用于筛选结果的可选查询参数。 您可以通过应用`name`属性并在搜索中指定`"google-big-query"`来检索[!DNL Google BigQuery]连接规范。 |

**请求**

以下请求检索[!DNL Google BigQuery]的连接规范。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回[!DNL Google BigQuery]的连接规范，包括有关其支持的查询语言和逻辑运算符的信息。

>[!NOTE]
>
>为简短起见，以下API响应被截断。

```json
"attributes": {
  "filterAtSource": {
    "enabled": true,
    "queryLanguage": "SQL",
    "logicalOperators": [
      "and",
      "or",
      "not"
    ],
    "comparisonOperators": [
      "=",
      "!=",
      "<",
      "<=",
      ">",
      ">=",
      "like",
      "in"
    ],
    "columnNameEscapeChar": "`",
    "valueEscapeChar": "'"
  }
```

| 属性 | 描述 |
| --- | --- |
| `attributes.filterAtSource.enabled` | 确定查询的源是否支持对行级数据进行筛选。 |
| `attributes.filterAtSource.queryLanguage` | 确定查询源支持的查询语言。 |
| `attributes.filterAtSource.logicalOperators` | 确定可用于为源筛选行级数据的逻辑运算符。 |
| `attributes.filterAtSource.comparisonOperators` | 确定可用于筛选源行级数据的比较运算符。 有关比较运算符的更多信息，请参阅下表。 |
| `attributes.filterAtSource.columnNameEscapeChar` | 确定用于转义列的字符。 |
| `attributes.filterAtSource.valueEscapeChar` | 确定在编写SQL查询时如何包围值。 |

{style="table-layout:auto"}

#### 比较运算符

| 操作员 | 描述 |
| --- | --- |
| `==` | 按属性是否等于提供的值筛选。 |
| `!=` | 按属性是否不等于提供的值筛选。 |
| `<` | 根据属性是否小于提供的值来进行筛选。 |
| `>` | 按属性是否大于提供的值筛选。 |
| `<=` | 根据属性是否小于或等于提供的值来进行筛选。 |
| `>=` | 按属性是否大于或等于提供的值筛选。 |
| `like` | 通过在`WHERE`子句中使用来搜索指定模式的筛选器。 |
| `in` | 按属性是否在指定范围内进行筛选。 |

{style="table-layout:auto"}

### 指定摄取的筛选条件

在确定了源支持的逻辑运算符和查询语言后，可以使用Profile Query Language (PQL)指定要应用于源数据的筛选条件。

在下面的示例中，条件仅应用于与作为参数列出的节点类型所提供的值相等的数据。

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "=",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "city"
      },
      {
        "nodeType": "literal",
        "value": "DDN"
      }
    ]
  }
}
```

### 预览数据

您可以预览数据，方法是向[!DNL Flow Service] API的`/explore`端点发出GET请求，同时提供`filters`作为查询参数的一部分，并在[!DNL Base64]中指定PQL输入条件。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 源的基本连接ID。 |
| `{TABLE_PATH}` | 要检查的表的path属性。 |
| `{FILTERS}` | 您的PQL筛选条件以[!DNL Base64]编码。 |

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的请求会返回以下响应。

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "FIRSTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "LASTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "CITY",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "AGE",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "HEIGHT",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "ISEMPLOYED",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "POSTG",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "LATITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "LONGITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "JOINEDDATE",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDAT",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDATTS",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  },
 "data": [
    {
        "CITY": "MZN",
        "LASTNAME": "Jain",
        "JOINEDDATE": "2022-06-22T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-06-22T17:19:33",
        "FIRSTNAME": "Shivam",
        "POSTG": true,
        "HEIGHT": "169",
        "CREATEDATTS": "2022-06-22T17:19:33",
        "ISEMPLOYED": true,
        "LATITUDE": 2000.89,
        "AGE": "25"
    },
    {
        "CITY": "MUM",
        "LASTNAME": "Kreet",
        "JOINEDDATE": "2022-09-07T00:00:00",
        "LONGITUDE": 10500.01,
        "CREATEDAT": "2022-09-07T17:19:33",
        "FIRSTNAME": "Rakul",
        "POSTG": true,
        "HEIGHT": "155",
        "CREATEDATTS": "2022-09-07T17:19:33",
        "ISEMPLOYED": false,
        "LATITUDE": 2500.89,
        "AGE": "42"
    },
    {
        "CITY": "MAN",
        "LASTNAME": "Lee",
        "JOINEDDATE": "2022-09-14T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-09-14T05:02:33",
        "FIRSTNAME": "Denzel",
        "POSTG": true,
        "HEIGHT": "185",
        "CREATEDATTS": "2022-09-14T05:02:33",
        "ISEMPLOYED": true,
        "LATITUDE": 123.89,
        "AGE": "16"
    }
  ]
}
```

### 为过滤的数据创建源连接

要创建源连接并摄取过滤的数据，请向`/sourceConnections`端点发出POST请求，同时将筛选条件作为正文参数的一部分提供。

**API格式**

```http
POST /sourceConnections
```

**请求**

以下请求创建一个源连接以从`test1.fasTestTable`中摄取数据，其中`city` = `DDN`。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "BigQuery Source Connection",
      "description": "Source Connection for Filter test",
      "baseConnectionId": "89d1459e-3cd0-4069-acb3-68f240db4eeb",
      "data": {
        "format": "tabular"
      },
      "params": {
        "tableName": "test1.fasTestTable",
        "filters": {
          "type": "PQL",
          "format": "pql/json",
          "value": {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "DDN"
              }
            ]
          }
        }
      },
      "connectionSpec": {
        "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
        "version": "1.0"
      }
    }'
```

**响应**

成功的响应返回新创建的源连接的唯一标识符(`id`)。

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## 附录

本节提供了用于筛选的不同有效负载的进一步示例。

### 奇异条件

对于只需要一个条件的方案，可以省略初始`fnApply`。

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "like",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "firstname"
      },
      {
        "nodeType": "literal",
        "value": "%s"
      }
    ]
  }
}
```

### 使用`in`运算符

有关运算符`in`的示例，请参阅下面的示例有效负载。

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "in",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "firstname"
          },
          {
            "nodeType": "literal",
            "value": [
              "Ramen",
              "John"
            ]
          }
        ]
      }
    ]
  }
}
```

### 使用`isNull`运算符

有关运算符`isNull`的示例，请参阅下面的示例有效负载。

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "isNull",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "complaint_type"
      }
    ]
  }
}
```

### 使用`NOT`运算符

有关运算符`NOT`的示例，请参阅下面的示例有效负载。

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "NOT",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "isNull",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "complaint_type"
          }
        ]
      }
    ]
  }
}
```

### 嵌套条件的示例

有关复杂嵌套条件的示例，请参阅下面的有效负荷示例。

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": ">=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 20
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "<=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 30
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "or",
        "params": [
          {
            "nodeType": "fnApply",
            "fnName": "!=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "PUD"
              }
            ]
          },
          {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "joinedDate"
              },
              {
                "nodeType": "literal",
                "value": "2020-04-22"
              }
            ]
          }
        ]
      }
    ]
  }
}
```

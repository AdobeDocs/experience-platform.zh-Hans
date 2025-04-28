---
title: 使用流服务API筛选Source的行级数据
description: 本教程介绍了有关如何使用流服务API在源级别过滤数据的步骤
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: fe7025b7e48634232d823f8380610c6409b2d4b1
workflow-type: tm+mt
source-wordcount: '1823'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API筛选源的行级数据

>[!AVAILABILITY]
>
>目前，仅对以下源支持筛选行级数据：
>
>* [[!DNL Amazon Redshift]](../../connectors/databases/redshift.md)
>* [[!DNL Google BigQuery]](../../connectors/databases/bigquery.md)
>* [[!DNL Marketo Engage] 标准活动](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)

阅读本指南，了解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)筛选源的行级数据的步骤。

## 快速入门

本教程要求您实际了解Adobe Experience Platform的以下组件：

* [源](../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../landing/api-guide.md)指南。

## 筛选源数据 {#filter-source-data}

下面概述了为筛选源的行级数据而采取的步骤。

### 检索连接规范 {#retrieve-your-connection-specs}

过滤源的行级数据的第一步是检索源的连接规范，并确定源支持的运算符和语言。

要检索给定源的连接规范，请向[!DNL Flow Service] API的`/connectionSpecs`端点发出GET请求，并在查询参数中提供源的属性名称。

**API格式**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{QUERY_PARAMS}` | 用于筛选结果的可选查询参数。 您可以通过应用`name`属性并在搜索中指定`"google-big-query"`来检索[!DNL Google BigQuery]连接规范。 |

+++请求

以下请求检索[!DNL Google BigQuery]的连接规范。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++响应

成功的响应返回[!DNL Google BigQuery]的状态代码200和连接规范，包括有关其支持的查询语言和逻辑运算符的信息。

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

+++

#### 比较运算符 {#comparison-operators}

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

### 指定摄取的筛选条件 {#specify-filtering-conditions-for-ingestion}

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

### 预览数据 {#preview-your-data}

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

+++请求

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++响应

成功的响应将返回数据的内容和结构。

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

+++

### 为过滤的数据创建源连接

要创建源连接并摄取过滤的数据，请对`/sourceConnections`端点发出POST请求，并在请求正文参数中提供筛选条件。

**API格式**

```http
POST /sourceConnections
```

+++请求

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

+++

+++响应

成功的响应返回新创建的源连接的唯一标识符(`id`)。

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

+++

## 筛选[!DNL Marketo Engage]的活动实体 {#filter-for-marketo}

使用[[!DNL Marketo Engage] 源连接器](../../connectors/adobe-applications/marketo/marketo.md)时，可以使用行级筛选来筛选活动实体。 目前，您只能筛选活动实体和标准活动类型。 自定义活动在[[!DNL Marketo] 字段映射](../../connectors/adobe-applications/mapping/marketo.md)下仍受管理。

### [!DNL Marketo]标准活动类型 {#marketo-standard-activity-types}

下表概述了[!DNL Marketo]的标准活动类型。 使用此表作为筛选条件的参考。

| 活动类型标识 | 活动类型名称 |
| --- | --- |
| 1 | 访问网页 |
| 2 | 填写表单 |
| 3 | 单击链接 |
| 6 | 发送电子邮件 |
| 7 | 电子邮件已送达 |
| 8 | 电子邮件退回 |
| 9 | 取消订阅电子邮件 |
| 10 | 打开电子邮件 |
| 11 | 单击电子邮件 |
| 12 | 新商机 |
| 21 | 转化商机 |
| 22 | 更改分数 |
| 24 | 添加到列表 |
| 25 | 从列表中删除 |
| 27 | 电子邮件软退信 |
| 32 | 合并商机 |
| 34 | 添加到机会 |
| 35 | 从机会中移除 |
| 36 | 更新机会 |
| 46 | 有趣的时刻 |
| 101 | 更改收入阶段 |
| 104 | 进程中的更改状态 |
| 110 | 调用 Webhook |
| 113 | 添加到培养 |
| 114 | 更改培养轨迹 |
| 115 | 更改培养节奏 |

{style="table-layout:auto"}

使用[!DNL Marketo]源连接器时，请按照以下步骤筛选标准活动实体。

### 创建草稿数据流

首先，创建[[!DNL Marketo] 数据流](../ui/create/adobe-applications/marketo.md)并将其另存为草稿。 有关如何创建草稿数据流的详细步骤，请参阅以下文档：

* [使用用户界面将数据流另存为草稿](../ui/draft.md)
* [使用API将数据流另存为草稿](../api/draft.md)

### 检索您的数据流ID

创建完草稿的数据流后，您必须检索其对应的ID。

在用户界面中，导航到源目录，然后从顶部标题中选择&#x200B;**[!UICONTROL 数据流]**。 使用状态列可识别在草稿模式下保存的所有数据流，然后选择数据流的名称。 接下来，使用右侧的&#x200B;**[!UICONTROL 属性]**&#x200B;面板来查找您的数据流ID。

### 检索数据流详细信息

接下来，必须检索数据流详细信息，尤其是与数据流关联的源连接ID。 要检索数据流详细信息，请向`/flows`端点发出GET请求，并提供您的数据流ID作为path参数。

**API格式**

```http
GET /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{FLOW_ID}` | 要检索的数据流的ID。 |

+++请求

以下请求检索有关数据流ID的信息： `a7e88a01-40f9-4ebf-80b2-0fc838ff82ef`。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++响应

成功的响应将返回数据流详细信息，包括其相应的源连接和目标连接的信息。 您必须记下源连接ID和目标连接ID，因为稍后需要使用这些值才能发布数据流。

```json {line-numbers="true" start-line="1" highlight="23, 26"}
{
    "items": [
        {
            "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "createdAt": 1728592929650,
            "updatedAt": 1728597187444,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "Marketo Engage Standard Activities ACME",
            "description": "",
            "flowSpec": {
                "id": "15f8402c-ba66-4626-b54c-9f8e54244d61",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "etag": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "sourceConnectionIds": [
                "56f7eb3a-b544-4eaa-b167-ef1711044c7a"
            ],
            "targetConnectionIds": [
                "7e53e6e8-b432-4134-bb29-21fc6e8532e5"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
                        "connectionSpec": {
                            "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "0137118b-373a-4c4e-847c-13a0abf73b33",
                            "connectionSpec": {
                                "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "isSampleDataflow": false,
                "errorDiagnosticsEnabled": true
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingVersion": 0,
                        "mappingId": "f6447514ef95482889fac1818972e285"
                    }
                }
            ],
            "runs": "/runs?property=flowId==a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "lastOperation": {
                "started": 1728592929650,
                "updated": 0,
                "operation": "create"
            },
            "lastRunDetails": {
                "id": "2d7863d5-ca4d-4313-ac52-2603eaf2cdbe",
                "state": "success",
                "startedAtUTC": 1728594713537,
                "completedAtUTC": 1728597183080
            },
            "labels": [],
            "recordTypes": [
                {
                    "type": "experienceevent",
                    "extensions": {}
                }
            ]
        }
    ]
}
```

+++

### 检索源连接详细信息

接下来，使用您的源连接ID并向`/sourceConnections`端点发出GET请求以检索您的源连接详细信息。

**API格式**

```http
GET /sourceConnections/{SOURCE_CONNECTION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | 要检索的源连接的ID。 |

+++请求

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++响应

成功的响应将返回源连接的详细信息。 记下版本，因为您在下一步中需要此值以更新源连接。

```json {line-numbers="true" start-line="1" highlight="30"}
{
    "items": [
        {
            "id": "b85b895f-a289-42e9-8fe1-ae448ccc7e53",
            "createdAt": 1729634331185,
            "updatedAt": 1729634331185,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "New Source Connection - 2024-10-23T03:28:50+05:30",
            "description": "Source connection created from the workflow",
            "baseConnectionId": "fd9f7455-1e23-4831-9283-7717e20bee40",
            "state": "draft",
            "data": {
                "format": "tabular",
                "schema": null,
                "properties": null
            },
            "connectionSpec": {
                "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                "version": "1.0"
            },
            "params": {
                "columns": [],
                "tableName": "Activity"
            },
            "version": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "etag": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "inheritedAttributes": {
                "baseConnection": {
                    "id": "fd9f7455-1e23-4831-9283-7717e20bee40",
                    "connectionSpec": {
                        "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                        "version": "1.0"
                    }
                }
            },
            "lastOperation": {
                "started": 1729634331185,
                "updated": 0,
                "operation": "draft_create"
            }
        }
    ]
}
```

+++

### 使用筛选条件更新源连接

现在您有了源连接ID及其相应版本，接下来可以使用指定标准活动类型的过滤条件发出PATCH请求。

要更新源连接，请向`/sourceConnections`端点发出PATCH请求，并提供源连接ID作为查询参数。 此外，您必须提供一个`If-Match`标头参数，以及源连接的相应版本。

>[!TIP]
>
>发出PATCH请求时需要使用`If-Match`标头。 此标头的值是要更新的数据流的唯一版本/电子标记。 每次成功更新数据流时，版本/电子标记值都会更新。

**API格式**

```http
PATCH /sourceConnections/{SOURCE_CONNECTION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | 要更新的源连接的ID |

+++请求

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: {VERSION_HERE}'
  -d '
      {
        "op": "add",
        "path": "/params/filters",
        "value": {
            "type": "PQL",
            "format": "pql/json",
            "value": {
                "nodeType": "fnApply",
                "fnName": "in",
                "params": [
                    {
                        "nodeType": "fieldLookup",
                        "fieldName": "activityType"
                    },
                    {
                        "nodeType": "literal",
                        "value": [
                            "Change Status in Progression",
                            "Fill Out Form"
                        ]
                    }
                ]
            }
        }
    }'
```

+++

+++响应

成功的响应将返回源连接ID和etag（版本）。

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"210068a6-0000-0200-0000-6718201b0000\""
}
```

+++

### 发布源连接

利用筛选条件更新源连接，您现在可以从草稿状态继续并发布源连接。 为此，请向`/sourceConnections`端点发出POST请求，并提供草稿源连接的ID以及用于发布的操作操作。

**API格式**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| 参数 | 描述 |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | 要发布的源连接的ID。 |
| `op` | 更新查询源连接的状态的操作操作。 要发布草稿源连接，请将`op`设置为`publish`。 |

+++请求

以下请求将发布起草的源连接。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++响应

成功的响应将返回源连接ID和etag（版本）。

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"9f007f7b-0000-0200-0000-670ef1150000\""
}
```

+++

### 发布目标连接

与上一步类似，您还必须发布目标连接，才能继续并发布草稿数据流。 向`/targetConnections`端点发出POST请求，并提供要发布的草稿目标连接的ID以及用于发布的操作操作。

**API格式**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| 参数 | 描述 |
| --- | --- |
| `{TARGET_CONNECTION_ID}` | 要发布的目标连接的ID。 |
| `op` | 更新查询的目标连接的状态的操作操作。 要发布草稿目标连接，请将`op`设置为`publish`。 |

+++请求

以下请求发布了ID为`7e53e6e8-b432-4134-bb29-21fc6e8532e5`的目标连接。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/7e53e6e8-b432-4134-bb29-21fc6e8532e5/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++响应

成功的响应将返回已发布目标连接的ID和相应的电子标记。

```json
{
    "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++


### 发布数据流

在源和目标连接均已发布的情况下，您现在可以继续最后步骤并发布数据流。 要发布数据流，请对`/flows`端点发出POST请求，并提供数据流ID和用于发布的操作操作。

**API格式**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| 参数 | 描述 |
| --- | --- |
| `{FLOW_ID}` | 要发布的数据流的ID。 |
| `op` | 更新查询数据流状态的操作操作。 要发布草稿数据流，请将`op`设置为`publish`。 |

+++请求

以下请求将发布您的草稿数据流。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++响应

成功的响应将返回数据流的ID和相应的`etag`。

```json
{
  "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
  "etag": "\"4b0354b7-0000-0200-0000-6716ce1f0000\""
}
```

+++

您可以使用Experience Platform UI验证草稿数据流是否已发布。 导航到源目录中的数据流页面并引用数据流的&#x200B;**[!UICONTROL 状态]**。 如果成功，状态现在应设置为&#x200B;**已启用**。

>[!TIP]
>
>* 启用了过滤的数据流将只回填一次。 您在筛选条件中所做的任何更改（无论是添加还是删除）都只能对增量数据生效。
>* 如果需要摄取任何新活动类型的历史数据，建议您创建新数据流，并在筛选条件中使用相应的活动类型定义筛选条件。
>* 您无法筛选自定义活动类型。
>* 无法预览过滤的数据。

## 附录

本节提供了用于筛选的不同有效负载的进一步示例。

### 奇异条件

对于只需要一个条件的方案，可以省略初始`fnApply`。

+++选择以查看示例

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

+++

### 使用`in`运算符

有关运算符`in`的示例，请参阅下面的示例有效负载。

+++选择以查看示例

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

+++

### 使用`isNull`运算符

+++选择以查看示例

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

+++

### 使用`NOT`运算符

有关运算符`NOT`的示例，请参阅下面的示例有效负载。


+++选择以查看示例

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

+++

### 嵌套条件的示例

有关复杂嵌套条件的示例，请参阅下面的有效负荷示例。

+++选择以查看示例

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

+++
---
title: 使用流服务API为SugarCRM事件创建源连接和数据流
description: 了解如何使用流服务API将Adobe Experience Platform连接到SugarCRM Events。
exl-id: 12d08010-569c-4111-ba95-697c6ce6f637
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 1%

---

# (Beta)使用流服务API为[!DNL SugarCRM Events]创建源连接和数据流

>[!NOTE]
>
>[!DNL SugarCRM Events]源为测试版。 有关使用测试版标记源的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

以下教程将指导您完成创建[!DNL SugarCRM Events]源连接和创建数据流以使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)将[[!DNL SugarCRM]](https://www.sugarcrm.com/)事件数据引入Adobe Experience Platform的步骤。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL SugarCRM]所需了解的其他信息。

### 收集所需的凭据

为了将[!DNL SugarCRM Events]连接到Experience Platform，您必须提供以下连接属性的值：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| `host` | 源连接到的SugarCRM API端点。 | `developer.salesfusion.com` |
| `username` | 您的SugarCRM开发人员帐户用户名。 | `abc.def@example.com@sugarmarketdemo000.com` |
| `password` | 您的SugarCRM开发人员帐户密码。 | `123456789` |

## 使用[!DNL Flow Service] API将[!DNL SugarCRM Events]连接到Experience Platform

下面概述了验证[!DNL SugarCRM]源、创建源连接以及创建数据流以将事件数据提交到Experience Platform时需要执行的步骤。

### 创建基本连接 {#base-connection}

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL SugarCRM Events]身份验证凭据作为请求正文的一部分时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL SugarCRM Events]创建基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Events base connection",
      "description": "Create a live inbound connection to your SugarCRM Events instance, to ingest both historic and scheduled data into Experience Platform",
      "connectionSpec": {
          "id": "59a4b493-a615-40f9-bd38-f823d0909a2b",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Refresh Code",
          "params": {
              "host": "developer.salesfusion.com",
              "username": "{SUGARCRM_DEVELOPER_ACCOUNT_USERNAME}",
              "password": "{SUGARCRM_DEVELOPER_ACCOUNT_PASSWORD}"
          }
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 基础连接的名称。 确保基本连接的名称是描述性的，因为您可以使用此名称查找有关基本连接的信息。 |
| `description` | 可包含的可选值，用于提供有关基本连接的更多信息。 |
| `connectionSpec.id` | 源的连接规范ID。 在您的源通过[!DNL Flow Service] API注册和批准后，可以检索此ID。 |
| `auth.specName` | 您用于向Experience Platform验证源的身份验证类型。 |
| `auth.params.host` | SugarCRM API主机： *developer.salesfusion.com* |
| `auth.params.username` | 您的SugarCRM开发人员帐户用户名。 |
| `auth.params.password` | 您的SugarCRM开发人员帐户密码。 |

**响应**

成功的响应返回新创建的基本连接，包括其唯一连接标识符(`id`)。 在下一步中浏览源的文件结构和内容时，需要此ID。

```json
{
     "id": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
     "etag": "\"4d08164f-0000-0200-0000-6368b7bf0000\""
}
```

### 浏览您的源 {#explore}

使用您在上一步中生成的基本连接ID，您可以通过执行GET请求来浏览文件和目录。
使用以下调用查找要带入[!DNL Experience Platform]的文件的路径：

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

执行GET请求以浏览源的文件结构和内容时，必须包括下表列出的查询参数：

| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 上一步中生成的基本连接ID。 |
| `objectType=rest` | 您希望探索的对象类型。 目前，此值始终设置为`rest`。 |
| `{OBJECT}` | 只有在查看特定目录时才需要此参数。 其值表示您希望浏览的目录的路径。 对于此源，该值将为`json`。 |
| `fileType=json` | 要带到Experience Platform的文件类型。 当前，`json`是唯一支持的文件类型。 |
| `{PREVIEW}` | 一个布尔值，定义连接的内容是否支持预览。 |
| `{SOURCE_PARAMS}` | 为要带到Experience Platform的源文件定义参数。 要检索`{SOURCE_PARAMS}`的已接受格式类型，必须在base64中编码整个字符串。<br> [!DNL SugarCRM Events]不需要任何有效负载。 `{SOURCE_PARAMS}`的值作为`{}`传递，在base64中进行编码，它等于`e30=`，如下所示。 |

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=e30=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回查询文件的结构。 *某些记录已被删除，以便更好地呈现。*

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "next": {
                "type": "string"
            },
            "page_number": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "previous": {},
            "total_count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "results": {
                "type": "object",
                "properties": {
                    "sessions": {
                        "type": "string"
                    },
                    "description": {
                        "type": "string"
                    },
                    "created_by": {
                        "type": "string"
                    },
                    "event_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "name": {
                        "type": "string"
                    },
                    "updated_by": {
                        "type": "string"
                    },
                    "updated_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "updated_date": {
                        "type": "string"
                    },
                    "created_date": {
                        "type": "string"
                    },
                    "created_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "event": {
                        "type": "string"
                    },
                    "folder_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "status": {
                        "type": "string"
                    }
                }
            },
            "page_size": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            }
        }
    },
    "data": [
        {
            "next": "https://developer.salesfusion.com/api/2.0/events/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 532,
            "count": 532,
            "results": {
                "event_id": 1,
                "event": "https://developer.salesfusion.com/api/2.0/events/1/",
                "sessions": "https://developer.salesfusion.com/api/2.0/events/1/sessions/",
                "name": "Test",
                "updated_date": "2022-08-30T11:20:11.813Z",
                "updated_by_id": 59,
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "created_date": "2022-08-28T23:40:11Z",
                "created_by_id": 59,
                "created_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "status": "Draft",
                "folder_id": 2
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/events/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 532,
            "count": 532,
            "results": {
                "event_id": 2,
                "event": "https://developer.salesfusion.com/api/2.0/events/2/",
                "sessions": "https://developer.salesfusion.com/api/2.0/events/2/sessions/",
                "name": "Infy Event",
                "description": "Test Event",
                "updated_date": "2022-09-15T16:26:43.697Z",
                "updated_by_id": 59,
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "created_date": "2022-09-27T23:40:11Z",
                "created_by_id": 59,
                "created_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "status": "Active",
                "folder_id": 2
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/events/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 532,
            "count": 532,
            "results": {
                "event_id": 3,
                "event": "https://developer.salesfusion.com/api/2.0/events/3/",
                "sessions": "https://developer.salesfusion.com/api/2.0/events/3/sessions/",
                "name": "Infy Workshop 1",
                "updated_date": "2022-10-11T18:12:28.767Z",
                "updated_by_id": 59,
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "created_date": "2022-09-14T23:40:11Z",
                "created_by_id": 59,
                "created_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "status": "Active",
                "folder_id": 2
            },
            "page_size": 100
        }
    ]
}
```

### 创建源连接 {#source-connection}

您可以通过向[!DNL Flow Service] API发出POST请求来创建源连接。 源连接由连接ID、源数据文件的路径以及连接规范ID组成。

**API格式**

```https
POST /sourceConnections
```

**请求**

以下请求为[!DNL SugarCRM Events]创建源连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Source Connection",
      "description": "SugarCRM Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 请确保源连接的名称是描述性的，因为您可以使用此名称查找有关源连接的信息。 |
| `description` | 可包含的可选值，用于提供有关源连接的更多信息。 |
| `baseConnectionId` | [!DNL SugarCRM Events]的基本连接ID。 此ID是在前面的步骤中生成的。 |
| `connectionSpec.id` | 与源对应的连接规范ID。 |
| `data.format` | 要摄取的[!DNL SugarCRM Events]数据的格式。 当前，唯一支持的数据格式为`json`。 |

**响应**

成功的响应返回新创建的源连接的唯一标识符(`id`)。 此ID是稍后步骤创建数据流所必需的。

```json
{
    "id": "ffac1ae1-c137-4133-9f8d-0279468c11c9",
    "etag": "\"ed05abc3-0000-0200-0000-6368b3280000\""
}
```

### 创建目标XDM架构 {#target-schema}

为了在Experience Platform中使用源数据，必须创建目标架构，以根据您的需求构建源数据。 然后，使用目标架构创建包含源数据的Experience Platform数据集。

通过对[架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)执行POST请求，可以创建目标XDM架构。

有关如何创建目标XDM架构的详细步骤，请参阅有关使用API [创建架构的教程](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html#create)。

### 创建目标数据集 {#target-dataset}

通过向[目录服务API](https://developer.adobe.com/experience-platform-apis/references/catalog/)执行POST请求，在有效负载中提供目标架构的ID，可以创建目标数据集。

有关如何创建目标数据集的详细步骤，请参阅有关[使用API创建数据集的教程](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html)。

### 创建目标连接 {#target-connection}

目标连接表示与要存储所摄取数据的目标的连接。 要创建目标连接，您必须提供对应于数据湖的固定连接规范ID。 此ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

现在，您拥有目标架构、目标数据集以及到数据湖的连接规范ID。 使用这些标识符，您可以使用[!DNL Flow Service] API创建目标连接，以指定将包含入站源数据的数据集。

**API格式**

```https
POST /targetConnections
```

**请求**

以下请求为[!DNL SugarCRM Events]创建目标连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Target Connection Generic Rest",
      "description": "SugarCRM Target Connection Generic Rest",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "version": "1.22"
          }
      },
      "params": {
          "dataSetId": "6365389d1d37d01c077a81da"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 目标连接的名称。 确保目标连接的名称是描述性的，因为您可以使用此名称查找有关目标连接的信息。 |
| `description` | 可包含的可选值，用于提供有关目标连接的更多信息。 |
| `connectionSpec.id` | 对应于数据湖的连接规范ID。 此固定ID为： `6b137bf6-d2a0-48c8-914b-d50f4942eb85`。 |
| `data.format` | 要摄取的[!DNL SugarCRM Events]数据的格式。 |
| `params.dataSetId` | 在上一步中检索到的目标数据集ID。 |

**响应**

成功的响应返回新目标连接的唯一标识符(`id`)。 此ID在后续步骤中是必需的。

```json
{
    "id": "dfe9113e-be98-4d63-80a9-f41761721049",
    "etag": "\"84050267-0000-0200-0000-6368b3640000\""
}
```

### 创建映射 {#mapping}

要将源数据摄取到目标数据集中，必须首先将其映射到目标数据集所遵循的目标架构。 这是通过在请求有效负载中定义数据映射的情况下对[[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/)执行POST请求来实现的。

**API格式**

```http
POST /conversion/mappingSets
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "mappings": [
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_by",
          "destination": "_extconndev.created_by"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_by_id",
          "destination": "_extconndev.created_by_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_date",
          "destination": "_extconndev.created_date"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.name",
          "destination": "_extconndev.name_event"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.event_id",
          "destination": "_extconndev.id_event"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.event_id",
          "destination": "_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.sessions",
          "destination": "_extconndev.sessions"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_by",
          "destination": "_extconndev.updated_by"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_by_id",
          "destination": "_extconndev.updated_by_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_date",
          "destination": "_extconndev.updated_date"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_date",
          "destination": "timestamp"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.event",
          "destination": "_extconndev.event"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.description",
          "destination": "_extconndev.description"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.folder_id",
          "destination": "_extconndev.folder_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.status",
          "destination": "_extconndev.status"
      }
      ]
  }'
```

| 属性 | 描述 |
| --- | --- |
| `outputSchema.schemaRef.id` | 在之前的步骤中生成的[目标XDM架构](#target-schema)的ID。 |
| `mappings.sourceType` | 正在映射的源属性类型。 |
| `mappings.source` | 需要映射到目标XDM路径的源属性。 |
| `mappings.destination` | 源属性将映射到的目标XDM路径。 |

**响应**

成功的响应返回新创建的映射的详细信息，包括其唯一标识符(`id`)。 在后续步骤中需要使用此值来创建数据流。

```json
{
    "id": "d3845beaceeb49669228973f5f937f89",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 创建流 {#flow}

将数据从[!DNL SugarCRM Events]引入Experience Platform的最后一步是创建数据流。 现在，您已准备以下必需值：

* [Source连接Id](#source-connection)
* [目标连接ID](#target-connection)
* [映射 ID](#mapping)

数据流负责从源中计划和收集数据。 您可以通过在有效负载中提供前面提到的值时执行POST请求来创建数据流。

要计划摄取，您必须先将开始时间值设置为纪元时间（以秒为单位）。 然后，必须将频率值设置为`hour`或`day`之一。 间隔值用于指定两次连续摄取之间的周期。 间隔值应设置为`1`或`24`，具体取决于`hour`或`day`的`scheduleParams.frequency`选择。

**API格式**

```http
POST /flows
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Connector Description Flow Generic Rest",
      "description": "SugarCRM Connector Description Flow Generic Rest",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3"
      ],
      "targetConnectionIds": [
          "6b137bf6-d2a0-48c8-914b-d50f4942eb85"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "d3845beaceeb49669228973f5f937f89",
                  "mappingVersion": "0"
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1625040887",
          "frequency": "hour",
          "interval": 1
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 您的数据流的名称。 确保数据流的名称是描述性的，因为您可以使用此名称查找数据流上的信息。 |
| `description` | 可包含的可选值，用于提供有关数据流的更多信息。 |
| `flowSpec.id` | 创建数据流所需的流规范ID。 此固定ID为： `6499120c-0b15-42dc-936e-847ea3c24d72`。 |
| `flowSpec.version` | 流规范ID的相应版本。 此值默认为`1.0`。 |
| `sourceConnectionIds` | 在之前的步骤中生成的[源连接ID](#source-connection)。 |
| `targetConnectionIds` | 在之前的步骤中生成的[目标连接ID](#target-connection)。 |
| `transformations` | 此属性包含需要应用于数据的各种转换。 将不符合XDM的数据引入Experience Platform时，需要此属性。 |
| `transformations.name` | 分配给转换的名称。 |
| `transformations.params.mappingId` | 在之前的步骤中生成的[映射ID](#mapping)。 |
| `transformations.params.mappingVersion` | 映射ID的相应版本。 此值默认为`0`。 |
| `scheduleParams.startTime` | 此属性包含有关数据流的摄取计划的信息。 |
| `scheduleParams.frequency` | 数据流收集数据的频率。 可接受的值包括： `hour`或`day`。 |
| `scheduleParams.interval` | 间隔指定两次连续流运行之间的周期。 间隔的值应为非零整数。 间隔值应设置为`1`或`24`，具体取决于`hour`或`day`的`scheduleParams.frequency`选择。 |

**响应**

成功的响应返回新创建的数据流的ID (`id`)。 您可以使用此ID监视、更新或删除数据流。

```json
{
     "id": "fcd16140-81b4-422a-8f9a-eaa92796c4f4",
     "etag": "\"9200a171-0000-0200-0000-6368c1da0000\""
}
```

## 附录

以下部分提供了有关监视、更新和删除数据流的步骤的信息。

### 监测数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关流运行、完成状态和错误的信息。 有关完整的API示例，请阅读有关[使用API监视源数据流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html)的指南。

### 更新您的数据流

通过提供数据流的ID，向[!DNL Flow Service] API的`/flows`端点发出PATCH请求来更新数据流的详细信息，例如其名称和描述，以及其运行计划和关联的映射集。 发出PATCH请求时，必须在`If-Match`标头中提供数据流唯一的`etag`。 有关完整的API示例，请阅读有关使用API [更新源数据流的指南](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### 更新您的帐户

在提供基本连接ID作为查询参数的同时，通过向[!DNL Flow Service] API执行PATCH请求来更新源帐户的名称、描述和凭据。 发出PATCH请求时，必须在`If-Match`标头中提供源帐户的唯一`etag`。 有关完整的API示例，请阅读有关[使用API更新源帐户](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html)的指南。

### 删除您的数据流

在查询参数中提供要删除的数据流的ID时，通过向[!DNL Flow Service] API执行DELETE请求来删除数据流。 有关完整的API示例，请阅读有关[使用API删除数据流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html)的指南。

### 删除您的帐户

在提供要删除的帐户的基本连接ID时，通过向[!DNL Flow Service] API执行DELETE请求来删除您的帐户。 有关完整的API示例，请阅读有关使用API[&#128279;](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html)删除源帐户的指南。

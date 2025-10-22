---
keywords: Experience Platform；主页；热门主题；云存储数据
solution: Experience Platform
title: 使用流服务API为云存储源创建数据流
type: Tutorial
description: 本教程涵盖了从第三方云存储检索数据，以及使用源连接器和API将数据引入Experience Platform的步骤。
exl-id: 95373c25-24f6-4905-ae6c-5000bf493e6f
source-git-commit: 2ad0ffba128e8c51f173d24d4dd2404b9cbbb59a
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API为云存储源创建数据流

本教程介绍了从云存储源检索数据以及使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)将数据引入Experience Platform的步骤。

>[!NOTE]
>
>要创建数据流，您必须已具有带云存储源的有效基本连接ID。 如果您没有此ID，请参阅[源概述](../../../home.md#cloud-storage)，以了解可创建基础连接的云存储源的列表。

## 快速入门

本教程要求您实际了解Adobe Experience Platform的以下组件：

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   - [架构组合的基础知识](../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   - [架构注册表开发人员指南](../../../../xdm/api/getting-started.md)：包含成功执行对架构注册表API的调用所需了解的重要信息。 这包括您的`{TENANT_ID}`、“容器”的概念以及发出请求所需的标头（请特别注意“接受”标头及其可能的值）。
- [[!DNL Catalog Service]](../../../../catalog/home.md)：目录是Experience Platform中数据位置和谱系的记录系统。
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md)：批量摄取API允许您将数据作为批处理文件摄取到Experience Platform中。
- [沙盒](../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../landing/api-guide.md)指南。

## 创建源连接 {#source}

您可以在提供基本连接ID、要摄取的源文件的路径以及源对应的连接规范ID的同时，通过向`sourceConnections` API的[!DNL Flow Service]端点发出POST请求来创建源连接。

创建源连接时，还必须为数据格式属性定义一个枚举值。

为基于文件的源使用以下枚举值：

| 数据格式 | 枚举值 |
| ----------- | ---------- |
| 已分隔 | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

对于所有基于表的源，将该值设置为`tabular`。

**API格式**

```http
POST /sourceConnections
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited",
          "properties": {
              "columnDelimiter": "{COLUMN_DELIMITER}",
              "encoding": "{ENCODING}",
              "compressionType": "{COMPRESSION_TYPE}"
          }
      },
      "params": {
          "path": "/acme/summerCampaign/account.csv",
          "type": "file",
          "cdcEnabled": true
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `baseConnectionId` | 云存储源的基本连接ID。 |
| `data.format` | 要带入Experience Platform的数据的格式。 支持的值为： `delimited`、`JSON`和`parquet`。 |
| `data.properties` | （可选）在创建源连接时可应用于数据的一组属性。 |
| `data.properties.columnDelimiter` | （可选）收集平面文件时可指定的单个字符列分隔符。 任何单个字符值都是允许的列分隔符。 如果未提供，则使用逗号(`,`)作为默认值。 **注意**： `columnDelimiter`属性只能在引入分隔文件时使用。 |
| `data.properties.encoding` | （可选）一个属性，定义将数据摄取到Experience Platform时要使用的编码类型。 支持的编码类型为： `UTF-8`和`ISO-8859-1`。 **注意**： `encoding`参数仅在摄取分隔的CSV文件时可用。 将使用默认编码`UTF-8`摄取其他文件类型。 |
| `data.properties.compressionType` | （可选）一个属性，定义用于摄取的压缩文件类型。 支持的压缩文件类型为： `bzip2`、`gzip`、`deflate`、`zipDeflate`、`tarGzip`和`tar`。 **注意**： `compressionType`属性只能在引入分隔文件或JSON文件时使用。 |
| `params.path` | 您正在访问的源文件的路径。 此参数指向单个文件或整个文件夹。  **注意**：您可以使用星号代替文件名来指定整个文件夹的摄取。 例如： `/acme/summerCampaign/*.csv`将摄取整个`/acme/summerCampaign/`文件夹。 |
| `params.type` | 您正在摄取的源数据文件的文件类型。 使用类型`file`摄取单个文件，使用类型`folder`摄取整个文件夹。 |
| `params.cdcEnabled` | 一个布尔值，指示是否启用更改历史记录捕获。 在与关系架构一起使用时，变更数据捕获依赖于`_change_request_type`控件列(`u` — upsert， `d` — delete)，该列在引入期间进行评估，但未存储在目标架构中。 以下云存储源支持此属性： <ul><li>[!DNL Azure Blob]</li><li>[!DNL Data Landing Zone]</li><li>[!DNL Google Cloud Storage]</li><li>[!DNL SFTP]</li></ul>有关此功能的概述，请参阅[Data Mirror概述](../../../../xdm/data-mirror/overview.md)。 有关实现详细信息，请阅读在源[中使用](../change-data-capture.md)更改数据捕获的指南[关系架构技术参考](../../../../xdm/schema/relational.md)。 |
| `connectionSpec.id` | 与特定云存储源关联的连接规范ID。 有关连接规范ID的列表，请参阅[附录](#appendix)。 |

**响应**

成功的响应返回新创建的源连接的唯一标识符(`id`)。 此ID是稍后步骤创建数据流所必需的。

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

### 使用正则表达式选择要摄取的特定文件集 {#regex}

在创建源连接时，您可以使用正则表达式将一组特定的文件从源摄取到Experience Platform。

**API格式**

```http
POST /sourceConnections
```

**请求**

在以下示例中，文件路径中使用正则表达式以指定摄取名称中包含`premium`的所有CSV文件。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/*premium*.csv",
          "type": "folder"
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

### 配置源连接以递归方式摄取数据

创建源连接时，可以使用`recursive`参数从深度嵌套的文件夹中摄取数据。

**API格式**

```http
POST /sourceConnections
```

**请求**

在以下示例中，`recursive: true`参数通知[!DNL Flow Service]在摄取过程中以递归方式读取所有子文件夹。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source with recursive ingestion",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/customers/premium/buyers/recursive",
          "type": "folder",
          "recursive": true
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

## 创建目标XDM架构 {#target-schema}

为了在Experience Platform中使用源数据，必须创建目标架构，以根据您的需求构建源数据。 然后，使用目标架构创建包含源数据的Experience Platform数据集。

通过对[架构注册表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)执行POST请求，可以创建目标XDM架构。

有关如何创建目标XDM架构的详细步骤，请参阅有关使用API [创建架构的教程](../../../../xdm/api/schemas.md)。

## 创建目标数据集 {#target-dataset}

通过向[目录服务API](https://developer.adobe.com/experience-platform-apis/references/catalog/)执行POST请求，在有效负载中提供目标架构的ID，可以创建目标数据集。

有关如何创建目标数据集的详细步骤，请参阅有关[使用API创建数据集的教程](../../../../catalog/api/create-dataset.md)。

## 创建目标连接 {#target-connection}

目标连接表示与所摄取数据所登陆的目标之间的连接。 要创建目标连接，您必须提供与数据湖关联的固定连接规范ID。 此连接规范ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

现在，您拥有目标架构、目标数据集以及到数据湖的连接规范ID。 使用这些标识符，您可以使用[!DNL Flow Service] API创建目标连接，以指定将包含入站源数据的数据集。

**API格式**

```http
POST /targetConnections
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f3c3cedb2805c194ff0b69a"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `data.schema.id` | 目标XDM架构的`$id`。 |
| `data.schema.version` | 架构的版本。 此值必须设置为`application/vnd.adobe.xed-full+json;version=1`，这将返回架构的最新次版本。 |
| `params.dataSetId` | 上一步中生成的目标数据集的ID。 **注意**：创建目标连接时，必须提供有效的数据集ID。 无效的数据集ID将导致错误。 |
| `connectionSpec.id` | 用于连接到数据湖的连接规范ID。 此ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |

**响应**

成功的响应返回新目标连接的唯一标识符(`id`)。 此ID在后续步骤中是必需的。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 创建映射 {#mapping}

要将源数据摄取到目标数据集中，必须首先将其映射到目标数据集所遵循的目标架构。

要创建映射集，请在提供目标XDM架构`mappingSets`和要创建的映射集的详细信息时，向[[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/)的`$id`端点发出POST请求。

>[!TIP]
>
>您可以使用云存储源连接器映射复杂数据类型，例如JSON文件中的数组。

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
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| 属性 | 描述 |
| --- | --- |
| `xdmSchema` | 目标XDM架构的ID。 |

**响应**

成功的响应返回新创建的映射的详细信息，包括其唯一标识符(`id`)。 在后续步骤中需要使用此值来创建数据流。

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 检索数据流规范 {#specs}

数据流负责从源收集数据并将这些数据引入Experience Platform。 要创建数据流，您必须首先获取负责收集云存储数据的数据流规范。

**API格式**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**请求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!NOTE]
>
>为简单起见，以下JSON响应有效负载已隐藏。 选择“payload”（有效负载）可查看响应有效负载。

+++ 查看有效负荷

**响应**

成功的响应将返回数据流规范的详细信息，该规范负责将数据从源引入Experience Platform。 响应包括创建新数据流所需的唯一流规范`id`。

```json
{
  "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
  "name": "CloudStorageToAEP",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "isSourceFlow": true,
    "flacValidationSupported": true,
    "frequency": "batch",
    "notification": {
      "category": "sources",
      "flowRun": {
        "enabled": true
      }
    }
  },
  "sourceConnectionSpecIds": [
    "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
    "ecadc60c-7455-4d87-84dc-2a0e293d997b",
    "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
    "4c10e202-c428-4796-9208-5f1f5732b1cf",
    "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
    "32e8f412-cdf7-464c-9885-78184cb113fd",
    "b7bf2577-4520-42c9-bae9-cad01560f7bc",
    "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
    "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
    "54e221aa-d342-4707-bcff-7a4bceef0001",
    "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
    "26f526f2-58f4-4712-961d-e41bf1ccc0e8"
  ],
  "targetConnectionSpecIds": [
    "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
  ],
  "permissionsInfo": {
    "view": [
      {
        "@type": "lowLevel",
        "name": "EnterpriseSource",
        "permissions": [
          "read"
        ]
      }
    ],
    "manage": [
      {
        "@type": "lowLevel",
        "name": "EnterpriseSource",
        "permissions": [
          "write"
        ]
      }
    ]
  },
  "optionSpec": {
    "name": "OptionSpec",
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "properties": {
        "errorDiagnosticsEnabled": {
          "title": "Error diagnostics.",
          "description": "Flag to enable detailed and sample error diagnostics summary.",
          "type": "boolean",
          "default": false
        },
        "partialIngestionPercent": {
          "title": "Partial ingestion threshold.",
          "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
          "type": "number",
          "exclusiveMinimum": 0
        }
      }
    }
  },
  "scheduleSpec": {
    "name": "PeriodicSchedule",
    "type": "Periodic",
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "properties": {
        "startTime": {
          "description": "epoch time",
          "type": "integer"
        },
        "frequency": {
          "type": "string",
          "enum": [
            "once",
            "minute",
            "hour",
            "day",
            "week"
          ]
        },
        "interval": {
          "type": "integer"
        },
        "backfill": {
          "type": "boolean",
          "default": true
        }
      },
      "required": [
        "startTime",
        "frequency"
      ],
      "if": {
        "properties": {
          "frequency": {
            "const": "once"
          }
        }
      },
      "then": {
        "allOf": [
          {
            "not": {
              "required": [
                "interval"
              ]
            }
          },
          {
            "not": {
              "required": [
                "backfill"
              ]
            }
          }
        ]
      },
      "else": {
        "required": [
          "interval"
        ],
        "if": {
          "properties": {
            "frequency": {
              "const": "minute"
            }
          }
        },
        "then": {
          "properties": {
            "interval": {
              "minimum": 15
            }
          }
        },
        "else": {
          "properties": {
            "interval": {
              "minimum": 1
            }
          }
        }
      }
    }
  },
  "transformationSpec": [
    {
      "name": "Mapping",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines various params required for different mapping from source to target",
        "properties": {
          "mappingId": {
            "type": "string"
          },
          "mappingVersion": {
            "type": "string"
          }
        }
      }
    }
  ],
  "runSpec": {
      "name": "ProviderParams",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines various params required for creating flow run.",
        "properties": {
          "startTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the run. The value is represented in Unix epoch time."
          },
          "windowStartTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the window against which data is to be pulled. The value is represented in Unix epoch time."
          },
          "windowEndTime": {
            "type": "integer",
            "description": "An integer that defines the end time of the window against which data is to be pulled.  The value is represented in Unix epoch time."
          }
        },
        "required": [
          "startTime",
          "windowStartTime",
          "windowEndTime"
        ]
      }
    }
}
```

+++

## 创建数据流

收集云存储数据的最后一步是创建数据流。 现在，您已准备以下必需值：

- [Source连接Id](#source)
- [目标连接ID](#target)
- [映射 ID](#mapping)
- [数据流规范ID](#specs)

数据流负责从源中计划和收集数据。 您可以通过在有效负载中提供前面提到的值时执行POST请求来创建数据流。

>[!NOTE]
>
>对于批量摄取，每个后续数据流会根据其&#x200B;**上次修改时间**&#x200B;时间戳选择从源中摄取的文件。 这意味着批处理数据流从源中选择新的文件，或者自上次数据流运行以来修改的文件。

要计划摄取，您必须先将开始时间值设置为纪元时间（以秒为单位）。 然后，必须将频率值设置为五个选项之一： `once`、`minute`、`hour`、`day`或`week`。 间隔值用于指定两次连续摄取之间的时间段，创建一次性摄取不需要设置间隔。 对于所有其他频率，间隔值必须设置为等于或大于`15`。

>[!IMPORTANT]
>
>强烈建议在使用[FTP连接器](../../../connectors/cloud-storage/ftp.md)时计划一次性摄取的数据流。

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
        "name": "Cloud Storage flow to Experience Platform",
        "description": "Cloud Storage flow to Experience Platform",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "26b53912-1005-49f0-b539-12100559f0e2"
        ],
        "targetConnectionIds": [
            "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": 0
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1597784298",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `flowSpec.id` | 在上一步中检索到[流规范ID](#specs)。 |
| `sourceConnectionIds` | 在之前的步骤中检索到[源连接ID](#source)。 |
| `targetConnectionIds` | 在之前的步骤中检索到[目标连接ID](#target-connection)。 |
| `transformations.params.mappingId` | 在之前的步骤中检索到[映射ID](#mapping)。 |
| `scheduleParams.startTime` | 以纪元时间表示的数据流开始时间。 |
| `scheduleParams.frequency` | 数据流收集数据的频率。 可接受的值包括： `once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 间隔指定两次连续流运行之间的周期。 间隔的值应为非零整数。 每个频率的最小接受间隔值如下：<ul><li>**一次**：不适用</li><li>**分钟**： 15</li><li>**小时**： 1</li><li>**天**： 1</li><li>**周**： 1</li></ul> |

**响应**

成功的响应返回新创建的数据流的ID (`id`)。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 监测数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关流运行、完成状态和错误的信息。 有关如何监视数据流的详细信息，请参阅有关API中[监视数据流的教程](../monitor.md)

## 后续步骤

在本教程之后，您已创建一个源连接器，以按计划从云存储中收集数据。 传入数据现在可供下游Experience Platform服务（如[!DNL Real-Time Customer Profile]和[!DNL Data Science Workspace]）使用。 有关更多详细信息，请参阅以下文档：

- [实时客户轮廓概述](../../../../profile/home.md)
- [数据科学工作区概述](../../../../data-science-workspace/home.md)

## 附录 {#appendix}

以下部分列出了不同的云存储源连接器及其连接规范。

### 连接规范

| 连接器名称 | 连接规范 |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) | `b3ba5556-48be-44b7-8b85-ff2b69b46dc4` |
| [!DNL Azure Event Hubs] （事件中心） | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |

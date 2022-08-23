---
keywords: Experience Platform；主页；热门主题；云存储数据
solution: Experience Platform
title: 使用流服务API为云存储源创建数据流
topic-legacy: overview
type: Tutorial
description: 本教程介绍了从第三方云存储检索数据，以及使用源连接器和API将数据导入平台的步骤。
exl-id: 95373c25-24f6-4905-ae6c-5000bf493e6f
source-git-commit: 962baf6258629f319c24ec1503ea82f04b6c9c95
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 1%

---

# 使用为云存储源创建数据流 [!DNL Flow Service] API

本教程介绍了从云存储源检索数据以及使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>要创建数据流，您必须已拥有与云存储源的有效基本连接ID。 如果您没有此ID，请参阅 [源概述](../../../home.md#cloud-storage) 有关可创建基本连接的云存储源列表。

## 快速入门

本教程要求您对Adobe Experience Platform的以下组件有一定的了解：

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   - [架构组合的基础知识](../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   - [架构注册开发人员指南](../../../../xdm/api/getting-started.md):包括成功调用架构注册表API所需了解的重要信息。 这包括您的 `{TENANT_ID}`、“容器”的概念以及发出请求所需的标头（请特别注意接受标头及其可能值）。
- [[!DNL Catalog Service]](../../../../catalog/home.md):目录是Experience Platform中数据位置和谱系的记录系统。
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md):批量摄取API允许您将数据作为批处理文件导入到Experience Platform中。
- [沙箱](../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../landing/api-guide.md).

## 创建源连接 {#source}

您可以通过向 `sourceConnections` 端点 [!DNL Flow Service] 提供基本连接ID时的API、要摄取的源文件的路径以及源的相应连接规范ID。

创建源连接时，还必须为数据格式属性定义枚举值。

为基于文件的源使用以下枚举值：

| 数据格式 | 枚举值 |
| ----------- | ---------- |
| 分隔 | `delimited` |
| JSON | `json` |
| 镶木 | `parquet` |

对于所有基于表的源，将值设置为 `tabular`.

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
                "encoding": "{ENCODING}"
                "compressionType": "{COMPRESSION_TYPE}"
            }
        },
        "params": {
            "path": "/acme/summerCampaign/account.csv",
            "type": "file"
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
| `data.format` | 要引入平台的数据格式。 支持的值包括： `delimited`, `JSON`和 `parquet`. |
| `data.properties` | （可选）一组属性，在创建源连接时可以应用于数据。 |
| `data.properties.columnDelimiter` | （可选）在收集平面文件时可指定的单字符列分隔符。 任何单个字符值都是允许的列分隔符。 如果未提供，请使用逗号(`,`)作为默认值。 **注意**:的 `columnDelimiter` 仅在摄取分隔文件时才能使用属性。 |
| `data.properties.encoding` | （可选）此属性定义将数据摄取到平台时要使用的编码类型。 支持的编码类型包括： `UTF-8` 和 `ISO-8859-1`. **注意**:的 `encoding` 参数仅在摄取分隔的CSV文件时可用。 其他文件类型将采用默认编码进行摄取， `UTF-8`. |
| `data.properties.compressionType` | （可选）用于定义要摄取的压缩文件类型的属性。 支持的压缩文件类型包括： `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip`和 `tar`. **注意**:的 `compressionType` 仅在摄取分隔文件或JSON文件时才能使用属性。 |
| `params.path` | 您访问的源文件的路径。 此参数指向单个文件或整个文件夹。  **注意**:您可以使用星号代替文件名来指定整个文件夹的摄取。 例如： `/acme/summerCampaign/*.csv` 会摄取整个 `/acme/summerCampaign/` 文件夹。 |
| `params.type` | 要摄取的源数据文件的文件类型。 使用类型 `file` 摄取单个文件并使用类型 `folder` 以摄取整个文件夹。 |
| `connectionSpec.id` | 与您的特定云存储源关联的连接规范ID。 请参阅 [附录](#appendix) ，以获取连接规范ID列表。 |

**响应**

成功的响应会返回唯一标识符(`id`)。 在后续步骤中需要此ID才能创建数据流。

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## 创建目标XDM架构 {#target-schema}

要在Platform中使用源数据，必须创建目标架构以根据您的需求构建源数据。 然后，目标架构用于创建包含源数据的Platform数据集。

通过对 [架构注册表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

有关如何创建目标XDM架构的详细步骤，请参阅 [使用API创建模式](../../../../xdm/api/schemas.md).

## 创建目标数据集 {#target-dataset}

通过对 [目录服务API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，在有效负载中提供目标架构的ID。

有关如何创建目标数据集的详细步骤，请参阅 [使用API创建数据集](../../../../catalog/api/create-dataset.md).

## 创建目标连接 {#target-connection}

目标连接表示所摄取数据所登陆目标的连接。 要创建目标连接，必须提供与数据湖关联的固定连接规范ID。 此连接规范ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

现在，您将唯一标识符作为目标数据集的目标架构，并将连接规范ID用于数据湖。 使用这些标识符，您可以使用 [!DNL Flow Service] 用于指定将包含集客源数据的数据集的API。

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
| `data.schema.id` | 的 `$id` 目标XDM架构的URL。 |
| `data.schema.version` | 架构的版本。 必须设置此值 `application/vnd.adobe.xed-full+json;version=1`，可返回架构的最新次要版本。 |
| `params.dataSetId` | 目标数据集的ID。 |
| `connectionSpec.id` | 修复了与数据湖的连接规范ID。 此ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**响应**

成功的响应会返回新目标连接的唯一标识符(`id`)。 此ID是后续步骤所必需的。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 创建映射 {#mapping}

要将源数据摄取到目标数据集，必须先将其映射到目标数据集所附加的目标架构。

要创建映射集，请向 `mappingSets` 的端点 [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) 提供目标XDM模式时 `$id` 以及要创建的映射集的详细信息。

>[!TIP]
>
>您可以使用云存储源连接器映射JSON文件中的数组等复杂数据类型。

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

成功的响应会返回新创建映射的详细信息，包括其唯一标识符(`id`)。 在后续步骤中需要此值才能创建数据流。

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

数据流负责从源中收集数据并将它们引入平台。 要创建数据流，必须首先获取负责收集云存储数据的数据流规范。

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
>为简便起见，下面隐藏了JSON响应有效负载。 选择“有效负荷”以查看响应有效负荷。

+++ 查看有效负载

**响应**

成功的响应会返回负责将数据从源引入平台的数据流规范的详细信息。 响应包括唯一流量规范 `id` 创建新数据流时需要。

```json
{
  "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
  "name": "CloudStorageToAEP",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "isSourceFlow": true,
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
          "windowStartTime": {
            "type": "integer",
            "description": "The start time for the dataflow in epoch time."
          },
          "windowEndTime": {
            "type": "integer",
            "description": "The end time for the dataflow in epoch time."
          }
        },
        "required": [
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

- [源连接ID](#source)
- [Target连接ID](#target)
- [映射ID](#mapping)
- [数据流规范ID](#specs)

数据流负责从源中调度和收集数据。 通过在有效负载中提供先前提到的值时执行POST请求，可以创建数据流。

>[!NOTE]
>
>对于批量摄取，每个后续数据流都会根据文件的源文件选择要摄取的文件 **上次修改时间** 时间戳。 这意味着批处理数据流从源中选择新文件或自上次数据流运行以来已修改的文件。

要计划摄取，您必须首先将开始时间值设置为以秒为单位的新纪元时间。 然后，您必须将频率值设置为以下五个选项之一： `once`, `minute`, `hour`, `day`或 `week`. 间隔值可指定两个连续摄取和创建一次性摄取之间的周期，而无需设置间隔。 对于所有其他频率，间隔值必须设置为等于或大于 `15`.

>[!IMPORTANT]
>
>强烈建议在使用 [FTP连接器](../../../connectors/cloud-storage/ftp.md).

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
        "name": "Cloud Storage flow to Platform",
        "description": "Cloud Storage flow to Platform",
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
| `flowSpec.id` | 的 [流规范ID](#specs) 已在上一步中检索。 |
| `sourceConnectionIds` | 的 [源连接ID](#source) 在之前的步骤中检索。 |
| `targetConnectionIds` | 的 [目标连接ID](#target-connection) 在之前的步骤中检索。 |
| `transformations.params.mappingId` | 的 [映射ID](#mapping) 在之前的步骤中检索。 |
| `scheduleParams.startTime` | 新纪元时间中数据流的开始时间。 |
| `scheduleParams.frequency` | 数据流收集数据的频率。 可接受的值包括： `once`, `minute`, `hour`, `day`或 `week`. |
| `scheduleParams.interval` | 该间隔指定两个连续流运行之间的周期。 间隔的值应为非零整数。 将频率设置为时，不需要间隔 `once` 且应大于或等于 `15` 的其他频率值。 |

**响应**

成功的响应会返回ID(`id`)。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 监控数据流

创建数据流后，您可以监视通过其摄取的数据，以查看有关流量运行、完成状态和错误的信息。 有关如何监视数据流的更多信息，请参阅 [监控API中的数据流](../monitor.md)

## 后续步骤

在本教程中，您创建了一个源连接器，用于按计划从云存储中收集数据。 传入数据现在可由下游Platform服务使用，例如 [!DNL Real-time Customer Profile] 和 [!DNL Data Science Workspace]. 有关更多详细信息，请参阅以下文档：

- [实时客户资料概述](../../../../profile/home.md)
- [数据科学工作区概述](../../../../data-science-workspace/home.md)

## 附录 {#appendix}

以下部分列出了不同的云存储源连接器及其连接规范。

### 连接规范

| 连接器名称 | 连接规范 |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] （ADLS第2代） | `b3ba5556-48be-44b7-8b85-ff2b69b46dc4` |
| [!DNL Azure Event Hubs] （事件中心） | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |

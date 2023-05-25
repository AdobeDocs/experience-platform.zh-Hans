---
keywords: Experience Platform；主页；热门主题；ETL；ETL集成；ETL集成
solution: Experience Platform
title: 为Adobe Experience Platform开发ETL集成
description: ETL集成指南概述了创建高性能、安全连接器以进行Experience Platform并将数据摄取到Platform的一般步骤。
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '4081'
ht-degree: 1%

---

# 为Adobe Experience Platform开发ETL集成

ETL集成指南概述了为创建高性能、安全连接器的常规步骤 [!DNL Experience Platform] 并将数据摄取到 [!DNL Platform].


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Batch Ingestion]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [[!DNL Streaming Ingestion]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Experience PlatformAPI的身份验证和授权](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

本指南还包括设计ETL连接器时要使用的示例API调用，以及概述每个调用和调用相关说明的文档的链接 [!DNL Experience Platform] 服务和其API的使用，更详细地介绍了。

示例集成位于 [!DNL GitHub] 通过 [ETL生态系统集成参考代码](https://github.com/adobe/acp-data-services-etl-reference) 在 [!DNL Apache] 许可证版本2.0。

## 工作流

以下工作流程图提供了Adobe Experience Platform组件与ETL应用程序和连接器的集成的高级概述。

![](images/etl.png)

## Adobe Experience Platform组件

ETL连接器集成涉及多个Experience Platform组件。 下表概述了几个关键组件和功能：

- **AdobeIdentity Management System (IMS)**  — 提供对Adobe服务进行身份验证的框架。
- **IMS组织**  — 拥有或许可产品和服务并允许访问其成员的企业实体。
- **IMS用户** - IMS组织的成员。 组织与用户的关系是多对多。
- **[!DNL Sandbox]**  — 虚拟分区单个 [!DNL Platform] 实例，以帮助开发和改进数字体验应用程序。
- **数据发现**  — 记录摄取和转换的数据的元数据 [!DNL Experience Platform].
- **[!DNL Data Access]**  — 为用户提供一个访问其数据的界面，位于 [!DNL Experience Platform].
- **[!DNL Data Ingestion]**  — 将数据推送到 [!DNL Experience Platform] 替换为 [!DNL Data Ingestion] API。
- **[!DNL Schema Registry]**  — 定义并存储描述要在其中使用的数据结构的模式 [!DNL Experience Platform].

## 快速入门 [!DNL Experience Platform] API

以下部分提供成功调用所需的其他信息或您掌握的其他信息 [!DNL Experience Platform] API。

### 正在读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定的虚拟沙盒隔离。 的所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../sandboxes/home.md).

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的标头：

- Content-Type： application/json

## 一般用户流程

首先，ETL用户登录到 [!DNL Experience Platform] 用户界面(UI)，并使用标准连接器或推送服务连接器创建用于摄取的数据集。

在UI中，用户通过选择数据集架构来创建输出数据集。 架构的选择取决于要引入的数据类型（记录或时间序列） [!DNL Platform]. 通过单击UI中的“架构”选项卡，用户将能够查看所有可用的架构，包括架构支持的行为类型。

在ETL工具中，用户将在配置适当的连接（使用其凭据）后开始设计其映射转换。 假设ETL工具已经具有 [!DNL Experience Platform] 连接器已安装（此集成指南中未定义进程）。

中提供了示例ETL工具和工作流的模型 [ETL工作流](./workflow.md). 虽然ETL工具在格式上可能有所不同，但大多数工具都显示了相似的功能。

>[!NOTE]
>
>ETL连接器必须指定时间戳过滤器，以标记摄取数据和偏移的日期(即要读取其数据的窗口)。 ETL工具应支持在此或其他相关UI中获取这两个参数。 在Adobe Experience Platform中，这些参数将映射到可用日期（如果存在）或数据集批次对象中存在的捕获日期。

### 查看数据集列表

使用数据源进行映射，可以使用获取所有可用数据集的列表 [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

您可以发出一个API请求以查看所有可用数据集(例如， `GET /dataSets`)，最佳实践为包含限制响应大小的查询参数。

在请求完整数据集信息的情况下，响应有效负载的大小可能会超过3GB，这可能会降低整体性能。 因此，使用查询参数仅过滤所需信息将使 [!DNL Catalog] 查询效率更高。

#### 列表筛选

在筛选响应时，您可以通过用&amp;符号(`&`)。 某些查询参数接受逗号分隔的值列表，例如以下示例请求中的“属性”过滤器。

[!DNL Catalog] 响应会根据配置的限制自动计数，但“limit”查询参数可用于自定义约束并限制返回的对象数。 预配置的 [!DNL Catalog] 响应限制为：

- 如果未指定限制参数，则每个响应有效负载的最大对象数为20。
- 所有其他的全局限制 [!DNL Catalog] 查询是100个对象。
- 对于数据集查询，如果使用属性查询参数请求observableSchema，则返回的最大数据集数为20。
- 限制参数无效(包括 `limit=0`)遇到HTTP 400错误，该错误概述了正确的范围。
- 如果限制或偏移作为查询参数传递，则它们优先于作为标头传递的限制或偏移。

有关查询参数的更多详细信息，请参见 [目录服务概述](../catalog/home.md).

**API格式**

```http
GET /catalog/dataSets
GET /catalog/dataSets?{filter1}={value1},{value2}&{filter2}={value3}
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3&properties=name,description,schemaRef" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

请参阅 [目录服务概述](../catalog/home.md) 有关如何调用 [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

**响应**

响应包括三项(`limit=3`)数据集显示“name”、“description”和“schemaRef”，如 `properties` 查询参数。

```json
{
    "5b95b155419ec801e6eee780": {
        "name": "Store Transactions",
        "description": "Retails Store Transactions",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c351fa2f5fee300000fa9e8": {
        "name": "Loyalty Members",
        "description": "Loyalty Program Members",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c1823b19e6f400000993885": {
        "name": "Web Traffic",
        "description": "Retail Web Traffic",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2025a705890c6d4a4a06b16f8cf6f4ca",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

### 查看数据集架构

数据集的“schemaRef”属性包含引用数据集所基于的XDM架构的URI。 XDM架构(“schemaRef”)表示数据集可以使用的所有潜在字段，不一定表示正在使用的字段（请参阅下面的“observableSchema”）。

XDM架构是您在需要向用户显示可写入的所有可用字段列表时使用的架构。

上一个响应对象中的第一个“schemaRef.id”值(`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`)是一个URI，指向中的特定XDM架构 [!DNL Schema Registry]. 可以通过向发出查找(GET)请求来检索架构 [!DNL Schema Registry] API。

>[!NOTE]
>
>“schemaRef”属性替换现已弃用的“schema”属性。 如果数据集中的“schemaRef”不存在或不包含值，则需要检查“schema”属性是否存在。 可以通过将“schemaRef”替换为 `properties` 查询参数。 有关“schema”属性的更多详细信息，请参阅 [数据集“架构”属性](#dataset-schema-property-deprecated---eol-2019-05-30) 章节。

**API格式**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**请求**

请求使用编码的URL `id` 架构的URI（“schemaRef.id”属性的值），并需要“接受”标头。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

响应格式取决于请求中发送的“接受”标头的类型。 查找请求还需要 `version` 包含在接受标头中。 下表概述了可用于查找的“接受”标头：

| Accept | 描述 |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | 列出(GET)请求、标题、ID和版本 |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs和allOf已解决，具有标题和描述 |
| `application/vnd.adobe.xed+json; version={major version}` | 使用$ref和allOf的原始，具有标题和描述 |
| `application/vnd.adobe.xed-notext+json; version={major version}` | 原始版本：$ref和allOf，无标题或描述 |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs和allOf已解决，无标题或描述 |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs和allOf已解决，包括描述符 |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` 和 `application/vnd.adobe.xed-full+json; version={major version}` 是最常用的接受标头。 `application/vnd.adobe.xed-id+json` 首选在中列出资源 [!DNL Schema Registry] 因为它只返回“title”、“id”和“version”。 `application/vnd.adobe.xed-full+json; version={major version}` 首选用于查看特定资源（按其“id”），因为它返回所有字段（嵌套在“属性”下），以及标题和描述。

**响应**

返回的JSON架构描述了结构和字段级别信息（“类型”、“格式”、“最小值”、“最大值”等） 数据的，序列化为JSON。 如果采用JSON以外的序列化格式进行摄取（例如Parquet或Scala），则 [架构注册表指南](../xdm/tutorials/create-schema-api.md) 包含一个表，其中显示了所需的JSON类型(“meta：xdmType”)及其在其他格式中的相应表示形式。

连同这张表格， [!DNL Schema Registry] 开发人员指南包含可以使用进行的所有可能调用的深入示例 [!DNL Schema Registry] API。

### 数据集“架构”属性（已弃用 — EOL 2019-05-30）

数据集可能包含“架构”属性，该属性现已弃用，暂时可用于向后兼容。 例如，一个与之前类似的列表(GET)请求，其中“schema”替换为 `properties` 查询参数，可能会返回以下内容：

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

如果填充了数据集的“schema”属性，则表示该架构已弃用 `/xdms` schema和ETL连接器（如果支持）应使用“schema”属性中的值搭配 `/xdms` 端点（中一个已弃用的端点） [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/))以检索旧架构。

**API格式**

```http
GET /catalog/{"schema" property without the "@"}
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE]
>
>可选的查询参数， `expansion=xdm`，告知API完全展开并内联任何引用的架构。 在向用户展示所有潜在字段的列表时，您可能希望执行此操作。

**响应**

与的步骤类似 [查看数据集架构](#view-dataset-schema)，响应中包含一个JSON架构，用于描述数据的结构和字段级信息，这些信息序列化为JSON。

>[!NOTE]
>
>当“schema”字段为空或完全缺失时，连接器应读取“schemaRef”字段并使用 [架构注册表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/) 如前面的步骤所示 [查看数据集架构](#view-dataset-schema).

### “observableSchema”属性

数据集的“observableSchema”属性具有与XDM架构JSON的JSON结构匹配的JSON结构。 “observableSchema”包含传入输入文件中存在的字段。 将数据写入时 [!DNL Experience Platform]，用户无需使用目标架构中的每个字段。 相反，他们应该只提供正在使用的字段。

可观察架构是读取数据或显示可读取/映射的字段列表时将使用的架构。

```json
{
    "598d6e81b2745f000015edcb": {
        "observableSchema": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "name": {
                    "type": "string",
                },
                "age": {
                    "type": "string",
                }
            }
        }
    }
}
```

### 预览数据

ETL应用程序可以提供预览数据的功能([ETL工作流中的“图8”](./workflow.md))。 数据访问API提供了多个预览数据的选项。

其他信息，包括使用数据访问API预览数据的分步指南，请参见 [数据访问教程](../data-access/tutorials/dataset-data.md).

### 使用“属性”查询参数获取数据集详细信息

如上面的步骤所示，对于 [查看数据集列表](#view-list-of-datasets)，您可以使用“属性”查询参数来请求“文件”。

您可参阅 [目录服务概述](../catalog/home.md) 有关查询数据集和可用响应过滤器的详细信息。

**API格式**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**响应**

响应将包含一个数据集(`limit=1`)显示“files”属性。

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### 使用“文件”属性列出数据集文件

您还可以使用“文件”属性通过GET请求获取文件详细信息。

**API格式**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**响应**

响应包括数据集文件ID作为顶级属性，并且文件详细信息包含在数据集文件ID对象中。

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542749145828,
        "updated": 1542749145828
    },
    "14d5758c107443e1a83c714e56ca79d0-1": {
        "batchId": "14d5758c107443e1a83c714e56ca79d0",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542752699111,
        "updated": 1542752699111
    },
    "ea40946ac03140ec8ac4f25da360620a-1": {
        "batchId": "ea40946ac03140ec8ac4f25da360620a",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542756935535,
        "updated": 1542756935535
    }
}
```

### 获取文件详细信息

在上一个响应中返回的数据集文件ID可用于GET请求，以通过 [!DNL Data Access] API。

此 [数据访问概述](../data-access/home.md) 包含有关如何使用 [!DNL Data Access] API。

**API格式**

```http
GET /export/files/{DATASET_FILE_ID}
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**响应**

```json
[
    {
    "name": "{FILE_NAME}.parquet",
    "length": 2576,
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet"
            }
        }
    }
]
```

### 预览文件数据

“href”属性可用于通过 [[!DNL Data Access API]](../data-access/home.md).

**API格式**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

对上述请求的响应将包含文件内容的预览。

欲知关于 [!DNL Data Access] API（包括详细的请求和响应）可在 [数据访问概述](../data-access/home.md).

### 从数据集获取“fileDescription”

目标组件作为转换后数据的输出，数据工程师将选择一个输出数据集([ETL工作流中的“图12”](workflow.md))。 XDM架构与输出数据集关联。 要写入的数据将由数据发现API中数据集实体的“fileDescription”属性标识。 可使用数据集ID (`{DATASET_ID}`)。 JSON响应中的“fileDescription”属性将提供请求的信息。

**API格式**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{DATASET_ID}` | 此 `id` 尝试访问的数据集的值。 |

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
```

**响应**

```JSON
{
  "59c93f3da7d0c00000798f68": {
    "version": "1.0.4",
    "fileDescription": {
        "persisted": false,
        "format": "parquet"
    }
  }
}
```

数据将写入 [!DNL Experience Platform] 使用 [批量摄取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).  数据写入是一个异步过程。 当数据写入Adobe Experience Platform时，将创建一个批次，并仅在完全写入数据后标记为成功。

数据输入 [!DNL Experience Platform] 应该以Parquet文件的形式编写。

## 执行阶段

在执行开始时，连接器（如源组件中所定义）将从以下位置读取数据 [!DNL Experience Platform] 使用 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/). 转换过程将读取特定时间范围内的数据。 在内部，它将查询批量源数据集。 查询时，它会使用参数化（滚动时序数据，或增量数据）的开始日期，列出这些批次的数据集文件，并开始请求这些数据集文件的数据。

### 转换示例

此 [示例ETL转换](./transformations.md) 文档包含许多转换示例，包括身份处理和数据类型映射。 请参考这些转换。

### 从以下位置读取数据 [!DNL Experience Platform]

使用 [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)中，您可以获取指定开始时间和结束时间之间的所有批次，并按其创建顺序对它们进行排序。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

有关筛选批次的详细信息，请参阅 [数据访问教程](../data-access/tutorials/dataset-data.md).

### 从批处理中获取文件

获得所查找批次的ID后(`{BATCH_ID}`)，则可以通过检索属于特定批次的文件列表 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/).  欲知详情，请参见 [[!DNL Data Access] 教程](../data-access/tutorials/dataset-data.md).

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### 使用文件ID访问文件

使用文件的唯一ID (`{FILE_ID`)，则 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 可用于访问文件的特定详细信息，包括其名称、大小（以字节为单位）和下载链接。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

响应可能指向单个文件或目录。 欲知各项详情，请参阅 [[!DNL Data Access] 教程](../data-access/tutorials/dataset-data.md).

### 访问文件内容

此 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 可用于访问特定文件的内容。 要获取内容，将使用返回的值发出GET请求 `_links.self.href` 使用文件ID访问文件时。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

对此请求的响应包含文件的内容。 欲知更多信息（包括响应分页的详细信息），请参见 [如何通过数据访问API查询数据](../data-access/tutorials/dataset-data.md) 教程。

### 验证记录以符合架构

在写入数据时，用户可以根据XDM架构中定义的验证规则选择验证数据。 有关架构验证的更多信息，请参阅 [上的ETL生态系统集成参考代码 [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

如果您使用的参考实施位于 [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md)，则可以使用系统属性在此实施中启用架构验证 `-DenableSchemaValidation=true`.

可以使用以下属性对逻辑XDM类型执行验证 `minLength` 和 `maxlength` 对于字符串， `minimum` 和 `maximum` 用于整数等。 此 [架构注册表API开发人员指南](../xdm/api/getting-started.md) 包含一个表，其中概述了XDM类型以及可用于验证的属性。

>[!NOTE]
>
>为各种类型提供的最小值和最大值 `integer` 类型是该类型可以支持的MIN和MAX值，但这些值可以进一步限制为您选择的最小值和最大值。

### 创建批次

处理完数据后， ETL工具会将数据写回 [!DNL Experience Platform] 使用 [批量摄取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). 将数据添加到数据集之前，必须将其链接到稍后将上传到特定数据集的批次。

**请求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

有关创建批的详细信息（包括示例请求和响应），请参阅 [批量摄取概述](../ingestion/batch-ingestion/overview.md).

### 写入数据集

成功创建新批次后，可将文件上传到特定数据集。 可以在批次中发布多个文件，直到提升为止。 可使用小文件上传API上传文件；但是，如果文件过大，并且超过了网关限制，则可以使用大文件上传API。 有关同时使用大文件上传和小文件上传的详细信息，请参阅 [批量摄取概述](../ingestion/batch-ingestion/overview.md).

**请求**

数据输入 [!DNL Experience Platform] 应该以Parquet文件的形式编写。

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{ORG_ID}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### 标记批次上传完成

将所有文件上载到批处理之后，可以发出完成该批处理的信号。 这样， [!DNL Catalog] 为已完成的文件创建“DataSetFile”条目，并将其与生成批处理关联。 此 [!DNL Catalog] 然后，将批处理标记为成功，这会触发下游流摄取可用数据。

数据将首先在Adobe Experience Platform上的暂存位置着陆，然后在编目和验证后移至最终位置。 将所有数据移动到永久位置后，批次将被标记为成功。

**请求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

如果成功，响应将返回HTTP状态200 OK，并且响应正文为空。

ETL工具将确保在读取数据时记下源数据集的时间戳。

在下一次执行转换时（可能通过调度或事件调用），ETL将开始从先前保存的时间戳中请求数据以及之后的所有数据。

### 获取上一批次状态

在ETL工具中运行新任务之前，必须确保上一个批次成功完成。 此 [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) 提供了特定于批次的选项，该选项可提供相关批次的详细信息。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**响应**

如果前一个批次“状态”值为“成功”，则可以计划新任务，如下所示：

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "CLIENT_USER_ID@AdobeID",
    "updatedUser": "CLIENT_USER_ID@AdobeID",
    "updated": 1494349963467,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

### 按ID获取上一批次状态

单个批次状态可通过 [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) GET通过使用 `{BATCH_ID}`. 此 `{BATCH_ID}` 使用的ID将与创建批次时返回的ID相同。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**响应 — 成功**

以下响应显示了“success”：

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

**响应 — 失败**

如果出现故障，“错误”可以从响应中提取，并在ETL工具上显示为错误消息。

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "failure",
    "errors": [
        {
            "code": "200",
            "description": "Error in validating schema for file: 'adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv' with errorMessage=adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv is not a Parquet file. expected magic number at tail [80, 65, 82, 49] but found [57, 98, 55, 10] and errorType=java.lang.RuntimeException",
            "rows": []
        }
    ],
    "version": "1.0.1",
    "availableDates": {}
}
```

## 增量数据与快照数据，事件与配置文件

数据可以用2 x 2矩阵表示，如下所示：

| 增量事件 | 增量配置文件 |
|-------------------------------|----------------------|
| 快照事件（可能性较小） | 快照配置文件 |

事件数据通常是在每行中有索引时间戳列时收集的。

通常，当数据中没有时间戳并且每行都可以通过主/复合键进行标识时，就会产生配置文件数据。

增量数据是指只有新的/更新的数据进入系统并附加到数据集中的当前数据的位置。

快照数据是指所有数据进入系统并替换数据集中某些或所有以前的数据的情况。

对于增量事件，ETL工具应使用批次实体的可用日期/创建日期。 对于推送服务，可用日期将不存在，因此工具将使用批次创建/更新日期来标记增量。 每批增量事件都需要处理。

对于增量用户档案，ETL工具将使用批次实体的创建/更新日期。 通常需要处理每批增量配置文件数据。

快照事件的可能性非常小，这是因为数据非常庞大。 但是，如果要求这样做，则ETL工具必须仅选取最后一批进行处理。

使用快照配置文件时，ETL工具必须选取到达系统的最后一批数据。 但是，如果要求跟踪更改的版本，则需要处理所有批次。 ETL流程中的重复数据消除处理将有助于控制存储成本。

## 批量重放和数据重新处理

如果客户端发现过去“n”天内，ETL处理的数据未按预期发生，或者源数据本身可能不正确，则可能需要批量重放和数据重新处理。

要实现此目的，客户端的数据管理员将使用 [!DNL Platform] 用于删除包含损坏数据的批次的UI。 然后，可能需要重新运行ETL，从而使用正确的数据重新填充。 如果源本身具有损坏的数据，则数据工程师/管理员需要更正源批次并重新摄取数据(通过Adobe Experience Platform或ETL连接器)。

根据生成的数据类型，数据工程师可以选择从特定数据集中删除单个批次或所有批次。 数据将根据以下条件删除/存档 [!DNL Experience Platform] 准则。

在可能的情况下，清除数据的ETL功能很重要。

清除完成后，客户端管理员必须重新配置Adobe Experience Platform，从删除批次时起重新开始处理核心服务。

## 并发批处理

根据客户的决定，数据管理员/工程师可以决定以顺序方式或并发方式提取、转换和加载数据，具体取决于特定数据集的特征。 这还将基于客户端使用转换后的数据定位的用例。

例如，如果客户端持久保留在可更新的持久性存储中，并且事件的顺序或顺序很重要，则客户端可能需要严格处理具有顺序ETL转换的作业。

在其他情况下，使用指定的时间戳在内部排序的下游应用程序/进程可以处理乱序数据。 在这些情况下，并行ETL转换可以改善处理时间。

对于源批次，它仍将取决于客户端首选项和使用者限制。 如果源数据可以并行提取，而不考虑行的区域/顺序，则转换过程可以创建并行度更高的过程批次（基于无序处理的优化）。 但是，如果转换必须遵循时间戳或更改优先顺序，则数据访问API或ETL工具调度程序/调用必须确保批次处理尽可能不按顺序进行。

## 延迟

延迟是一个过程，在该过程中，输入数据还不够完整，无法发送到下游进程，但将来可能可用。 客户将确定他们个人对于未来匹配的数据窗口与处理成本的容忍度，以告知他们是否决定保留数据并在下一次转换执行中重新处理数据，希望可以在保留窗口内的某个未来时间扩充和协调/拼合数据。 此周期持续进行，直到行得到充分处理，或认为行太旧，无法继续投资。 每个迭代将生成延迟数据，该延迟数据是先前迭代中所有延迟数据的超集。

Adobe Experience Platform当前无法识别延期的数据，因此客户端实施必须依靠ETL和数据集手动配置在中创建另一个数据集 [!DNL Platform] 镜像可用于保留延期数据的源数据集。 在这种情况下，延迟的数据将与快照数据类似。 在每次执行ETL转换时，源数据将与延迟的数据合并并发送以供处理。

## Changelog

| 日期 | 操作 | 描述 |
| ---- | ------ | ----------- |
| 2019-01-19 | 从数据集中删除了“字段”属性 | 数据集以前包含一个“字段”属性，该属性包含架构的副本。 此功能不应再使用。 如果找到“fields”属性，则应忽略该属性，并改用“observedSchema”或“schemaRef”。 |
| 2019-03-15 | 已将“schemaRef”属性添加到数据集 | 数据集的“schemaRef”属性包含引用数据集所基于的XDM架构的URI，并代表数据集可以使用的所有潜在字段。 |
| 2019-03-15 | 所有最终用户标识符都映射到“identityMap”属性 | “identityMap”是主题的所有唯一标识符的封装，例如CRM ID、ECID或忠诚度计划ID。 此映射的使用者 [[!DNL Identity Service]](../identity-service/home.md) 解析主体的所有已知和匿名身份，为每个最终用户形成单个身份图。 |
| 2019-05-30 | 生命周期结束并删除数据集中的“架构”属性 | 数据集“schema”属性提供了使用已弃用的架构的引用链接 `/xdms` 中的端点 [!DNL Catalog] API。 该名称已被提供新文件中引用的架构的“id”、“version”和“contentType”的“schemaRef”替换 [!DNL Schema Registry] API。 |

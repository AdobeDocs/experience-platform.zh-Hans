---
keywords: Experience Platform；主页；热门主题；ETL；ETL集成；ETL集成
solution: Experience Platform
title: 为Adobe Experience Platform开发ETL集成
description: ETL集成指南概述了为Experience Platform创建高性能、安全连接器以及将数据摄取到Experience Platform的一般步骤。
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3978'
ht-degree: 2%

---

# 为Adobe Experience Platform开发ETL集成

ETL集成指南概述了为[!DNL Experience Platform]创建高性能、安全连接器并将数据摄取到[!DNL Experience Platform]中的常规步骤。


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Batch Ingestion]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [[!DNL Streaming Ingestion]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Experience Platform API的身份验证和授权](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

本指南还包括设计ETL连接器时要使用的示例API调用，其中包含指向概述每个[!DNL Experience Platform]服务的文档的链接以及其API的更详细的使用情况。

在[!DNL GitHub]上，通过[!DNL Apache]许可证版本2.0下的[ETL生态系统集成参考代码](https://github.com/adobe/acp-data-services-etl-reference)提供了示例集成。

## 工作流

以下工作流程图提供了Adobe Experience Platform组件与ETL应用程序和连接器的集成的高级概述。

![](images/etl.png)

## Adobe Experience Platform组件

ETL连接器集成涉及多个Experience Platform组件。 下表概述了几个关键组件和功能：

- **Adobe Identity Management System (IMS)** — 提供用于向Adobe服务进行身份验证的框架。
- **IMS组织** — 可以拥有或许可产品和服务并允许访问其成员的公司实体。
- **IMS用户** - IMS组织的成员。 组织到用户的关系是多对多。
- **[!DNL Sandbox]** — 虚拟分区单个[!DNL Experience Platform]实例，以帮助开发和改进数字体验应用程序。
- **数据发现** — 在[!DNL Experience Platform]中记录已摄取和转换数据的元数据。
- **[!DNL Data Access]** — 为用户提供一个访问他们在[!DNL Experience Platform]中的数据的界面。
- **[!DNL Data Ingestion]** — 使用[!DNL Data Ingestion] API将数据推送到[!DNL Experience Platform]。
- **[!DNL Schema Registry]** — 定义和存储描述要在[!DNL Experience Platform]中使用的数据结构的架构。

## [!DNL Experience Platform] API快速入门

以下部分提供了您需要了解或拥有的其他信息，以便成功调用[!DNL Experience Platform] API。

### 正在读取示例 API 调用

本指南提供了示例 API 调用来演示如何格式化请求。这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中有关[如何读取示例API调用](../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

### 收集所需标头的值

要调用[!DNL Experience Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

- 授权：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../sandboxes/home.md)。

包含负载 (POST、PUT、PATCH) 的所有请求都需要额外的标头：

- Content-Type： application/json

## 一般用户流程

首先，ETL用户登录到[!DNL Experience Platform]用户界面(UI)，并使用标准连接器或推送服务连接器创建用于摄取的数据集。

在UI中，用户通过选择数据集架构来创建输出数据集。 架构的选择取决于被摄取到[!DNL Experience Platform]中的数据类型（记录或时间序列）。 通过单击UI中的“架构”选项卡，用户将能够查看所有可用的架构，包括架构支持的行为类型。

在ETL工具中，用户将在配置适当的连接（使用其凭据）后开始设计其映射转换。 假设ETL工具已安装[!DNL Experience Platform]连接器（此集成指南中未定义进程）。

[ETL工作流](./workflow.md)中提供了示例ETL工具和工作流的模型。 虽然ETL工具在格式上可能有所不同，但大多数工具都会显示类似的功能。

>[!NOTE]
>
>ETL连接器必须指定时间戳过滤器，以标记摄取数据和偏移的日期(即要读取其数据的窗口)。 ETL工具应支持在此或其他相关UI中获取这两个参数。 在Adobe Experience Platform中，这些参数将映射到数据集的批处理对象中存在的可用日期（如果存在）或捕获日期。

### 查看数据集列表

使用用于映射的数据源，可以使用[[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)获取所有可用数据集的列表。

您可以发出单个API请求以查看所有可用数据集（例如`GET /dataSets`），最佳做法是包含查询参数，以限制响应的大小。

在请求完整数据集信息的情况下，响应有效负载的大小可能会超过3 GB，这可能会降低整体性能。 因此，使用查询参数仅筛选所需信息将提高[!DNL Catalog]查询的效率。

#### 列表筛选

在过滤响应时，可通过使用&amp;符号(`&`)分隔参数，在单个调用中使用多个过滤器。 某些查询参数接受以逗号分隔的值列表，例如，以下示例请求中的“属性”过滤器。

[!DNL Catalog]响应是根据配置的限制自动计量的，但“limit”查询参数可用于自定义约束和限制返回的对象数。 预配置的[!DNL Catalog]响应限制为：

- 如果未指定限制参数，则每个响应有效负载的最大对象数为20。
- 所有其他[!DNL Catalog]查询的全局限制为100个对象。
- 对于数据集查询，如果使用属性查询参数请求observableSchema，则返回的最大数据集数为20。
- HTTP 400错误（概述了正确的范围）符合无效的限制参数（包括`limit=0`）。
- 如果限制或偏移作为查询参数传递，则它们优先于作为标头传递的限制或偏移。

[目录服务概述](../catalog/home.md)中详细介绍了查询参数。

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

有关如何调用[[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)的详细示例，请参阅[目录服务概述](../catalog/home.md)。

**响应**

响应包括三个数据集(`limit=3`)，这些数据集显示由`properties`查询参数指示的“name”、“description”和“schemaRef”。

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

数据集的“schemaRef”属性包含引用数据集所基于的XDM架构的URI。 XDM架构(“schemaRef”)表示数据集可以使用的所有潜在字段，不一定是正在使用的字段（请参阅下面的“observableSchema”）。

XDM架构是您在需要向用户显示可写入的所有可用字段列表时使用的架构。

上一个响应对象(`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`)中的第一个“schemaRef.id”值是指向[!DNL Schema Registry]中的特定XDM架构的URI。 通过对[!DNL Schema Registry] API发出查找(GET)请求，可以检索架构。

>[!NOTE]
>
>“schemaRef”属性替换现已弃用的“schema”属性。 如果数据集中的“schemaRef”不存在或不包含值，您将需要检查是否存在“schema”属性。 可以通过在上一次调用中将`properties`查询参数中的“schemaRef”替换为“schema”来完成此操作。 有关“架构”属性的更多详细信息可在随后的[数据集“架构”属性](#dataset-schema-property-deprecated---eol-2019-05-30)部分中获得。

**API格式**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**请求**

该请求使用架构的URL编码的`id` URI（“schemaRef.id”属性的值），并需要Accept标头。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

响应格式取决于请求中发送的“接受”标头的类型。 查找请求还要求在“接受”标头中包含`version`。 下表概述了可用于查找的“接受”标头：

| 接受 | 描述 |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | 列出(GET)请求、标题、ID和版本 |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs和allOf已解决，具有标题和描述 |
| `application/vnd.adobe.xed+json; version={major version}` | 以$ref和allOf为原始，具有标题和描述 |
| `application/vnd.adobe.xed-notext+json; version={major version}` | 原始，带有$ref和allOf，无标题或描述 |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs和allOf已解决，无标题或描述 |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs和allOf已解决，包括描述符 |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json`和`application/vnd.adobe.xed-full+json; version={major version}`是最常用的接受标头。 在[!DNL Schema Registry]中列出资源时首选使用`application/vnd.adobe.xed-id+json`，因为它仅返回“title”、“id”和“version”。 `application/vnd.adobe.xed-full+json; version={major version}`首选用于查看特定资源（按其“id”），因为它返回所有字段（嵌套在“properties”下）以及标题和描述。

**响应**

返回的JSON架构描述了数据的结构和字段级信息（“类型”、“格式”、“最小值”、“最大值”等），这些信息序列化为JSON。 如果使用非JSON的序列化格式进行摄取（如Parquet或Scala），则[架构注册表指南](../xdm/tutorials/create-schema-api.md)包含一个表，该表以其他格式显示所需的JSON类型(&quot;meta：xdmType&quot;)及其相应表示形式。

除了此表外，[!DNL Schema Registry]开发人员指南还包含可以使用[!DNL Schema Registry] API进行的所有可能调用的深入示例。

### 数据集“架构”属性（已弃用 — EOL 2019-05-30）

数据集可能包含一个“架构”属性，该属性现已弃用，暂时可用于向后兼容。 例如，与之前类似的列表(GET)请求（其中`properties`查询参数中的“schema”被替换为“schemaRef”）可能会返回以下内容：

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

如果填充了数据集的“schema”属性，则表示该架构是已弃用的`/xdms`架构，如果支持，则ETL连接器应使用“schema”属性中的值以及`/xdms`端点（[[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)中已弃用的端点）来检索旧架构。

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
>可选的查询参数`expansion=xdm`告知API完全展开并内联任何引用的架构。 在向用户展示所有潜在字段的列表时，您可能希望这样做。

**响应**

与[查看数据集架构](#view-dataset-schema)的步骤类似，响应包含一个JSON架构，该架构描述序列化为JSON的数据的结构和字段级信息。

>[!NOTE]
>
>当“架构”字段为空或完全缺失时，连接器应读取“schemaRef”字段并使用[架构注册表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)，如用于[查看数据集架构](#view-dataset-schema)的先前步骤中所示。

### “observableSchema”属性

数据集的“observableSchema”属性具有与XDM架构JSON匹配的JSON结构。 “observableSchema”包含传入输入文件中存在的字段。 将数据写入[!DNL Experience Platform]时，用户不需要使用目标架构中的每个字段。 相反，他们应该只提供正在使用的字段。

可观察架构是读取数据或显示可从中读取/映射的字段列表时将使用的架构。

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

ETL应用程序可以提供预览数据的功能（[“图8”，在ETL工作流](./workflow.md)中）。 数据访问API提供了多个用于预览数据的选项。

其他信息，包括使用数据访问API预览数据的分步指南，可在[数据访问教程](../data-access/tutorials/dataset-data.md)中找到。

### 使用“属性”查询参数获取数据集详细信息

如上面的步骤中所示，在[查看数据集列表](#view-list-of-datasets)时，您可以使用“properties”查询参数请求“files”。

有关查询数据集和可用响应筛选器的详细信息，请参阅[目录服务概述](../catalog/home.md)。

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

响应将包含一个显示“文件”属性的数据集(`limit=1`)。

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSetFiles?dataSetId=5bf479a6a8c862000050e3c7"
  }
}
```

### 使用“文件”属性列出数据集文件

您还可以使用GET请求通过“文件”属性获取文件详细信息。

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

响应包括作为顶级属性的数据集文件ID，以及包含在数据集文件ID对象中的文件详细信息。

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

在上一个响应中返回的数据集文件ID可用于GET请求，以通过[!DNL Data Access] API获取更多文件详细信息。

[数据访问概述](../data-access/home.md)包含有关如何使用[!DNL Data Access] API的详细信息。

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

“href”属性可用于通过[[!DNL Data Access API]](../data-access/home.md)获取预览数据。

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

有关[!DNL Data Access] API的详细信息（包括详细的请求和响应）可在[数据访问概述](../data-access/home.md)中获取。

### 从数据集获取“fileDescription”

作为转换后数据的输出的目标组件，数据工程师将选择一个输出数据集([&quot;图12&quot; （在ETL工作流](workflow.md)中）。 XDM架构与输出数据集关联。 要写入的数据将由数据发现API中数据集实体的“fileDescription”属性标识。 可以使用数据集ID (`{DATASET_ID}`)获取此信息。 JSON响应中的“fileDescription”属性将提供所请求的信息。

**API格式**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{DATASET_ID}` | 尝试访问的数据集的`id`值。 |

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

将使用[批次摄取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)将数据写入[!DNL Experience Platform]。  数据写入是一个异步过程。 当数据写入Adobe Experience Platform时，将创建一个批次，并且仅在完全写入数据后标记为成功。

[!DNL Experience Platform]中的数据应以Parquet文件的形式写入。

## 执行阶段

在执行开始时，连接器（如源组件中所定义）将使用[[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/)从[!DNL Experience Platform]中读取数据。 转换过程将读取特定时间范围内的数据。 在内部，它将查询批量源数据集。 在查询时，它会使用参数化（滚动时序数据，或增量数据）的开始日期，列出这些批次的数据集文件，并开始请求这些数据集文件的数据。

### 转换示例

[示例ETL转换](./transformations.md)文档包含许多示例转换，包括身份处理和数据类型映射。 请参考这些转换。

### 从[!DNL Experience Platform]读取数据

使用[[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)，您可以获取指定开始时间和结束时间之间的所有批次，并按照其创建顺序对它们进行排序。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

可在[数据访问教程](../data-access/tutorials/dataset-data.md)中找到有关筛选批次的详细信息。

### 从批处理中获取文件

一旦您找到要查找的批次的ID (`{BATCH_ID}`)，就可以通过[[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/)检索属于特定批次的文件列表。  有关此操作的详细信息，请参阅[[!DNL Data Access] 教程](../data-access/tutorials/dataset-data.md)。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### 使用文件ID访问文件

使用文件(`{FILE_ID`)的唯一ID，[[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/)可用于访问文件的特定详细信息，包括其名称、大小（字节）以及下载文件的链接。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

响应可能指向单个文件或目录。 在[[!DNL Data Access] 教程](../data-access/tutorials/dataset-data.md)中可找到有关每个教程的详细信息。

### 访问文件内容

[[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/)可用于访问特定文件的内容。 为了获取内容，在使用文件ID访问文件时，会使用为`_links.self.href`返回的值发出GET请求。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

对此请求的响应包含文件的内容。 有关详细信息（包括有关响应分页的详细信息），请参阅[如何通过数据访问API查询数据](../data-access/tutorials/dataset-data.md)教程。

### 验证记录是否符合架构要求

在写入数据时，用户可以根据XDM架构中定义的验证规则选择验证数据。 有关架构验证的更多信息，请参阅 [!DNL GitHub][&#128279;](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation)上的ETL生态系统集成参考代码。

如果您使用在[[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md)上找到的引用实现，则可以使用系统属性`-DenableSchemaValidation=true`在此实现中启用架构验证。

可以对逻辑XDM类型执行验证，对字符串使用`minLength`和`maxlength`等属性，对整数使用`minimum`和`maximum`等属性。 [架构注册API开发人员指南](../xdm/api/getting-started.md)包含一个表，其中概述了XDM类型以及可用于验证的属性。

>[!NOTE]
>
>为各种`integer`类型提供的最小值和最大值是该类型可以支持的MIN和MAX值，但这些值可以进一步限制为您选择的最小值和最大值。

### 创建批次

处理数据后，ETL工具将使用[批处理摄取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)将数据写回[!DNL Experience Platform]。 将数据添加到数据集之前，必须将其链接到稍后将上传到特定数据集的批次。

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

可在[批次摄取概述](../ingestion/batch-ingestion/overview.md)中找到有关创建批次的详细信息，包括示例请求和响应。

### 写入数据集

成功创建新批次后，可将文件上传到特定数据集。 可以在批次中发布多个文件，直到提升为止。 可使用小文件上传API上传文件；但是，如果文件过大，并且超过了网关限制，则可使用大文件上传API。 有关同时使用大文件上传和小文件上传的详细信息，请参阅[批次摄取概述](../ingestion/batch-ingestion/overview.md)。

**请求**

[!DNL Experience Platform]中的数据应以Parquet文件的形式写入。

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

将所有文件都上载到批处理之后，可以向批处理发出完成信号。 这样，将为已完成的文件创建[!DNL Catalog]个“DataSetFile”条目，并将其与生成批次关联。 然后，[!DNL Catalog]批次被标记为成功，这会触发下游流摄取可用数据。

数据将首先在Adobe Experience Platform上的暂存位置着陆，然后在编目和验证后移至最终位置。 将所有数据移动到永久位置后，批次将标记为成功。

**请求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

如果成功，响应将返回HTTP状态200 OK ，并且响应正文为空。

ETL工具将确保在读取数据时记下源数据集的时间戳。

在下一次执行转换时，可能通过调度或事件调用，ETL将开始从先前保存的时间戳以及之后的所有数据请求数据。

### 获取上一批次状态

在ETL工具中运行新任务之前，必须确保上一个批次已成功完成。 [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/)提供了一个特定于批次的选项，该选项提供了相关批次的详细信息。

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

通过使用`{BATCH_ID}`发出GET请求，可以通过[[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/)检索单个批次状态。 使用的`{BATCH_ID}`将与创建批次时返回的ID相同。

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

如果失败，则可以从响应中提取“错误”，并将其作为错误消息显示在ETL工具上。

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

| 增量事件 | 增量用户档案 |
|-------------------------------|----------------------|
| 快照事件（不太可能） | 快照配置文件 |

事件数据通常是在每行中存在索引时间戳列时生成的。

通常情况下，当数据中没有时间戳并且每行都可以通过主/复合键进行标识时，会生成配置文件数据。

增量数据是指只有新数据/更新数据进入系统并附加到数据集中当前数据的位置。

快照数据是指所有数据进入系统并替换数据集中某些或所有以前的数据的情况。

在增量事件的情况下，ETL工具应使用批次实体的可用日期/创建日期。 在推送服务的情况下，可用日期将不存在，因此工具将使用批次创建/更新日期来标记增量。 每批增量事件都需要进行处理。

对于增量用户档案，ETL工具将使用批次实体的创建/更新日期。 通常需要处理每批增量配置文件数据。

由于数据的绝对大小，快照事件的可能性非常小。 但是，如果要求这样做，则ETL工具必须仅选取最后一批进行处理。

使用快照配置文件时，ETL工具必须选取到达系统的最后一批数据。 但是，如果要跟踪更改的版本，则需要处理所有批次。 ETL流程中的重复数据消除处理将有助于控制存储成本。

## 批量重放和数据重新处理

如果客户端发现过去“n”天内ETL处理的数据未按预期发生或源数据本身可能不正确，则可能需要批量重放和数据重新处理。

为此，客户端的数据管理员将使用[!DNL Experience Platform] UI删除包含损坏数据的批次。 然后，可能需要重新运行ETL，从而使用正确的数据重新填充。 如果源本身具有损坏的数据，则数据工程师/管理员需要更正源批次并重新摄取数据(通过Adobe Experience Platform或ETL连接器摄取)。

根据生成的数据类型，数据工程师可以选择从特定数据集中删除单个批次或所有批次。 将根据[!DNL Experience Platform]准则删除/存档数据。

很可能，清除数据的ETL功能会很重要。

清除完成后，客户端管理员必须重新配置Adobe Experience Platform，从删除批次时起重新开始处理核心服务。

## 并发批处理

根据客户的决定，数据管理员/工程师可以决定以顺序方式或并发方式提取、转换和加载数据，具体取决于特定数据集的特征。 这还将基于客户端使用转换后的数据定位的用例。

例如，如果客户端持久保留在可更新的持久性存储中，并且事件的顺序或顺序很重要，则客户端可能需要严格处理具有顺序ETL转换的作业。

在其他情况下，使用指定的时间戳在内部排序的下游应用程序/进程可以处理乱序数据。 在这些情况下，并行ETL转换可以改善处理时间。

对于源批次，它再次取决于客户端首选项和使用者限制。 如果源数据可以并行提取，而不考虑行的区域/顺序，则转换过程可以创建具有较高并行度的处理批次（基于乱序处理的优化）。 但是，如果转换必须遵循时间戳或更改优先顺序，则数据访问API或ETL工具调度程序/调用必须尽可能确保批处理不会乱序处理。

## 延期

延迟是一个过程，在该过程中，输入数据还不够完整，无法发送到下游进程，但将来可能可以使用。 客户将确定他们个人对未来匹配的数据窗口化容忍度与处理成本的容忍度，以告知他们决定保留数据并在下次转换执行中重新处理它，希望可以在保留窗口内的某个未来时间扩充和协调/拼合数据。 此周期将持续进行，直到行得到充分处理，或认为该行太旧，无法继续投资。 每次迭代都会生成延迟数据，该延迟数据是先前迭代中所有延迟数据的超集。

Adobe Experience Platform当前未识别延迟数据，因此客户端实施必须依赖ETL和数据集手动配置，在[!DNL Experience Platform]中镜像可用于保留延迟数据的源数据集创建另一个数据集。 在这种情况下，延迟数据将与快照数据类似。 在每次执行ETL转换时，源数据将与延迟数据合并并发送以供处理。

## Changelog

| 日期 | 操作 | 描述 |
| ---- | ------ | ----------- |
| 2019-01-19 | 从数据集中删除了“fields”属性 | 数据集以前包含一个“字段”属性，该属性包含架构副本。 此功能不应再使用。 如果找到“fields”属性，则应忽略该属性，并改用“observedSchema”或“schemaRef”。 |
| 2019-03-15 | 已将“schemaRef”属性添加到数据集 | 数据集的“schemaRef”属性包含引用数据集所基于的XDM架构的URI，并代表数据集可以使用的所有潜在字段。 |
| 2019-03-15 | 所有最终用户标识符都映射到“identityMap”属性 | “identityMap”是主体所有唯一标识符（如CRMID、ECID或忠诚度计划ID）的封装。 [[!DNL Identity Service]](../identity-service/home.md)使用此映射解析主体的所有已知和匿名身份，为每个最终用户形成一个身份图。 |
| 2019-05-30 | 生命周期结束并删除数据集中的“架构”属性 | 数据集“架构”属性提供了对架构的引用链接，该链接使用[!DNL Catalog] API中已弃用的`/xdms`端点。 该架构已被提供新[!DNL Schema Registry] API中引用的架构的“id”、“version”和“contentType”的“schemaRef”所取代。 |

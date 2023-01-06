---
keywords: Experience Platform；主页；热门主题；ETL;etl;etl集成；ETL集成
solution: Experience Platform
title: 为Adobe Experience Platform开发ETL集成
description: ETL集成指南概述了创建高性能、安全的连接器以Experience Platform数据并将数据引入平台的一般步骤。
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '4075'
ht-degree: 1%

---

# 为Adobe Experience Platform开发ETL集成

ETL集成指南概述了为创建高性能、安全的连接器而需执行的一般步骤 [!DNL Experience Platform] 并将数据摄取到 [!DNL Platform].


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Data Ingestion]](https://www.adobe.io/experience-platform-apis/references/data-ingestion/)
- [Experience PlatformAPI的身份验证和授权](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

本指南还包括在设计ETL连接器时要使用的示例API调用，其中包含指向文档的链接，其中概述了每个文档 [!DNL Experience Platform] ，以及其API的使用。

集成示例位于 [!DNL GitHub] 通过 [ETL生态系统集成参考代码](https://github.com/adobe/acp-data-services-etl-reference) 下 [!DNL Apache] 许可证版本2.0。

## 工作流

以下工作流程图为Adobe Experience Platform组件与ETL应用程序和连接器的集成提供了高级概述。

![](images/etl.png)

## Adobe Experience Platform组件

ETL连接器集成涉及多个Experience Platform组件。 以下列表概述了几个关键组件和功能：

- **AdobeIdentity Management系统(IMS)**  — 为Adobe服务提供身份验证框架。
- **IMS组织**  — 拥有或许可产品和服务并允许其成员访问的公司实体。
- **IMS用户** - IMS组织的成员。 组织与用户的关系是多对多的关系。
- **[!DNL Sandbox]**  — 一个虚拟分区 [!DNL Platform] 实例，以帮助开发和改进数字体验应用程序。
- **数据发现**  — 将摄取和转换数据的元数据记录在 [!DNL Experience Platform].
- **[!DNL Data Access]**  — 为用户提供一个界面，以访问 [!DNL Experience Platform].
- **[!DNL Data Ingestion]**  — 将数据推送到 [!DNL Experience Platform] with [!DNL Data Ingestion] API。
- **[!DNL Schema Registry]**  — 定义并存储描述要在 [!DNL Experience Platform].

## 入门 [!DNL Experience Platform] API

以下各节提供了为成功调用而需要了解或掌握的其他信息 [!DNL Experience Platform] API。

### 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关 [!DNL Platform]，请参阅 [沙盒概述文档](../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

- Content-Type:application/json

## 一般用户流量

首先，ETL用户登录到 [!DNL Experience Platform] 用户界面(UI)，并使用标准连接器或推送服务连接器创建用于摄取的数据集。

在UI中，用户通过选择数据集架构来创建输出数据集。 架构的选择取决于被摄取到的数据类型（记录或时间系列） [!DNL Platform]. 通过单击UI中的架构选项卡，用户将能够查看所有可用的架构，包括架构支持的行为类型。

在ETL工具中，用户将在配置相应的连接（使用其凭据）后开始设计其映射转换。 假定ETL工具已具有 [!DNL Experience Platform] 已安装连接器（此集成指南中未定义的进程）。

中提供了ETL工具和工作流示例的模型 [ETL工作流程](./workflow.md). 虽然ETL工具的格式可能有所不同，但大多数工具都会提供类似的功能。

>[!NOTE]
>
>ETL连接器必须指定一个时间戳过滤器来标记要摄取数据和偏移的日期（即要读取数据的窗口）。 ETL工具应支持在此UI或其他相关UI中获取这两个参数。 在Adobe Experience Platform中，这些参数将映射到数据集批处理对象中存在的可用日期（如果存在）或捕获日期。

### 查看数据集列表

使用数据源进行映射，可以使用 [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

您可以发出单个API请求以查看所有可用数据集(例如， `GET /dataSets`)，最佳实践是包含可限制响应大小的查询参数。

在请求完整数据集信息时，响应有效负载的大小可能超过3GB，这可能会降低整体性能。 因此，使用查询参数仅过滤所需信息将会做出 [!DNL Catalog] 查询更高效。

#### 列表筛选

在过滤响应时，您可以在单个调用中使用多个过滤器，方法是使用与号(`&`)。 某些查询参数接受以逗号分隔的值列表，例如以下示例请求中的“properties”过滤器。

[!DNL Catalog] 响应将根据配置的限制自动进行计量，但“limit”查询参数可用于自定义约束并限制返回的对象数量。 预配置 [!DNL Catalog] 响应限制为：

- 如果未指定限制参数，则每个响应有效负载的最大对象数为20。
- 所有其他 [!DNL Catalog] 查询是100个对象。
- 对于数据集查询，如果使用属性查询参数请求可观察模式，则返回的最大数据集数为20。
- 限制参数无效(包括 `limit=0`)会遇到HTTP 400错误，该错误会列出正确的范围。
- 如果限制或偏移作为查询参数进行传递，则优先于作为标题传递的限制或偏移。

有关查询参数的详细信息，请参阅 [目录服务概述](../catalog/home.md).

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

请参阅 [目录服务概述](../catalog/home.md) 以详细了解如何调用 [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

**响应**

响应包括三个(`limit=3`)数据集，其中显示了 `properties` 查询参数。

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

数据集的“schemaRef”属性包含引用数据集所基于的XDM架构的URI。 XDM架构(“schemaRef”)表示数据集可以使用的所有潜在字段，而不一定是正在使用的字段（请参阅下面的“overbaidSchema”）。

XDM架构是您在需要向用户显示所有可写入的可用字段的列表时所使用的架构。

上一个响应对象(`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`)是指向 [!DNL Schema Registry]. 可通过对 [!DNL Schema Registry] API。

>[!NOTE]
>
>“schemaRef”属性取代了现已弃用的“schema”属性。 如果数据集中缺少“schemaRef”或不包含值，则需要检查是否存在“schema”属性。 可通过在 `properties` 查询参数。 有关“schema”属性的更多详细信息，请参阅 [数据集“架构”属性](#dataset-schema-property-deprecated---eol-2019-05-30) 部分。

**API格式**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**请求**

请求使用经过编码的URL `id` 架构的URI（“schemaRef.id”属性的值），需要Accept标头。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

响应格式取决于请求中发送的Accept标头类型。 查找请求还需要 `version` 包含在接受标头中。 下表概述了可用于查找的Accept标头：

| Accept | 描述 |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | 列表(GET)请求、标题、ID和版本 |
| `application/vnd.adobe.xed-full+json; version={major version}` | $ref和allOf已解析，有标题和描述 |
| `application/vnd.adobe.xed+json; version={major version}` | 带有$ref和allOf的Raw，具有标题和描述 |
| `application/vnd.adobe.xed-notext+json; version={major version}` | 带有$ref和allOf的原始，无标题或描述 |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $ref和allOf已解析，无标题或描述 |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs和allOf已解析，包含描述符 |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` 和 `application/vnd.adobe.xed-full+json; version={major version}` 是最常用的接受标头。 `application/vnd.adobe.xed-id+json` 首选在 [!DNL Schema Registry] 因为它只返回“title”、“id”和“version”。 `application/vnd.adobe.xed-full+json; version={major version}` 查看特定资源（按其“id”）时，首选使用，因为它会返回所有字段（嵌套在“properties”下）以及标题和描述。

**响应**

返回的JSON架构描述了结构和字段级信息（“type”、“format”、“minimum”、“maximum”等） ，序列化为JSON。 如果使用JSON以外的序列化格式进行摄取（例如，Parquet或Scala），则 [架构注册指南](../xdm/tutorials/create-schema-api.md) 包含一个表，其中显示了所需的JSON类型(&quot;meta:xdmType&quot;)及其其他格式的相应表示形式。

除了这张桌子， [!DNL Schema Registry] 开发人员指南包含所有可能使用 [!DNL Schema Registry] API。

### 数据集“架构”属性(已弃用 — EOL 2019-05-30)

数据集可能包含“架构”属性，该属性现已弃用，但暂时仍可用于向后兼容性。 例如，列表(GET)请求与先前发出的请求类似，其中“schema”在 `properties` 查询参数，可能会返回以下内容：

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

如果填充了数据集的“schema”属性，则表示该架构已弃用 `/xdms` 架构中，如果支持，则ETL连接器应将“schema”属性中的值与 `/xdms` 端点( [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/))以检索旧版架构。

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
>可选查询参数， `expansion=xdm`，告知API完全展开任何引用的架构并将其串联起来。 当向用户显示所有潜在字段的列表时，您可能希望执行此操作。

**响应**

与 [查看数据集架构](#view-dataset-schema)，则响应包含一个JSON架构，该架构描述数据的结构和字段级别信息，并序列化为JSON。

>[!NOTE]
>
>当“schema”字段为空或完全不存在时，连接器应读取“schemaRef”字段并使用 [架构注册表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/) 如 [查看数据集架构](#view-dataset-schema).

### “ovearableSchema”属性

数据集的“ovebaibleSchema”属性的JSON结构与XDM架构JSON的JSON结构相匹配。 “ovearableSchema”包含传入输入文件中存在的字段。 将数据写入时 [!DNL Experience Platform]，则用户无需使用目标架构中的每个字段。 相反，它们应仅提供正在使用的字段。

可观察的架构是您在读取数据或显示可从中读取/映射的字段列表时使用的架构。

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

ETL应用可提供预览数据([ETL工作流中的“图8”](./workflow.md))。 数据访问API提供了多个用于预览数据的选项。

其他信息（包括使用数据访问API预览数据的分步指南）可在 [数据访问教程](../data-access/tutorials/dataset-data.md).

### 使用“properties”查询参数获取数据集详细信息

如上面的步骤所示， [查看数据集列表](#view-list-of-datasets)，则可以使用“properties”查询参数请求“文件”。

您可以将 [目录服务概述](../catalog/home.md) 有关查询数据集和可用响应过滤器的详细信息。

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

### 使用“files”属性列出数据集文件

您还可以使用GET请求来使用“files”属性获取文件详细信息。

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

响应包含数据集文件ID作为顶级属性，其中文件详细信息包含在数据集文件ID对象中。

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

在上一个响应中返回的GET集文件ID可用于数据请求，以通过 [!DNL Data Access] API。

的 [数据访问概述](../data-access/home.md) 包含有关如何使用的详细信息 [!DNL Data Access] API。

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

有关 [!DNL Data Access] API（包括详细的请求和响应）可在 [数据访问概述](../data-access/home.md).

### 从数据集获取“fileDescription”

作为转换数据输出的目标组件，数据工程师将选择一个输出数据集([ETL工作流中的“图12”](workflow.md))。 XDM架构与输出数据集关联。 要写入的数据将由Data Discovery API中数据集实体的“fileDescription”属性标识。 可以使用数据集ID(`{DATASET_ID}`)。 JSON响应中的“fileDescription”属性将提供所请求的信息。

**API格式**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{DATASET_ID}` | 的 `id` 您尝试访问的数据集的值。 |

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

数据将写入 [!DNL Experience Platform] 使用 [数据摄取API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/).  数据写入是一个异步过程。 将数据写入Adobe Experience Platform时，只有在数据完全写入后，才会创建批处理并将其标记为成功。

数据输入 [!DNL Experience Platform] 应以Parquet文件的形式写入。

## 执行阶段

执行开始时，连接器（如源组件中定义）将从中读取数据 [!DNL Experience Platform] 使用 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/). 转换过程将读取某个时间范围内的数据。 在内部，它将查询批量源数据集。 在查询时，它将使用参数化（对时间系列数据或增量数据进行滚动）的开始日期和列出这些批次的数据集文件，并开始对这些数据集文件发出数据请求。

### 示例转换

的 [ETL转换示例](./transformations.md) 文档包含许多示例转换，包括身份处理和数据类型映射。 请使用这些转换作参考。

### 从读取数据 [!DNL Experience Platform]

使用 [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)，则可以获取指定开始时间和结束时间之间的所有批次，并按创建顺序对它们进行排序。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

有关过滤批的详细信息，请参阅 [数据访问教程](../data-access/tutorials/dataset-data.md).

### 从批中获取文件

获得要查找的批次的ID后(`{BATCH_ID}`)，则可以通过 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/).  有关执行此操作的详细信息，请参阅 [[!DNL Data Access] 教程](../data-access/tutorials/dataset-data.md).

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### 使用文件ID访问文件

使用文件的唯一ID(`{FILE_ID`)、 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 可用于访问文件的特定详细信息，包括其名称、大小（以字节为单位）以及用于下载该文件的链接。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

响应可以指向单个文件或目录。 有关每个报表包的详细信息，请参阅 [[!DNL Data Access] 教程](../data-access/tutorials/dataset-data.md).

### 访问文件内容

的 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 可用于访问特定文件的内容。 要获取内容，会使用为 `_links.self.href` 使用文件ID访问文件时。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

对此请求的响应包含文件的内容。 有关更多信息（包括有关响应分页的详细信息），请参阅 [如何通过数据访问API查询数据](../data-access/tutorials/dataset-data.md) 教程。

### 验证架构合规性记录

写入数据时，用户可以根据XDM架构中定义的验证规则选择验证数据。 有关架构验证的更多信息，请参阅 [ETL生态系统集成参考代码 [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

如果您使用的是 [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md)，您可以在此实施中使用系统属性打开模式验证 `-DenableSchemaValidation=true`.

可以使用属性(如 `minLength` 和 `maxlength` 对于字符串， `minimum` 和 `maximum` 对于整数等。 的 [架构注册API开发人员指南](../xdm/api/getting-started.md) 包含一个表，其中概述了XDM类型和可用于验证的属性。

>[!NOTE]
>
>为各种 `integer` 类型是类型可支持的MIN和MAX值，但这些值可进一步限制为您选择的最小值和最大值。

### 创建批处理

一旦处理了数据，ETL工具会将数据写回 [!DNL Experience Platform] 使用 [批量摄取API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). 在将数据添加到数据集之前，必须先将其链接到批次，该批次稍后会上传到特定数据集。

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

成功创建新批量后，可以将文件上传到特定数据集。 多个文件可以批量发布，直到提升为止。 可使用小文件上传API上传文件；但是，如果文件过大，并且超出了网关限制，则可以使用大文件上传API。 有关同时使用大文件和小文件上传的详细信息，请参阅 [批量摄取概述](../ingestion/batch-ingestion/overview.md).

**请求**

数据输入 [!DNL Experience Platform] 应以Parquet文件的形式写入。

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{ORG_ID}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### 标记批量上传完成

将所有文件上传到批处理后，可以发出批处理完成的信号。 通过执行此操作， [!DNL Catalog] 为已完成的文件创建“DataSetFile”条目，并与生成批处理关联。 的 [!DNL Catalog] 然后，批次会标记为成功，这会触发下游流以摄取可用数据。

数据将首先登陆Adobe Experience Platform的暂存位置，然后在编目和验证后移至最终位置。 将所有数据移动到永久位置后，批次将标记为成功。

**请求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

如果响应成功，则将返回HTTP状态200 OK，并且响应正文将为空。

ETL工具将确保在读取数据时记录源数据集的时间戳。

在下次执行转换时，ETL将开始从之前保存的时间戳和以后的所有数据中请求数据，这可能是通过计划或事件调用来完成的。

### 获取上次批处理状态

在ETL工具中运行新任务之前，必须确保成功完成最后一批任务。 的 [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) 提供特定于批的选项，其中提供了相关批的详细信息。

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

如果上一批“状态”值为“成功”，则可以计划新任务，如下所示：

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

### 按ID获取上次批处理状态

单个批状态可以通过 [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) 通过使用 `{BATCH_ID}`. 的 `{BATCH_ID}` 使用与创建批处理时返回的ID相同。

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

以下响应显示“成功”：

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

如果失败，可以从响应中提取“错误”，并在ETL工具上作为错误消息显示。

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

## 增量数据、快照数据、事件和配置文件

数据可以由两个矩阵表示，如下所示：

| 增量事件 | 增量配置文件 |
|-------------------------------|----------------------|
| 快照事件（不太可能） | 快照配置文件 |

当每行都有索引时间戳列时，通常会使用事件数据。

当数据中没有时间戳，并且每行都可以由主/复合键标识时，通常会使用用户档案数据。

增量数据是指仅新/更新的数据进入系统并附加到数据集中的当前数据的位置。

快照数据是指所有数据进入系统并替换数据集中的部分或全部以前数据时。

对于增量事件，ETL工具应使用批处理实体的可用日期/创建日期。 对于推送服务，可用日期将不存在，因此该工具将使用批量创建/更新日期进行标记增量。 需要处理每批增量事件。

对于增量配置文件，ETL工具将使用批处理实体的创建/更新日期。 通常，需要处理每批增量配置文件数据。

由于数据的大小，快照事件发生的可能性很小。 但是，如果需要这样做，则ETL工具必须只选取最后一个批进行处理。

使用快照配置文件时，ETL工具必须选取到达系统的最后一批数据。 但是，如果要求跟踪更改的版本，则需要处理所有批次。 在ETL过程中进行重复数据消除处理将有助于控制存储成本。

## 批量重播和数据重新处理

如果客户发现过去“n”天内，正在进行ETL处理的数据未按预期发生，或源数据本身可能不正确，则可能需要批量重播和数据重新处理。

为此，客户端的数据管理员将使用 [!DNL Platform] 用于删除包含损坏数据的批次的UI。 然后，可能需要重新运行ETL，从而使用正确的数据重新填充。 如果源本身存在损坏的数据，则数据工程师/管理员将需要更正源批次并重新摄取数据(通过Adobe Experience Platform或ETL连接器)。

根据所生成的数据类型，数据工程师可以选择从某些数据集中删除单个批次或所有批次。 数据将根据 [!DNL Experience Platform] 准则。

很可能的情况是，清除数据的ETL功能将非常重要。

清除完成后，客户端管理员将必须重新配置Adobe Experience Platform，以便从删除批次时起重新开始处理核心服务。

## 并发批处理

根据客户的决定，数据管理员/工程师可以根据特定数据集的特性决定以顺序或并发方式提取、转换和加载数据。 这还将基于客户使用转换后的数据定向的用例。

例如，如果客户端保留到可更新的持久性存储，并且事件的顺序或顺序很重要，则客户端可能需要严格处理具有连续ETL转换的作业。

在其他情况下，下游应用程序/进程可以使用指定的时间戳进行内部排序，从而可以处理顺序错误的数据。 在这些情况下，并行ETL转换可以缩短处理时间。

对于源批次，它将再次依赖于客户端首选项和用户约束。 如果源数据可以并行提取而不考虑行的摄政/排序，则转换过程可以创建具有更高并行度的处理批次（基于无序处理的优化）。 但是，如果转换必须遵循时间戳或更改优先顺序，则数据访问API或ETL工具调度程序/调用必须确保批次的处理不会出现异常。

## 递延

延迟是指输入数据尚未足够完整地发送到下游进程，但将来可能可用的流程。 客户将确定他们针对数据窗口的容差与处理成本，以告知他们决定在下次转换执行中保留数据并重新处理数据，希望在保留窗口内的将来某个时间对其进行扩充和协调/拼合。 此周期一直持续，直到行得到充分处理或认为过于陈旧，无法继续投资。 每个迭代都将生成延迟数据，该数据是先前迭代中所有延迟数据的超集。

Adobe Experience Platform当前不识别延迟数据，因此客户端实施必须依赖ETL和数据集手动配置在中创建另一个数据集 [!DNL Platform] 镜像可用于保留延迟数据的源数据集。 在这种情况下，延期数据将与快照数据类似。 在每次执行ETL转换时，源数据都将与延迟数据合并，并发送以进行处理。

## Changelog

| 日期 | 操作 | 描述 |
| ---- | ------ | ----------- |
| 2019-01-19 | 从数据集中删除了“fields”属性 | 数据集之前包含“字段”属性，该属性包含架构的副本。 不应再使用此功能。 如果找到“fields”属性，则应忽略该属性，并改用“observedSchema”或“schemaRef”。 |
| 2019-03-15 | 向数据集添加了“schemaRef”属性 | 数据集的“schemaRef”属性包含一个URI，该URI引用数据集所基于的XDM架构，并表示数据集可以使用的所有潜在字段。 |
| 2019-03-15 | 所有最终用户标识符都映射到“identityMap”属性 | “identityMap”是对主体所有唯一标识符（如CRM ID、ECID或忠诚度计划ID）的封装。 此地图由 [[!DNL Identity Service]](../identity-service/home.md) 要解析主题的所有已知身份和匿名身份，请为每个最终用户形成单个身份图。 |
| 2019-05-30 | EOL和从数据集中删除“架构”属性 | 数据集“schema”属性提供了指向使用已弃用架构的引用链接 `/xdms` 的端点 [!DNL Catalog] API。 此名称已被“schemaRef”替换，该“schemaRef”提供了新架构中引用的架构的“id”、“version”和“contentType” [!DNL Schema Registry] API。 |

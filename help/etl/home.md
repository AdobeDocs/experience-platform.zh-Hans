---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 创建ETL集成
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# 为Adobe Experience Platform开发ETL集成

ETL集成指南概述了为Experience Platform创建高性能、安全连接器以及将数据引入Platform的一般步骤。


- [Catalog](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)
- [数据访问](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)
- [数据摄取](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [身份验证和授权API](../tutorials/authentication.md)
- [模式注册](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)

本指南还包括设计ETL连接器时使用的示例API调用，其中包含描述每个Experience Platform服务的文档的链接，以及API的使用，这些链接更加详细。

GitHub上提供了一个示例集成，可通过Apache License Version 2.0下的 [ETL Esystem Integration Reference Code](https://github.com/adobe/acp-data-services-etl-reference) （ETL生态系统集成参考代码）获取该集成。

## 工作流

以下工作流程图提供了Adobe Experience Platform组件与ETL应用程序和连接器集成的高级概述。

![](images/etl.png)

## Adobe Experience Platform组件

ETL连接器集成涉及多个Experience Platform组件。 以下列表概述了几个关键组件和功能：

- **Adobe Identity Management System(IMS)** -为Adobe服务提供身份验证框架。
- **IMS组织** -拥有或许可产品和服务并允许访问其成员的公司实体。
- **IMS用户** - IMS组织的成员。 “组织与用户”的关系是多对多的。
- **沙箱** -单个平台实例的虚拟分区，可帮助开发和发展数字体验应用程序。
- **数据发现** -在Experience Platform中记录摄取和转换的数据的元数据。
- **数据访问** -为用户提供在Experience Platform中访问其数据的界面。
- **数据摄取** -使用数据摄取API将数据推送到Experience Platform。
- **模式注册** -定义和存储描述要在Experience Platform中使用的数据结构的模式。

## Experience Platform API入门

以下各节提供了成功调用Experience Platform API所需了解或现有的其他信息。

### 读取示例API调用

本指南提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权：承载人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

- 内容类型：application/json

## 一般用户流

首先，ETL用户登录到Experience Platform用户界面(UI)，并使用标准连接器或推送服务连接器创建数据集以用于获取。

在UI中，用户通过选择数据集模式来创建输出数据集。 模式的选择取决于被引入平台中的数据类型（记录或时间序列）。 通过单击UI中的模式选项卡，用户将能够视图所有可用的模式，包括模式支持的行为类型。

在ETL工具中，用户将在配置相应的连接（使用其凭据）后开始设计其映射转换。 假定ETL工具已安装Experience Platform连接器（此集成指南中未定义流程）。

ETL工作流中已提供示例ETL工具和工作流的 [模型](./workflow.md)。 虽然ETL工具的格式可能不同，但大多数工具都提供类似的功能。

>[!NOTE] ETL连接器必须指定一个时间戳过滤器，用于标记要摄取数据和偏移的日期（即要读取数据的窗口）。 ETL工具应支持在此或其他相关UI中使用这两个参数。 在Adobe Experience Platform中，这些参数将映射到数据集的批处理对象中存在的可用日期（如果存在）或捕获的日期。

### 视图数据集列表

使用数据源进行映射，可以使用Catalog API获取所有可用数据集的 [列表](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)。

您可以发出单个API请求以视图所有可用数据集(例如，), `GET /dataSets`最佳实践是包含限制响应大小的查询参数。

在请求完 _整数据集信息_ 时，响应有效负荷可能超过3GB，这会降低总体性能。 因此，使用查询参数仅筛选所需信息将使目录查询更加高效。

#### 列表过滤

在筛选响应时，您可以通过用“和号”(`&`)分隔参数，在单个调用中使用多个过滤器。 某些查询参数接受以逗号分隔的列表值，如以下示例请求中的“属性”过滤器。

目录响应会根据配置的限制自动按量收费，但“limit”查询参数可用于自定义约束并限制返回的对象数。 预配置的目录响应限制包括：

- 如果未指定限制参数，则每个响应有效负荷的最大对象数为20。
- 所有其他目录查询的全局限制为100个对象。
- 对于数据集查询，如果使用属性查询参数请求veoctableSchema，则返回的最大数据集数为20。
- 无效的限制参数( `limit=0`包括)会遇到HTTP 400错误，该错误勾勒了正确的范围。
- 如果限制或偏移作为查询参数传递，则其优先于作为标题传递的限制或偏移。

查询参数在目录服务概述中有更 [多详细介绍](../catalog/home.md)。

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
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

有关如何调 [用目录API的详细示例](../catalog/home.md) ，请参阅目录服 [务概述](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)。

**响应**

响应包括三个(`limit=3`)数据集，它们显示由查询参数指示的“name”、“description”和“schemaRef” `properties` 。

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

### 视图数据集模式

数据集的“schemaRef”属性包含引用数据集所基于的XDM模式的URI。 XDM模式(“schemaRef”)表示数据集可使用的所有潜在字段，而不一定是正在使 _用的字段___ （请参阅下面的“veoctableSchema”）。

XDM模式是您在需要向用户展示可写入的所有可用字段的列表时使用的模式。

上一个响应对象(`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`)中的第一个“schemaRef.id”值是指向模式注册表中特定XDM模式的URI。 可以通过对模式注册表API发出查找(GET)请求来检索模式。

>[!NOTE] “schemaRef”属性替换了现已弃用的“模式”属性。 如果数据集中缺少“schemaRef”或不包含值，则需要检查是否存在“模式”属性。 这可以通过将上一个调用的模式参数中的“schemaRef”替换 `properties` 为“查询”来完成。 有关“模式”属性的更多详细信息，请参阅随 [后的数据集“模式](#dataset-schema-property-deprecated---eol-2019-05-30) ”属性部分。

**API格式**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**请求**

请求使用模式的URL编码 `id` URI（“schemaRef.id”属性的值），并需要一个Accept头。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

响应格式取决于在请求中发送的接受头的类型。 查找请求还要求 `version` 在“接受”标题中包含。 下表概述了代码的接受标题：

| 接受 | 描述 |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | 列表(GET)请求、标题、ID和版本 |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs和allOf已解析，有标题和说明 |
| `application/vnd.adobe.xed+json; version={major version}` | 带有$ref和allOf的原始数据包含标题和说明 |
| `application/vnd.adobe.xed-notext+json; version={major version}` | 原始数据（带有$ref和allOf，无标题或说明） |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs和all已解析，无标题或说明 |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs和allOf已解析，包含描述符 |

>[!NOTE] 并且 `application/vnd.adobe.xed-id+json` 是最常 `application/vnd.adobe.xed-full+json; version={major version}` 用的“接受”标题。 `application/vnd.adobe.xed-id+json` 首选将资源列在模式注册表中，因为它只返回“title”、“id”和“version”。 `application/vnd.adobe.xed-full+json; version={major version}` 首选查看特定资源（按其“id”），因为它返回所有字段（嵌套在“属性”下）以及标题和说明。

**响应**

返回的JSON模式描述结构和字段级信息（“类型”、“格式”、“最小”、“最大”等）序列化为JSON的数据。 如果使用非JSON的序列化格式进行获取（如Parke或Scala），则《 [模式注册指南》(](../xdm/tutorials/create-schema-api.md) Segristry Guide)包含一个表，其中显示了所需的JSON类型(“meta:xdmType”)及其以其他格式的相应表示形式。

除此表外，《模式注册表开发人员指南》还包含使用模式注册表API可进行的所有可能调用的详细示例。

### 数据集“模式”属性(DEPRECATED - EOL 2019-05-30)

数据集可能包含“模式”属性，该属性现已弃用，但为了向后兼容性，该属性仍暂时可用。 例如，与先前所做的列表(GET)请求类似，其中“模式”被“查询”参数中的“schemaRef”所替代，可能会返回以下内容： `properties`

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

如果填充了数据集的“模式”属性，则表明模式是已弃用的 `/xdms` 模式，并且在支持的情况下，ETL连接器应使用“模式”属性中的值与端点( `/xdms`[](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalog API中已弃用的端点)一起检索旧模式。

**API格式**

```http
GET /catalog/{"schema" property without the "@"}
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE] 可选的查询参 `expansion=xdm`数告知API完全扩展并串联所有引用的模式。 当向用户展示所有潜在字段的列表时，您可能希望这样做。

**响应**

与查看数据集模式 [的步骤相似](#view-dataset-schema)，响应包含一个JSON模式，用于描述数据的结构和字段级信息（序列化为JSON）。

>[!NOTE] 当“模式”字段为空或完全不存在时，连接器应读取“schemaRef”字段，并使用 [模式注册表API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) ，如前几步所示，以 [视图数据集模式](#view-dataset-schema)。

### “overtableSchema”属性

数据集的“vocableSchema”属性具有与XDM模式JSON匹配的JSON结构。 “overtableSchema”包含传入输入文件中存在的字段。 向Experience Platform写入数据时，用户无需使用目标模式中的每个字段。 相反，他们应仅提供正在使用的字段。

可观察模式是您读取数据或显示可从中读取／映射的字段列表时使用的模式。

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

ETL应用程序可以提供预览数据的功能([“ETL工作流程中的图8](./workflow.md)”)。 数据访问API提供了多个选项来预览数据。

其他信息（包括使用数据访问API预览数据的分步指南）可在数据访问教程中 [找到](../data-access/tutorials/dataset-data.md)。

### 使用“properties”查询参数获取数据集详细信息

如上述视图数据集 [列表的步骤所示](#view-list-of-datasets)，您可以使用“properties”查询参数请求“files”。

有关查询数据集和可 [用响应过滤器的详细信息](../catalog/home.md) ，请参阅目录服务概述。

**API格式**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**响应**

响应将包含一个显示“`limit=1`files”属性的数据集()。

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### 列表使用“files”属性的数据集文件

您还可以使用GET请求来获取使用“files”属性的文件详细信息。

**API格式**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

**响应**

响应包括作为顶级属性的数据集文件ID，其文件详细信息包含在数据集文件ID对象中。

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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

在先前响应中返回的数据集文件ID可用于GET请求中，以通过数据访问API获取更多文件详细信息。

数据 [访问概述](../data-access/home.md) ，包含有关如何使用数据访问API的详细信息。

**API格式**

```http
GET /export/files/{DATASET_FILE_ID}
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
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

“href”属性可用于通过数据访问API获取预览 [数据](../data-access/home.md)。

**API格式**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

对上述请求的响应将包含文件内容的预览。

有关数据访问API的更多信息（包括详细的请求和响应），请参阅数 [据访问概述](../data-access/home.md)。

### 从数据集获取“fileDescription”

目标组件作为转换后数据的输出，数据工程师将选择一个输出数据集([ETL工作流中的“图12”](workflow.md))。 XDM模式与输出数据集相关联。 要写入的数据将由Data Discovery API中数据集实体的“fileDescription”属性标识。 可以使用数据集ID()获取此`{DATASET_ID}`信息。 JSON响应中的“fileDescription”属性将提供所请求的信息。

**API格式**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{DATASET_ID}` | 您 `id` 尝试访问的数据集的值。 |

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
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

数据将使用Data Ingestion API写入Experience [Platform](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)。  数据写入是一个异步过程。 将数据写入Adobe Experience Platform时，只有在完全写入数据后，才会创建批次并将其标记为成功。

Experience Platform中的数据应以镶木文件的形式写入。

## 执行阶段

作为执行开始，连接器（如源组件中所定义）将使用数据访问API从Experience Platform读取 [数据](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)。 转换过程将读取特定时间范围的数据。 在内部，它将查询成批的源数据集。 在查询时，它将为这些批量使用参数化（滚动时间序列数据或增量数据）开始日期和列表数据集文件，并开始对这些数据集文件发出数据请求。

### 示例转换

示 [例ETL转换文档包含许多示例转换](./transformations.md) ，包括标识处理和数据类型映射。 请参考这些转换。

### 从Experience Platform读取数据

使用 [Catalog API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，您可以提取指定开始时间和结束时间之间的所有批次，并按它们的创建顺序对它们进行排序。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

有关筛选批的详细信息，请参阅数 [据访问教程](../data-access/tutorials/dataset-data.md)。

### 批量获取文件

一旦您获得了所查找(`{BATCH_ID}`)的批次的ID，就可以通过数据访问API检索属于特定批次的一列表 [文件](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)。  数据访问教程中提供了相关的 [详细信息](../data-access/tutorials/dataset-data.md)。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

### 使用文件ID访问文件

使用文件(`{FILE_ID`)的唯一ID，数据访问 [API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) （数据访问API）可用于访问文件的特定详细信息，包括其名称、大小（以字节为单位）以及用于下载文件的链接。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key : {API_KEY}"
```

响应可指向单个文件或目录。 有关每个教程的详细信息，请参阅 [数据访问教程](../data-access/tutorials/dataset-data.md)。

### 访问文件内容

数 [据访问API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) ，可用于访问特定文件的内容。 要获取内容，使用使用文件ID访问文件时返回 `_links.self.href` 的值发出GET请求。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

对此请求的响应包含文件的内容。 有关详细信息（包括有关响应分页的详细信息），请参 [阅如何通过数据访问API教程查询数据](../data-access/tutorials/dataset-data.md) 。

### 验证记录以符合模式

写入数据时，用户可以根据XDM模式中定义的验证规则选择验证数据。 有关模式验证的更多信息，请参阅GitHub上的 [ETL生态系统集成参考代码](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation)。

如果您使用 [GitHub上的引用实现](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md)，则可以使用系统属性在此实现中打开模式验证 `-DenableSchemaValidation=true`。

可以使用字符串和属性等属性对逻辑XDM类型执行验 `minLength` 证， `maxlength` 对 `minimum` 整数和 `maximum` 整数等属性执行验证。 模式注 [册表API开发人员指南中包含一个表](../xdm/api/getting-started.md) ，该表概述了XDM类型和可用于验证的属性。

>[!NOTE] 为各种类型提供的最小值和最 `integer` 大值是类型可支持的MIN和MAX值，但这些值可进一步限制为您选择的最小值和最大值。

### 创建批

处理数据后，ETL工具将使用批处理摄取API将数据写回 [Experience Platform](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)。 在将数据添加到数据集之前，必须先将其链接到一个批，随后该批将上传到特定数据集。

**请求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

有关创建批的详细信息（包括示例请求和响应），请参阅批 [摄取概述](../ingestion/batch-ingestion/overview.md)。

### 写入数据集

在成功创建新批后，文件随后可以上传到特定数据集。 在提升多个文件之前，可以批量发布多个文件。 文件可以使用小文件 _上传API上传_;但是，如果文件过大且超出了网关限制，则可以使用“大文件 _上传API”_。 有关同时使用“大文件上传”和“小文件上传”的详细信息，请参阅“批 [处理”概述](../ingestion/batch-ingestion/overview.md)。

**请求**

Experience Platform中的数据应以镶木文件的形式写入。

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{IMS_ORG}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### 标记批上传完成

在所有文件已上传到该批后，可以指示该批完成。 通过执行此操作，将为已完成的文件创建目录“DataSetFile”条目，并与生成批次相关联。 然后，将目录批标记为成功，这将触发下游流以获取可用数据。

数据将首先登陆到Adobe Experience Platform上的分阶段位置，然后在编目和验证后移至最终位置。 将所有数据移到永久位置后，批次将标记为成功。

**请求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

如果响应成功，则返回HTTP状态200 OK，且响应正文为空。

ETL工具将确保在读取数据时记录源数据集的时间戳。

在下一次转换执行中，ETL将开始从先前保存的时间戳和所有向前的数据请求数据，这可能通过计划或事件调用来实现。

### 获取上一批状态

在ETL工具中运行新任务之前，您必须确保已成功完成最后一批。 Catalog [Service API提供了一个特定于批的选项](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) ，其中提供了相关批的详细信息。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**响应**

如果上一批“状态”值为“成功”，则可计划新任务，如下所示：

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
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

### 按ID获取上一批状态

通过Catalog Service API [，可以使用发出GET请求来检索单个批状态](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)`{BATCH_ID}`。 使 `{BATCH_ID}` 用的ID与创建批时返回的ID相同。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**响应——成功**

以下响应显示“成功”:

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
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

**响应——失败**

如果失败，可以从响应中提取“错误”，并在ETL工具上作为错误消息显示。

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
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

## 增量与快照数据及事件与用户档案

数据可以由两个矩阵表示，如下所示：

| 增量事件 | 增量用户档案 |
|-------------------------------|----------------------|
| 快照事件（不太可能） | 快照用户档案 |

事件数据通常在每行中都有索引时间戳列时显示。

用户档案数据通常在数据中没有时间戳且每行可由主键／复合键标识时。

增量数据是指只有新的／更新的数据才会进入系统并附加到数据集中的当前数据的位置。

快照数据是指所有数据进入系统并替换数据集中的部分或全部以前数据时。

对于增量事件,ETL工具应使用批实体的可用日期／创建日期。 在推送服务中，可用日期不存在，因此工具将使用批量创建／更新日期来标记增量。 每批增量事件都需要处理。

对于增量用户档案,ETL工具将使用批实体的创建／更新日期。 通常，每批增量用户档案数据都需要处理。

由于数据的庞大，快照事件的可能性很小。 但是，如果这是必需的，则ETL工具必须只选择最后一个批处理。

使用快照用户档案时，ETL工具将必须选取到达系统的最后一批数据。 但是，如果要求跟踪更改版本，则所有批都将需要进行处理。 ETL流程中的重复数据消除处理将有助于控制存储成本。

## 批量重放和数据重新处理

如果客户发现在过去的“n”天中，正在处理的数据未按预期发生，或源数据本身可能不正确，则可能需要进行批量重放和数据重新处理。

为此，客户端的数据管理员将使用平台UI删除包含损坏数据的批。 然后，ETL可能需要重新运行，从而使用正确的数据重新填充。 如果源本身有损坏的数据，则数据工程师／管理员需要更正源批次并重新摄取数据（通过Adobe Experience Platform或ETL连接器）。

根据生成的数据类型，数据工程师可以选择从某些数据集中删除单个批次或所有批次。 根据Experience Platform准则，将删除／存档数据。

可能的情况是，清除数据的ETL功能将非常重要。

完成清除后，客户端管理员必须重新配置Adobe Experience Platform，以从删除批次开始重新开始处理核心服务。

## 并发批处理

由客户决定，数据管理员／工程师可以根据特定数据集的特性决定以顺序或并发方式提取、转换和加载数据。 这也将基于客户端使用转换后的数据定位的用例。

例如，如果客户端持久到可更新的持久存储，并且事件的顺序或顺序很重要，则客户端可能需要严格处理具有连续ETL转换的作业。

在其他情况下，无序数据可以由下游应用程序／进程处理，这些应用程序／进程使用指定的时间戳在内部进行排序。 在这些情况下，并行ETL转换可能可以缩短处理时间。

对于源批，它将再次取决于客户偏好和消费者约束。 如果源数据可以并行地拾取而不考虑行的摄政／排序，那么转换过程可以创建具有更高并行度的处理批（基于无序处理的优化）。 但是，如果转换必须遵守时间戳或更改优先级排序，则数据访问API或ETL工具的调度程序/调用必须确保批处理不会在可能的情况下无序进行。

## 递延

延迟是一种过程，其中输入数据尚未足够完整以发送到下游进程，但可能在将来可用。 客户将确定他们对数据窗口的个别容忍度，以便将来进行匹配，而不是处理成本，以告知他们决定在下次转换执行中保留数据并重新处理它，希望它能够在保留窗口的将来某个时间被丰富和协调／拼接。 这个周期一直持续，直到行被充分处理，或者被认为过于陈旧，无法继续投资。 每个迭代都将生成延迟数据，该数据是先前迭代中所有延迟数据的超集。

Adobe Experience Platform当前不识别延迟数据，因此客户端实施必须依赖ETL和数据集手动配置在平台中创建另一个数据集，该数据集镜像可用于保留延迟数据的源数据集。 在这种情况下，延迟数据将类似于快照数据。 在ETL转换的每次执行中，源数据将与延迟数据相统一并发送以进行处理。

## 更改日志

| 日期 | 操作 | 描述 |
| ---- | ------ | ----------- |
| 2019-01-19 | 从数据集中删除了“字段”属性 | 数据集之前包含“fields”属性，该属性包含模式的副本。 不应再使用此功能。 如果找到“fields”属性，则应忽略该属性，并改用“osceptedSchema”或“schemaRef”。 |
| 2019-03-15 | 向数据集添加的“schemaRef”属性 | 数据集的“schemaRef”属性包含引用数据集所基于的XDM模式的URI，并表示数据集可以使用的所有潜在字段。 |
| 2019-03-15 | 所有最终用户标识符映射到“identityMap”属性 | “identityMap”是对主题的所有唯一标识符(如CRM ID、ECID或忠诚度项目ID)的封装。 此地图由 [Identity Service用来解析主题的所有已知和匿名身份](../identity-service/home.md) ，为每个最终用户形成一个单一的身份图。 |
| 2019-05-30 | EOL和从数据集中删除“模式”属性 | 数据集“模式”属性使用目录API中已弃用的端点提供了指向模式 `/xdms` 的引用链接。 它已被“schemaRef”替换，该“schemaRef”提供新模式注册表API中引用的模式的“id”、“version”和“contentType”。 |
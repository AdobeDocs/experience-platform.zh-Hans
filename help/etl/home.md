---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 创建ETL集成
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '4227'
ht-degree: 0%

---


# 开发ETL集成以实现Adobe Experience Platform

ETL集成指南概述了创建高性能、安全连接器以进行Experience Platform并将数据引入平台的一般步骤。


- [Catalog](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)
- [数据访问](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)
- [数据获取](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [身份验证和授权API](../tutorials/authentication.md)
- [模式注册](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)

本指南还包括设计ETL连接器时要使用的示例API调用，其中包含描述每个Experience Platform服务的文档的链接，以及其API的使用。

GitHub上可通过Apache License Version 2.0 [下的ETL Eystem Integration Reference Code](https://github.com/adobe/acp-data-services-etl-reference) （ETL生态系统集成参考代码）获得示例集成。

## 工作流

以下工作流图提供了将Adobe Experience Platform组件与ETL应用程序和连接器集成的高级概述。

![](images/etl.png)

## Adobe Experience Platform组件

ETL连接器集成涉及多个Experience Platform组件。 以下列表概述了几个关键组件和功能：

- **AdobeIdentity Management系统(IMS)** -为Adobe服务提供身份验证框架。
- **IMS组织** -拥有或许可产品和服务并允许访问其成员的公司实体。
- **IMS用户** - IMS组织的成员。 “组织与用户”关系是多对多的。
- **沙箱** -单个平台实例的虚拟分区，用于帮助开发和发展数字体验应用程序。
- **数据发现** -在Experience Platform中记录所摄取和转换数据的元数据。
- **数据访问** -为用户提供一个界面，以Experience Platform方式访问其数据。
- **数据摄取** -使用数据摄取API将数据推送到Experience Platform。
- **模式注册** -定义和存储描述要在Experience Platform中使用的数据结构的模式。

## Experience PlatformAPI入门

以下各节提供您需要了解或掌握的其他信息，以便成功调用Experience PlatformAPI。

### 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的章节。

### 收集所需标题的值

要调用平台API，您必须先完成身份验证 [教程](../tutorials/authentication.md)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

- 授权： 承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都隔离到特定虚拟沙箱。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

- 内容类型： application/json

## 一般用户流

首先，ETL用户登录到Experience Platform用户界面(UI)，并使用标准连接器或推送服务连接器创建数据集以供获取。

在UI中，用户通过选择数据集模式来创建输出数据集。 模式的选择取决于被引入平台的数据类型（记录或时间序列）。 通过单击UI中的模式选项卡，用户将能够视图所有可用模式，包括模式支持的行为类型。

在ETL工具中，用户将在配置相应连接（使用其凭据）后开始设计其映射转换。 假定ETL工具已安装Experience Platform连接器（此集成指南中未定义流程）。

ETL工作流中已提供示例ETL工具和工作流的 [模型](./workflow.md)。 虽然ETL工具的格式可能不同，但大多数工具都提供类似的功能。

>[!NOTE]
>
>ETL连接器必须指定一个时间戳过滤器，用于标记要摄取数据和偏移的日期（即要读取数据的窗口）。 ETL工具应支持在此或其他相关UI中采用这两个参数。 在Adobe Experience Platform中，这些参数将映射到数据集的批处理对象中存在的可用日期（如果存在）或捕获日期。

### 视图列表数据集

使用数据源进行映射，可以使用Catalog API获取所有可用数据集 [的列表](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)。

您可以发出单个API请求以视图所有可用数据集(例如， `GET /dataSets`)，最佳实践是包含限制响应大小的查询参数。

在请求完 _整数据集_ 信息时，响应有效负荷可能超过3GB大小，这会降低整体性能。 因此，使用查询参数仅筛选所需信息将提高目录查询的效率。

#### 列表过滤

在筛选响应时，可以通过用“和号”()分隔参数，在单个调用中使用多个`&`过滤器。 某些查询参数接受以逗号分隔的列表值，如以下示例请求中的“属性”筛选器。

目录响应会根据配置的限制自动按量收费，但“limit”查询参数可用于自定义约束并限制返回的对象数。 预配置的目录响应限制包括：

- 如果未指定限制参数，则每个响应有效负荷的最大对象数为20。
- 所有其他目录查询的全局限制为100个对象。
- 对于数据集查询，如果使用属性查询参数请求vocableSchema，则返回的最大数据集数为20。
- 无效的限制参数( `limit=0`包括)会遇到HTTP 400错误，该错误勾勒出正确的范围。
- 如果限制或偏移作为查询参数传递，则优先于作为标头传递的限制或偏移。

查询参数在目录服务概述中有 [更详细的介绍](../catalog/home.md)。

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

有关如何调 [用目录API的详](../catalog/home.md) 细示例，请参阅目录 [服务概述](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)。

**响应**

响应包括三(`limit=3`)个数据集，这些数据集显示查询参数所指示的“name”、“description”和“schemaRef” `properties` 。

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

数据集的“schemaRef”属性包含引用数据集所基于的XDM模式的URI。 XDM模式(“schemaRef”)表示 _集_ 可使用的所有潜在字段 _，而不一定是正在使用_ 的字段（请参阅下面的“可观察模式”）。

XDM模式是您在需要向用户显示可写入的所有可用字段的列表时使用的模式。

上一个响应对象()中的第一个“schemaRef.id”`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`值是指向模式注册表中特定XDM模式的URI。 通过对模式注册表API发出查找(GET)请求，可以检索模式。

>[!NOTE]
>
>“schemaRef”属性替换现已弃用的“模式”属性。 如果数据集中缺少“schemaRef”或不包含值，您需要检查是否存在“模式”属性。 这可以通过将上一个调用的模式参数中的“schemaRef”替 `properties` 换为“查询”来完成。 有关“模式”属性的更多详细信息，请参 [阅后面的“模式”属性](#dataset-schema-property-deprecated---eol-2019-05-30) 。

**API格式**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**请求**

请求使用模式的 `id` URL编码URI（“schemaRef.id”属性的值），并需要一个“接受”标头。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

响应格式取决于在请求中发送的接受头的类型。 查找请求也需 `version` 要包含在“接受”标题中。 下表概述了代码的接受标题：

| 接受 | 描述 |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | 列表(GET)请求、标题、ID和版本 |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs and allOf已解析，有标题和说明 |
| `application/vnd.adobe.xed+json; version={major version}` | 带有$ref和allOf的原始数据包含标题和说明 |
| `application/vnd.adobe.xed-notext+json; version={major version}` | 带有$ref和allOf的原始数据，无标题或描述 |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs和allOf已解析，无标题或说明 |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs和allOf已解析，包含描述符 |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` 和 `application/vnd.adobe.xed-full+json; version={major version}` 最常用的“接受”标头。 `application/vnd.adobe.xed-id+json` 首选在模式注册表中列出资源，因为它只返回“title”、“id”和“version”。 `application/vnd.adobe.xed-full+json; version={major version}` 首选用于查看特定资源（按其“id”），因为它返回所有字段（嵌套在“属性”下）以及标题和说明。

**响应**

返回的JSON模式描述结构和字段级信息（“类型”、“格式”、“最小”、“最大”等） 序列号为JSON。 如果使用非JSON的序列化格式进行获取(如Parke或 [Scala)](../xdm/tutorials/create-schema-api.md) ，则模式注册表指南包含一个表，其中显示所需的JSON类型(“meta:xdmType”)及其以其他格式的相应表示形式。

除此表外，《模式注册表开发人员指南》还包含使用模式注册表API进行的所有可能调用的详细示例。

### 数据集“模式”属性(DEPRECATED - EOL 2019-05-30)

数据集可能包含“模式”属性，该属性现已弃用，但为了向后兼容，它仍可临时使用。 例如，与先前所做的列表(GET)请求类似，其中“模式”被查询参数中的“schemaRef” `properties` 替换，可能返回以下内容：

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

如果填充了数据集的“模式”属性，则表明该模式是已弃用的 `/xdms` 模式，并且ETL连接器应在“模式”属性中使用端点（目录API中已弃用的端点）的 `/xdms` 值来检索旧 [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)模式。

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

>[!NOTE]
>
>可选查询参 `expansion=xdm`数告知API完全扩展并串联所有引用的模式。 当向用户显示所有潜在字段的列表时，您可能希望执行此操作。

**响应**

与查看数据集模式 [的步骤类似](#view-dataset-schema)，响应包含一个JSON模式，用于描述数据的结构和字段级信息（序列化为JSON）。

>[!NOTE]
>
>当“模式”字段为空或完全不存在时，连接器应读取“schemaRef”字段并使用 [模式注册表API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) ，如前几步所 [示视图数据集模式](#view-dataset-schema)。

### “可观察架构”属性

数据集的“voobableSchema”属性具有与XDM模式JSON匹配的JSON结构。 “可观察架构”包含传入输入文件中存在的字段。 向Experience Platform写入数据时，用户无需使用目标模式中的每个字段。 相反，它们应仅提供正在使用的字段。

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

ETL应用程序可以提供预览数据的[功能(ETL工作流中的“图8](./workflow.md)”)。 数据访问API提供多个预览数据选项。

其他信息，包括使用数据访问API预览数据的分步指南，可在数据访问教 [程中找到](../data-access/tutorials/dataset-data.md)。

### 使用“属性”查询参数获取数据集详细信息

如上述步骤所示，用 [于视图列表数据集](#view-list-of-datasets)，您可以使用“properties”查询参数请求“文件”。

有关查询数据集和 [可用响应过滤器的详](../catalog/home.md) 细信息，请参阅目录服务概述。

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

该响应包括数据集文件ID作为顶级属性，其文件详细信息包含在数据集文件ID对象中。

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

在以前的响应中返回的数据集文件ID可用于GET请求中，以通过数据访问API获取更多文件详细信息。

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

“href”属性可用于通过数据访问API获取 [预览数据](../data-access/home.md)。

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

有关数据访问API的更多信息（包括详细的请求和响应），请参阅 [数据访问概述](../data-access/home.md)。

### 从数据集获取“fileDescription”

目标组件作为转换数据的输出，数据工程师将选择一个输出数[据集(ETL工作流中的“](workflow.md)图12”)。 XDM模式与输出数据集关联。 要写入的数据将由Data Discovery API中数据集实体的“fileDescription”属性标识。 可以使用数据集ID()获取此`{DATASET_ID}`信息。 JSON响应中的“fileDescription”属性将提供所请求的信息。

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

数据将使用Data Ingestion API写 [入Experience Platform](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)。  数据写入是一个异步过程。 将数据写入Adobe Experience Platform时，仅在完全写入数据后，才会创建批处理并将其标记为成功。

Experience Platform中的数据应以镶木地板文件的形式写入。

## 执行阶段

作为执行开始，连接器（如源组件中定义）将使用数据访问API从Experience Platform [读取数据](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)。 转换过程将读取特定时间范围内的数据。 在内部，它将查询成批的源数据集。 在查询时，它将使用参数化（滚动时间序列数据或增量数据）开始日期和列表数据集文件来查询这些批，并开始请求这些数据集文件的数据。

### 示例转换

示 [例ETL转换文档](./transformations.md) 包含许多示例转换，包括标识处理和数据类型映射。 请使用这些转换作为参考。

### 从Experience Platform读取数据

使用 [目录API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，您可以提取指定开始时间和结束时间之间的所有批，并按它们的创建顺序对它们进行排序。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

有关过滤批的详细信息，请参阅数 [据访问教程](../data-access/tutorials/dataset-data.md)。

### 从批处理中获取文件

在您获得要查找的批的ID(`{BATCH_ID}`)后，可以通过数据访问API检索属于特定批的一列表 [文件](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)。  数据访问教程中提供了相关 [详细信息](../data-access/tutorials/dataset-data.md)。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

### 使用文件ID访问文件

使用文件()的唯`{FILE_ID`一ID, [数据访问API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) 可用于访问文件的特定详细信息，包括其名称、字节大小和用于下载文件的链接。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key : {API_KEY}"
```

响应可以指向单个文件或目录。 有关每个教程的详细信息，请参 [阅数据访问教程](../data-access/tutorials/dataset-data.md)。

### 访问文件内容

数 [据访问](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) API可用于访问特定文件的内容。 要获取内容，使用使用文件ID访问文件时返回 `_links.self.href` 的值发出GET请求。

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

对此请求的响应包含文件的内容。 有关详细信息（包括有关响应分页的详细信息），请 [参阅如何通过查询访问API教程数据](../data-access/tutorials/dataset-data.md) 。

### 验证记录以符合模式

写入数据时，用户可以根据XDM模式中定义的验证规则选择验证数据。 有关模式验证的更多信息，请参 [阅GitHub上的ETL Eystem Integration Reference Code](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation)。

如果您使用GitHub上的引用实 [现](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md)，则可以使用系统属性在此实现中打开模式验证 `-DenableSchemaValidation=true`。

可以使用属性（如字符串、字符串、整数等）对逻 `minLength` 辑XDM `maxlength` 类型 `minimum` 执行验 `maximum` 证，还可以对整数等进行验证。 模式 [注册表API开发人员指南](../xdm/api/getting-started.md) （包含一个表），其中概述了XDM类型和可用于验证的属性。

>[!NOTE]
>
>为各种类型提供的最小值和 `integer` 最大值是类型可支持的MIN和MAX值，但这些值可进一步限制为您选择的最小值和最大值。

### 创建批

处理数据后，ETL工具将使用批处理摄取API将数据写回 [Experience Platform](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)。 在将数据添加到数据集之前，必须将其链接到一个批次，该批次稍后将上传到特定数据集。

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

成功创建新批后，文件可上传到特定数据集。 在提升多个文件之前，可以在一个批中发布它。 文件可以使用“小文 _件上传API”上传_; 但是，如果文件太大并且超出了网关限制，则可以使用“大 _文件上传API”_。 有关同时使用“大文件上传”和“小文件上传”的详细信息，请参 [阅批处理概述](../ingestion/batch-ingestion/overview.md)。

**请求**

Experience Platform中的数据应以镶木地板文件的形式写入。

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

在所有文件都上传到该批后，可以指示该批完成。 通过执行此操作，将为已完成的文件创建目录“DataSetFile”条目，并与生成批关联。 然后，目录批被标记为成功，这将触发下游流以获取可用数据。

数据将首先降落在Adobe Experience Platform的分阶段位置，然后在编目和验证后移至最终位置。 将所有数据移动到永久位置后，批次将标记为成功。

**请求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

如果响应成功，则返回“HTTP状态200 OK”，且响应正文为空。

ETL工具将确保在读取数据时记录源数据集的时间戳。

在下次转换执行中，ETL将开始请求先前保存的时间戳中的数据以及将要执行的所有数据，这可能通过计划或事件调用来实现。

### 获取上一批状态

在ETL工具中运行新任务之前，必须确保成功完成上一批。 目 [录服务API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) 提供一个批特定选项，它提供相关批的详细信息。

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

如果上一批“状态”值为“成功”，则可以计划新任务，如下所示：

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

通过使用发出GET请求，可以 [通过Catalog Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) API检索单个批处理状态 `{BATCH_ID}`。 使 `{BATCH_ID}` 用的ID与创建批时返回的ID相同。

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

如果失败，可以从响应中提取“错误”，并在ETL工具上以错误消息的形式呈现。

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

## 增量与快照事件与用户档案

数据可以用两个矩阵表示，如下所示：

| 增量事件 | 增量用户档案 |
|-------------------------------|----------------------|
| 快照事件（不太可能） | 快照用户档案 |

事件数据通常在每行中有索引时间戳列时。

用户档案数据通常在数据中没有时间戳且每行都可由主／复合键标识时。

增量数据是指只有新／更新的数据才会进入系统并附加到数据集中的当前数据。

快照数据是指所有数据进入系统并替换数据集中的部分或全部以前数据时。

对于增量事件,ETL工具应使用批实体的可用日期／创建日期。 在推送服务中，可用日期不存在，因此工具将使用批量创建／更新日期来标记增量。 每批增量事件都需要处理。

对于增量用户档案,ETL工具将使用批实体的创建／更新日期。 通常，每批增量用户档案数据都需要处理。

快照事件的可能性很小，因为数据的大小很大。 但是，如果需要这些，则ETL工具只能选择最后一个批进行处理。

使用快照用户档案时，ETL工具将必须选取系统中到达的最后一批数据。 但是，如果要求跟踪更改的版本，则需要处理所有批次。 ETL流程中的重复数据消除处理将有助于控制存储成本。

## 批处理重放和数据重新处理

如果客户发现过去“n”天中，ETL处理的数据未按预期发生，或源数据本身可能不正确，则可能需要进行批量重放和数据重新处理。

为此，客户端的数据管理员将使用平台UI删除包含损坏数据的批。 然后，ETL可能需要重新运行，从而使用正确的数据重新填充。 如果源本身有损坏的数据，数据工程师／管理员需要更正源批次并重新摄取数据(输入Adobe Experience Platform或通过ETL连接器)。

根据所生成的数据类型，数据工程师可以选择从特定数据集中删除单个批或所有批。 将根据Experience Platform准则删除／存档数据。

很可能，清除数据的ETL功能将非常重要。

清除完成后，客户端管理员将必须重新配置Adobe Experience Platform，以从删除批时起重新开始核心服务的处理。

## 并发批处理

数据管理员／工程师可以根据特定数据集的特征决定以顺序或并发方式提取、转换和加载数据。 这还将基于客户端使用转换后的数据定位的用例。

例如，如果客户端持续到可更新的持久性存储，并且事件的顺序或顺序很重要，则客户端可能需要使用顺序ETL转换严格处理作业。

在其他情况下，无序数据可由下游应用程序／进程处理，这些应用程序／进程使用指定的时间戳在内部进行排序。 在这些情况下，并行ETL转换可能可以缩短处理时间。

对于源批，它将再次取决于客户端首选项和用户约束。 如果源数据可以并行地拾取而不考虑行的摄政／排序，则转换过程可以创建具有较高并行度的处理批（基于不顺序处理的优化）。 但是，如果转换必须遵守时间戳或更改优先级排序，则数据访问API或ETL工具的调度程序/调用必须确保批处理不会在可能的情况下无序进行。

## 递延

延迟是一种过程，在该过程中，输入数据尚未足够完整，无法发送到下游进程，但将来可能可用。 客户将确定他们对数据窗口的容忍度，以便将来进行匹配，而不是处理成本，以告知他们决定在下一次转换执行中搁置数据并重新处理它，希望在保留窗口内的将来某个时间对其进行丰富和协调／拼接。 这一周期一直持续，直到该行被充分处理，或者它被认为过于陈旧，无法继续投资。 每个迭代都将生成延迟数据，该数据是先前迭代中所有延迟数据的超集。

Adobe Experience Platform当前不识别延迟数据，因此客户端实施必须依赖ETL和数据集手动配置在平台中创建另一个数据集，以镜像源数据集，该数据集可用于保留延迟数据。 在这种情况下，延迟数据将类似于快照数据。 每次执行ETL转换时，源数据都会与延迟数据相统一，并发送给处理。

## Changelog

| 日期 | 操作 | 描述 |
| ---- | ------ | ----------- |
| 2019-01-19 | 从数据集中删除了“字段”属性 | 数据集之前包含“字段”属性，该属性包含模式的副本。 不应再使用此功能。 如果找到“fields”属性，则应忽略它，改用“opectedSchema”或“schemaRef”。 |
| 2019-03-15 | 已向数据集添加“schemaRef”属性 | 数据集的“schemaRef”属性包含引用数据集所基于的XDM模式的URI，并表示数据集可以使用的所有潜在字段。 |
| 2019-03-15 | 所有最终用户标识符都映射到“identityMap”属性 | “identityMap”是对主题的所有唯一标识符(如CRM ID、ECID或忠诚度项目ID)的封装。 此地图由Identity Service [用来解析主体的](../identity-service/home.md) 所有已知和匿名身份，从而为每个最终用户形成一个单一的身份图。 |
| 2019-05-30 | EOL和从数据集中删除“模式”属性 | 数据集“模式”属性使用目录API中已弃用的端点提供指向模式 `/xdms` 的引用链接。 它已被“schemaRef”替换，该“schemaRef”提供新模式注册表API中引用的模式的“id”、“version”和“contentType”。 |
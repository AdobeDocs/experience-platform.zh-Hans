---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 实时客户用户档案API开发人员指南
topic: guide
translation-type: tm+mt
source-git-commit: 95e002c60389ca7e4c1dcf32bbcf6f552cd55d95

---


# 用户档案搜索

用户档案搜索用于搜索包含在各种数据源中的可配置字段并为其编制索引，并近乎实时地返回这些字段。

本指南提供了帮助您更好地了解用户档案搜索的信息，并包含使用API执行基本操作的示例API调用。

## 入门指南

本指南中使用的API端点是实时客户用户档案API的一部分。 在继续之前，请查阅实 [时客户用户档案开发人员指南](getting-started.md)。

特别是，用户档案开发人 [员指南的入门部分](getting-started.md) ，包括指向相关主题的链接、阅读本文档中示例API调用的指南以及成功调用任何Experience Platform API所需的标题的重要信息。

### 获取搜索结果

该搜索端点可用于根据所需参数的值和附加的可选查询参 `schema.name` 数来获得搜索结果。 可以使用多个参数，用&amp;符号(&amp;)分隔。

**API格式**

```http
GET /search?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `schema.name` | **必需.** 包含要搜索内容的模式类的名称，以点记号格式编写。 目前，仅 `schema.name=_xdm.context.segmentdefinition` 受支持。 |
| `limit` | 要返回的搜索结果数。 默认值为 50。 |
| `page` | 用于对搜索的查询结果进行分页的页码。 |
| `s` | 一个符合Microsoft实现 [Lucene搜索语法的查询](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 如果未指定搜索词，则将返回与之关联的所 `schema.name` 有记录。 此文档的“搜索参数”部分提供 [了更详细的说](#search-parameters) 明。 |
| `namespace` | 标识要在参数中指定的模式类上搜索的实际数 `schema.name` 据。 |
| `organization.type` | 确定响应的内容。 返回的内容的格式取决于中使用的值 `schema.name`。 对 `_xdm.context.segmentdefinition`于，有效值为 `hierarchy` 或 `hierarchyinfo`。 |
| `organization.id` | **如果指定，`organization.type`则为必需。** 在与层次结构一起使用时，提供指定组织的 `organization.type` 层次结构。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回一组满足搜索条件的对象。 在此示例中，由于参 `schema.name` 数是 `_xdm.context.segmentdefinition`，因此将返回区段定义的列表。

```json
{
  "aam-hierarchy": {
    "_xdm.context.segmentdefinition": [
      {
        "isFolder": true,
        "id": "100023",
        "name": "Segment Definition 1",
        "description": "Sample description.",
        "parentFolderId": "99970"
      },
      {
        "isFolder": false,
        "id": "1000028",
        "name": "Segment Definition 2",
        "description": "Sample description.",
        "parentFolderId": "103584"
      }
    ]
  },
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": "1",
    "pageSize": 2,
    "limit": 2
  }
}
```

### 创建供应请求

您可以通过向端点发出POST请求，创建供应请求以启用用户档案搜索功 `/search/provisioning/component/init` 能。

**请求**

>[!CAUTION]
>此POST请求不包含有效负荷，因此不需要内容类型标题。 此外，没有沙箱头，因为所有数据都发送到全局沙箱中。

```shell
curl -X POST \
    https://platform.adobe.io/data/core/ups/search/provisioning/component/init \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' 
```

**响应**

成功的响应会返回HTTP状态201（已创建）和以下消息：

```plaintext
The request has been fulfilled and resulted in a new resource being created.
```

### 处理配置请求

配置端点可用于为新的IMS组织设置正确的索引、索引器和数据源连接。 处理配置请求需要两个属性： `databaseName` 和 `containerName`。

`databaseName` 表示要配置的组织的用户档案数据库的名称。

`containerName` 表示由数据连接器填充的容器的名称，数据连接器是配置过程中读取的内容。 POST请求中有两 `containerName`个值，一个或两个值都可以使用：
- `_xdm.content.segmentdefinition`
- `_experience.audiencemanager.segmentfolder`

### 创建配置请求

以下API调用基于在请求有效负荷中提供的参数生成所需的数据源、索引器和索引。

**API格式**

```http
POST /search/configure
```

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**响应**

成功的响应会返回HTTP状态202（已接受）和纯文本消息。

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

### 删除配置请求

以下API调用删除匹配索引条目，并基于请求有效负荷中提供的参数删除索引器和数据源。

>[!NOTE]
>索引本身不会被删除，因为它是共享资源。

**API格式**

```http
DELETE /search/configure
```

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**响应**

成功的响应会返回HTTP状态202（已接受）和纯文本消息。

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

## 后续步骤

阅读本指南后，您现在可以更好地了解实时客户用户档案搜索的工作方式。 有关实时客户用户档案的更多信息，请阅读实 [时客户用户档案概述](../home.md)。 有关分段的详细信息，请阅读分段 [概述](../../segmentation/home.md)。

## 附录 {#appendix}

### 搜索参数 {#search-parameters}

下表列表了在使用搜索API时搜索参数的具体工作方式。

| 搜索查询 | 描述 |
|------------ | -----------|
| foo | 搜索任何单词。 如果在任何可搜索字段中都找到单词“foo”，则返回结果。 |
| foo AND栏 | 布尔搜索。 如果在任何可搜 **索字段** 中都找到“foo”和“bar”两个词，则返回结果。 |
| foo OR栏 | 布尔搜索。 如果在任何可搜 **索的字段** 中都找到单词“foo”或单词“bar”，则返回结果。 |
| foo NOT栏 | 布尔搜索。 如果找到单词“foo”，但在任何可搜索字段中都找不到单词“bar”，则返回结果。 |
| name:foo AND栏 | 布尔搜索。 如果在“名 **称** ”字段中找到“foo”和“bar”两个词，则返回结果。 |
| run* | 通配符搜索。 使用星号(*)匹配0个或多个字符，这意味着如果任何可搜索字段的内容包含一个与“run”开始的单词，则返回结果。 例如，如果出现“runs”、“running”、“runner”或“runt”等字样，则返回结果。 |
| 小卡？ | 通配符搜索。 使用问号(?)只匹配一个字符，这意味着如果任何可搜索字段的内容开始有“cam”和其他字母，则返回结果。 例如，如果出现“camp”或“cams”这两个字，则返回结果；如果出现“camera”或“campfire”这两个字，则返回结果。 |
| “蓝伞” | 短语搜索。 如果任何可搜索字段的内容包含完整短语“蓝色雨伞”，则返回结果。 |
| 蓝色\~ | 模糊搜索。 或者，您可以在代字符(~)后加上一个介于0-2之间的数字来指定编辑距离。 例如，“blue\~1”将返回“blue”、“blues”或“glue”。 模糊搜索 **只能应用** 于术语，而不能应用于短语。 但是，您可以在短语中每个单词的末尾附加代字符。 例如，“camping\~ in\~ the\~ summer\~”将与“camping in the summer”匹配。 |
| “酒店机场”\~5 | 近距离搜索。 此类搜索用于查找文档中彼此相近的术语。 例如，短语将 `"hotel airport"~5` 在文档中找到“hotel”和“airport”这两个词的5个字。 |
| `/a[0-9]+b$/` | 定期表达式搜索。 这种搜索类型根据正斜杠“/”之间的内容查找匹配项，如RegExp类中所述。 例如，要查找包含“motel”或“hotel”的文档，请指定 `/[mh]otel/`。 常规表达式搜索与单词匹配。 |

有关查询语法的更详细文档，请阅读 [Lucene查询语法文档](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。

---
keywords: Experience Platform;segmentation;segmentation service;troubleshooting;API;seg;
solution: Adobe Experience Platform
title: 分段API开发人员指南
topic: guide
translation-type: tm+mt
source-git-commit: 7c33ba8edc886d2b689e1125b5c378e16a487324
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 2%

---


# 区段搜索

“细分搜索”用于搜索和索引各个数据源中包含的可配置字段，并近乎实时地返回它们。

本指南提供相关信息，帮助您更好地了解细分搜索，并包含使用API执行基本操作的示例API调用。

## 入门指南

本指南中使用的API端点是分段API的一部分。 在继续之前，请查阅分段开 [发人员指南](getting-started.md)。

特别是，分段开 [发人员指南的](getting-started.md) “入门”部分包括相关主题的链接、阅读此文档中示例API调用的指南，以及成功调用Experience Platform API所需标头的重要信息。

除了入门部分中概述的所需标头外，对Segment Search API的所有请求都需要以下附加标头：

- x-ups-search-version: “1.0”

### 跨多个命名空间搜索

此搜索端点可用于在各种命名空间中进行搜索，返回搜索计数结果的列表。 可以使用多个参数，用和号(&amp;)分隔。

**API格式**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| 参数 | 描述 |
| ---------- | ----------- | 
| schema.name={SCHEMA} | **(必需** )其中{模式}表示与搜索对象关联的模式类值。 目前，仅 `_xdm.context.segmentdefinition` 受支持。 |
| s={SEARCH_TERM} | *(可选* )其中{SEARCH_TERM}表示符合Microsoft对Lucene搜索语法 [的实现的查询](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 如果未指定搜索词，则将返回与相关的所 `schema.name` 有记录。 本文档的附录中提供了更详 [细的](#appendix) 解释。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**响应**

成功的响应返回HTTP状态200，并包含以下信息。

```json
{
  "namespaces": [
    {
      "name": "AAMTraits",
      "count": 45
    },
    {
      "name": "AAMSegments",
      "count": 10
    },
    {
      "name": "SegmentsAISegments",
      "count": 3
    }
  ],
  "status": {
    "message": "Success"
  }
}
```

### 搜索单个实体

此搜索端点可用于检索指定列表内所有全文索引对象的命名空间。 可以使用多个参数，用和号(&amp;)分隔。

**API格式**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 参数 | 描述 |
| ---------- | ----------- | 
| schema.name={SCHEMA} | **（必需）** 其中{模式}包含与搜索对象关联的模式类值。 目前，仅 `_xdm.context.segmentdefinition` 受支持。 |
| 命名空间={命名空间} | **（必需）** {命名空间}包含要在其中搜索的命名空间。 |
| s={SEARCH_TERM} | *(可选* )其中{SEARCH_TERM}包含符合Microsoft实现Lucene搜索语 [法的查询](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 如果未指定搜索词，则将返回与相关的所 `schema.name` 有记录。 本文档的附录中提供了更详 [细的](#appendix) 解释。 |
| entityId={ENTITY_ID} | *（可选）* 将搜索限制在指定文件夹内，该文件夹由{ENTITY_ID}指定。 |
| limit={LIMIT} | *(可选* )其中{LIMIT}表示要返回的搜索结果数。 默认值为 50。 |
| page={PAGE} | *（可选）其中* {PAGE}表示用于对搜索的查询结果进行分页的页码。 请注意，页码开始为 **0**。 |


**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**响应**

成功的响应返回HTTP状态200，结果与搜索查询匹配。

```json
{
  "entities": [
    {
       "id": "1012667",
       "base64EncodedSourceId": "RFVGamdydHpEdy01ZTE1ZGJlZGE4YjAxMzE4YWExZWY1MzM1",
       "sourceId": "DUFjgrtzDw-5e15dbeda8b01318aa1ef533",
       "isFolder": true,
       "parentFolderId": "974139",
       "name": "aam-47995 verification (100)"
    },
    {
       "id": "14653311",
       "base64EncodedSourceId": "REVGamduLVgzdy01ZTE2ZjRhNjc1ZDZhMDE4YThhZDM3NmY1",
       "sourceId": "DEFjgn-X3w-5e16f4a675d6a018a8ad376f",
       "isFolder": false,
       "parentFolderId": "324050",
       "name": "AAM - Heavy equipment",
       "description": "AAM - Acme Equipment"
    }
 
 ],
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": 0,
    "pageSize": 10
  },
  "status": {
    "message": "Success"
  }
}
```

### 获取有关搜索对象的结构信息

此搜索端点可用于获取有关所请求搜索对象的结构信息。

**API格式**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 参数 | 描述 |
| ---------- | ----------- | 
| schema.name={SCHEMA} | **（必需）** 其中{模式}包含与搜索对象关联的模式类值。 目前，仅 `_xdm.context.segmentdefinition` 受支持。 |
| 命名空间={命名空间} | **（必需）** {命名空间}包含要在其中搜索的命名空间。 |
| entityId={ENTITY_ID} | **(必需** )要获取相关结构信息的搜索对象的ID，用{ENTITY_ID}指定。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**响应**

成功的响应返回HTTP状态200，其中包含有关所请求搜索对象的详细结构信息。

```json
{
    "taxonomy": [
        {
            "id": "0",
            "base64EncodedSourceId": "RFVGZ01BLTVlNjgzMGZjMzk3YjQ1MThhYWExYTA4Zg2",
            "name": "AAMTraits for Cars",
            "parentFolderId": "root"
        },
        {
            "id": "150561",
            "base64EncodedSourceId": "RFVGamdpRk1BZy01ZTY4MzBmYzM5N2I0NTE4YWFhMWEwOGY1",
            "name": "Fast Cars",
            "parentFolderId": "carTraits"
        },
        {
            "id": "porsche11037",
            "base64EncodedSourceId": "REFGZ01CLTVlNjczMGZjMzk3YjQ1MThhZGIxYTA4Zg==",
            "name": "Porsche",
            "parentFolderId": "redCarsFolderId"
        }
    ],
    "status": {
        "message": "Success"
    }
}
```

## 后续步骤

阅读本指南后，您现在可以更好地了解区段搜索的工作方式。 有关分段的详细信息，请阅读分段 [概述](../home.md)。

## 附录 {#appendix}

以下各节提供了有关搜索词工作原理的更多信息。 搜索查询的编写方式如下： `s={FieldName}:{SearchExpression}`. 因此，例如，要搜索名为AAM或平台的区段，您应使用以下搜索查询: `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] 为获得最佳实践，搜索表达式应进行HTML编码，如上面所示的示例。

### 搜索字段 {#search-fields}

下表列表了可在搜索查询参数中搜索的字段。

| 字段名称 | 描述 |
| ---------- | ----------- |
| folderId | 具有您指定搜索的文件夹ID的文件夹。 |
| folderLocation | 具有指定搜索的文件夹位置的位置。 |
| parentFolderId | 具有指定搜索的父文件夹ID的区段或文件夹。 |
| segmentId | 区段与指定搜索的区段ID匹配。 |
| segmentName | 区段与指定搜索的区段名称匹配。 |
| segmentDescription | 区段与指定搜索的区段描述匹配。 |

### 搜索表达式 {#search-expression}

下表列表了在使用区段搜索API时搜索查询的具体工作方式。

>!![NOTE] 以下示例以非HTML编码格式显示，以提高清晰度。 为获得最佳实践，HTML会对搜索表达式进行编码。

| 示例搜索表达式 | 描述 |
| ------------------------- | ----------- |
| foo | 搜索任何单词。 如果在任何可搜索字段中都找到单词“foo”，则返回结果。 |
| FOO和栏 | 布尔搜索。 如果在任何可搜 **索字段** 中都找到“foo”和“bar”两个词，则返回结果。 |
| FOO或栏 | 布尔搜索。 如果在任何可搜 **索字段** 中都找到单词“foo”或单词“bar”，则返回结果。 |
| FOO NOT栏 | 布尔搜索。 如果找到单词“foo”，但在任何可搜索字段中都找不到单词“bar”，则返回结果。 |
| 名称： FOO和栏 | 布尔搜索。 如果在“名 **称** ”字段中同时找到“foo”和“bar”，则返回结果。 |
| run* | 通配符搜索。 使用星号(*)匹配0个或更多字符，这意味着如果任何可搜索字段的内容包含带有“run”开始的单词，则返回结果。 例如，如果出现“runs”、“running”、“runner”或“runt”等词，则返回结果。 |
| 小卡？ | 通配符搜索。 使用问号(?) 只匹配一个字符，这意味着如果任何可搜索字段的内容都带有“cam”和附加字母开始，则返回结果。 例如，如果出现“camp”或“cams”字样，则返回结果；如果出现“camera”或“campfire”字样，则不返回结果。 |
| “蓝伞” | 词组搜索。 如果任何可搜索字段的内容包含完整短语“blue bulle”，则返回结果。 |
| 蓝色\~ | 模糊搜索。 或者，您可以在代字符(~)后加上一个介于0-2之间的数字来指定编辑距离。 例如，“blue\~1”将返回“blue”、“blues”或“glue”。 模糊搜索 **只能** 应用于术语，而不能应用于短语。 但是，可以在短语中的每个单词的末尾附加代号。 例如，“露营\~入夏”与“夏令营”相匹配。 |
| “酒店机场”\~5 | 近距搜索。 此类搜索用于在文档中查找彼此相近的术语。 例如，短语将 `"hotel airport"~5` 在文档中找到5个单词内的“hotel”和“airport”。 |
| `/a[0-9]+b$/` | 定期表达式搜索。 这种搜索类型根据正斜杠“/”之间的内容查找匹配项，如RegExp类中所述。 例如，要查找包含“motel”或“hotel”的文档，请指定 `/[mh]otel/`。 常规表达式搜索与单词匹配。 |

有关查询语法的更详细文档，请阅读 [Lucene查询语法文档](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。

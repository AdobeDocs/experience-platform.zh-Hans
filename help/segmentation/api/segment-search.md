---
keywords: Experience Platform；分段；分段服务；故障诊断；API；设置；区段；区段；搜索；区段搜索；
title: 区段搜索API端点
topic-legacy: guide
description: 在Adobe Experience Platform Segmentation Service API中，区段搜索用于搜索跨各种数据源包含的字段，并近乎实时地返回它们。 本指南提供了有助于您更好地了解区段搜索的信息，并包含用于使用API执行基本操作的示例API调用。
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 2%

---

# 区段搜索端点

区段搜索用于搜索跨各种数据源包含的字段，并近乎实时地返回它们。

本指南提供了有助于您更好地了解区段搜索的信息，并包含用于使用API执行基本操作的示例API调用。

## 快速入门

本指南中使用的端点是 [!DNL Adobe Experience Platform Segmentation Service] API。 在继续之前，请查看 [入门指南](./getting-started.md) 有关成功调用API所需的重要信息，包括所需的标头以及如何读取示例API调用。

除了快速入门部分中列出的所需标头之外，所有对区段搜索端点的请求都需要以下额外的标头：

- x-ups-search-version:&quot;1.0&quot;

### 跨多个命名空间搜索

此搜索端点可用于跨各种命名空间搜索，从而返回搜索计数结果列表。 可以使用多个参数，并用与号(&amp;)分隔。

**API格式**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| 参数 | 描述 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必需）** 其中{SCHEMA}表示与搜索对象关联的架构类值。 目前，仅 `_xdm.context.segmentdefinition` 支持。 |
| `s={SEARCH_TERM}` | *（可选）* 其中{SEARCH_TERM}表示符合Microsoft [Lucene的搜索语法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 如果未指定搜索词，则与关联的所有记录 `schema.name` 将被返回。 有关更详细的说明，请参阅 [附录](#appendix) 文档的“隐藏主体”。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**响应**

成功响应会返回包含以下信息的HTTP状态200。

```json
{
  "namespaces": [
    {
      "namespace": "AAMTraits",
      "displayName": "AAMTraits",
      "count": 45
    },
    {
      "namespace": "AAMSegments",
      "displayName": "AAMSegment",
      "count": 10
    },
    {
      "namespace": "SegmentsAISegments",
      "displayName": "SegmentSAISegment",
      "count": 3
    }
  ],
  "totalCount": 3,
  "status": {
    "message": "Success"
  }
}
```

### 搜索单个实体

此搜索端点可用于检索指定命名空间内所有全文索引对象的列表。 可以使用多个参数，并用与号(&amp;)分隔。

**API格式**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 参数 | 描述 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必需）** 其中{SCHEMA}包含与搜索对象关联的架构类值。 目前，仅 `_xdm.context.segmentdefinition` 支持。 |
| `namespace={NAMESPACE}` | **（必需）** 其中{NAMESPACE}包含您要在其中搜索的命名空间。 |
| `s={SEARCH_TERM}` | *（可选）* 其中{SEARCH_TERM}包含符合Microsoft [Lucene的搜索语法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 如果未指定搜索词，则与关联的所有记录 `schema.name` 将被返回。 有关更详细的说明，请参阅 [附录](#appendix) 文档的“隐藏主体”。 |
| `entityId={ENTITY_ID}` | *（可选）* 将搜索限制为在指定的文件夹内（使用{ENTITY_ID}指定）。 |
| `limit={LIMIT}` | *（可选）* 其中{LIMIT}表示要返回的搜索结果数。 默认值为 50。 |
| `page={PAGE}` | *（可选）* 其中{PAGE}表示用于对搜索的查询结果进行分页的页码。 请注意，页码开始于 **0**. |


**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**响应**

成功响应会返回HTTP状态200，且结果与搜索查询匹配。

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
| `schema.name={SCHEMA}` | **（必需）** 其中{SCHEMA}包含与搜索对象关联的架构类值。 目前，仅 `_xdm.context.segmentdefinition` 支持。 |
| `namespace={NAMESPACE}` | **（必需）** 其中{NAMESPACE}包含您要在其中搜索的命名空间。 |
| `entityId={ENTITY_ID}` | **（必需）** 要获取相关结构信息的搜索对象的ID，使用{ENTITY_ID}指定。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

现在，您阅读本指南后，可以更好地了解区段搜索的工作方式。

## 附录 {#appendix}

以下部分提供了有关搜索词工作方式的其他信息。 搜索查询的编写方式如下： `s={FieldName}:{SearchExpression}`. 例如，搜索名为AAM或 [!DNL Platform]，则需使用以下搜索查询： `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] 为获得最佳实践，搜索表达式应进行HTML编码，如上面显示的示例。

### 搜索字段 {#search-fields}

下表列出了可在搜索查询参数中搜索的字段。

| 字段名称 | 描述 |
| ---------- | ----------- |
| folderId | 具有您指定搜索的文件夹ID的文件夹。 |
| folderLocation | 具有指定搜索的文件夹位置的位置。 |
| parentFolderId | 具有指定搜索的父文件夹ID的区段或文件夹。 |
| segmentId | 区段与您指定搜索的区段ID匹配。 |
| segmentName | 区段与您指定搜索的区段名称匹配。 |
| segmentDescription | 区段与您指定搜索的区段描述匹配。 |

### 搜索表达式 {#search-expression}

下表列出了使用区段搜索API时搜索查询工作方式的具体说明。

>!![NOTE] 以下示例以非HTML编码格式显示，以提高清晰度。 要获取最佳实践，请HTML对搜索表达式进行编码。

| 示例搜索表达式 | 描述 |
| ------------------------- | ----------- |
| foo | 搜索任何词。 如果在任何可搜索的字段中都找到“foo”一词，则将返回结果。 |
| FOO和Bar | 布尔搜索。 如果 **both** “foo”和“bar”一词可在任何可搜索的字段中找到。 |
| FOO或条 | 布尔搜索。 如果 **e** “foo”或“bar”一词可在任何可搜索的字段中找到。 |
| FOO NOT栏 | 布尔搜索。 如果在任何可搜索的字段中找到单词“foo”，但未找到单词“bar”，则将返回结果。 |
| 名称：FOO和Bar | 布尔搜索。 如果 **both** 在“name”字段中可以找到“foo”和“bar”字样。 |
| run* | 通配符搜索。 使用星号(*)匹配0个或更多字符，这意味着如果任何可搜索字段的内容包含以“run”开头的单词，则将返回结果。 例如，如果显示“runs”、“running”、“runner”或“runt”等字样，则返回结果。 |
| 卡姆？ | 通配符搜索。 使用问号(?) 只匹配一个字符，这意味着如果任何可搜索字段的内容以“cam”和附加字母开头，则将返回结果。 例如，如果显示“camp”或“cams”字样，则返回结果；如果显示“camera”或“campfire”字样，则返回结果。 |
| &quot;蓝伞&quot; | 词组搜索。 如果任何可搜索字段的内容包含完整短语“蓝伞”，则将返回结果。 |
| 蓝色\~ | 模糊搜索。 或者，您可以在颚化符(~)后面放置一个介于0-2之间的数字，以指定编辑距离。 例如，“blue\~1”将返回“blue”、“blues”或“glue”。 模糊搜索 **仅** 应用于术语，而不是短语。 但是，您可以在短语中的每个单词的末尾附加替换符。 例如，“夏令营”与“夏令营”相匹配。 |
| &quot;酒店机场&quot;\~5 | 近距离搜索。 此类搜索用于查找文档中彼此接近的术语。 例如，短语 `"hotel airport"~5` 将在文档中找到“hotel”和“airport”这两个词语的5个词。 |
| `/a[0-9]+b$/` | 正则表达式搜索。 此类搜索根据正斜杠“/”之间的内容查找匹配项，如RegExp类中所述。 例如，要查找包含“motel”或“hotel”的文档，请指定 `/[mh]otel/`. 正则表达式搜索与单个词匹配。 |

有关查询语法的更多详细文档，请阅读 [Lucene查询语法文档](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).

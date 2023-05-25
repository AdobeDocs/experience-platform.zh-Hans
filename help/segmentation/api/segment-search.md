---
keywords: Experience Platform；分段；分段服务；故障排除；API；seg；区段；区段；搜索；区段搜索；
title: 区段搜索API端点
description: 在Adobe Experience Platform Segmentation Service API中，区段搜索用于搜索各种数据源中包含的字段并近乎实时地返回它们。 本指南提供的信息可帮助您更好地了解区段搜索，包括用于使用API执行基本操作的示例API调用。
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 2%

---

# 区段搜索端点

区段搜索用于搜索各种数据源中包含的字段并近乎实时地返回它们。

本指南提供的信息可帮助您更好地了解区段搜索，包括用于使用API执行基本操作的示例API调用。

## 快速入门

本指南中使用的端点是 [!DNL Adobe Experience Platform Segmentation Service] API。 在继续之前，请查看 [快速入门指南](./getting-started.md) 有关成功调用API所需了解的重要信息，包括所需的标头以及如何读取示例API调用。

除了快速入门部分中概述的必需标头之外，对区段搜索端点的所有请求还需要以下附加标头：

- x-ups-search-version： &quot;1.0&quot;

### 跨多个命名空间搜索

此搜索端点可用于跨各种命名空间搜索，并返回搜索计数结果的列表。 可以使用多个参数，以&amp;分隔。

**API格式**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| 参数 | 描述 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必需）** 其中{SCHEMA}表示与搜索对象关联的架构类值。 当前，仅限 `_xdm.context.segmentdefinition` 受支持。 |
| `s={SEARCH_TERM}` | *（可选）* 其中{SEARCH_TERM}表示符合Microsoft实施的查询 [Lucene的搜索语法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 如果未指定搜索词，则与关联的所有记录 `schema.name` 将被返回。 欲知更详细的解释，请参见 [附录](#appendix) 本文档的URL。 |

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

成功的响应会返回包含以下信息的HTTP状态200。

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

此搜索端点可用于检索指定命名空间内所有全文检索索引对象的列表。 可以使用多个参数，以&amp;分隔。

**API格式**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 参数 | 描述 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必需）** 其中{SCHEMA}包含与搜索对象关联的架构类值。 当前，仅限 `_xdm.context.segmentdefinition` 受支持。 |
| `namespace={NAMESPACE}` | **（必需）** 其中{NAMESPACE}包含要搜索的命名空间。 |
| `s={SEARCH_TERM}` | *（可选）* 其中{SEARCH_TERM}包含一个符合Microsoft实施的查询 [Lucene的搜索语法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 如果未指定搜索词，则与关联的所有记录 `schema.name` 将被返回。 欲知更详细的解释，请参见 [附录](#appendix) 本文档的URL。 |
| `entityId={ENTITY_ID}` | *（可选）* 将搜索限制为使用{ENTITY_ID}指定的指定文件夹内的内容。 |
| `limit={LIMIT}` | *（可选）* 其中{LIMIT}表示要返回的搜索结果数。 默认值为 50。 |
| `page={PAGE}` | *（可选）* 其中{PAGE}表示用于分页搜索的查询结果的页码。 请注意，页码开始于 **0**. |


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

成功的响应返回HTTP状态200，且结果与搜索查询匹配。

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

此搜索端点可用于获取有关所请求的搜索对象的结构信息。

**API格式**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 参数 | 描述 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必需）** 其中{SCHEMA}包含与搜索对象关联的架构类值。 当前，仅限 `_xdm.context.segmentdefinition` 受支持。 |
| `namespace={NAMESPACE}` | **（必需）** 其中{NAMESPACE}包含要搜索的命名空间。 |
| `entityId={ENTITY_ID}` | **（必需）** 要获取有关结构信息的搜索对象的ID，使用{ENTITY_ID}指定。 |

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

成功的响应返回HTTP状态200，其中包含有关所请求的搜索对象的详细结构信息。

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

阅读本指南后，您现在可以更好地了解区段搜索的工作方式。

## 附录 {#appendix}

以下部分提供有关搜索词如何工作的更多信息。 搜索查询的编写方式如下： `s={FieldName}:{SearchExpression}`. 例如，搜索名为AAM的区段或 [!DNL Platform]，您可以使用以下搜索查询： `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] 对于最佳实践，搜索表达式应进行HTML编码，如上面的示例。

### 搜索字段 {#search-fields}

下表列出了可在搜索查询参数中搜索的字段。

| 字段名称 | 描述 |
| ---------- | ----------- |
| folderId | 具有指定搜索的文件夹ID的一个或多个文件夹。 |
| 文件夹位置 | 具有指定搜索的文件夹位置的一个或多个位置。 |
| parentFolderId | 具有指定搜索的父文件夹ID的区段或文件夹。 |
| segmentId | 区段与您指定的搜索的区段ID匹配。 |
| segmentName | 区段与您指定的搜索的区段名称匹配。 |
| segmentDescription | 区段与指定搜索的区段描述匹配。 |

### 搜索表达式 {#search-expression}

下表列出了使用区段搜索API时搜索查询的工作方式的详细信息。

>!![NOTE] 为了更加清晰明了，以下示例以非HTML编码格式显示。 为获得最佳实践，HTML可对搜索表达式进行编码。

| 示例搜索表达式 | 描述 |
| ------------------------- | ----------- |
| foo | 搜索任意单词。 如果在任何可搜索字段中找到“foo”一词，则将返回结果。 |
| foo AND bar | 布尔搜索。 这将返回以下情况的结果： **两者** “foo”和“bar”这两个词可以在任何可搜索的字段中找到。 |
| foo OR栏 | 布尔搜索。 这将返回以下情况的结果： **任一** “foo”一词或“bar”一词可在任何可搜索字段中找到。 |
| foo NOT栏 | 布尔搜索。 如果找到单词“foo”，但在任何可搜索字段中都找不到单词“bar”，则将返回结果。 |
| 名称：foo AND栏 | 布尔搜索。 这将返回以下情况的结果： **两者** 单词“foo”和“bar”可在“name”字段中找到。 |
| 运行* | 通配符搜索。 使用星号(*)可匹配0个或更多字符，这意味着如果任何可搜索字段的内容包含以“run”开头的单词，则将返回结果。 例如，如果出现“runs”、“running”、“runner”或“runt”这些词，则将返回结果。 |
| 小卡？ | 通配符搜索。 使用问号(？) 只匹配一个字符，这意味着如果任何可搜索字段的内容以“cam”和附加字母开头，则会返回结果。 例如，如果出现“camp”或“cams”单词，这将返回结果，但是如果出现“camera”或“campfire”单词，将不会返回结果。 |
| “蓝伞” | 短语搜索。 如果任何可搜索字段的内容包含完整的短语“蓝色雨伞”，则将返回结果。 |
| 蓝色\~ | 模糊搜索。 或者，也可以在波状符号(~)后面放置一个介于0-2之间的数字以指定编辑距离。 例如，“blue\~1”将返回“blue”、“blues”或“glue”。 模糊搜索可以 **仅限** 适用于词语，而不是短语。 但是，您可以在短语中每个单词的末尾附加颚化符。 因此，例如，“夏令营”与“夏令营”将匹配。 |
| “机场旅馆”\~5 | 近接搜索。 此类搜索用于查找文档中彼此相邻的术语。 例如，短语 `"hotel airport"~5` 会在文档中找到“hotel”和“airport”这两个词，并且这两个词之间不超过5个字符。 |
| `/a[0-9]+b$/` | 正则表达式搜索。 此类搜索根据正斜杠“/”之间的内容查找匹配项，如RegExp类中所述。 例如，要查找包含“motel”或“hotel”的文档，请指定 `/[mh]otel/`. 正则表达式搜索仅针对单个单词进行匹配。 |

有关查询语法的更多详细文档，请阅读 [Lucene查询语法文档](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).

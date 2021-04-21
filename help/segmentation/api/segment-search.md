---
keywords: Experience Platform；分段；分段服务；故障排除；API；搜索；分段；搜索；分段搜索；
title: 区段搜索API端点
topic-legacy: guide
description: 在Adobe Experience Platform Segmentation Service API中，“区段搜索”用于搜索各个数据源中包含的字段并近乎实时地返回它们。 本指南提供相关信息，帮助您更好地了解区段搜索，并包含使用API执行基本操作的示例API调用。
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 2%

---

# 区段搜索端点

“区段搜索”用于搜索各个数据源中包含的字段，并近乎实时地返回它们。

本指南提供相关信息，帮助您更好地了解区段搜索，并包含使用API执行基本操作的示例API调用。

## 入门指南

本指南中使用的端点是[!DNL Adobe Experience Platform Segmentation Service] API的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)以了解成功调用API所需的重要信息，包括必需的标头以及如何读取示例API调用。

除了入门部分中概述的所需标头之外，所有发往区段搜索端点的请求都需要以下附加标头：

- x-ups-search-version:&quot;1.0&quot;

### 在多个命名空间中搜索

此搜索端点可用于在各种命名空间中搜索，并返回搜索计数结果的列表。 可以使用多个参数，用&amp;符号(&amp;)分隔。

**API格式**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| 参数 | 描述 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必需）其** 中{模式}表示与搜索对象关联的模式类值。当前仅支持`_xdm.context.segmentdefinition`。 |
| `s={SEARCH_TERM}` | *（可选）* 其中{SEARCH_TERM}表示符合Microsoft对Lucene的搜索语法 [的实现的查询](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。如果未指定搜索词，则将返回与`schema.name`关联的所有记录。 本文档的[附录](#appendix)中有更详细的说明。 |

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

成功的响应返回包含以下信息的HTTP状态200。

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

此搜索端点可用于检索指定命名空间内所有全文索引对象的列表。 可以使用多个参数，用&amp;符号(&amp;)分隔。

**API格式**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 参数 | 描述 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必需）** 其中{模式}包含与搜索对象关联的模式类值。当前仅支持`_xdm.context.segmentdefinition`。 |
| `namespace={NAMESPACE}` | **（必需）** 其中{命名空间}包含要在其中搜索的命名空间。 |
| `s={SEARCH_TERM}` | *（可选）* 其中{SEARCH_TERM}包含符合Microsoft实现Lucene搜索语 [法的查询](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。如果未指定搜索词，则将返回与`schema.name`关联的所有记录。 本文档的[附录](#appendix)中有更详细的说明。 |
| `entityId={ENTITY_ID}` | *（可选）* 将搜索限制在指定文件夹内（使用{ENTITY_ID}指定）。 |
| `limit={LIMIT}` | *（可选）* 其中{LIMIT}表示要返回的搜索结果数。默认值为 50。 |
| `page={PAGE}` | *（可选）* 其中{PAGE}表示用于将搜索的查询结果分页的页码。请注意，页码开始位于&#x200B;**0**。 |


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

成功的响应返回HTTP状态200，其结果与搜索查询匹配。

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
| `schema.name={SCHEMA}` | **（必需）** 其中{模式}包含与搜索对象关联的模式类值。当前仅支持`_xdm.context.segmentdefinition`。 |
| `namespace={NAMESPACE}` | **（必需）** 其中{命名空间}包含要在其中搜索的命名空间。 |
| `entityId={ENTITY_ID}` | **（必需）** 要获取有关的结构信息的搜索对象的ID，用{ENTITY_ID}指定。 |

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

以下各节提供了有关搜索词工作原理的更多信息。 搜索查询的编写方式如下：`s={FieldName}:{SearchExpression}`。 因此，例如，要搜索名为AAM或[!DNL Platform]的区段，您应使用以下搜索查询:`s=segmentName:AAM%20OR%20Platform`。

> !![NOTE] 为获得最佳实践，搜索表达式应采用HTML编码，如上例所示。

### 搜索字段{#search-fields}

下表列表了可在搜索查询参数中搜索的字段。

| 字段名称 | 描述 |
| ---------- | ----------- |
| folderId | 具有指定搜索的文件夹ID的文件夹或文件夹。 |
| folderLocation | 具有指定搜索的文件夹位置的位置。 |
| parentFolderId | 具有指定搜索的父文件夹ID的区段或文件夹。 |
| segmentId | 区段与您指定搜索的区段ID匹配。 |
| segmentName | 区段与指定搜索的区段名称匹配。 |
| segmentDescription | 区段与您指定搜索的区段描述匹配。 |

### 搜索表达式{#search-expression}

下表列表了使用区段搜索API时搜索查询的具体工作方式。

>!![NOTE] 以下示例以非HTML编码格式显示，以提高清晰度。为获得最佳实践，HTML可对您的搜索表达式进行编码。

| 示例搜索表达式 | 描述 |
| ------------------------- | ----------- |
| fo | 搜索任何词。 如果在任何可搜索字段中都找到“foo”一词，则返回结果。 |
| FOO和栏 | 布尔搜索。 如果在任何可搜索字段中都找到&#x200B;****&#x200B;单词&quot;foo&quot;和&quot;bar&quot;，则返回结果。 |
| FOO或栏 | 布尔搜索。 如果在任何可搜索字段中都找到&#x200B;****&#x200B;单词“foo”或单词“bar”，则返回结果。 |
| FOO not bar | 布尔搜索。 如果在任何可搜索字段中都找不到单词“foo”，但“bar”，则返回结果。 |
| name:FOO和栏 | 布尔搜索。 如果在“name”字段中找到&#x200B;**两个**&#x200B;单词“foo”和“bar”，则返回结果。 |
| run* | 通配符搜索。 使用星号(*)匹配0个或多个字符，这意味着如果任何可搜索字段的内容包含带有“run”开始的单词，则返回结果。 例如，如果出现“runs”、“running”、“runner”或“runt”等词，则返回结果。 |
| 小卡？ | 通配符搜索。 使用问号(?) 只匹配一个字符，这意味着如果任何可搜索字段的内容开始为“cam”，并且附加了一个字母，则返回结果。 例如，如果显示“camp”或“cams”，则返回结果；如果显示“camera”或“campfire”，则不返回结果。 |
| “蓝伞” | 词组搜索。 如果任何可搜索字段的内容包含完整短语“blue burmal”，则返回结果。 |
| 蓝色\~ | 模糊搜索。 或者，您可以在代字符(~)后加上一个介于0-2之间的数字来指定编辑距离。 例如，“blue\~1”将返回“blue”、“blues”或“gluse”。 模糊搜索只能&#x200B;**对术语应用**，而不能对短语应用。 但是，可以在短语中的每个单词的末尾附加代字符。 比如，“露营\~入夏”与“夏令营”相匹配。 |
| &quot;酒店机场&quot;\~5 | 近距搜索。 此类搜索用于查找文档中彼此接近的词。 例如，短语`"hotel airport"~5`将在文档中找到相互之间5个字内的术语“hotel”和“airport”。 |
| `/a[0-9]+b$/` | 定期表达式搜索。 这类搜索根据正斜杠“/”之间的内容查找匹配项，如RegExp类中所述。 例如，要查找包含&quot;motel&quot;或&quot;hotel&quot;的文档，请指定`/[mh]otel/`。 常规表达式搜索与单词匹配。 |

有关查询语法的更详细文档，请阅读[Lucene查询语法文档](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。

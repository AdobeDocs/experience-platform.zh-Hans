---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；架构注册表；架构注册表；行为；行为；行为；
solution: Experience Platform
title: 行为API端点
description: 架构注册表API中的/behaviors端点允许您检索全局容器中的所有可用行为。
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 2%

---

# 行为端点

在Experience Data Model (XDM)中，行为定义架构描述的数据的性质。 每个XDM类都必须引用一个特定行为，使用该类的所有架构都将继承该行为。 对于Experience Platform中的几乎所有用例，有两种可用行为：

* **[!UICONTROL 记录]**：提供有关主题属性的信息。 主体可以是组织，也可以是个人。
* **[!UICONTROL 时间序列]**：提供记录主体直接或间接执行操作时系统的快照。

>[!NOTE]
>
>Experience Platform中的一些用例需要使用未采用上述任一行为的架构。 对于这些情况，还有第三种“临时”行为可用。 有关详细信息，请参阅有关[创建临时架构](../tutorials/ad-hoc.md)的教程。
>
>有关数据行为如何影响架构合成的更多常规信息，请参阅[架构合成基础知识](../schema/composition.md)指南。

[!DNL Schema Registry] API中的`/behaviors`端点允许您查看`global`容器中的可用行为。

## 快速入门

本指南中使用的终结点是[[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)，以获取相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience Platform API所需的所需标头的重要信息。

## 检索行为列表 {#list}

您可以通过向`/behaviors`端点发出GET请求来检索所有可用行为的列表。

**API格式**

```http
GET /global/behaviors
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**响应**

```json
{
    "results": [
        {
            "$id": "https://ns.adobe.com/xdm/data/record",
            "meta:altId": "_xdm.data.record",
            "version": "1.16.4",
            "title": "Record Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/adhoc",
            "meta:altId": "_xdm.data.adhoc",
            "version": "1.16.4",
            "title": "Ad Hoc Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/time-series",
            "meta:altId": "_xdm.data.time-series",
            "version": "1.16.4",
            "title": "Time-series Schema"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null
    }
}
```

## 查找行为 {#lookup}

通过在`/behaviors`端点的GET请求路径中提供其ID，您可以查找特定行为。

**API格式**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{BEHAVIOR_ID}` | 要查找的行为的`meta:altId`或URL编码的`$id`。 |

{style="table-layout:auto"}

**请求**

以下请求通过在请求路径中提供其`meta:altId`来检索记录行为的详细信息。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**响应**

成功的响应将返回行为的详细信息，包括其版本、描述以及行为提供给采用它的类的属性。

```json
{
    "$id": "https://ns.adobe.com/xdm/data/record",
    "meta:altId": "_xdm.data.record",
    "meta:resourceType": "behaviors",
    "version": "1.16.4",
    "title": "Record Schema",
    "type": "object",
    "description": "Used to indicate the behavior of record data semantic when composed into data schemas.",
    "definitions": {
        "record": {
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "A unique identifier for the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/record",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:xdmType": "object",
    "meta:status": "stable",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:registryMetadata": {
        "repo:createdDate": 1606266789446,
        "repo:lastModifiedDate": 1606266789446,
        "eTag": "2cc114a54949a9668fe2ad046ccece59192e1bfa28f14e5ac7c893acb7820ba2",
        "meta:globalLibVersion": "1.16.4"
    }
}
```

## 后续步骤

本指南介绍了[!DNL Schema Registry] API中`/behaviors`端点的使用。 要了解如何使用API将行为分配给类，请参阅[类端点指南](./classes.md)。

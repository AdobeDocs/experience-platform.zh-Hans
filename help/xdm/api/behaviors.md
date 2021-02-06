---
keywords: Experience Platform；主题；热门主题；API;XDM;XDM系统；体验数据模型；体验数据模型；数据模型；模式注册；模式注册；行为；行为；行为；行为；
solution: Experience Platform
title: 行为API端点
description: 模式注册表API中的/behaviors端点允许您检索全局容器中的所有可用行为。
topic: developer guide
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---


# 行为端点

在体验数据模型(XDM)中，行为定义模式描述的数据性质。 每个XDM类必须引用特定行为，使用该类的所有模式都将继承该行为。 对于平台中的几乎所有用例，有两种可用行为：

* **[!UICONTROL 记录]**:提供有关主题属性的信息。主题可以是组织或个人。
* **[!UICONTROL 时间系列]**:提供记录主体直接或间接采取操作时系统的快照。

>[!NOTE]
>
>在平台中，有些用例要求使用不采用上述任何一种行为的模式。 对于这些情况，有第三种“临时”行为可用。 有关详细信息，请参阅教程中的[创建点对点模式](../tutorials/ad-hoc.md)。
>
>有关模式行为如何影响模式合成的更多一般信息，请参阅[合成基础知识指南](../schema/composition.md)。

[!DNL Schema Registry] API中的`/behaviors`端点允许您视图`global`容器中的可用行为。

## 入门指南

本指南中使用的端点是[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml)的一部分。 在继续之前，请查看[入门指南](./getting-started.md)，了解相关文档的链接、阅读此文档中示例API调用的指南，以及成功调用任何Experience PlatformAPI所需的重要头信息。

## 检索行为列表{#list}

通过向`/behaviors`端点发出列表请求，可以检索所有可用行为的GET。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## 查找行为{#lookup}

您可以通过在GET请求路径中向`/behaviors`端点提供其ID来查找特定行为。

**API格式**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{BEHAVIOR_ID}` | 要查找的行为的`meta:altId`或URL编码的`$id`。 |

**请求**

以下请求通过在请求路径中提供其`meta:altId`来检索记录行为的详细信息。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**响应**

成功的响应会返回行为的详细信息，包括其版本、描述以及行为提供给使用它的类的属性。

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

本指南介绍了在[!DNL Schema Registry] API中使用`/behaviors`端点。 要了解如何使用API将行为指定给类，请参阅[类端点指南](./classes.md)。
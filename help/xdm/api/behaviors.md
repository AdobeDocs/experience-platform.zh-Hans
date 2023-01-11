---
keywords: Experience Platform；主页；热门主题；API;XDM;XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；模式注册表；模式注册表；行为；行为；行为；
solution: Experience Platform
title: 行为API端点
description: 架构注册表API中的/behaviors端点允许您检索全局容器中的所有可用行为。
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 3%

---

# 行为端点

在体验数据模型(XDM)中，行为定义模式描述的数据性质。 每个XDM类必须引用特定行为，采用该类的所有架构都将继承该特定行为。 对于Platform中的几乎所有用例，有两种可用行为：

* **[!UICONTROL 记录]**:提供有关主题属性的信息。 主题可以是组织或个人。
* **[!UICONTROL 时间系列]**:提供记录主体直接或间接执行某项操作时系统的快照。

>[!NOTE]
>
>平台中有一些用例要求使用不采用上述任一行为的架构。 对于这些情况，可以使用第三种“临时”行为。 请参阅 [创建临时架构](../tutorials/ad-hoc.md) 以了解更多信息。
>
>有关数据行为如何影响模式组成的更多常规信息，请参阅 [架构组合基础知识](../schema/composition.md).

的 `/behaviors` 的端点 [!DNL Schema Registry] API允许您在 `global` 容器。

## 快速入门

本指南中使用的端点是 [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). 在继续之前，请查看 [入门指南](./getting-started.md) 有关相关文档的链接，请参阅本文档中的API调用示例指南，以及有关成功调用任何Experience PlatformAPI所需标头的重要信息。

## 检索行为列表 {#list}

通过向 `/behaviors` 端点。

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

您可以查找特定行为，方法是在向GET请求的路径中提供其ID `/behaviors` 端点。

**API格式**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{BEHAVIOR_ID}` | 的 `meta:altId` 或URL编码 `$id` 你想查的行为。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求通过提供其 `meta:altId` 在请求路径中。

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

成功的响应会返回行为的详细信息，包括其版本、描述以及行为提供给使用该行为的类的属性。

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

本指南介绍了 `/behaviors` 的端点 [!DNL Schema Registry] API。 要了解如何使用API将行为分配给类，请参阅 [classes endpoint guide](./classes.md).

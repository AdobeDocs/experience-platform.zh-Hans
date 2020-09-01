---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;lookup;Lookup;get;GET
solution: Experience Platform
title: 查找资源
description: 通过发出模式注册表API中的GET请求，可在请求路径中查找该资源的$id（URL编码的URI）。
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 2%

---


# 查找资源

您可以通过发出GET请求来查找特定资源，该请求 `$id` 在请求路径中包含该资源的（URL编码的URI）。

**API格式**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 资源所在的容器（“全局”或“租户”）。 |
| `{RESOURCE_TYPE}` | 要从中检索的资源的类型 [!DNL Schema Library]。 有效类 `datatypes`型 `mixins`有、 `schemas`和 `classes`。 |
| `{RESOURCE_ID}` | 资源的URL编 `$id` 码的 `meta:altId` URI或URI。 |

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/mixins/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile-person-details \
  -H 'Accept: application/vnd.adobe.xed+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

资源查找请求需 `version` 要包含在“接受”标题中。 以下“接受”标题可用于查找：

| 接受 | 描述 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | 包含和 `$ref` 的 `allOf`原始数据，有标题和说明。 |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 并 `allOf` 且有标题和说明。 |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | 原始数 `$ref` 据， `allOf`无标题或说明。 |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 并解 `allOf` 析，无标题或说明。 |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 和包 `allOf` 含的描述符。 |

>[!NOTE]
>
>如果仅提 `major` 供版本（1、2、3等），注册表将自动返回最 `minor` 新版本（.1、.2、.3等）。

**响应**

成功的响应会返回资源的详细信息。 返回的字段取决于请求中发送的接受标头。 尝试不同的接受标题以比较响应并确定最适合您的用例的标题。

```JSON
{
    "$id": "https://ns.adobe.com/xdm/context/profile-person-details",
    "title": "Profile Person Details",
    "type": "object",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Profile person details including naming, gender etc.",
    "definitions": {
        "profile-person-details": {
            "properties": {
                "person": {
                    "title": "Person",
                    "$ref": "https://ns.adobe.com/xdm/context/person",
                    "description": "An individual actor, contact, or owner.",
                    "meta:xdmField": "xdm:person"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
        },
        {
            "$ref": "#/definitions/profile-person-details"
        }
    ],
    "meta:xdmId": "https://ns.adobe.com/xdm/context/profile-person-details",
    "meta:altId": "_xdm.context.profile-person-details",
    "meta:xdmType": "object",
    "meta:status": "experimental",
    "version": "1",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1551745787442,
        "repo:lastModifiedDate": 1551745787442
    }
}
```

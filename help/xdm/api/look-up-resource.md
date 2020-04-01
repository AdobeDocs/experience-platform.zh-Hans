---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 查找资源
topic: developer guide
translation-type: tm+mt
source-git-commit: 71c73a3899ccdd1c024a811b36c411915a3b14be

---


# 查找资源

您可以通过发出GET请求来查找特定资源，该请求在请 `$id` 求路径中包含该资源的（URL编码的URI）。

**API格式**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 资源所在的容器（“全局”或“租户”）。 |
| `{RESOURCE_TYPE}` | 要从模式库检索的资源类型。 有效类 `datatypes`型有 `mixins`、 `schemas`和 `classes`。 |
| `{RESOURCE_ID}` | 资源的URL编 `$id` 码的URI `meta:altId` 或URI。 |

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
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | 原始数 `$ref` 据包 `allOf`含和，有标题和说明。 |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 并且 `allOf` 有标题和描述。 |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | 原始数 `$ref` 据，无 `allOf`标题或说明。 |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 并且 `allOf` 不会解析标题或说明。 |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 和已 `allOf` 解析的描述符。 |

>[!NOTE] 如果仅提 `major` 供版本（1、2、3等），注册表将自动返回最 `minor` 新版本（.1、.2、.3等）。

**响应**

成功的响应会返回资源的详细信息。 返回的字段取决于请求中发送的接受标题。 尝试不同的接受标题以比较响应并确定最适合您的用例的标题。

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

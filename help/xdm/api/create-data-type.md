---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;datatype;Datatype;data type;Data type;create
solution: Experience Platform
title: 创建数据类型
topic: developer guide
description: '如果您的组织希望以多种方式使用常见的数据结构，您可能希望定义一种数据类型。 数据类型允许多字段结构的一致使用，比混音更灵活，因为通过将它们添加为字段的“类型”，可以将它们包含在模式的任意位置。 '
translation-type: tm+mt
source-git-commit: ed1f2fdac0f9c977d11c867327c084353c1bcd0f
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# 创建数据类型

如果您的组织希望以多种方式使用常见的数据结构，您可能希望定义一种数据类型。 数据类型允许多字段结构的一致使用，比混音更灵活，因为通过将它们添加为字段，可以将它们包含在模式的任 `type` 何位置。

换言之，数据类型允许您定义对象层次结构一次，并以与任何其他标量类型相同的方式在字段中引用它。

**API格式**

```http
POST /tenant/datatypes
```

**请求**

定义数据类型不需要 `meta:extends` 或字 `meta:intendedToExtend` 段，也无需嵌套字段以避免冲突。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the property construction",
        "type":"object",
        "properties": {
          "yearBuilt": {
            "type":"integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCentre": "Shopping Center"
            }
          }
        } 
      }'
```

**响应**

成功的响应会返回HTTP状态201（已创建）和包含新创建数据类型详细信息（包括、和） `$id`的 `meta:altId`有效负荷 `version`。 这三个值是只读的，由指定 [!DNL Schema Registry]。

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the property construction",
    "type": "object",
    "properties": {
        "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed.",
            "meta:xdmType": "int"
        },
        "constructionType": {
            "type": "string",
            "title": "Construction Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "freeStanding",
                "mall",
                "shoppingCenter"
            ],
            "meta:enum": {
                "freeStanding": "Free Standing Building",
                "mall": "Mall Space",
                "shoppingCentre": "Shopping Center"
            },
            "meta:xdmType": "string"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.0",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552087079285,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

执行GET请求以列表租户容器中的所有数据类型现在将包括属性构建数据类型。 您还可以使用URL编码的URI执行查找(GET)请 `$id` 求，以直接视图新数据类型。 请务必在查找请 `version` 求的“接受”标题中包含该标题。

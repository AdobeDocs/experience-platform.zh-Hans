---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 创建数据类型
topic: developer guide
translation-type: tm+mt
source-git-commit: b0d8c8ee4df11d601d8feb122c70a9cd5d7d5b77

---


# 创建数据类型

如果您的组织希望以多种方式使用常见的数据结构，您可能希望定义一种数据类型。 数据类型允许一致地使用多字段结构，比混音更灵活，因为可以通过将它们作为字段添加到模式的任意位置来包 `type` 含它们。

换句话说，数据类型允许您定义对象层次结构一次，并在字段中引用它的方式与任何其他标量类型相同。

**API格式**

```http
POST /tenant/datatypes
```

**请求**

定义数据类型不需要或字 `meta:extends` 段， `meta:intendedToExtend` 也不需要嵌套字段以避免冲突。

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

成功的响应会返回HTTP状态201（已创建）和包含新创建数据类型的详细信息（包括、和）的 `$id`有效 `meta:altId`负荷 `version`。 这三个值是只读的，由模式注册表分配。

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

执行GET请求以列表租户容器中的所有数据类型现在将包括“属性构建”数据类型。 您还可以使用URL编码的 `$id` URI执行查找(GET)请求以直接视图新数据类型。 请务必在查找请 `version` 求的“接受”标题中包含该标题。

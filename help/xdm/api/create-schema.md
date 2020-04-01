---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 创建模式
topic: developer guide
translation-type: tm+mt
source-git-commit: 162316c3b908ffa87d8df4dff72e26ba237993db

---


# 创建模式

可以将模式视为要收录到Experience Platform中的数据的蓝图。 每个模式由类和零个或多个混音组成。 换句话说，您不必添加混音来定义模式，但在大多数情况下，将至少使用一个混音。

模式合成过程首先指定一个类。 该类定义数据（记录或时间序列）的关键行为方面以及描述将要摄取的数据所需的最小字段。

**API格式**

```http
POST /tenant/schemas
```

**请求**

请求必须包含 `allOf` 引用类的 `$id` 属性。 此属性定义模式将实现的“基类”。 在此示例中，基类是先前创建的“属性信息”类。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `allOf > $ref` | 新 `$id` 模式将实现的类的值。 |

**响应**

成功的响应会返回HTTP状态201（已创建）和包含新创建模式的详细信息（包括、和）的 `$id`有效 `meta:altId`负荷 `version`。 这些值是只读的，由模式注册表分配。

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

执行GET请求以列表租户容器中的所有模式现在将包括属性信息模式，或者您可以使用URL编码的 `$id` URI执行查找(GET)请求以直接视图新模式。 请记住，在“接 `version` 受”标题中包含所有查找请求。

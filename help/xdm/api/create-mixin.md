---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 创建混音
topic: developer guide
translation-type: tm+mt
source-git-commit: b2ceac3de73ac622dc885eb388e46e93551f43a8

---


# 创建混音

Mixin是用于描述特定概念的一组字段，如“地址”或“用户档案首选项”。 有许多标准混音可用，或者，当您希望捕获贵组织特有的信息时，您可以定义自己的混音。 每个混音都包 `meta:intendedToExtend` 含一个字段，该字段列表混音所兼容的类。

您可能会发现查看所有可用的混音很有帮助，以熟悉其中包含的字段。 您可以列表(GET)与特定类兼容的所有混音，方法是对“全局”和“租户”容器执行请求，只返回那些“meta:intenedToExtend”字段与您使用的类匹配的混音。 以下示例将返回可与XDM单个用户档案类一起使用的所有混音：

```http
GET /global/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
GET /tenant/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
```

下面的示例API请求在租户容器中创建新的混音。

**API格式**

```http
POST /tenant/mixins
```

**请求**

定义新的混音时，它必须包含一 `meta:intendedToExtend` 个属性，并列出 `$id` 与混音兼容的类。 在此示例中，mixin与您先前定义的Property类兼容。 自定义字段必须嵌套在 `_{TENANT_ID}` （如示例所示）下，以避免与类模式中的其他混音或字段发生任何冲突。 请注意， `propertyConstruction` 该字段是对在上一个调用中创建的数据类型的引用。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Details",
        "description":"Detailed information related to the properties owned and operated by the company.",
        "type":"object",
        "meta:intendedToExtend":["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
              "type":"object",
              "properties": {
                  "propertyName": {
                    "type": "string",
                    "title": "Property Name",
                    "description": "Name of the property"
                  },
                  "propertyCity": {
                    "title": "Property City",
                    "description": "City where the property is located.",
                    "type": "string"
                  },
                  "phoneNumber": {
                    "title": "Phone Number",
                    "description": "Primary phone number for the property.",
                    "type": "string"
                  },
                  "propertyType": {
                    "type": "string",
                    "title": "Property Type",
                    "description": "Type and primary use of property.",
                    "enum": [
                        "retail",
                        "yoga",
                        "fitness"
                    ],
                    "meta:enum": {
                        "retail": "Retail Store",
                        "yoga": "Yoga Studio",
                        "fitness": "Fitness Center"
                    }
                  },
                  "propertyConstruction": {
                    "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
                  }
                }
              }
            }
          }
        },
        "allOf": [
            {
                "$ref": "#/definitions/property"
            }
        ]
}'
```

**响应**

成功的响应会返回HTTP状态201（已创建）和包含新创建混音的详细信息（包括、和） `$id`的 `meta:altId`有效负荷 `version`。 这些值是只读的，由模式注册表分配。

```JSON
{
    "title": "Property Details",
    "description": "Detailed information related to the properties owned and operated by the company.",
    "type": "object",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
    ],
    "definitions": {
        "property": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "propertyName": {
                            "type": "string",
                            "title": "Property Name",
                            "description": "Name of the property",
                            "meta:xdmType": "string"
                        },
                        "propertyCity": {
                            "title": "Property City",
                            "description": "City where the property is located.",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "phoneNumber": {
                            "title": "Phone Number",
                            "description": "Primary phone number for the property.",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "propertyType": {
                            "type": "string",
                            "title": "Property Type",
                            "description": "Type and primary use of property.",
                            "enum": [
                                "retail",
                                "yoga",
                                "fitness"
                            ],
                            "meta:enum": {
                                "retail": "Retail Store",
                                "yoga": "Yoga Studio",
                                "fitness": "Fitness Center"
                            },
                            "meta:xdmType": "string"
                        },
                        "propertyConstruction": {
                            "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/property"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf",
    "version": "1.0",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552088205144,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

执行GET请求以列表租户容器中的所有混音现在将包括“车辆详细信息”混音，或者您可以使用URL编码的 `$id` URI执行查找(GET)请求以直接视图新混音。 请记住，在“接 `version` 受”标题中包含所有查找请求。

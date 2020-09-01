---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;update;Update;patch;PATCH
solution: Experience Platform
title: 更新资源
description: '您可以使用PATCH请求修改或更新租户容器中的资源。 模式注册表支持所有标准JSON修补程序操作，包括添加、删除和替换。 '
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---


# 更新资源

您可以使用PATCH请求修改或更新租户容器中的资源。 支持 [!DNL Schema Registry] 所有标准JSON修补程序操作，包括添加、删除和替换。

有关JSON修补程序（包括可用操作）的详细信息，请参阅官方 [JSON修补程序文档](http://jsonpatch.com/)。

>[!NOTE]
>
>如果要用新值替换整个资源，而不是更新单个字段，请参阅使用 [PUT操作替换资源的文档](replace-resource.md)。

## 向模式添加混音

最常见的PATCH操作之一是向XDM模式添加以前定义的混音，如下例所示。

**API格式**

```http
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{RESOURCE_TYPE}` | 要从中更新的资源类型 [!DNL Schema Library]。 有效类 `datatypes`型 `mixins`有、 `schemas`和 `classes`。 |
| `{RESOURCE_ID}` | 资源的URL编 `$id` 码的 `meta:altId` URI或URI。 |

**请求**

使用PATCH操作，您可以更新模式以包含在先前创建的混音中定义的字段。 为此，必须使用PATCH的URI或URL编码的URI `meta:altId` 对模式执行 `$id` 请求。

请求主体包括`op`要执行的操作(`path`)、要执行操作的位置()以及要包括在操作中的信息(`value`)。 在此示例中，mixin的值 `$id` 将添加到目标模式的 `meta:extends` 和 `allOf` 字段中。

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "add", "path": "/meta:extends/-", "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"},
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"}}
      ]'
```

**响应**

响应显示两个操作都成功执行。 混音已 `$id` 添加到数组 `meta:extends` 中，现在在数组中显示对混`$ref`音的引用( `$id``allOf` )。

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## 更新资源的各个字段

您还可以发送对PATCH注册表资源中的各个字段进行多次更改的模式请求。

**API格式**

```SHELL
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{RESOURCE_TYPE}` | 要从中更新的资源类型 [!DNL Schema Library]。 有效类 `datatypes`型 `mixins`有、 `schemas`和 `classes`。 |
| `{RESOURCE_ID}` | 资源的URL编 `$id` 码的 `meta:altId` URI或URI。 |

**请求**

请求主体包括更新`op`混音所需的操作`path`()、位置(`value`)和信息()。 此请求更新“属性详细信息”混音，以删除“propertyCity”字段并添加新的“propertyAddress”字段，该字段引用包含地址信息的标准数据类型。 它还添加一个新的“emailAddress”字段，该字段引用带有电子邮件信息的标准数据类型。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
          { "op": "remove", "path": "/definitions/vehicles/properties/_{TENANT_ID}/properties/propertyCity"},
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyAddress", "value":
            {
              "title": "Property Address",
              "description": "Address of the Property",
              "$ref": "https://ns.adobe.com/xdm/common/address"
            } 
          },
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/emailAddress", "value":
            {
              "title": "Property Email Address",
              "description": "Email address of the Property",
              "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
            } 
          },
      ]'
```

**响应**

成功的响应表明操作已成功完成，因为新字段存在且“propertyCity”字段已被删除。

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
                        },
                        "propertyAddress": {
                            "title": "Property Address",
                            "description": "Address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/common/address"
                        },
                        "emailAddress": {
                            "title": "Property Email Address",
                            "description": "Email address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
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
    "version": "1.1",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552089776535,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

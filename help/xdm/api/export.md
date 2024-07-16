---
title: 导出API端点
description: 架构注册表API中的/export端点允许您在沙盒之间共享XDM资源。
exl-id: 1dcbfa59-af98-4db5-b6f4-f848e5bf5e81
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---

# 导出端点

[!DNL Schema Library]中的所有资源都包含在Adobe Experience Platform中的特定沙盒中。 在某些情况下，您可能希望在沙盒和组织之间共享Experience Data Model (XDM)资源。 [!DNL Schema Registry] API中的`/rpc/export`端点允许您为[!DNL Schema Library]中的任何架构、架构字段组或数据类型生成导出有效负载，然后使用该有效负载通过[`/rpc/import`端点](./import.md)将该资源（以及所有依赖的资源）导入目标沙盒和组织。

## 快速入门

`/rpc/export`终结点是[[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)，以获取相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience PlatformAPI所需的所需标头的重要信息。

`/rpc/export`端点是[!DNL Schema Registry]支持的远程过程调用(RPC)的一部分。 与[!DNL Schema Registry] API中的其他端点不同，RPC端点不需要`Accept`或`Content-Type`等其他标头，也不使用`CONTAINER_ID`。 相反，他们必须使用`/rpc`命名空间，如下面的API调用中所示。

## 为资源生成导出有效负载 {#export}

对于[!DNL Schema Library]中的任何现有架构、字段组或数据类型，您可以通过向`/export`端点发出GET请求来生成导出有效负载，并在路径中提供资源的ID。

**API格式**

```http
GET /rpc/export/{RESOURCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{RESOURCE_ID}` | 要导出的XDM资源的`meta:altId`或URL编码的`$id`。 |

{style="table-layout:auto"}

**请求**

以下请求检索`Restaurant`字段组的导出有效负载。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/export/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

**响应**

成功的响应会返回一个对象数组，这些对象表示目标XDM资源及其所有依赖资源。 在此示例中，数组中的第一个对象是`Restaurant`字段组采用的租户创建的`Property`数据类型，而第二个对象是`Restaurant`字段组本身。 然后，此有效负载可用于[将资源](#import)导入到其他沙盒或组织中。

请注意，该资源的租户ID的所有实例都将被替换为`<XDM_TENANTID_PLACEHOLDER>`。 这允许架构注册表根据在后续导入调用中发送资源的位置，自动将正确的租户ID应用于资源。

```json
[
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.datatypes.fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:resourceType": "datatypes",
        "version": "1.0",
        "title": "Property",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "properties": {
                    "propertyId": {
                        "title": "Property ID",
                        "description": "ID for a company-owned property.",
                        "type": "string",
                        "isRequired": false,
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.propertyId",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    },
                    "jurisdiction": {
                        "title": "Jurisdiction",
                        "description": "",
                        "type": "string",
                        "isRequired": false,
                        "enum": [
                            "NA",
                            "UK",
                            "EU"
                        ],
                        "meta:enum": {
                            "NA": "North America",
                            "UK": "United Kingdom",
                            "EU": "European Union"
                        },
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.jurisdiction",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    }
                }
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    },
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:resourceType": "mixins",
        "version": "1.0",
        "title": "Restaurant",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "type": "object",
                "properties": {
                    "_<XDM_TENANTID_PLACEHOLDER>": {
                        "type": "object",
                        "properties": {
                            "capacity": {
                                "title": "Capacity",
                                "description": "Restaurant capacity",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "kitchen": {
                                "title": "Kitchen Style",
                                "description": "Style of kitchen",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "rating": {
                                "title": "Rating",
                                "description": "",
                                "type": "integer",
                                "isRequired": false,
                                "meta:xdmType": "int"
                            },
                            "property": {
                                "title": "Property",
                                "description": "",
                                "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
                                "type": "object",
                                "meta:xdmType": "object"
                            }
                        },
                        "meta:xdmType": "object"
                    }
                },
                "meta:xdmType": "object"
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [],
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    }
]
```

## 导入资源 {#import}

从CSV文件生成导出有效负载后，您可以将该有效负载发送到`/rpc/import`端点以生成架构。

有关如何从导出有效负载生成架构的详细信息，请参阅[导入终结点指南](./import.md)。

---
keywords: Experience Platform；主页；热门主题；api;API;XDM;XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；导出；导入；rpc;
solution: Experience Platform
title: 导出/导入API端点
description: 模式 Registry API中的/export和/import端点允许您在IMS组织和沙箱之间共享XDM资源。
topic-legacy: developer guide
exl-id: 33b62f75-2670-42f4-9aac-fa1540cd7d4a
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 1%

---

# 导出/导入终结点

[!DNL Schema Library]中的所有资源都包含在IMS组织内的特定沙箱中。 在某些情况下，您可能希望在沙箱和IMS组织之间共享体验数据模型(XDM)资源。 [!DNL Schema Registry] API提供两个端点，允许您为[!DNL  Schema Library]中的任何模式、模式字段组或数据类型生成导出有效负荷，然后使用该有效负荷将该资源（及所有相关资源）导入目标沙箱和IMS组织。

## 入门指南

本指南中使用的端点是[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)的一部分。 在继续之前，请查阅[快速入门指南](./getting-started.md)，了解相关文档的链接、阅读此文档中示例API调用的指南以及成功调用任何Experience PlatformAPI所需标头的重要信息。

导出/导入端点是[!DNL Schema Registry]支持的远程过程调用(RPC)的一部分。 与[!DNL Schema Registry] API中的其他端点不同，RPC端点不需要额外的标头，如`Accept`或`Content-Type`，也不使用`CONTAINER_ID`。 相反，他们必须使用`/rpc`命名空间，如以下API调用中所示。

## 检索资源{#export}的导出负载

对于[!DNL Schema Library]中的任何现有模式、字段组或数据类型，您可以通过向`/export`端点发出GET请求，提供路径中资源的ID来生成导出负载。

**API格式**

```http
GET /rpc/export/{RESOURCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{RESOURCE_ID}` | 要导出的XDM资源的`meta:altId`或URL编码的`$id`。 |

**请求**

以下请求将检索`Restaurant`字段组的导出有效负荷。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/export/_{TENANT_ID}.fieldgroups.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

**响应**

成功的响应返回一组对象，这些对象表示目标 XDM资源及其所有相关资源。 在此示例中，数组中的第一个对象是由租户创建的`Restaurant`字段组使用的`Property`数据类型，而第二个对象是`Restaurant`字段组本身。 然后，此负载可用于[将资源](#import)导入到其他沙箱或IMS组织中。

请注意，资源的租户ID的所有实例都替换为`<XDM_TENANTID_PLACEHOLDER>`。 这样，模式注册表就可以根据资源在后续导入调用中的发送位置，自动将正确的租户ID应用到资源。

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
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/fieldgroups/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.fieldgroups.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:resourceType": "fieldgroups",
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

## 导入资源{#import}

一旦您为XDM资源生成了[导出负载](#export)，您就可以在向`/import`端点的POST请求中使用该负载，将该资源导入到目标IMS组织和沙箱中。

**API格式**

```http
POST /rpc/import
```

**请求**

以下请求采用上一个[导出示例](#export)中返回的有效负荷，以将`Restaurant`字段组导入新的IMS组织和沙箱中，具体由`x-gw-ims-org-id`和`x-sandbox-name`头确定。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/import \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
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
          "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/fieldgroups/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
          "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.fieldgroups.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
          "meta:resourceType": "fieldgroups",
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
          "meta:intendedToExtend": [
            
          ],
          "meta:xdmType": "object",
          "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
          "meta:sandboxType": "production"
        }
      ]'
```

**响应**

成功的响应会返回导入资源的列表，并应用相应的租户ID和IMS组织值。

```json
[
    {
        "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:altId": "_{TENANT_ID}.datatypes.fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
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
                            "path": "{}._{TENANT_ID}{}.property{}.propertyId",
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
                            "path": "{}._{TENANT_ID}{}.property{}.jurisdiction",
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
        "refs": [],
        "imsOrg": "{IMS_ORG}",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:xdmType": "object",
        "meta:registryMetadata": {
            "repo:createdDate": 1606250624257,
            "repo:lastModifiedDate": 1606250624257,
            "xdm:createdClientId": "{CLIENT_ID}",
            "xdm:lastModifiedClientId": "{CLIENT_ID}",
            "xdm:createdUserId": "{USER_ID}",
            "xdm:lastModifiedUserId": "{USER_ID}",
            "eTag": "9dadfaf8168af30eae1a745de95eace760680cfc9a69bcc938f68fe3caf57317",
            "meta:globalLibVersion": "1.16.3"
        },
        "meta:containerId": "tenant",
        "meta:sandboxId": "52c8dbe0-ced2-11e9-a524-cd79ba95ea3a",
        "meta:sandboxType": "production",
        "meta:tenantNamespace": "_{TENANT_ID}"
    },
    {
        "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:altId": "_{TENANT_ID}.fieldgroups.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:resourceType": "fieldgroups",
        "version": "1.0",
        "title": "Restaurant",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "type": "object",
                "properties": {
                    "_{TENANT_ID}": {
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
                                "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
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
        "refs": [
            "https://ns.adobe.com/{TENANT_ID}/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495"
        ],
        "imsOrg": "{IMS_ORG}",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [],
        "meta:xdmType": "object",
        "meta:registryMetadata": {
            "repo:createdDate": 1606250624357,
            "repo:lastModifiedDate": 1606250624357,
            "xdm:createdClientId": "{CLIENT_ID}",
            "xdm:lastModifiedClientId": "{CLIENT_ID}",
            "xdm:createdUserId": "{USER_ID}",
            "xdm:lastModifiedUserId": "{USER_ID}",
            "eTag": "5a5401ba8e6845b2f42d330002331e6e96c031c4e228f860423a3d5cd3598b40",
            "meta:globalLibVersion": "1.16.3"
        },
        "meta:containerId": "tenant",
        "meta:sandboxId": "52c8dbe0-ced2-11e9-a524-cd79ba95ea3a",
        "meta:sandboxType": "production",
        "meta:tenantNamespace": "_{TENANT_ID}"
    }
]
```

---
title: CSV模板到架构转换API端点
description: 架构注册表API中的/rpc/csv2schema端点允许您使用CSV模板自动创建Experience Data Model (XDM)架构。
exl-id: cf08774a-db94-4ea1-a22e-bb06385f8d0e
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 5%

---

# CSV模板到架构转换API端点

[!DNL Schema Registry] API中的`/rpc/csv2schema`端点允许您使用CSV文件作为模板自动创建体验数据模型(XDM)架构。 使用此端点，您可以创建模板以批量导入架构字段，并减少手动API或UI工作。

## 快速入门

`/rpc/csv2schema`终结点是[[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)，以获取相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Adobe Experience Platform API所需的所需标头的重要信息。

`/rpc/csv2schema`端点是[!DNL Schema Registry]支持的远程过程调用(RPC)的一部分。 与[!DNL Schema Registry] API中的其他端点不同，RPC端点不需要`Accept`或`Content-Type`等其他标头，也不使用`CONTAINER_ID`。 相反，他们必须使用`/rpc`命名空间，如下面的API调用中所示。

## CSV文件要求

要使用此端点，您必须首先创建一个CSV文件，该文件具有相应的列标题和相应的值。 某些列是必需的，而其余列是可选的。 下表描述了这些列及其在模式构建中的作用。

| CSV标头位置 | CSV标头名称 | 必需/可选 | 描述 |
| --- | --- | --- | --- |
| 1 | `isIgnored` | 可选 | 如果包含字段并设置为`true`，则表示该字段未准备好上传API，应当忽略。 |
| 2 | `isCustom` | 必需 | 指示字段是否为自定义字段。 |
| 3 | `fieldGroupId` | 可选 | 自定义字段应关联的字段组的ID。 |
| 4 | `fieldGroupName` | （请参阅描述） | 要与此字段关联的字段组的名称。对于未扩展现有标准字段的自定义字段，<br><br>可选。 如果留空，系统将自动指定名称。<br><br>扩展标准字段组的标准字段或自定义字段必须填写，用于查询`fieldGroupId`。 |
| 5 | `fieldPath` | 必需 | 字段的完整XED点表示法路径。 要包含标准字段组中的所有字段（如`fieldGroupName`下所示），请将该值设置为`ALL`。 |
| 6 | `displayName` | 可选 | 字段的标题或友好显示名称。 也可以是标题的别名（如果存在）。 |
| 7 | `fieldDescription` | 可选 | 字段的描述。 也可以是说明的别名（如果存在）。 |
| 8 | `dataType` | （请参阅描述） | 指示字段的[基本数据类型](../schema/field-constraints.md#basic-types)。 所有自定义字段均需要填写此字段。<br><br>如果将`dataType`设置为`object`，则还需要为同一行定义`properties`或`$ref`，但不能同时为这两行定义。 |
| 9 | `isRequired` | 可选 | 指示字段是否为数据摄取所必需。 |
| 10 | `isArray` | 可选 | 指示字段是否为所指示`dataType`的数组。 |
| 11 | `isIdentity` | 可选 | 指示字段是否为标识字段。 |
| 12 | `identityNamespace` | 如果`isIdentity`为true则必需 | 标识字段的[标识命名空间](../../identity-service/features/namespaces.md)。 |
| 13 | `isPrimaryIdentity` | 可选 | 指示字段是否为架构的主要标识。 |
| 14 | `minimum` | 可选 | （仅适用于数字字段）字段的最小值。 |
| 15 | `maximum` | 可选 | （仅适用于数字字段）字段的最大值。 |
| 16 | `enum` | 可选 | 字段的枚举值列表，以数组表示（例如`[value1,value2,value3]`）。 |
| 17 | `stringPattern` | 可选 | （仅适用于字符串字段）一种正则表达式模式，字符串值必须匹配该模式才能在数据引入期间通过验证。 |
| 18 | `format` | 可选 | （仅适用于字符串字段）字符串字段的格式。 |
| 19 | `minLength` | 可选 | （仅适用于字符串字段）字符串字段的最小长度。 |
| 20 | `maxLength` | 可选 | （仅适用于字符串字段）字符串字段的最大长度。 |
| 21 | `properties` | （请参阅描述） | 如果`dataType`设置为`object`并且未定义`$ref`，则此为必填字段。 这会将对象正文定义为JSON字符串（例如`{"myField": {"type": "string"}}`）。 |
| 22 | `$ref` | （请参阅描述） | 如果`dataType`设置为`object`并且未定义`properties`，则此为必填字段。 这会为对象类型（例如`https://ns.adobe.com/xdm/context/person`）定义引用对象的`$id`。 |
| 23 | `comment` | 可选 | 当`isIgnored`设置为`true`时，此列用于提供架构的标头信息。 |

{style="table-layout:auto"}

请参阅以下[CSV模板](../assets/sample-csv-template.csv)，确定CSV文件的格式设置。

## 从CSV文件创建导出有效负载

设置CSV模板后，您可以将该文件发送到`/rpc/csv2schema`端点并将其转换为导出有效负载。

**API格式**

```http
POST /rpc/csv2schema
```

**请求**

请求有效负载必须使用表单数据作为其格式。 必填表单字段如下所示。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/csv2schema \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'csv-file=@"/Users/userName/Documents/sample-csv-template.csv"' \
  -F 'schema-class-id="https://ns.adobe.com/xdm/context/profile"' \
  -F 'schema-name="Example Schema"' \
  -F 'schema-description="Example schema description."'
```

| 属性 | 描述 |
| --- | --- |
| `csv-file` | 存储在本地计算机上的CSV模板的路径。 |
| `schema-class-id` | 此架构将采用的XDM [类](../schema/composition.md#class)的`$id`。 |
| `schema-name` | 架构的显示名称。 |
| `schema-description` | 架构的描述。 |

**响应**

成功的响应将返回从CSV文件生成的导出有效负载。 有效负载采用数组的形式，每个数组项都是一个对象，表示架构的依赖XDM组件。 选择以下部分可查看从CSV文件生成的导出有效负载的完整示例。

+++ 示例响应有效负载

```json
[
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "description": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "required": [
            "_ddgxdmint"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField1": {
                        "type": "string",
                        "title": "my custom field1",
                        "description": "Sample custom field1"
                    },
                    "customField2": {
                        "properties": {
                            "customerField22": {
                                "type": "string",
                                "title": "my custom field22",
                                "description": "Sample custom field22"
                            }
                        },
                        "type": "object",
                        "required": [
                            "customerField22"
                        ]
                    },
                    "customField3": {
                        "type": "number",
                        "title": "my custom field3",
                        "description": "Sample custom field3",
                        "minimum": 0,
                        "maximum": 10
                    },
                    "customField4": {
                        "type": "string",
                        "title": "my custom field4",
                        "description": "Sample custom field4",
                        "enum": [
                            "one",
                            "two",
                            "three"
                        ]
                    },
                    "customField5": {
                        "type": "array",
                        "title": "my custom field5",
                        "description": "Sample custom field5",
                        "items": {
                            "type": "string"
                        }
                    },
                    "customField6": {
                        "type": "string",
                        "title": "my custom field6",
                        "description": "Sample custom field6",
                        "format": "date"
                    }
                },
                "type": "object",
                "required": [
                    "customField1",
                    "customField2"
                ]
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "SampleFieldGroup",
        "description": "Generated field group 7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField7": {
                        "type": "object",
                        "title": "my custom field7",
                        "description": "Sample custom field7",
                        "properties": {
                            "myField": {
                                "type": "string"
                            }
                        }
                    },
                    "customField8": {
                        "type": "array",
                        "title": "my custom field8",
                        "description": "Sample custom field8",
                        "items": {
                            "type": "object",
                            "$ref": "https://ns.adobe.com/xdm/context/person"
                        }
                    }
                },
                "type": "object"
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Demographic Details:Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "description": "Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile-person-details"
        ],
        "allOf": [
            {
                "properties": {
                    "person": {
                        "properties": {
                            "name": {
                                "properties": {
                                    "_ddgxdmint": {
                                        "properties": {
                                            "nickName": {
                                                "type": "string"
                                            }
                                        },
                                        "type": "object",
                                        "required": [
                                            "nickName"
                                        ]
                                    }
                                },
                                "type": "object",
                                "required": [
                                    "_ddgxdmint"
                                ]
                            }
                        },
                        "type": "object",
                        "required": [
                            "name"
                        ]
                    }
                },
                "required": [
                    "person"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Loyalty Details:Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "description": "Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
        ],
        "allOf": [
            {
                "properties": {
                    "loyalty": {
                        "properties": {
                            "_ddgxdmint": {
                                "properties": {
                                    "joinDate": {
                                        "type": "string"
                                    }
                                },
                                "type": "object"
                            }
                        },
                        "type": "object"
                    }
                }
            },
            {
                "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "schemas",
        "title": "My Sample Schema",
        "description": "My Sample Schema",
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
                "meta:refProperty": [
                    "/person/name/firstName",
                    "/person/name/lastName",
                    "/person/name/_ddgxdmint/nickName"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241"
            }
        ]
    },
    {
        "@type": "xdm:alternateDisplayInfo",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/person/name/firstName",
        "xdm:title": {
            "en_us": "My first name"
        }
    },
    {
        "@type": "xdm:descriptorIdentity",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_ddgxdmint/customField1",
        "xdm:namespace": "email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": true
    }
]
```

+++

## 导入架构有效负载

从CSV文件生成导出有效负载后，您可以将该有效负载发送到`/rpc/import`端点以生成架构。

有关如何从导出有效负载生成架构的详细信息，请参阅[导入终结点指南](./import.md)。

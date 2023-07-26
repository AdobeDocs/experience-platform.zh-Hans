---
title: 使用流服务API为SAP Commerce创建源连接和数据流
description: 了解如何使用Flow Service API创建源连接和数据流以将SAP Commerce数据引入Experience Platform。
badge: Beta
source-git-commit: a848ea11e388678ade780fd81ef3ff6a3477b741
workflow-type: tm+mt
source-wordcount: '2358'
ht-degree: 1%

---

# 为以下对象创建源连接和数据流 [!DNL SAP Commerce] 使用流服务API

>[!NOTE]
>
>此 [!DNL SAP Commerce] 源为测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记源代码的更多信息。

以下教程将指导您完成创建 [!DNL SAP Commerce] 源连接和要引入的数据流 [[!DNL SAP] 订阅帐单](https://www.sap.com/products/financial-management/subscription-billing.html) 使用将联系人和客户数据发送到Adobe Experience Platform [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供成功连接时需要了解的其他信息 [!DNL SAP Commerce] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了连接 [!DNL SAP Commerce] 要Experience Platform，必须提供以下连接属性的值：

| 凭据 | 描述 |
| --- | --- |
| `clientId` | 的值 `clientId` 服务密钥。 |
| `clientSecret` | 的值 `clientSecret` 服务密钥。 |
| `tokenEndpoint` | 的值 `url` 从服务密钥中，它将类似于 `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| `region` | 您的数据中心位置。 此区域出现在 `url` 且其值类似于 `eu10` 或 `us10`. 例如，如果 `url` 是 `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`，然后您需要 `eu10`. |

有关这些凭证的更多信息，请参阅 [[!DNL SAP Commerce] 文档](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/c5fcaf96daff4c7a8520188e4d8a1843.html).

## 连接 [!DNL SAP Commerce] 到平台，使用 [!DNL Flow Service] API

下面概述了进行身份验证所需的步骤 [!DNL SAP Commerce] 创建源连接，然后创建数据流以将您的帐户和联系人数据引入Experience Platform。

### 创建基本连接 {#base-connection}

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL SAP Commerce] 作为请求正文一部分的身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求为创建基本连接 [!DNL SAP Commerce]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce base connection",
      "description": "Authenticated base connection for SAP Commerce",
      "connectionSpec": {
          "id": "d8ee38de-7ae9-4058-9610-c79ce75f8e92",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params": {
              "region": "{REGION}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
              "tokenEndpoint": "{TOKEN_ENDPOINT}"
          }
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 基础连接的名称。 确保基本连接的名称是描述性的，因为您可以使用此名称查找有关基本连接的信息。 |
| `description` | 可包含的可选值，用于提供有关基本连接的更多信息。 |
| `connectionSpec.id` | 源的连接规范ID。 在您的源注册并批准后，可通过以下方式检索此ID： [!DNL Flow Service] API。 |
| `auth.specName` | 用于向Platform验证源的身份验证类型。 |
| `auth.params.region` | 您的数据中心位置。 此区域出现在 `url` 且其值类似于 `eu10` 或 `us10`. 例如，如果 `url` 是 `https://subscriptionbilling.authentication.eu10.hana.ondemand.com` 您将需要 `eu10`. |
| `auth.params.clientId` | 的值 `clientId` 服务密钥。 |
| `auth.params.clientSecret` | 的值 `clientSecret` 服务密钥。 |
| `auth.params.tokenEndpoint` | 的值 `url` 从服务密钥中，它将类似于 `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |

**响应**

成功的响应会返回新创建的基本连接，包括其唯一连接标识符(`id`)。 在下一步中浏览源的文件结构和内容时，需要此ID。

```json
{
     "id": "5f6d6022-3f64-400c-ba01-d4010de2d8ff",
     "etag": "\"f8018de1-0000-0200-0000-6482d7210000\""
}
```

### 浏览您的源 {#explore}

获得基本连接ID后，您现在可以通过向以下对象执行GET请求来探索源数据的内容和结构： `/connections` 端点，同时提供您的基本连接ID作为查询参数。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

执行GET请求以浏览源的文件结构和内容时，必须包括下表列出的查询参数：

| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 上一步中生成的基本连接ID。 |
| `objectType=rest` | 您希望探索的对象类型。 目前，此值始终设置为 `rest`. |
| `{OBJECT}` | 只有在查看特定目录时才需要此参数。 其值表示您希望浏览的目录的路径。 对于此源，值将为 `json`. |
| `fileType=json` | 您要带到Platform的文件类型。 目前， `json` 是唯一支持的文件类型。 |
| `{PREVIEW}` | 一个布尔值，定义连接的内容是否支持预览。 |
| `{SOURCE_PARAMS}` | 为要带到Platform的源文件定义参数。 检索接受的格式类型 `{SOURCE_PARAMS}`中，您必须以base64为单位编码整个字符串。 <br> [!DNL SAP Commerce] 支持多个API。 根据您要使用的对象类型，传递以下任一项： <ul><li>`customers`</li><li>`contacts`</li></ul> |

此 [!DNL SAP Commerce] 源支持多个API。 根据您利用请求发送的对象类型，如下所示：

>[!NOTE]
>
>一些响应记录已被截断，以便更好地呈现。

>[!BEGINTABS]

>[!TAB 客户]

+++请求

对象 [!DNL SAP Commerce] 客户API值 `{SOURCE_PARAMS}` 传递为 `{"object_type":"customers"}`. 在base64中进行编码时，它等于 `eyJvYmplY3RfdHlwZSI6ImN1c3RvbWVycyJ9` 如下所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImN1c3RvbWVycyJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++响应

成功的响应会返回类似于以下内容的JSON结构：

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "personalInfo": {
                "type": "object",
                "properties": {
                    "firstName": {
                        "type": "string"
                    },
                    "lastName": {
                        "type": "string"
                    }
                }
            },
            "addresses": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "country": {
                            "type": "string"
                        },
                        "isDefault": {
                            "type": "boolean"
                        },
                        "phone": {
                            "type": "string"
                        },
                        "city": {
                            "type": "string"
                        },
                        "street": {
                            "type": "string"
                        },
                        "postalCode": {
                            "type": "string"
                        },
                        "addressUUID": {
                            "type": "string"
                        },
                        "houseNumber": {
                            "type": "string"
                        },
                        "additionalAddressInfo": {
                            "type": "string"
                        },
                        "state": {
                            "type": "string"
                        },
                        "email": {
                            "type": "string"
                        }
                    }
                }
            },
            "customerNumber": {
                "type": "string"
            },
            "corporateInfo": {
                "type": "object",
                "properties": {}
            },
            "customReferences": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {}
                }
            },
            "externalObjectReferences": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "externalSystemId": {
                            "type": "string"
                        },
                        "externalId": {
                            "type": "string"
                        },
                        "externalIdTypeCode": {
                            "type": "string"
                        }
                    }
                }
            },
            "createdAt": {
                "type": "string"
            },
            "customerType": {
                "type": "string"
            },
            "markets": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "country": {
                            "type": "string"
                        },
                        "salesArea": {
                            "type": "object",
                            "properties": {
                                "division": {
                                    "type": "string"
                                },
                                "distributionChannel": {
                                    "type": "string"
                                },
                                "salesOrganization": {
                                    "type": "string"
                                }
                            }
                        },
                        "priceType": {
                            "type": "string"
                        },
                        "active": {
                            "type": "boolean"
                        },
                        "currency": {
                            "type": "string"
                        },
                        "marketId": {
                            "type": "string"
                        }
                    }
                }
            },
            "createdBy": {
                "type": "string"
            },
            "changedBy": {
                "type": "string"
            },
            "changedAt": {
                "type": "string"
            },
            "defaultAddress": {
                "type": "object",
                "properties": {
                    "country": {
                        "type": "string"
                    },
                    "isDefault": {
                        "type": "boolean"
                    },
                    "phone": {
                        "type": "string"
                    },
                    "city": {
                        "type": "string"
                    },
                    "street": {
                        "type": "string"
                    },
                    "postalCode": {
                        "type": "string"
                    },
                    "addressUUID": {
                        "type": "string"
                    },
                    "houseNumber": {
                        "type": "string"
                    },
                    "additionalAddressInfo": {
                        "type": "string"
                    },
                    "state": {
                        "type": "string"
                    },
                    "email": {
                        "type": "string"
                    }
                }
            }
        }
    },
    "data": [
        {
            "personalInfo": {
                "firstName": "Test 1",
                "lastName": "User 1"
            },
            "addresses": [
                {
                    "email": "user1@test.com",
                    "phone": "123456890",
                    "houseNumber": "123",
                    "city": "New Orleans",
                    "state": "LA",
                    "postalCode": "700089",
                    "country": "US",
                    "addressUUID": "ff871221-ab48-435c-b1f5-903db1c3cea2",
                    "isDefault": true
                }
            ],
            "customerNumber": "2863620303",
            "externalObjectReferences": [
                {
                    "externalSystemId": "t090000",
                    "externalId": "1324566",
                    "externalIdTypeCode": "201"
                }
            ],
            "createdAt": "2023-05-31T06:39:28.499Z",
            "customerType": "INDIVIDUAL",
            "markets": [
                {
                    "marketId": "US",
                    "active": true,
                    "currency": "USD",
                    "country": "US",
                    "salesArea": {
                        "salesOrganization": "SE10",
                        "distributionChannel": "00",
                        "division": "00"
                    },
                    "priceType": "Net"
                }
            ],
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedAt": "2023-05-31T06:39:28.499Z",
            "defaultAddress": {
                "email": "user1@test.com",
                "phone": "123456890",
                "houseNumber": "123",
                "city": "New Orleans",
                "state": "LA",
                "postalCode": "700089",
                "country": "US",
                "addressUUID": "ff871221-ab48-435c-b1f5-903db1c3cea2",
                "isDefault": true
            }
        },
        {
            "personalInfo": {
                "firstName": "Test 2",
                "lastName": "User 2"
            },
            "addresses": [
                {
                    "email": "user2@test.com",
                    "phone": "1234567899",
                    "houseNumber": "876",
                    "city": "New Orleans",
                    "state": "LA",
                    "postalCode": "700089",
                    "country": "US",
                    "addressUUID": "1cd039aa-5b86-4e46-8e37-9ef263332c6b",
                    "isDefault": true
                }
            ],
            "customerNumber": "6776445404",
            "externalObjectReferences": [
                {
                    "externalSystemId": "t089999",
                    "externalId": "1324565",
                    "externalIdTypeCode": "201"
                }
            ],
            "createdAt": "2023-05-31T06:39:28.142Z",
            "customerType": "INDIVIDUAL",
            "markets": [
                {
                    "marketId": "US",
                    "active": true,
                    "currency": "USD",
                    "country": "US",
                    "salesArea": {
                        "salesOrganization": "SE10",
                        "distributionChannel": "00",
                        "division": "00"
                    },
                    "priceType": "Net"
                }
            ],
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b12345",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b12345",
            "changedAt": "2023-05-31T06:39:28.142Z",
            "defaultAddress": {
                "email": "user2@test.com",
                "phone": "1234567899",
                "houseNumber": "876",
                "city": "New Orleans",
                "state": "LA",
                "postalCode": "700089",
                "country": "US",
                "addressUUID": "1cd039aa-5b86-4e46-8e37-9ef263332c6b",
                "isDefault": true
            }
        }
    ]
}
```

+++

>[!TAB 联系人]

+++请求

对象 [!DNL SAP Commerce] Contacts API的值 `{SOURCE_PARAMS}` 传递为 `{"object_type":"contacts"}`. 在base64中进行编码时，它等于 `eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=` 如下所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++响应

成功的响应会返回类似于以下内容的JSON结构：

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "externalObjectReferences": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {}
                }
            },
            "personalInfo": {
                "type": "object",
                "properties": {
                    "firstName": {
                        "type": "string"
                    },
                    "lastName": {
                        "type": "string"
                    }
                }
            },
            "createdAt": {
                "type": "string"
            },
            "createdBy": {
                "type": "string"
            },
            "changedBy": {
                "type": "string"
            },
            "contactNumber": {
                "type": "string"
            },
            "changedAt": {
                "type": "string"
            }
        }
    },
    "data": [
        {
            "personalInfo": {
                "firstName": "Test 1",
                "lastName": "User 1"
            },
            "createdAt": "2023-05-31T13:33:52.689Z",
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "contactNumber": "4365374130",
            "changedAt": "2023-05-31T13:33:52.689Z"
        },
        {
            "personalInfo": {
                "firstName": "Test 2",
                "lastName": "User 2"
            },
            "createdAt": "2023-05-31T13:33:52.37Z",
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "contactNumber": "4075431868",
            "changedAt": "2023-05-31T13:33:52.37Z"
        }
    ]
}
```

+++

>[!ENDTABS]

### 创建源连接 {#source-connection}

您可以通过向以下对象发出POST请求来创建源连接： `/sourceConnections` 的端点 [!DNL Flow Service] API。 源连接由连接ID、源数据文件的路径以及连接规范ID组成。

**API格式**

```https
POST /sourceConnections
```

根据您使用的对象类型，从以下选项卡中选择：

>[!BEGINTABS]

>[!TAB 客户]

+++请求

以下请求为创建源连接 [!DNL SAP Commerce] 客户数据：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce Source Connection",
      "description": "SAP Commerce Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "object_type": "customers"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 请确保源连接的名称是描述性的，因为您可以使用此名称查找有关源连接的信息。 |
| `description` | 可包含的可选值，用于提供有关源连接的更多信息。 |
| `baseConnectionId` | 的基本连接ID [!DNL SAP Commerce]. 此ID是在前面的步骤中生成的。 |
| `connectionSpec.id` | 与源对应的连接规范ID。 |
| `data.format` | 的格式 [!DNL SAP Commerce] 要摄取的数据。 目前，唯一支持的数据格式为 `json`. |
| `object_type` | [!DNL SAP Commerce] 支持多个API。 对于客户API， `object_type` 参数应设置为 `customers`. |
| `path` | 这将具有与您选择的相同的值 `object_type`. |

+++

+++响应

成功的响应将返回唯一标识符(`id`)。 此ID是稍后步骤创建数据流所必需的。

```json
{
    "id": "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3",
    "etag": "\"ed05f1e1-0000-0200-0000-6368b8710000\""
}
```

+++

>[!TAB 联系人]

+++请求

以下请求为创建源连接 [!DNL SAP Commerce] 联系人数据：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce Source Connection",
      "description": "SAP Commerce Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "object_type": "contacts"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 请确保源连接的名称是描述性的，因为您可以使用此名称查找有关源连接的信息。 |
| `description` | 可包含的可选值，用于提供有关源连接的更多信息。 |
| `baseConnectionId` | 的基本连接ID [!DNL SAP Commerce]. 此ID是在前面的步骤中生成的。 |
| `connectionSpec.id` | 与源对应的连接规范ID。 |
| `data.format` | 的格式 [!DNL SAP Commerce] 要摄取的数据。 目前，唯一支持的数据格式为 `json`. |
| `object_type` | [!DNL SAP Commerce] 支持多个API。 对于联系人API， `object_type` 参数应设置为 `contacts`. |
| `path` | 这将具有与您选择的相同的值 *`object_type`*. |

+++

+++响应

成功的响应将返回唯一标识符(`id`)。 此ID是稍后步骤创建数据流所必需的。

```json
{
    "id": "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3",
    "etag": "\"ed05f1e1-0000-0200-0000-6368b8710000\""
}
```

+++

>[!ENDTABS]

### 创建目标XDM架构 {#target-schema}

为了在Platform中使用源数据，必须创建目标架构，以根据您的需求构建源数据。 然后，使用目标架构创建包含源数据的Platform数据集。

可以通过向以下对象执行POST请求来创建目标XDM架构 [架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

有关如何创建目标XDM架构的详细步骤，请参阅关于的教程 [使用API创建架构](../../../../../xdm/api/schemas.md#create-a-schema).

### 创建目标数据集 {#target-dataset}

可以通过向执行POST请求来创建目标数据集 [目录服务API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，在有效负载中提供目标架构的ID。

有关如何创建目标数据集的详细步骤，请参阅关于的教程 [使用API创建数据集](../../../../../catalog/api/create-dataset.md).

### 创建目标连接 {#target-connection}

目标连接表示与要存储所摄取数据的目标的连接。 要创建目标连接，您必须提供对应于数据湖的固定连接规范ID。 此ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

现在，您拥有目标架构、目标数据集以及到数据湖的连接规范ID。 使用这些标识符，您可以使用 [!DNL Flow Service] 用于指定将包含入站源数据的数据集的API。

**API格式**

```https
POST /targetConnections
```

**请求**

以下请求创建目标连接 [!DNL SAP Commerce]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce Target Connection Generic Rest",
      "description": "SAP Commerce Target Connection Generic Rest",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
              "version": "1.2"
          }
      },
      "params": {
          "dataSetId": "645923cd7aeeea1c06c5e92e"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 目标连接的名称。 确保目标连接的名称是描述性的，因为您可以使用此名称查找有关目标连接的信息。 |
| `description` | 可包含的可选值，用于提供有关目标连接的更多信息。 |
| `connectionSpec.id` | 对应于数据湖的连接规范ID。 此固定ID为： `6b137bf6-d2a0-48c8-914b-d50f4942eb85`. |
| `data.format` | 的格式 [!DNL SAP Commerce] 要摄取的数据。 |
| `params.dataSetId` | 在上一步中检索到的目标数据集ID。 |

**响应**

成功的响应将返回新目标连接的唯一标识符(`id`)。 此ID在后续步骤中是必需的。

```json
{
    "id": "5b72a4b6-2fb8-4ca7-8ad8-4114a3063c5c",
    "etag": "\"db00c6dc-0000-0200-0000-6482d8280000\""
}
```

### 创建映射 {#mapping}

要将源数据摄取到目标数据集中，必须首先将其映射到目标数据集所遵循的目标架构。 这可以通过向以下对象执行POST请求来实现 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) 请求有效负载中定义的数据映射。

**API格式**

```http
POST /conversion/mappingSets
```

>[!BEGINTABS]

>[!TAB 客户]

+++请求

以下请求创建映射 [!DNL SAP Commerce] 客户API数据

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "customerNumber",
            "destination": "_extconndev.customerNumber"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "customerType",
            "destination": "_extconndev.customerType"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "changedAt",
            "destination": "_extconndev.changedAt"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "addresses[*].email",
            "destination": "_extconndev.addresses[*].email"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "addresses[*].city",
            "destination": "_extconndev.addresses[*].city"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "addresses[*].addressUUID",
            "destination": "_extconndev.addresses[*].addressUUID"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalSystemId",
            "destination": "_extconndev.externalObjectReferences[*].externalSystemId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalId",
            "destination": "_extconndev.externalObjectReferences[*].externalId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalIdTypeCode",
            "destination": "_extconndev.externalObjectReferences[*].externalIdTypeCode"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "customReferences[*].id",
            "destination": "_extconndev.customReferences[*].id"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "customReferences[*].typeCode",
            "destination": "_extconndev.customReferences[*].typeCode"
        }
    ],
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `outputSchema.schemaRef.id` | 的ID [目标XDM架构](#target-schema) 在之前的步骤中生成。 |
| `mappings.sourceType` | 正在映射的源属性类型。 |
| `mappings.source` | 需要映射到目标XDM路径的源属性。 |
| `mappings.destination` | 源属性将映射到的目标XDM路径。 |

+++

+++响应

成功响应将返回新创建映射的详细信息，包括其唯一标识符(`id`)。 在后续步骤中需要使用此值来创建数据流。

```json
{
    "id": "ddf0592bcc9d4ac391803f15f2429f87",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

+++

>[!TAB 联系人]

+++请求

以下请求创建映射 [!DNL SAP Commerce] 联系人API数据

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "contactNumber",
            "destination": "_extconndev.contactNumber"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "createdAt",
            "destination": "_extconndev.createdAt"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "changedAt",
            "destination": "_extconndev.changedAt"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "personalInfo.lastName",
            "destination": "_extconndev.personalInfo.lastName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "personalInfo.firstName",
            "destination": "_extconndev.personalInfo.firstName"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectRefereneces[*].externalSystemId",
            "destination": "_extconndev.externalObjectReferences[*].externalSystemId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalId",
            "destination": "_extconndev.externalObjectReferences[*].externalId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalIdTypeCode",
            "destination": "_extconndev.externalObjectReferences[*].externalIdTypeCode"
        }
    ],
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/extconndev/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
      }
    }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `outputSchema.schemaRef.id` | 的ID [目标XDM架构](#target-schema) 在之前的步骤中生成。 |
| `mappings.sourceType` | 正在映射的源属性类型。 |
| `mappings.source` | 需要映射到目标XDM路径的源属性。 |
| `mappings.destination` | 源属性将映射到的目标XDM路径。 |

+++

+++响应

成功响应将返回新创建映射的详细信息，包括其唯一标识符(`id`)。 在后续步骤中需要使用此值来创建数据流。

```json
{
    "id": "ddf0592bcc9d4ac391803f15f2429f87",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

+++

>[!ENDTABS]

### 创建流 {#flow}

从以下来源获取数据的最后一步 [!DNL SAP Commerce] 到Platform就是创建数据流。 现在，您已准备以下必需值：

* [源连接ID](#source-connection)
* [目标连接ID](#target-connection)
* [映射 ID](#mapping)

数据流负责从源中计划和收集数据。 您可以通过在有效负载中提供上述值时执行POST请求来创建数据流。

**API格式**

```http
POST /flows
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce Connector Description Flow Generic Rest",
      "description": "SAP Commerce Connector Description Flow Generic Rest",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "2ef2e831-f4f1-4363-a0f7-08b4ea347164"
      ],
      "targetConnectionIds": [
          "5b72a4b6-2fb8-4ca7-8ad8-4114a3063c5c"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "ddf0592bcc9d4ac391803f15f2429f87",
                  "mappingVersion": "0"
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1625040887",
          "frequency": "once",
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 您的数据流的名称。 确保数据流的名称是描述性的，因为您可以使用此名称查找数据流上的信息。 |
| `description` | 可包含的可选值，用于提供有关数据流的更多信息。 |
| `flowSpec.id` | 创建数据流所需的流规范ID。 此固定ID为： `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | 流规范ID的相应版本。 此值默认为 `1.0`. |
| `sourceConnectionIds` | 此 [源连接ID](#source-connection) 在之前的步骤中生成。 |
| `targetConnectionIds` | 此 [目标连接Id](#target-connection) 在之前的步骤中生成。 |
| `transformations` | 此属性包含需要应用于数据的各种转换。 将不符合XDM的数据引入到Platform时需要此属性。 |
| `transformations.name` | 分配给转换的名称。 |
| `transformations.params.mappingId` | 此 [映射ID](#mapping) 在之前的步骤中生成。 |
| `transformations.params.mappingVersion` | 映射ID的相应版本。 此值默认为 `0`. |
| `scheduleParams.startTime` | 此属性包含有关数据流的摄取计划的信息。 |
| `scheduleParams.frequency` | 数据流收集数据的频率。 |
| `scheduleParams.interval` | 间隔指定两次连续流运行之间的周期。 间隔的值应为非零整数。 |

**响应**

成功的响应会返回ID (`id`)。 您可以使用此ID监视、更新或删除数据流。

```json
{
     "id": "fcd16140-81b4-422a-8f9a-eaa92796c4f4",
     "etag": "\"9200a171-0000-0200-0000-6368c1da0000\""
}
```

## 附录

以下部分提供了有关监视、更新和删除数据流的步骤的信息。

### 监测数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关流运行、完成状态和错误的信息。 有关完整的API示例，请阅读以下指南： [使用API监控源数据流](../../monitor.md).

### 更新您的数据流

通过向发出PATCH请求，更新数据流的详细信息，例如其名称和描述，以及其运行计划和关联的映射集。 `/flows` 端点 [!DNL Flow Service] API，同时提供数据流的ID。 发出PATCH请求时，必须提供数据流的唯一值 `etag` 在 `If-Match` 标题。 有关完整的API示例，请阅读以下指南： [使用API更新源数据流](../../update-dataflows.md).

### 更新您的帐户

PATCH通过向 [!DNL Flow Service] API，同时将您的基本连接ID作为查询参数提供。 发出PATCH请求时，必须提供源帐户的唯一帐户 `etag` 在 `If-Match` 标题。 有关完整的API示例，请阅读以下指南： [使用API更新源帐户](../../update.md).

### 删除您的数据流

通过向以下对象执行DELETE请求来删除您的数据流： [!DNL Flow Service] API，同时提供您要作为查询参数的一部分删除的数据流的ID。 有关完整的API示例，请阅读以下指南： [使用API删除数据流](../../delete-dataflows.md).

### 删除您的帐户

向以下网站发出DELETE请求，删除您的帐户： [!DNL Flow Service] API，同时提供要删除帐户的基本连接ID。 有关完整的API示例，请阅读以下指南： [使用API删除源帐户](../../delete.md).
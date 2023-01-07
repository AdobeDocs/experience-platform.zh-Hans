---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API
title: 边缘投影API端点
type: Documentation
description: Adobe Experience Platform让您能够在多个渠道中实时为客户提供协调、一致的个性化体验，方法是随时提供正确的数据，并在发生更改时不断更新这些数据。 这是通过使用边缘来完成的，边缘是一个地理上放置的服务器，用于存储数据并使应用程序能够轻松访问数据。
exl-id: ce429164-8e87-412d-9a9d-e0d4738c7815
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 2%

---

# 边缘投影配置和目标端点

为了跨多个渠道为客户实时提供协调、一致和个性化的体验，需要随时提供适当的数据，并在发生更改时不断更新。 Adobe Experience Platform允许通过使用称为边缘的内容来实时访问数据。 边缘是位于地理位置的服务器，用于存储数据并使应用程序能够轻松访问它。 例如，Adobe应用程序(如Adobe Target和Adobe Campaign)使用边缘，以便实时提供个性化的客户体验。 数据通过投影被路由到边缘，其中，投影目标定义要向其发送数据的边缘，以及投影配置定义将在边缘上提供的特定信息。 本指南提供了有关使用 [!DNL Real-Time Customer Profile] 用于处理边缘投影的API，包括目标和配置。

## 快速入门

本指南中使用的API端点是 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). 在继续之前，请查看 [入门指南](getting-started.md) 有关相关文档的链接、本文档中的API调用示例指南，以及有关成功调用任何代码所需标头的重要信息 [!DNL Experience Platform] API。

>[!NOTE]
>
>包含有效负载(POST、PUT、PATCH)的请求需要 `Content-Type` 标题。 多个 `Content-Type` 在本文档中使用。 请特别注意示例调用中的标头，以确保您使用的是正确的 `Content-Type` 的次数。

## 投影目标

通过指定要发送数据的位置，可以将投影路由到一个或多个边缘。 创建的每个投影目标都有一个唯一ID，然后用于创建投影配置。

### 列出所有目标

您可以通过向 `/config/destinations` 端点。

**API格式**

```http
GET /config/destinations
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应包括 `projectionDestinations` 数组，其中每个目标的详细信息显示为数组中的单个对象。 如果尚未配置投影，则 `projectionDestinations` 数组返回空。

>[!NOTE]
>
>此响应因空间而缩短，仅显示两个目标。

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/destinations",
            "templated": false
        }
    },
    "_embedded": {
        "projectionDestinations": [
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
                        "templated": false
                    }
                },
                "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "VA5"
                ],
                "version": 1
            },
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/7d26263f-a5df-43ce-b088-7f70e187f549",
                        "templated": false
                    }
                },
                "id": "7d26263f-a5df-43ce-b088-7f70e187f549",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "OR1"
                ],
                "version": 1
            }
        ]
    }
}
```

| 属性 | 描述 |
|---|---|
| `_links.self.href` | 在顶级，与用于发出GET请求的路径匹配。 在每个单独的目标对象中，此路径可用于GET请求中，以直接查找特定目标的详细信息。 |
| `id` | 在每个目标对象中， `"id"` 显示目标的只读、系统生成的唯一ID。 引用特定目标和创建投影配置时，会使用此ID。 |

有关单个目标属性的更多信息，请参阅 [创建目标](#create-a-destination) 接下来。

### 创建目标 {#create-a-destination}

如果所需的目标不存在，则可以通过向 `/config/destinations` 端点。

**API格式**

```http
POST /config/destinations
```

**请求**

以下请求会创建新的边缘目标。

>[!NOTE]
>
>创建目标的POST请求需要 `Content-Type` 标题，如下所示。 使用错误 `Content-Type` 标头会导致“HTTP状态415（不支持的媒体类型）”错误。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json; version=1' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1" 
        ],
        "ttl": 3600,
        "replicationPolicy": REACTIVE
      }'
```

| 属性 | 描述 |
|---|---|
| `type` **（必需）** | 要创建的目标类型。 唯一接受的值“EDGE”会创建边缘目标。 |
| `dataCenters` **（必需）** | 一个字符串数组，列出要将投影路由到的边。 可以包含以下一个或多个值：“OR1” — 美国西部，“VA5” — 美国东部，“NLD1” - EMEA。 |
| `ttl` **（必需）** | 指定投影过期。 接受的值范围：600至604800。 默认值：3600。 |
| `replicationPolicy` **（必需）** | 定义从集线器到边缘的数据复制行为。  支持的值：主动、被动。 默认值：反应。 |

**响应**

成功的响应会返回新创建的边缘目标的详细信息，包括由系统生成的只读唯一ID(`id`)。

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
        "templated": false
    },
    "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
    "type": "EDGE",
    "dataCenters": [
       "OR1"
    ],
    "ttl": 3600,
    "version": 1
}
```

| 属性 | 描述 |
|---|---|
| `self.href` | 此路径用于直接查找(GET)目标，也可用于更新(PUT)或删除(DELETE)目标。 |
| `id` | 目标的只读、系统生成的唯一ID。 在创建投影配置时，此ID用于直接引用目标。 |
| `version` | 此只读值显示目标的当前版本。 更新目标后，版本号会自动递增。 |

### 查看目标

如果您知道投影目标的唯一ID，则可以执行查找请求以查看其详细信息。 这是通过向 `/config/destinations` 端点，并在请求路径中包含目标的ID。

**API格式**

```http
GET /config/destinations/{DESTINATION_ID}
```

| 参数 | 描述 |
|---|---|
| `{DESTINATION_ID}` | 要查看的投影目标的唯一ID。 |

**请求**

以下请求执行查找(GET)以查看请求路径中提供的ID的目标。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应对象显示投影目标的详细信息。 的 `id` 属性应与请求中提供的投影目标的ID匹配。

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
        "templated": false
    },
    "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
    "type": "EDGE",
    "ttl": 3600,
    "dataCenters": [
        "OR1"
    ],
    "version": 1
}
```

### 更新目标

通过向 `/config/destinations` 端点，并包括要在请求路径中更新的目标ID。 此操作实质上是重写目标，因此，在请求正文中必须提供与创建新目标时相同的属性。

>[!CAUTION]
>
>对更新请求的API响应是即时的，但是会异步应用对预测所做的更改。 换句话说，在对目标的定义进行更新和应用目标定义之间存在时间差。

**API格式**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| 参数 | 描述 |
|---|---|
| `{DESTINATION_ID}` | 要更新的投影目标的唯一ID。 |

**请求**

以下请求会更新现有目标以包含第二个位置(`dataCenters`)。

>[!IMPORTANT]
>
>PUT请求需要 `Content-Type` 标题，如下所示。 使用错误 `Content-Type` 标头会导致“HTTP状态415（不支持的媒体类型）”错误。

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1",
          "VA5" 
        ],
        "replicationPolicy": REACTIVE,
        "currentVersion": 1
      }'
```

| 属性 | 描述 |
|---|---|
| `currentVersion` | 现有目标的当前版本。 的值 `version` 属性。 |

**响应**

响应包含目标的更新详细信息，包括其ID和新 `version` 目标位置。

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7",
        "templated": false
    },
    "id": "8b90ce19-e7dd-403a-ae24-69683a6674e7",
    "type": "EDGE",
    "ttl": 8000,
    "dataCenters": [
        "OR1",
        "VA5"
    ],
    "version": 2
}
```

### 删除目标

如果贵组织不再需要投影目标，则可以通过向 `/config/destinations` 端点，并在请求路径中包含要删除的目标的ID。

>[!CAUTION]
>
>对删除请求的API响应是即时的，但边缘上的数据的实际更改是异步进行的。 换言之，将从所有边缘( `dataCenters` 在投影目标中指定)，但完成该过程需要时间。

**API格式**

```http
DELETE /config/destinations/{DESTINATION_ID}
```

| 参数 | 描述 |
|---|---|
| `{DESTINATION_ID}` | 要删除的投影目标的唯一ID。 |


**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

删除请求会返回HTTP状态204（无内容）和空的响应正文。 您可以通过使用目标的ID对目标执行查找请求来确认删除成功。 查找应返回HTTP状态404（未找到）。

## 投影配置

投影配置提供有关每个边缘上哪些数据可用的信息。 而不是投射完整 [!DNL Experience Data Model] (XDM)架构到边缘，投影仅提供架构中的特定数据或字段。 贵组织可以为每个XDM架构定义多个投影配置。

### 列出所有投影配置

您可以通过向 `/config/projections` 端点。 您还可以向请求路径中添加可选参数以访问特定架构的投影配置或按名称查找单个投影。

**API格式**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| 参数 | 描述 |
|---|---|
| `{SCHEMA_NAME}` | 与要访问的投影配置关联的架构类的名称。 |
| `{PROJECTION_NAME}` | 要访问的投影配置的名称。 |

>[!NOTE]
>
>`schemaName` 使用 `name` 参数，因为投影配置名称在模式类的上下文中是唯一的。

**请求**

以下请求列出了与 [!DNL Experience Data Model] 模式类， [!DNL XDM Individual Profile]. 有关XDM及其在 [!DNL Platform]，请首先阅读 [XDM系统概述](../../xdm/home.md).

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回根内的投影配置列表 `_embedded` 属性，包含在 `projectionConfigs` 数组。 如果尚未为贵组织进行投影配置，则 `projectionConfigs` 数组将为空。

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/projections",
            "templated": false
        }
    },
    "_embedded": {
        "projectionConfigs": [
            {
                "_links": {
                    "destination": {
                        "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "templated": false
                    },
                    "self": {
                        "href": "/data/core/ups/config/projections/99aed0bc-c183-4997-ada7-7843642e08f6",
                        "templated": false
                    }
                },
                "_embedded": {
                    "destination": {
                        "self": {
                            "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                            "templated": false
                        },
                        "id": "a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "type": "EDGE",
                        "ttl": 1000,
                        "dataCenters": [
                            "OR1"
                        ],
                        "version": 1
                    }
                },
                "selector": "strategy",
                "version": 2,
                "id": "99aed0bc-c183-4997-ada7-7843642e08f6",
                "schemaName": "_xdm.context.profile",
                "name": "adcloud_rlsa",
                "destinationId": "a689248a-5d2b-44af-bb70-c8f17f97011b"
            },
        ]
    }
}
```

### 创建投影配置

您可以创建(POST)新的投影配置，以指示哪些XDM字段在边缘上可用。

**API格式**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| 参数 | 描述 |
|---|---|
| `{SCHEMA_NAME}` | 与要访问的投影配置关联的架构类的名称。 |

**请求**

>[!NOTE]
>
>创建配置的POST请求需要 `Content-Type` 标题，如下所示。 使用错误 `Content-Type` 标头会导致“HTTP状态415（不支持的媒体类型）”错误。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionConfig+json; version=1' \
  -d '{
        "selector": "emails,person(firstName)",
        "name": "my_test_projection",
        "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
      }'
```

| 属性 | 描述 |
|---|---|
| `selector` | 一个字符串，其中包含要复制到边缘的架构内的属性列表。 有关使用选择器的最佳实践，请参阅 [选择器](#selectors) 部分。 |
| `name` | 新投影配置的描述性名称。 |
| `destinationId` | 数据将投影到的边缘目标的标识符。 |

**响应**

成功的响应会返回新创建的投影配置的详细信息。

```json
{
    "_links": {
        "destination": {
            "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "templated": false
        },
        "self": {
            "href": "/data/core/ups/config/projections/87fcd0bc-c183-4997-daf9-7843642g95a1",
            "templated": false
        }
    },
    "_embedded": {
        "destination": {
            "self": {
                "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
                "templated": false
            },
            "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "type": "EDGE",
            "ttl": 1000,
            "dataCenters": [
                "OR1"
            ],
            "version": 1
        }
    },
    "selector": "emails,person(firstName)",
    "version": 2,
    "id": "87fcd0bc-c183-4997-daf9-7843642g95a1",
    "schemaName": "_xdm.context.profile",
    "name": "my_test_projection",
    "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
}
```

## 选择器 {#selectors}

选择器是以逗号分隔的XDM字段名称列表。 在投影配置中，选择器指定要包含在投影中的属性。 的格式 `selector` 参数值基于XPath语法。 支持的语法概述如下，并提供了其他供参考的示例。

### 支持的语法

* 使用逗号选择多个字段。 请勿使用空格。
* 使用点表示法选择嵌套字段。
   * 例如，选择名为 `field` 嵌套在名为 `foo`，使用选择器 `foo.field`.
* 如果包含包含子字段的字段，则默认情况下也会投影所有子字段。 但是，您可以使用圆括号过滤返回的子字段 `"( )"`.
   * 例如， `addresses(type,city.country)` 仅返回每个地址类型和地址城市所在的国家/地区 `addresses` 数组元素。
   * 上例等效于 `addresses.type,addresses.city.country`.

>[!NOTE]
>
>引用子字段支持点记号和圆括号记号。 但是，最好使用点表示法，因为它更简洁，更好地说明了字段层次结构。

* 选择器中的每个字段都是相对于响应的根指定的。
   * 如果数据是资源集合，则投影将包含资源数组。
   * 如果数据是单个资源，则投影将包含与该资源相关的字段。
   * 如果所选字段是（或是数组的一部分），则投影将包括数组中所有元素的选定部分。

### 选择器参数示例

以下示例显示示例 `selector` 参数，后跟它们表示的结构化值。

**person.lastName**

返回 `lastName` 的子字段 `person` 对象。

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**地址**

返回 `addresses` 数组，包括每个元素中的所有字段，但没有其他字段。

```json
{
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**person.lastName，addresses**

返回 `person.lastName` 字段和 `addresses` 数组。

```json
{
  "person": {
    "lastName": "Smith"
  },
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**addresses.city**

仅返回地址数组中所有元素的“城市”字段。

```json
{
  "addresses": [
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

>[!NOTE]
>
>每当返回嵌套字段时，投影都包括封闭的父对象。 除非也明确选择父字段，否则父字段不包含任何其他子字段。

**地址（类型，城市）**

仅返回 `type` 和 `city` 字段 `addresses` 数组。 每个子字段中包含的所有其他子字段 `addresses` 元素被过滤掉。

```json
{
  "addresses": [
    {
      "type": "home",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

## 后续步骤

本指南向您展示了配置投影和目标所涉及的步骤，包括如何正确设置 `selector` 参数。 您现在可以创建新的投影目标和配置，以满足您组织的需求。

---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 实时客户用户档案API开发人员指南
topic: guide
translation-type: tm+mt
source-git-commit: 5aad9fa71051a58fe1c4678553f47077d81d23fc

---


# 边缘目标和预测

为了在多个渠道中实时为客户提供协调、一致和个性化的体验，需要随时随地提供正确的数据并在发生变化时不断更新。 Adobe Experience Platform通过使用所谓的边缘实现对数据的实时访问。 边缘是地理上放置的服务器，它存储数据并使应用程序可以很容易地访问它。 例如，Adobe目标和Adobe Campaign等Adobe应用程序使用边缘，以实时提供个性化的客户体验。 通过投影将数据路由到边缘，投影目标定义要向其发送数据的边缘，投影配置定义将在边缘上提供的特定信息。 本指南提供了使用实时客户用户档案API处理边缘预测（包括目标和配置）的详细说明。

## 入门指南

本指南中使用的API端点是实时客户用户档案API的一部分。 在继续之前，请查阅实 [时客户用户档案开发人员指南](getting-started.md)。 特别是，用户档案开发人 [员指南的入门部分](getting-started.md#getting-started) ，包括指向相关主题的链接、阅读本文档中示例API调用的指南以及成功调用任何Experience Platform API所需的标题的重要信息。

## 投影目标

通过指定要发送数据的位置，可将投影路由到一个或多个边缘。 创建的每个投影目标都有一个唯一的ID，然后该ID用于创建投影配置。

### 列表所有目标

您可以通过向端点发出GET请求，列表已为您的组织创建的边缘目 `/config/destinations` 标。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

该响应包括一个数 `projectionDestinations` 组，每个目标的详细信息显示为该数组中的单个对象。 如果尚未配置任何投影，则数 `projectionDestinations` 组返回空。

>[!NOTE]
>此响应已缩短，只显示两个目标。

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
| `_links.self.href` | 在顶级，匹配用于发出GET请求的路径。 在每个目标对象中，此路径可用于GET请求中，以直接查找特定目标的详细信息。 |
| `id` | 在每个目标对象中， `"id"` 显示由系统生成的只读目标唯一ID。 此ID在引用特定目标和创建投影配置时使用。 |

有关单个目标的属性的详细信息，请参阅下面有关创建 [目标的部分](#create-a-destination) 。

### 创建目标 {#create-a-destination}

如果所需的目标尚不存在，则可以通过向端点发出POST请求来创建新的投影目 `/config/destinations` 标。

**API格式**

```http
POST /config/destinations
```

**请求**

以下请求将创建新的边缘目标。

>[!NOTE]
>创建目标的POST请求需要特定的标 `Content-Type` 题，如下所示。 使用错误的 `Content-Type` 头会导致HTTP状态415（不支持的媒体类型）错误。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

|属性|描述||`type` ( **必需)** |要创建的目标类型。 唯一接受的值“EDGE”创建边缘目标。||`dataCenters` ( **必需)** |一个字符串数组，它列表要布线投影的边缘。 可能包含以下一个或多个值：“OR1”-美国西部，“VA5”-美国东部，“NLD1”- EMEA。||`ttl` ( **必需)** |指定投影到期。 接受的值范围：600至604800。 默认值：3600。||`replicationPolicy` ( **必需)** |定义从集线器到边缘的数据复制行为。  支持的值：主动、被动。 默认值：反应。|

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
| `id` | 目标的只读、由系统生成的唯一ID。 此ID用于直接引用目标以及创建投影配置时的目标。 |
| `version` | 此只读值显示目标的当前版本。 更新目标后，版本号会自动递增。 |

### 视图目标

如果您知道投影目标的唯一ID，则可以执行查找请求以视图其详细信息。 这是通过向端点发出GET请求并 `/config/destinations` 在请求路径中包括目标的ID来完成的。

**API格式**

```http
GET /config/destinations/{DESTINATION_ID}
```

| 参数 | 描述 |
|---|---|
| `{DESTINATION_ID}` | 要视图的投影目标的唯一ID。 |

**请求**

以下请求执行查找(GET)以视图请求路径中提供的ID的目标。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应对象显示投影目标的详细信息。 该 `id` 属性应与请求中提供的投影目标的ID匹配。

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

通过向端点发出PUT请求并在请求路径中包括要更 `/config/destinations` 新的目标的ID，可以更新现有目标。 此操作实质上是 _重写目标_ ，因此必须在请求主体中提供与创建新目标时提供的相同属性。

>[!CAUTION]
>对更新请求的API响应是即时的，但是对预测所做的更改是异步应用的。 换句话说，在对目标的定义进行更新和应用该定义之间存在时间差。

**API格式**

```
PUT /config/destinations/{DESTINATION_ID}
```

| 参数 | 描述 |
|---|---|
| `{DESTINATION_ID}` | 要更新的投影目标的唯一ID。 |

**请求**

以下请求更新现有目标以包含第二位置(`dataCenters`)。

>[!IMPORTANT]
>PUT请求需要特定的 `Content-Type` 标题，如下所示。 使用错误的 `Content-Type` 头会导致HTTP状态415（不支持的媒体类型）错误。

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `currentVersion` | 现有目标的当前版本。 执行目标的 `version` 查找请求时属性的值。 |

**响应**

响应包括目标的更新详细信息，包括其ID和目标 `version` 的新ID。

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

如果您的组织不再需要投影目标，则可以通过向端点发出DELETE请求并在请求路径中包含要删除的目标的ID来删除该目标。 `/config/destinations`

>[!CAUTION]
>对删除请求的API响应是即时的，但边缘上数据的实际更改是异步进行的。 换句话说，用户档案数据将从所有边缘（在投影目标中指定）中删除，但该过程将需要时间完成。 `dataCenters`

**API格式**

```
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

删除请求返回HTTP状态204（无内容）和空的响应主体。 您可以通过按目标ID对目标执行查找请求来确认删除成功。 查找应返回HTTP状态404（找不到）。

## 投影配置

投影配置提供了关于每个边缘上应提供哪些数据的信息。 投影不是将完整的体验数据模型(XDM)模式投影到边缘，而是只提供模式中的特定数据或字段。 您的组织可以为每个XDM模式定义多个投影配置。

### 列表所有投影配置

您可以通过向端点发出GET请求来列表为组织创建的所有投影配 `/config/projections` 置。 您还可以向请求路径添加可选参数以访问特定模式的投影配置或按其名称查找单个投影。

**API格式**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| 参数 | 描述 |
|---|---|
| `{SCHEMA_NAME}` | 与要访问的投影配置关联的模式类的名称。 |
| `{PROJECTION_NAME}` | 要访问的投影配置的名称。 |

>[!NOTE]
>`schemaName` 当使用参数时 `name` 是必需的，因为投影配置名称仅在模式类的上下文中是唯一的。

**请求**

以下请求列表与“体验数据模型模式”类(XDM单个用户档案)关联的所有投影配置。 有关XDM及其在平台中的角色的更多信息，请首先阅读 [XDM系统概述](../../xdm/home.md)。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回包含在数组中的根属 `_embedded` 性内的投影配置的列表 `projectionConfigs` 值。 如果尚未为您的组织建立投影配置，则 `projectionConfigs` 阵列将为空。

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

您可以创建(POST)新的投影配置，该配置将指示哪些XDM字段在边缘上可用。

**API格式**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| 参数 | 描述 |
|---|---|
| `{SCHEMA_NAME}` | 与要访问的投影配置关联的模式类的名称。 |

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "selector": "emails,person(firstName)",
        "name": "my_test_projection",
        "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
      }'
```

| 属性 | 描述 |
|---|---|
| `selector` | 一个字符串，其中包含要复制到边的模式中属性的列表。 此文档的“选择器”部分提供了有关使用选 [择器的最](#selectors) 佳实践。 |
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

## Selectors {#selectors}

选择器是XDM字段名称的逗号分隔列表。 在投影配置中，选择器指定要包括在投影中的属性。 参数值的格 `selector` 式基于XPath语法松散。 支持的语法概述如下，并提供了其他示例供参考。

### 支持的语法

* 使用逗号选择多个字段。 请勿使用空格。
* 使用点记号选择嵌套字段。
   * 例如，要选择一个名为的字段， `field` 该字段嵌套在一个名为的字 `foo`段中，请使用选择器 `foo.field`。
* 当包含包含子字段的字段时，默认情况下，所有子字段也会被投影。 但是，您可以使用括号过滤返回的子字段 `"( )"`。
   * 例如，只 `addresses(type,city.country)` 为每个数组元素返回地址类型和地址城市所在的国 `addresses` 家／地区。
   * 以上示例与相同 `addresses.type,addresses.city.country`。

>[!NOTE]
>引用子字段时支持点记号和括号记号。 但是，最好使用点记号，因为它更简洁，并更好地说明了字段层次结构。

* 选择器中的每个字段都是相对于响应的根指定的。
   * 如果数据是资源集合，则投影将包括资源数组。
   * 如果数据是单个资源，则投影将包括与该资源相关的字段。
   * 如果您选择的字段是（或是）数组的一部分，则投影将包括该数组中所有元素的选定部分。

### 选择器参数的示例

以下示例显示示 `selector` 例参数，后跟它们表示的结构化值。

**person.lastName**

返回 `lastName` 所请求资源中对 `person` 象的子字段。

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**地址**

返回数组中的所有元 `addresses` 素，包括每个元素中的所有字段，但不返回其他字段。

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

**person.lastName,addresses**

返回字 `person.lastName` 段和数组中的所有 `addresses` 元素。

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

仅返回地址数组中所有元素的city字段。

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
>每当返回嵌套字段时，投影都会包括封闭的父对象。 除非也明确选择父字段，否则父字段不包括任何其他子字段。

**地址（类型，城市）**

仅返回数组中每个 `type` 元素 `city` 的和字段的值 `addresses` 。 每个元素中包含的所有其他子字 `addresses` 段都会被过滤掉。

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

本指南向您展示了配置边缘投影和目标所涉及的步骤，包括如何正确设置参数的格 `selector` 式。 您现在可以根据组织的需求创建新的边缘目标和预测。 要发现通过用户档案API可用的其他操作，请参阅 [实时客户用户档案API开发人员指南](getting-started.md)。
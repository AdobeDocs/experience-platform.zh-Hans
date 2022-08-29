---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK;SDK
title: 为自助源配置源规范（批处理SDK）
topic-legacy: overview
description: 本文档概述了为使用自助源（批处理SDK）而需要准备的配置。
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: adaa0e1a63536bc1fdf751eec477e5cda9fd20ae
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 1%

---

# 为自助源配置源规范（批处理SDK）

源规范包含特定于源的信息，包括与源的类别、测试版状态和目录图标相关的属性。 它们还包含URL参数、内容、标题和计划等有用信息。 源规范还描述了从基本连接创建源连接所需参数的模式。 要创建源连接，必须使用架构。

请参阅 [附录](#source-spec) 例如，完全填充的源规范。


```json
"sourceSpec": {
  "attributes": {
    "uiAttributes": {
      "isSource": true,
      "isPreview": true,
      "isBeta": true,
      "category": {
        "key": "protocols"
      },
      "icon": {
        "key": "genericRestIcon"
      },
      "description": {
        "key": "genericRestDescription"
      },
      "label": {
        "key": "genericRestLabel"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Defines static and user input parameters to fetch resource values.",
      "properties": {
        "urlParams": {
          "type": "object",
          "properties": {
            "host": {
              "type": "string",
              "description": "Enter resource url host path.",
              "example": "https://{domain}.api.mailchimp.com"
            },
            "path": {
              "type": "string",
              "description": "Enter resource path",
              "example": "/3.0/reports/campaignId/email-activity"
            },
            "method": {
              "type": "string",
              "description": "HTTP method type.",
              "enum": [
                "GET",
                "POST"
              ]
            },
            "queryParams": {
              "type": "object",
              "description": "The query parameters in json format",
            }
          },
          "required": [
            "host",
            "path",
            "method"
          ]
        },
        "headerParams": {
          "type": "object",
          "description": "The header parameters in json format",
        },
        "contentPath": {
          "type": "object",
          "description": "The parameters required for main collection content.",
          "properties": {
            "path": {
              "description": "The path to the main content.",
              "type": "string",
              "example": "$.emails"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the root content path node.",
              "example": "email"
            }
          },
          "required": [
            "path"
          ]
        },
        "explodeEntityPath": {
          "type": "object",
          "description": "The parameters required for the sub-array content.",
          "properties": {
            "path": {
              "description": "The path to the sub-array content.",
              "type": "string",
              "example": "$.email.activity"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the  root content path node.",
              "example": "activity"
            }
          },
          "required": [
            "path"
          ]
        },
        "paginationParams": {
          "type": "object",
          "description": "The parameters required to fetch data using pagination.",
          "properties": {
            "type": {
              "description": "The pagination fetch type.",
              "type": "string",
              "enum": [
                "OFFSET",
                "POINTER"
              ]
            },
            "limitName": {
              "type": "string",
              "description": "The limit property name",
              "example": "limit or count"
            },
            "limitValue": {
              "type": "integer",
              "description": "The number of records to fetch per page.",
              "example": "limit=10 or count=10"
            },
            "offsetName": {
              "type": "string",
              "description": "The offset property name",
              "example": "offset"
            },
            "pointerPath": {
              "type": "string",
              "description": "The path to pointer property",
              "example": "$.paging.next"
            }
          },
          "required": [
            "type",
            "limitName",
            "limitValue"
          ]
        },
        "scheduleParams": {
          "type": "object",
          "description": "The parameters required to fetch data for batch schedule.",
          "properties": {
            "scheduleStartParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleEndParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleStartParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            },
            "scheduleEndParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            }
          },
          "required": [
            "scheduleStartParamName",
            "scheduleEndParamName"
          ]
        }
      },
      "required": [
        "urlParams",
        "contentPath",
        "paginationParams",
        "scheduleParams"
      ]
    }
  },
}
```

| 属性 | 描述 | 示例 |
| --- | --- | --- |
| `sourceSpec.attributes` | 包含有关特定于UI或API的源的信息。 |
| `sourceSpec.attributes.uiAttributes` | 显示有关特定于UI的源的信息。 |
| `sourceSpec.attributes.uiAttributes.isBeta` | 布尔属性，用于指示源是否需要客户提供更多反馈才能添加到其功能中。 | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | 定义源的类别。 | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | 定义用于在Platform UI中呈现源的图标。 | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | 显示源的简要描述。 |
| `sourceSpec.attributes.uiAttributes.label` | 显示用于在平台UI中呈现源的标签。 |
| `sourceSpec.attributes.spec.properties.urlParams` | 包含有关URL资源路径、方法和支持的查询参数的信息。 |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | 定义从中获取数据的资源路径。 | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | 定义用于向资源发出获取数据的请求的HTTP方法。 | `GET`、`POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | 定义支持的查询参数，当发出获取数据的请求时，这些参数可用于附加源URL。 **注意**:任何用户提供的参数值都必须格式化为占位符。 例如：`${USER_PARAMETER}`。 | `"queryParams" : {"key" : "value", "key1" : "value1"}` 将作为以下内容附加到源URL中： `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | 定义在获取数据时，需要在对源URL的HTTP请求中提供的标头。 | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | 此属性可配置为通过POST请求发送HTTP主体。 |
| `sourceSpec.attributes.spec.properties.contentPath` | 定义包含需要摄取到平台的项目列表的节点。 此属性应遵循有效的JSON路径语法，并且必须指向特定数组。 | 查看 [其他资源科](#content-path) 例如，内容路径中包含的资源示例。 |
| `sourceSpec.attributes.spec.properties.contentPath.path` | 指向要摄取到Platform的收集记录的路径。 | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | 此属性允许您识别内容路径中已识别的要被排除以阻止摄取的资源的特定项目。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | 利用此属性，可明确指定要保留的单个属性。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | 此属性允许您覆盖您在 `contentPath`. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | 此属性允许您拼合两个数组并将资源数据转换为平台资源。 |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | 指向要拼合的集合记录的路径。 | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | 利用此属性，可识别实体路径中标识的要被排除以阻止摄取的资源的特定项目。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | 利用此属性，可明确指定要保留的单个属性。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | 此属性允许您覆盖您在 `explodeEntityPath`. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | 定义必须提供的参数或字段，以便从用户的当前页面响应中获取指向下一页面的链接，或在创建下一页面URL时获取该链接。 |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | 显示源支持的分页类型的类型。 | <ul><li>`OFFSET`:此分页类型允许您通过指定从何处开始生成数组的索引以及返回结果数量的限制来解析结果。</li><li>`POINTER`:此分页类型允许您使用 `pointer` 变量来指向需要随请求一起发送的特定项目。 指针类型分页需要有效负荷中指向下一页的路径。</li><li>`CONTINUATION_TOKEN`:此分页类型允许您将查询或标头参数附加到连续令牌，以从源中检索最初由于预定最大值而未返回的剩余返回数据。</li><li>`PAGE`:此分页类型允许您将查询参数附加到分页参数，以逐页遍历返回数据，从零页开始。</li><li>`NONE`:此分页类型可用于不支持任何可用分页类型的源。 分页类型 `NONE` 在请求后返回整个响应数据。</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | API可以指定在页面中获取的记录数的限制的名称。 | `limit` 或 `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | 页面中要获取的记录数。 | `limit=10` 或 `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | 偏移属性名称。 如果分页类型设置为 `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | 指针属性名称。 这需要指向下一页的属性的json路径。 如果分页类型设置为 `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | 包含为源定义支持的计划格式的参数。 计划参数包括 `startTime` 和 `endTime`，这两种方法都允许您为批量运行设置特定时间间隔，这样可确保不会再次获取在之前批量运行中获取的记录。 |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | 定义开始时间参数名称 | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | 定义结束时间参数名称 | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | 为 `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | 为 `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | 定义用户提供的参数以获取资源值。 | 请参阅 [其他资源](#user-input) 例如，用户为 `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## 其他资源 {#appendix}

以下部分提供了关于您可以对 `sourceSpec`，包括高级计划和自定义模式。

### 内容路径示例 {#content-path}

以下示例介绍了 `contentPath` 属性 [!DNL MailChimp Members] 连接规范。

```json
"contentPath": {
  "path": "$.members",
  "skipAttributes": [
    "_links",
    "total_items",
    "list_id"
  ],
  "overrideWrapperAttribute": "member"
}
```

### `spec.properties` 用户输入示例 {#user-input}

以下是用户提供的示例 `spec.properties` 使用 [!DNL MailChimp Members] 连接规范。

在本例中， `listId` 作为 `urlParams.path`. 如果需要检索 `listId` 从客户处，则您还必须将其定义为 `spec.properties`.


```json
"urlParams": {
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      }
"spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
```

### 源规范示例 {#source-spec}

以下是使用 [!DNL MailChimp Members]:

```json
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "isSource": true,
        "isPreview": true,
        "isBeta": true,
        "category": {
          "key": "marketingAutomation"
        },
        "icon": {
          "key": "mailchimpMembersIcon"
        },
        "description": {
          "key": "mailchimpMembersDescription"
        },
        "label": {
          "key": "mailchimpMembersLabel"
        }
      },
      "urlParams": {
        "host": "https://{domain}.api.mailchimp.com",
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      },
      "contentPath": {
        "path": "$.members",
        "skipAttributes": [
          "_links",
          "total_items",
          "list_id"
        ],
        "overrideWrapperAttribute": "member"
      },
      "paginationParams": {
        "type": "OFFSET",
        "limitName": "count",
        "limitValue": "100",
        "offSetName": "offset"
      },
      "scheduleParams": {
        "scheduleStartParamName": "since_last_changed",
        "scheduleEndParamName": "before_last_changed",
        "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
        "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
  }
```

### 为源配置不同的分页类型 {#pagination}

以下是自助源（批量SDK）支持的其他分页类型的示例：

#### `CONTINUATION_TOKEN`

分页的连续令牌类型返回字符串令牌，该令牌表示由于在单个响应中可返回的预定最大项目数，所以存在无法返回的更多项目。

支持连续令牌类型分页的源可能具有与以下内容类似的分页参数：

```json
"paginationParams": {
  "type": "CONTINUATION_TOKEN",
  "continuationTokenPath": "$.meta.after_cursor",
  "parameterType": "QUERYPARAM",
  "parameterName": "page[after]",
  "delayRequestMillis": "850"
}
```

| 属性 | 描述 |
| --- | --- |
| `type` | 用于返回数据的分页类型。 |
| `continuationTokenPath` | 要移动到返回结果的下一页，必须附加到查询参数的值。 |
| `parameterType` | 的 `parameterType` 属性定义 `parameterName` 必须添加。 的 `QUERYPARAM` 类型允许您在查询后附加 `parameterName`. 的 `HEADERPARAM` 允许您将 `parameterName` 到头请求。 |
| `parameterName` | 用于包含连续令牌的参数的名称。 格式如下： `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | 的 `delayRequestMillis` 分页中的属性允许您控制对源发出的请求率。 某些源可能会限制每分钟可以发出的请求数。 例如， [!DNL Zendesk] 限制每分钟100个请求，并定义  `delayRequestMillis` to `850` 允许您将源配置为每分钟只发出大约80个请求，这远低于每分钟100个请求的阈值。 |

以下是使用连续令牌类型分页返回的响应示例：

```json
{
  "results": [
    {
      "id": 5624716025745,
      "url": "https://dev.zendesk.com/api/v2/users/5624716025745.json",
      "name": "newinctest@zenaep.com",
      "email": "newinctest@zenaep.com",
      "created_at": "2022-04-22T10:27:30Z",
      
    }
  ],
  "facets": null,
  "meta": {
    "has_more": false,
    "after_cursor": "eyJmaWVsZCI6ImNyZWF0ZWRfYXQiLCJk",
    "before_cursor": null
  },
  "links": {
    "prev": null,
    "next": "https://dev.zendesk.com/api/v2/search/export.json?filter%5Btype%5D=user&page%5Bafter%5D=eyJmaWVsZCI6"
  }
}
```

#### `PAGE`

的 `PAGE` 分页类型允许您按从零开始的页数遍历返回的数据。 使用 `PAGE` 类型分页，则必须提供单个页面中给定的记录数。

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "records",
  "limitValue": "100",
  "pageParamName": "pageIndex",
  "maximumRequest": 10000
}
```

| 属性 | 描述 |
| --- | --- |
| `type` | 用于返回数据的分页类型。 |
| `limitName` | API可以指定在页面中获取的记录数的限制的名称。 |
| `limitValue` | 页面中要获取的记录数。 |
| `pageParamName` | 要遍历返回数据的不同页面，必须附加到查询参数的参数名称。 例如， `https://abc.com?pageIndex=1` 将返回API返回负载的第二页。 |
| `maximumRequest` | 源针对给定增量运行可发出的最大请求数。 当前默认限制为10000。 |

#### `NONE`

的 `NONE` 分页类型可用于不支持任何可用分页类型的源。 使用分页类型的源 `NONE` 只需在发出GET请求时返回所有可检索的记录即可。

```json
"paginationParams": {
  "type": "NONE"
}
```

### 自助源的高级计划（批处理SDK）

使用高级计划配置源的增量和回填计划。 的 `incremental` 资产允许您配置计划，源将仅摄取新记录或修改记录，而 `backfill` 属性允许您创建计划以摄取历史数据。

通过高级计划，您可以使用特定于源的表达式和函数来配置增量计划和回填计划。 在以下示例中， [!DNL Zendesk] 源要求增量计划的格式为 `type:user updated > {START_TIME} updated < {END_TIME}` 回填为 `type:user updated < {END_TIME}`.

```json
"scheduleParams": {
        "type": "ADVANCE",
        "paramFormat": "yyyy-MM-ddTHH:mm:ssK",
        "incremental": "type:user updated > {START_TIME} updated < {END_TIME}",
        "backfill": "type:user updated < {END_TIME}"
      }
```

| 属性 | 描述 |
| --- | --- |
| `scheduleParams.type` | 源将使用的计划类型。 将此值设置为 `ADVANCE` 以使用高级计划类型。 |
| `scheduleParams.paramFormat` | 计划参数的定义格式。 此值可以与源的 `scheduleStartParamFormat` 和 `scheduleEndParamFormat` 值。 |
| `scheduleParams.incremental` | 源的增量查询。 增量是指仅摄取新数据或修改数据的摄取方法。 |
| `scheduleParams.backfill` | 源的回填查询。 回填是指在其中摄取历史数据的摄取方法。 |

配置高级计划后，您必须参考 `scheduleParams` 在URL、body或header参数部分中，具体取决于您的特定源支持的内容。 在以下示例中， `{SCHEDULE_QUERY}` 是用于指定将使用增量和回填计划表达式的位置的占位符。 对于 [!DNL Zendesk] 来源， `query` 的 `queryParams` 指定高级计划。

```json
"urlParams": {
        "path": "/api/v2/search/export@{if(empty(coalesce(pipeline()?.parameters?.ingestionStart,'')),'?query=type:user&filter[type]=user&','')}",
        "method": "GET",
        "queryParams": {
          "query": "{SCHEDULE_QUERY}",
          "filter[type]": "user"
        }
      }
```

### 添加自定义架构以定义源的动态属性

您可以将自定义架构包含到 `sourceSpec` 定义源所需的所有属性，包括您可能需要的任何动态属性。 您可以通过向 `/connectionSpecs` 的端点 [!DNL Flow Service] API，同时在 `sourceSpec` 连接规范的部分。

以下是可添加到源连接规范中的自定义架构示例：

```json
      "schema": {
        "type": "object",
        "properties": {
          "results": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "organization_id": {
                  "type": "integer",
                  "minimum": -9007199254740992,
                  "maximum": 9007199254740991
                }
                "active": {
                  "type": "boolean"
                },
                "created_at": {
                  "type": "string"
                },
                "email": {
                  "type": "string"
                },
                "iana_time_zone": {
                  "type": "string"
                },
                "id": {
                  "type": "integer"
                },
                "locale": {
                  "type": "string"
                },
                "locale_id": {
                  "type": "integer"
                },
                "moderator": {
                  "type": "boolean"
                },
                "name": {
                  "type": "string"
                },
                "only_private_comments": {
                  "type": "boolean"
                },
                "report_csv": {
                  "type": "boolean"
                },
                "restricted_agent": {
                  "type": "boolean"
                },
                "result_type": {
                  "type": "string"
                },
                "role": {
                  "type": "integer"
                },
                "shared": {
                  "type": "boolean"
                },
                "shared_agent": {
                  "type": "boolean"
                },
                "suspended": {
                  "type": "boolean"
                },
                "ticket_restriction": {
                  "type": "string"
                },
                "time_zone": {
                  "type": "string"
                },
                "two_factor_auth_enabled": {
                  "type": "boolean"
                },
                "updated_at": {
                  "type": "string"
                },
                "url": {
                  "type": "string"
                },
                "verified": {
                  "type": "boolean"
                },
                "tags": {
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                }
              }
            }
          }
        }
      }
```


## 后续步骤

填充源规范后，您可以继续为要集成到平台的源配置浏览规范。 查看 [配置浏览规范](./explorespec.md) 以了解更多信息。

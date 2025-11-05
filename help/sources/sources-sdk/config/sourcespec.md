---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源sdk；sdk；SDK
title: 为自助源配置源规范(批处理SDK)
description: 本文档概述了为使用自助源(批处理SDK)而需要准备的配置。
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 2ff70ee6e4aa7fd723293e66000ccb161d61ab6a
workflow-type: tm+mt
source-wordcount: '2107'
ht-degree: 0%

---

# 为自助源配置源规范(批处理SDK)

Source规范包含特定于某个源的信息，包括与源的类别、测试版状态和目录图标相关的属性。 它们还包含有用的信息，如URL参数、内容、标题和计划。 Source规范还描述了从基本连接创建源连接所需的参数架构。 要创建源连接，必须使用架构。

有关完全填充的源规范示例，请参阅[附录](#source-spec)。


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
| `sourceSpec.attributes` | 包含有关UI或API专属源的信息。 |  |
| `sourceSpec.attributes.uiAttributes` | 显示特定于UI的源的信息。 |  |
| `sourceSpec.attributes.uiAttributes.isPreview` | 布尔属性，指示源是否显示为预览（不适用于生产/一般可用性）。 | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.isBeta` | 一个布尔属性，指示源是否需要客户提供更多反馈才能添加到其功能中。 | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | 定义源的类别。 | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | 定义用于在Experience Platform UI中呈现源的图标。 | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | 显示源的简要说明。 |  |
| `sourceSpec.attributes.uiAttributes.label` | 显示用于在Experience Platform UI中呈现源的标签。 |  |
| `sourceSpec.attributes.spec.properties.urlParams` | 包含有关URL资源路径、方法和支持的查询参数的信息。 |  |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | 定义从中获取数据的资源路径。 | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | 定义请求资源获取数据时使用的HTTP方法。 | `GET`、`POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | 定义支持的查询参数，这些参数可用于在发出获取数据的请求时附加源URL。 **注意**：任何用户提供的参数值都必须设置为占位符格式。 例如： `${USER_PARAMETER}`。 | `"queryParams" : {"key" : "value", "key1" : "value1"}`将附加到源URL中： `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | 定义在提取数据时需要在到源URL的HTTP请求中提供的标头。 | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | 此属性可以配置为通过POST请求发送HTTP正文。 |  |
| `sourceSpec.attributes.spec.properties.contentPath` | 定义包含需要摄取到Experience Platform的项列表的节点。 此属性应遵循有效的JSON路径语法，且必须指向特定数组。 | 查看[其他资源部分](#content-path)以了解内容路径中包含的资源示例。 |
| `sourceSpec.attributes.spec.properties.contentPath.path` | 指向要引入到Experience Platform的收藏集记录的路径。 | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | 通过此属性，可识别内容路径中标识的资源中将被排除在摄取范围之外的特定项目。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | 此属性允许您明确指定要保留的个别属性。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | 此属性允许您覆盖在`contentPath`中指定的属性名称值。 | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | 此属性允许您扁平化两个数组并将资源数据转换为Experience Platform资源。 |  |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | 指向要拼合的收藏集记录的路径。 | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | 此属性允许您从实体路径中标识的资源中标识要排除以不被引入的特定项目。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | 此属性允许您明确指定要保留的个别属性。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | 此属性允许您覆盖在`explodeEntityPath`中指定的属性名称值。 | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | 定义从用户的当前页面响应中或在创建下一页URL时必须提供的参数或字段，才能获取到下一页的链接。 |  |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | 显示源支持的分页类型的类型。 | <ul><li>`OFFSET`：此分页类型允许您通过指定从何处开始结果数组的索引以及返回结果数的限制来解析结果。</li><li>`POINTER`：此分页类型允许您使用`pointer`变量指向需要随请求发送的特定项。 指针类型分页要求有效负载中的路径指向下一页。</li><li>`CONTINUATION_TOKEN`：此分页类型允许您将查询或标头参数附加到接续令牌，以从源中检索因预设最大值而未最初返回的剩余返回数据。</li><li>`PAGE`：此分页类型允许您将查询参数附加到分页参数，以按页遍历返回数据，从第0页开始。</li><li>`NONE`：此分页类型可用于不支持任何可用分页类型的源。 分页类型`NONE`在请求后返回整个响应数据。</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | 限制的名称，API可通过该名称指定页面中要提取的记录数。 | `limit`或`count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | 页面中要获取的记录数。 | `limit=10`或`count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | 偏移属性名称。 如果分页类型设置为`offset`，则需要此项。 | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | 指针属性名称。 这需要指向指向下一页的属性的json路径。 如果分页类型设置为`pointer`，则需要此项。 | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | 包含定义源支持的计划格式的参数。 计划参数包括`startTime`和`endTime`，这两个参数允许您为批处理运行设置特定的时间间隔，从而确保不再获取在上一次批处理运行中获取的记录。 |  |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | 定义开始时间参数名称 | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | 定义结束时间参数名称 | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | 为`scheduleStartParamName`定义支持的格式。 | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | 为`scheduleEndParamName`定义支持的格式。 | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | 定义用户提供的用于获取资源值的参数。 | 有关[的用户输入参数的示例，请参阅](#user-input)其他资源`spec.properties`。 |

{style="table-layout:auto"}

## 其他资源 {#appendix}

以下部分提供了有关可对`sourceSpec`进行的其他配置的信息，包括高级计划和自定义架构。

### 内容路径示例 {#content-path}

以下是`contentPath`连接规范中[!DNL MailChimp Members]属性的内容示例。

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

### `spec.properties`用户输入示例 {#user-input}

以下是用户提供的`spec.properties`使用[!DNL MailChimp Members]连接规范的示例。

在此示例中，`listId`作为`urlParams.path`的一部分提供。 如果需要从客户检索`listId`，则还必须将其定义为`spec.properties`的一部分。


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

### Source规范示例 {#source-spec}

以下是使用[!DNL MailChimp Members]完成的源规范：

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

以下是自助源(批处理SDK)支持的其他分页类型示例：

>[!BEGINTABS]

>[!TAB 偏移]

此分页类型允许您通过指定从何处开始结果数组的索引以及返回结果数的限制来解析结果。 例如：

```json
"paginationParams": {
        "type": "OFFSET",
        "limitName": "limit",
        "limitValue": "4",
        "offSetName": "offset",
        "endConditionName": "$.hasMore",
        "endConditionValue": "Const:false"
}
```

| 属性 | 描述 |
| --- | --- |
| `type` | 用于返回数据的分页类型。 |
| `limitName` | 限制的名称，API可通过该名称指定页面中要提取的记录数。 |
| `limitValue` | 页面中要获取的记录数。 |
| `offSetName` | 偏移属性名称。 如果分页类型设置为`offset`，则需要此项。 |
| `endConditionName` | 用户定义的值，指示将在下一个HTTP请求中结束分页循环的条件。 必须提供要放置结束条件的属性名称。 |
| `endConditionValue` | 要放置结束条件的属性值。 |

>[!TAB 指针]

此分页类型允许您使用`pointer`变量指向需要随请求发送的特定项。 指针类型分页要求有效负载中的路径指向下一页。 例如：

```json
{
 "type": "POINTER",
 "limitName": "limit",
 "limitValue": 1,
 "pointerPath": "paging.next"
}
```

| 属性 | 描述 |
| --- | --- |
| `type` | 用于返回数据的分页类型。 |
| `limitName` | 限制的名称，API可通过该名称指定页面中要提取的记录数。 |
| `limitValue` | 页面中要获取的记录数。 |
| `pointerPath` | 指针属性名称。 这需要指向指向下一页的属性的json路径。 |

>[!TAB 继续令牌]

连续令牌类型的分页会返回一个字符串令牌，表示存在更多无法返回的项目，因为单个响应中可以返回的项目数已达到预设的最大值。

支持连续令牌类型分页的源可能具有类似于以下内容的分页参数：

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
| `continuationTokenPath` | 为移动到返回结果的下一页而必须附加到查询参数的值。 |
| `parameterType` | `parameterType`属性定义必须添加`parameterName`的位置。 `QUERYPARAM`类型允许您使用`parameterName`附加查询。 `HEADERPARAM`允许您将`parameterName`添加到标头请求。 |
| `parameterName` | 用于合并连续令牌的参数的名称。 格式如下： `{PARAMETER_NAME}={CONTINUATION_TOKEN}`。 |
| `delayRequestMillis` | 分页中的`delayRequestMillis`属性允许您控制向源发出的请求速率。 某些源对每分钟可以发出的请求数存在限制。 例如，[!DNL Zendesk]限制每分钟有100个请求，将`delayRequestMillis`定义为`850`允许您配置源以大约每分钟80个请求进行调用，远低于每分钟100个请求的阈值。 |

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

>[!TAB 页]

`PAGE`分页类型允许您按从零开始的页数遍历返回数据。 使用`PAGE`类型分页时，必须提供单个页面中给定的记录数。

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "pageSize",
  "limitValue": 100,
  "initialPageIndex": 1,
  "endPageIndex": "headers.x-pagecount",
  "pageParamName": "pageNumber",
  "maximumRequest": 10000
}
```

| 属性 | 描述 |
| --- | --- |
| `type` | 用于返回数据的分页类型。 |
| `limitName` | 限制的名称，API可通过该名称指定页面中要提取的记录数。 |
| `limitValue` | 页面中要获取的记录数。 |
| `initialPageIndex` | （可选）初始页索引定义分页将开始的页码。 此字段可用于分页不是从0开始的源。 如果未提供，则初始页面索引将默认为0。 此字段应为整数。 |
| `endPageIndex` | （可选）利用结束页面索引，可建立结束条件并停止分页。 当默认结束条件不可用以停止分页时，可以使用此字段。 如果要摄取的页数或通过响应标头提供最后一个页码，则也可以使用此字段，使用`PAGE`类型分页时通常会出现这种情况。 结束页索引的值可以是最后一个页码，也可以是响应标头中的字符串类型表达式值。 例如，您可以使用`headers.x-pagecount`将结束页面索引分配给响应标头中的`x-pagecount`值。 **注意**： `x-pagecount`是某些源的必需响应标头，它保存要摄取的页数的值。 |
| `pageParamName` | 为遍历返回数据的不同页面而必须附加到查询参数的参数名称。 例如，`https://abc.com?pageIndex=1`将返回API返回有效负载的第二页。 |
| `maximumRequest` | 源可为给定的增量运行发出的最大请求数。 当前的默认限制为10000。 |

{style="table-layout:auto"}


>[!TAB 无]

`NONE`分页类型可用于不支持任何可用分页类型的源。 在发出GET请求时，使用`NONE`分页类型的源只会返回所有可检索的记录。

```json
"paginationParams": {
  "type": "NONE"
}
```

>[!ENDTABS]

### 自助式源的高级计划(批处理SDK)

使用高级计划配置源的增量计划和回填计划。 `incremental`属性允许您配置计划，其中源将仅摄取新的或修改的记录，而`backfill`属性允许您创建计划以摄取历史数据。

通过高级计划，您可以使用特定于源的表达式和函数来配置增量计划和回填计划。 在下面的示例中，[!DNL Zendesk]源要求将增量计划的格式设置为`type:user updated > {START_TIME} updated < {END_TIME}`，并将回填设置为`type:user updated < {END_TIME}`。

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
| `scheduleParams.type` | 您的源将使用的计划类型。 将此值设置为`ADVANCE`以使用高级计划类型。 |
| `scheduleParams.paramFormat` | 计划参数的定义格式。 此值可以与源的`scheduleStartParamFormat`和`scheduleEndParamFormat`值相同。 |
| `scheduleParams.incremental` | 源的增量查询。 增量是指仅摄取新数据或修改数据的摄取方法。 |
| `scheduleParams.backfill` | 源的回填查询。 回填是指摄取历史数据的摄取方法。 |

配置高级计划后，您必须在URL、正文或标头参数部分中引用`scheduleParams`，具体取决于特定源支持的内容。 在下面的示例中，`{SCHEDULE_QUERY}`是用于指定将使用增量计划和回填计划表达式的占位符。 在[!DNL Zendesk]源的情况下，`query`中使用`queryParams`来指定高级计划。

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

您可以在`sourceSpec`中包含自定义架构，以定义源所需的所有属性，包括可能需要的任何动态属性。 您可以更新源对应的连接规范，方法是向`/connectionSpecs` API的[!DNL Flow Service]端点发出PUT请求，同时在连接规范的`sourceSpec`部分中提供自定义架构。

以下是您可以添加到源的连接规范中的自定义架构示例：

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

填充源规范后，您可以继续为要集成到Experience Platform的源配置浏览规范。 有关详细信息，请参阅有关[配置浏览规范](./explorespec.md)的文档。

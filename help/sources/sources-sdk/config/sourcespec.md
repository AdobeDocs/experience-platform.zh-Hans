---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK;SDK
title: 为源SDK配置源规范
topic-legacy: overview
description: 本文档概述了使用源SDK需要准备的配置。
hide: true
hidefromtoc: true
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 9727f7b0e8eaae92c85f102e5e7bea018a2ee6de
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---

# 为源SDK配置源规范

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
| `sourceSpec.attributes.spec.properties.contentPath` | 定义包含需要摄取到平台的项目列表的节点。 此属性应遵循有效的JSON路径语法，并且必须指向特定数组。 | 请参阅 [附录](#content-path) 例如，内容路径中包含的资源示例。 |
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
| `sourceSpec.attributes.spec.properties.paginationParams.type` | 显示源支持的分页类型的类型。 | <ul><li>`offset`:此分页类型允许您通过指定从何处开始生成数组的索引以及返回结果数量的限制来解析结果。</li><li>`pointer`:此分页类型允许您使用 `pointer` 变量来指向需要随请求一起发送的特定项目。 指针类型分页需要有效负荷中指向下一页的路径</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | API可以指定在页面中获取的记录数的限制的名称。 | `limit` 或 `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | 页面中要获取的记录数。 | `limit=10` 或 `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | 偏移属性名称。 如果分页类型设置为 `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | 指针属性名称。 这需要指向下一页的属性的json路径。 如果分页类型设置为 `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | 包含为源定义支持的计划格式的参数。 计划参数包括 `startTime` 和 `endTime`，这两种方法都允许您为批量运行设置特定时间间隔，这样可确保不会再次获取在之前批量运行中获取的记录。 |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | 定义开始时间参数名称 | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | 定义结束时间参数名称 | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | 为 `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | 为 `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | 定义用户提供的参数以获取资源值。 | 请参阅 [附录](#user-input) 例如，用户为 `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## 附录 {#appendix}

### 内容路径示例 {#content-path}

以下示例介绍了 `contentPath` 属性 [!DNL MailChimp Campaigns] 连接规范。

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

## 后续步骤

填充源规范后，您可以继续为要集成到平台的源配置浏览规范。 查看 [配置浏览规范](./explorespec.md) 以了解更多信息。

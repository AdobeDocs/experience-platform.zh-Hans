---
title: 搜索端点
description: 了解如何在Reactor API中调用/search端点。
exl-id: 14eb8d8a-3b42-42f3-be87-f39e16d616f4
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 1%

---

# 搜索端点

Reactor API中的`/search`端点提供了一种查找符合所需条件（以查询表示）的资源的方法。

以下API资源类型是可搜索的，它们使用与通过API返回的基于资源的文档相同的数据结构：

* `audit_events`
* `builds`
* `callbacks`
* `data_elements`
* `environments`
* `extension_packages`
* `extensions`
* `hosts`
* `libraries`
* `properties`
* `rule_components`
* `rules`

所有查询的范围均为您当前的公司和可访问属性。

>[!IMPORTANT]
>
>搜索功能具有以下注意事项和例外：
>
>* meta不可搜索，且未在搜索结果中返回。
>* 扩展包代理（操作、条件等）的架构字段可作为文本进行搜索，而非作为嵌套数据结构进行搜索。
>* 范围查询目前仅支持整数。

有关如何使用此功能的详细信息，请参阅[搜索指南](../guides/search.md)。

## 快速入门

本指南中使用的端点是[Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/)的一部分。 在继续之前，请查看[快速入门指南](../getting-started.md)，以了解有关如何对API进行身份验证的重要信息。

## 执行搜索 {#perform}

您可以通过发出POST请求来执行搜索。

**API格式**

```http
POST /search
```

**请求**

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "from": 0,
          "size": 25,
          "query": {
            "attributes.name": {
              "value": "Performance"
            },
            "attributes.revision_number": {
              "range": {
                "lte": "2",
                "gt": "0"
              }
            }
          },
          "sort": [
            {
              "attributes.revision_number": "desc"
            }
          ],
          "resource_types": [
            "data_elements",
            "rule_components"
          ]
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `from` | 响应偏移所依据的结果数。 |
| `size` | 要返回的最大结果数量。 结果不能超过100项。 |
| `query` | 表示搜索查询的对象。 对于此对象中的每个属性，键必须表示查询依据的字段路径，该值必须是其子属性决定查询对象的对象。<br><br>对于每个字段路径，您可以使用以下子属性：<ul><li>`exists`：如果资源中存在该字段，则返回true。</li><li>`value`：如果字段的值与此属性的值匹配，则返回true。</li><li>`value_operator`：布尔逻辑，用于确定应如何处理`value`查询。 允许值为`AND`和`OR`。 排除时，假定为`AND`逻辑。 有关详细信息，请参阅[值运算符逻辑](#value-operator)部分。</li><li>`range`如果字段的值在特定的数字范围内，则返回true。 范围本身由以下子属性决定：<ul><li>`gt`：大于提供的值，不包括。</li><li>`gte`：大于或等于提供的值。</li><li>`lt`：小于提供的值，不包括。</li><li>`lte`：小于或等于提供的值。</li></ul></li></ul> |
| `sort` | 一个对象数组，指示对结果进行排序的顺序。 每个对象必须包含一个属性：键代表排序依据的字段路径，值代表排序顺序（`asc`表示升序，`desc`表示降序）。 |
| `resource_types` | 字符串的数组，指示要搜索的特定资源类型。 |

{style="table-layout:auto"}

**响应**

成功的响应将返回查询的匹配资源列表。 有关API如何为特定值确定匹配的详细信息，请参阅[匹配约定](#conventions)的附录部分。

```json
{
  "data": [
    {
      "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:36:09.045Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Performance Indicator",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:36:09.045Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/property"
          },
          "data": {
            "id": "PR97d92a379a5f48758947cdf44f607a0d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/origin"
          },
          "data": {
            "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/extension"
          },
          "data": {
            "id": "EX0348d463358c4c89afe726245576f112",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension"
          },
          "data": {
            "id": "EX1cc78b39339242da82a0e0752fa53375",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d",
        "origin": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "self": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "extension": "https://reactor.adobe.io/extensions/EX0348d463358c4c89afe726245576f112"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "total_hits": 1
  }
}
```

## 附录

以下部分包含有关使用`/search`终结点的其他信息。

### 值运算符逻辑 {#value-operator}

搜索查询值将被拆分为多个搜索词，以便与已编制索引的文档进行匹配。 每个术语之间假定有`AND`关系。

使用`AND`作为`value_operator`时，`My Rule Holiday Sale`的查询值被解释为字段包含`My AND Rule AND Holiday AND Sale`的文档。

使用`OR`作为`value_operator`时，`My Rule Holiday Sale`的查询值被解释为字段包含`My OR Rule OR Holiday OR Sale`的文档。 匹配的术语越多，`match_score`越高。 由于部分术语匹配的性质，当没有任何内容与所需值接近时，您可以获得一个结果集，其中值仅在非常基本的级别上匹配，例如文本的少数字符。

### 匹配约定 {#conventions}

搜索涉及回答文档与所提供查询的相关程度。 文档数据的分析和索引方式直接影响着这一点。

下表列出了常见字段类型的匹配约定：

| 字段类型 | 匹配惯例 |
| --- | --- |
| 字符串 | 包含部分术语分析的文本，不区分大小写 |
| 枚举值 | 完全匹配，区分大小写 |
| 整数 | 完全匹配 |
| 浮动 | 完全匹配 |
| 时间戳 | 完全匹配（日期时间格式） |
| 显示名称 | 包含部分术语分析的文本，不区分大小写 |

API中出现的特定字段还有其他约定：

| 字段 | 匹配惯例 |
| --- | --- |
| `id` | 完全匹配，区分大小写 |
| `delegate_descriptor_id` | 完全匹配，区分大小写，术语在`::`上拆分 |
| `name` | 完全匹配，区分大小写 |
| `settings` | 包含部分术语分析的文本，不区分大小写 |
| `type` | 完全匹配，区分大小写 |

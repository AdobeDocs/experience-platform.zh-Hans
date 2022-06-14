---
title: 回调端点
description: 了解如何在Reactor API中对/callbacks端点进行调用。
exl-id: dd980f91-89e3-4ba0-a6fc-64d66b288a22
source-git-commit: 7f3b9ef9270b7748bc3366c8c39f503e1aee2100
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 8%

---

# 回调端点

回调是指Reactor API发送到特定URL（通常是您的组织托管的URL）的消息。

回调将与 [审核事件](./audit-events.md) 来跟踪Reactor API中的活动。 每次生成特定类型的审核事件时，回调都可以向指定的URL发送一条匹配的消息。

回调中指定URL后面的服务必须使用HTTP状态代码200（确定）或201（已创建）做出响应。 如果服务未通过以下任一状态代码做出响应，则会按以下时间间隔重试消息投放：

* 1分钟
* 5 分钟
* 30 分钟
* 1 小时
* 12 小时
* 1 天
* 3 天

>[!NOTE]
>
>重试间隔是相对于上一个间隔的。 例如，如果一分钟重试失败，则计划在一分钟尝试失败后（消息生成后六分钟）再进行五分钟的下一次尝试。

如果所有投放尝试均失败，则会丢弃消息。

回调恰好属于一个 [属性](./properties.md). 一个资产可以有多个回调。

## 快速入门

本指南中使用的端点是 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/). 在继续之前，请查看 [入门指南](../getting-started.md) 以了解有关如何对API进行身份验证的重要信息。

## 列表回调 {#list}

您可以通过发出GET请求，在资产下列出所有回调。

**API格式**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 的 `id` 要列出其回调的属性的。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>使用查询参数，可以根据以下属性过滤列出的回调：<ul><li>`created_at`</li><li>`updated_at`</li></ul>请参阅 [筛选响应](../guides/filtering.md) 以了解更多信息。

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应会返回指定属性的回调列表。

```json
{
  "data": [
    {
      "id": "CB26edef8d709243579589107bcda034da",
      "type": "callbacks",
      "attributes": {
        "created_at": "2020-12-14T17:34:47.082Z",
        "subscriptions": [
          "rule.created"
        ],
        "updated_at": "2020-12-14T17:34:47.082Z",
        "url": "https://www.example.com"
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da/property"
          },
          "data": {
            "id": "PR66a3356c73fc4aabb67ee22caae53d70",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70",
        "self": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## 查找回调 {#lookup}

您可以通过在GET请求的路径中提供回调的ID来查找该回调。

**API格式**

```http
GET /callbacks/{CALLBACK_ID}
```

| 参数 | 描述 |
| --- | --- |
| `CALLBACK_ID` | 的 `id` 你想查的回调函数。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应会返回回调的详细信息。

```json
{
  "data": {
    "id": "CBeef389cee8d84e69acef8665e4dcbef6",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:36.872Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:36.872Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6/property"
        },
        "data": {
          "id": "PRb513bbab52114573ac87f9848eea6ead",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb513bbab52114573ac87f9848eea6ead",
      "self": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6"
    }
  }
}
```

## 创建回调 {#create}

您可以通过发出POST请求来创建新回调。

**API格式**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| 参数 | 描述 |
| --- | --- |
| `PROPERTY_ID` | 的 `id` 的 [属性](./properties.md) 您正在定义下的回调。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.com",
            "subscriptions": [
              "rule.created"
            ]
          }
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `url` | 回调消息的URL目标。 URL必须使用HTTPS协议扩展。 |
| `subscriptions` | 字符串数组，用于指示将触发回调的审核事件类型。 请参阅 [audit events endpoint指南](./audit-events.md) ，以查看可能的事件类型列表。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回新创建回调的详细信息。

```json
{
  "data": {
    "id": "CB32d8f23d5ee548278d32076af4c442a0",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:27.059Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:27.059Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0/property"
        },
        "data": {
          "id": "PR5e22de986a7c4070965e7546b2bb108d",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d",
      "self": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0"
    }
  }
}
```

## 更新回调

您可以通过在回调请求的路径中包含其ID来更新回调PATCH。

**API格式**

```http
PATCH /callbacks/{CALLBACK_ID}
```

| 参数 | 描述 |
| --- | --- |
| `CALLBACK_ID` | 的 `id` 的回调函数。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求更新了 `subscriptions` 现有回调的数组。

```shell
curl -X PATCH \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.net",
            "subscriptions": [
              "rule.created",
              "build.created"
            ]
          },
          "type": "callbacks",
          "id": "CB4310904d415549888cc9e31ebe1e1e45"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `attributes` | 一个对象，其属性表示要为回调更新的属性。 每个键值都表示要更新的特定回调属性，以及应将其更新到的相应值。<br><br>可以为回调更新以下属性：<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | 的 `id` 的回调函数。 这应该与 `{CALLBACK_ID}` 值。 |
| `type` | 要更新的资源类型。 对于此端点，值必须为 `callbacks`. |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回更新的回调的详细信息。

```json
{
  "data": {
    "id": "CB4310904d415549888cc9e31ebe1e1e45",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:56.884Z",
      "subscriptions": [
        "rule.created",
        "build.created"
      ],
      "updated_at": "2020-12-14T17:34:57.614Z",
      "url": "https://www.example.net"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45/property"
        },
        "data": {
          "id": "PR0a8ef3ca31dc456a8566e9288960bd79",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR0a8ef3ca31dc456a8566e9288960bd79",
      "self": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45"
    }
  }
}
```

## 删除回调

您可以通过在回调请求的路径中包含其ID来删除该回调。

**API格式**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| 参数 | 描述 |
| --- | --- |
| `CALLBACK_ID` | 的 `id` 的回调函数。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X DELETE \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应会返回没有响应正文的HTTP状态204（无内容），表示已删除回调。

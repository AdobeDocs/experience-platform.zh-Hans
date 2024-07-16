---
title: 回调端点
description: 了解如何在Reactor API中调用/callbacks端点。
exl-id: dd980f91-89e3-4ba0-a6fc-64d66b288a22
source-git-commit: 7f3b9ef9270b7748bc3366c8c39f503e1aee2100
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 6%

---

# 回调端点

回调是Reactor API发送到特定URL（通常由您的组织托管）的消息。

回调旨在与[审核事件](./audit-events.md)结合使用，以跟踪Reactor API中的活动。 每次生成特定类型的审核事件时，回调都会向指定的URL发送匹配消息。

位于回调中指定的URL后面的服务必须使用HTTP状态代码200 （确定）或201 （已创建）进行响应。 如果服务没有响应这两个状态代码中的任何一个，则按以下时间间隔重试消息投放：

* 1分钟
* 5 分钟
* 30 分钟
* 1 小时
* 12 小时
* 1 天
* 3 天

>[!NOTE]
>
>重试间隔相对于上一个间隔。 例如，如果在一分钟时重试失败，则下次尝试安排在一分钟尝试失败后（生成消息后6分钟）的5分钟内。

如果所有投放尝试都不成功，则消息将被丢弃。

回调只属于一个[属性](./properties.md)。 资产可以有许多回调。

## 快速入门

本指南中使用的端点是[Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/)的一部分。 在继续之前，请查看[快速入门指南](../getting-started.md)，以了解有关如何对API进行身份验证的重要信息。

## 列出回调 {#list}

您可以通过发出GET请求来列出资产下的所有回调。

**API格式**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 要列出其回调的属性`id`。 |

{style="table-layout:auto"}

>[!NOTE]
>
>使用查询参数，可以根据以下属性过滤列出的回调：<ul><li>`created_at`</li><li>`updated_at`</li></ul>有关详细信息，请参阅[筛选响应](../guides/filtering.md)指南。

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

成功的响应将返回指定属性的回调列表。

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
| `CALLBACK_ID` | 要查找的回调的`id`。 |

{style="table-layout:auto"}

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

成功的响应将返回回调的详细信息。

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

您可以通过发出POST请求来创建新的回调。

**API格式**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| 参数 | 描述 |
| --- | --- |
| `PROPERTY_ID` | 您正在定义回调的[属性](./properties.md)的`id`。 |

{style="table-layout:auto"}

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
| `subscriptions` | 一个字符串数组，指示将触发回调的审核事件类型。 有关可能的事件类型列表，请参阅[审核事件终结点指南](./audit-events.md)。 |

{style="table-layout:auto"}

**响应**

成功的响应将返回新创建的回调的详细信息。

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

您可以通过在PATCH请求的路径中包含回调的ID来更新回调。

**API格式**

```http
PATCH /callbacks/{CALLBACK_ID}
```

| 参数 | 描述 |
| --- | --- |
| `CALLBACK_ID` | 要更新的回调的`id`。 |

{style="table-layout:auto"}

**请求**

以下请求更新现有回调的`subscriptions`数组。

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
| `attributes` | 一个对象，其属性表示要针对回调更新的属性。 每个键表示要更新的特定回调属性以及应更新到的相应值。<br><br>可以更新回调的以下属性：<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | 要更新的回调的`id`。 这应当与在请求路径中提供的`{CALLBACK_ID}`值匹配。 |
| `type` | 正在更新的资源类型。 对于此终结点，值必须为`callbacks`。 |

{style="table-layout:auto"}

**响应**

成功的响应将返回已更新回调的详细信息。

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

您可以通过在DELETE请求的路径中包含回调的ID来删除回调。

**API格式**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| 参数 | 描述 |
| --- | --- |
| `CALLBACK_ID` | 要删除的回调的`id`。 |

{style="table-layout:auto"}

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

成功的响应返回HTTP状态204（无内容），没有响应正文，这表示已删除回调。

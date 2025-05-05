---
title: 将Offer Decisioning与Experience Platform Web SDK一起使用
description: Adobe Experience Platform Web SDK可以交付和呈现Offer Decisioning中管理的个性化优惠。 您可以使用Offer Decisioning UI或API创建优惠和其他相关对象。
keywords: offer decisioning；decisioning；Web SDK；Experience Platform Web SDK；个性化优惠；投放优惠；优惠投放；优惠个性化；
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 3%

---

# 将Offer Decisioning与Experience Platform Web SDK一起使用

Adobe Experience Platform [!DNL Web SDK]可以投放和渲染在Offer Decisioning中管理的个性化优惠。 您可以使用Offer Decisioning用户界面(UI)或API创建优惠和其他相关对象。

## 先决条件

* 为边缘决策启用组织
* 优惠，创建的活动
* 数据流已发布

## 术语

在使用Offer Decisioning时，请务必了解以下术语。 有关更多信息和查看更多术语，请访问[Offer Decisioning术语表](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html?lang=zh-Hans)。

* **决策范围：**&#x200B;对于Offer Decisioning，决策范围是JSON的Base64编码字符串，其中包含您希望优惠决策服务用来建议优惠的活动和版面ID。

  *决策范围JSON：*

  ```json
  {
    "activityId":"xcore:offer-activity:11cfb1fa93381aca",
    "placementId":"xcore:offer-placement:1175009612b0100c"
  }
  ```

  *决策范围Base64编码字符串：*

  ```json
  "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
  ```

  >[!TIP]
  >
  >您可以从UI中的&#x200B;**活动概述**&#x200B;页面复制决策范围值。

  ![决策副本设置。](assets/decision-scope-copy.png)

* **数据流：**&#x200B;有关详细信息，请阅读[数据流](/help/datastreams/overview.md)文档。

* **标识**：有关详细信息，请阅读此文档，其中概述了[Experience Platform Web SDK如何使用标识服务](../../identity/overview.md)。

## 启用Offer Decisioning

要启用Offer Decisioning，请执行以下步骤：

1. 已在[数据流](/help/datastreams/overview.md)中启用Adobe Experience Platform并选中“Offer Decisioning”框

   ![offer-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)

1. 按照说明[安装SDK](/help/web-sdk/install/overview.md) (SDK可以独立安装，也可以通过UI安装。 有关详细信息，请参阅[标记快速入门指南](/help/tags/quick-start/quick-start.md)。
1. 使用`personalization.decisionScopes`为Offer Decisioning配置SDK。 下面提供了其他Offer Decisioning特定步骤。

   * 安装独立的SDK

      1. 使用`personalization.decisionScopes`配置“sendEvent”操作

     ```javascript
     alloy("sendEvent", {
       ...
       "personalization": {
         "decisionScopes": [
           "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
           "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
         ]
       }
     });
     ```

   * 通过标记安装SDK

      1. [创建标记属性](/help/tags/ui/administration/companies-and-properties.md)
      1. [添加嵌入代码](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html?lang=zh-Hans)
      1. 通过从“数据流”下拉列表中选择配置，使用您创建的数据流安装和配置Experience Platform Web SDK扩展。 请参阅有关[扩展](/help/tags/ui/managing-resources/extensions/overview.md)的文档。

         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)

      1. 创建必要的[数据元素](/help/tags/ui/managing-resources/data-elements.md)。 您必须至少创建一个Experience Platform Web SDK标识映射和一个Experience Platform Web SDK XDM对象数据元素。

         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)

      1. 创建您的[规则](/help/tags/ui/managing-resources/rules.md)。

         * 添加Experience Platform Web SDK“发送事件”操作，并将相关的`decisionScopes`添加到该操作的配置

         ![send-event-action-decisionScopes](./assets/send-event-action-decisionScopes.png)

      1. [创建并发布一个库](/help/tags/ui/publishing/libraries.md)，其中包含您已配置的所有相关规则、数据元素和扩展

## 示例请求和响应

### 一个`decisionScopes`值

**请求**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
          ]
        }
      }
    }
  ]
}
```

| 属性 | 必需 | 描述 | 限制 | 示例 |
|---|---|---|---|---|
| `identityMap` | 是 | 请参阅此[Identity Service文档](../../identity/overview.md)。 | 每个请求一个身份。 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`的问题。<br><br>注意：用户不需要在API调用中包含`ECID`参数。 如果需要，此参数会自动添加到调用中。 |
| `decisionScopes` | 是 | 包含活动和版面ID的JSON的Base64编码字符串数组。 | 每个请求最多30 `decisionScopes`。 | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

**响应**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:124cc332095cfa74",
                "format": "text/html",
                "language": [
                  "en-US"
                ],
                "content": "<p>20% Off on shipping</p>",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| 属性 | 描述 | 示例 |
|---|---|---|
| `scope` | 导致建议优惠的决策范围。 | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | 优惠活动的唯一ID。 | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | 优惠投放位置的唯一ID。 | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | 建议优惠的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 与建议选件关联的内容的架构。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 建议优惠的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 与建议选件关联的内容的格式。 | `"format": "text/html"` |
| `language` | 与建议选件中的内容关联的一系列语言。 | `"language": [ "en-US" ]` |
| `content` | 以字符串格式与建议选件关联的内容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式显示的与建议选件关联的图像内容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 与JSON对象格式中提议的选件关联的特征。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### 多个`decisionScopes`值

**请求**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyYzkxMzg1Mjc2MDE4YyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMzMxZjU2MTYyYWEyZjcifQ=="
          ]
        }
      }
    }
  ]
}
```

| 属性 | 必需 | 描述 | 限制 | 示例 |
|---|---|---|---|---|
| `identityMap` | 是 | 请参阅此[Identity Service文档](../../identity/overview.md)。 | 每个请求一个身份。 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`的问题。<br><br>注意：用户不需要在API调用中包含`ECID`参数。 如果需要，此参数会自动添加到调用中。 |
| `decisionScopes` | 是 | 包含活动和版面ID的JSON的Base64编码字符串数组。 | 每个请求最多30 `decisionScopes`。 | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

**响应**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MTEyMyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDExMjMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381123",
            "etag": "1"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b01123",
            "etag": "3"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a22954123",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-text",
              "etag": "2",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a22954123",
                "format": "text/text",
                "language": [
                  "en"
                ],
                "content": "20% Off on shipping",
                "characteristics": {
                  "foo2": "bar2"
                }
              }
            }
          ]
        },
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a2295415d",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a2295415d",
                "format": "image/png",
                "language": [
                  "en"
                ],
                "deliveryURL": "https://image.jpeg",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| 属性 | 描述 | 示例 |
|---|---|---|
| `scope` | 导致建议优惠的决策范围。 | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | 优惠活动的唯一ID。 | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | 优惠投放位置的唯一ID。 | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | 建议优惠的ID。 | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | 与建议选件关联的内容的架构。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | 建议优惠的ID。 | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | 与建议选件关联的内容的格式。 | `"format": "text/text"` |
| `language` | 与建议选件中的内容关联的一系列语言。 | `"language": [ "en-US" ]` |
| `content` | 以字符串格式与建议选件关联的内容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式显示的与建议选件关联的图像内容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 与JSON对象格式中提议的选件关联的特征。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

## 限制

当前移动设备Edge Network工作流不支持某些优惠限制，例如上限。 “上限”字段值指定选件在所有用户中显示的次数。 有关更多详细信息，请参阅[优惠资格规则和约束文档](https://experienceleague.adobe.com/docs/offer-decisioning/using/managing-offers-in-the-offer-library/creating-personalized-offers.html?lang=zh-Hans#eligibility)。

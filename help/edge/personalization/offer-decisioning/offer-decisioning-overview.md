---
title: Offer Decisioning概述
seo-title: Offer Decisioning和Adobe Experience PlatformWeb SDK
description: Adobe Experience PlatformWeb SDK可交付和呈现在Offer Decisioning管理的个性化优惠。 您可以使用Offer DecisioningUI或API创建优惠和其他相关对象。
seo-description: Adobe Experience PlatformWeb SDK可交付和呈现在Offer Decisioning管理的个性化优惠。 您可以使用Offer DecisioningUI或API创建优惠和其他相关对象。
keywords: offer decisioning;decisioning;Web SDK;Platform Web SDK;personalized offers;deliver offers;offer delivery;offer personalization;
translation-type: tm+mt
source-git-commit: a0ede8c7d3088fe80d6ea014b4a4f9f08ee8a7aa
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 9%

---


# [!DNL Offer Decisioning] 概述

>[!NOTE]
>
>Offer Decisioning在Adobe Experience PlatformWeb SDK中的使用目前可供选定用户早期访问。 此功能并非所有IMS组织都可用。

Adobe Experience Platform [!DNL Web SDK] 可以提供和呈现在Offer Decisioning管理的个性化优惠。 您可以使用Offer Decisioning用户界面(UI)或API创建优惠和其他相关对象。

## 先决条件

* IMS组织已启用边缘决策
* 优惠,活动创建
* 已发布边缘配置

## 术语

与Offer Decisioning合作时，必须了解以下术语。 <!--For more information and to view additional terms, please visit the [Offer Decisioning glossary](/docs/offer-decisioning/using/get-started/glossary.html)-->.

* **容器:** 容器是一种隔离机制，可以分开不同的关注点。 容器ID是所有存储库API的第一个路径元素。 所有决策对象都驻留在容器中。

* **决策范围：** 对于Offer Decisioning，这些是Base64编码的JSON字符串，包含您希望优惠决策服务用于建议优惠的活动和位置ID。

   *决策范围JSON:*

   ```json
   {
     "activityId":"xcore:offer-activity:11cfb1fa93381aca",
     "placementId":"xcore:offer-placement:1175009612b0100c"
   }
   ```

   *决策范围Base64编码的字符串：*

   ```json
   "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
   ```

   >[!TIP]
   >
   >您可以从UI的“活动概述”页 **面复制** 决策范围值。

   ![](assets/decision-scope-copy.png)

* **边缘配置：** 有关详细信息，请阅读 [边缘配置](../../fundamentals/edge-configuration.md) 文档。

* **身份**:有关详细信息，请阅读本文档，其中概 [述了Platform Web SDK如何利用Identity Service](../../identity/overview.md)。

## 使Offer Decisioning

要启用Offer Decisioning，您需要执行以下步骤：

1. 在边缘配置中 [启用Adobe Experience Platform](../../fundamentals/edge-configuration.md) ，并选中“Offer Decisioning”框
   ![优惠决策——边缘配置](./assets/offer-decisioning-edge-config.png)
2. 按照说明安 [装SDK](../../fundamentals/installing-the-sdk.md) (SDK可以单独安装或通过 [Adobe Experience Platform Launch安装](http://launch.adobe.com/)。 以下是平 [台启动的快速开始指南](https://docs.adobe.com/content/help/zh-Hans/launch/using/intro/get-started/quick-start.html))。
3. [为Offer Decisioning配置](../../fundamentals/configuring-the-sdk.md) SDK。 下文提供Offer Decisioning的其他具体步骤。
   * 独立安装的SDK
      1. 使用 `decisionScopes`

      ```javascript
      alloy("sendEvent", {
          ...
          "decisionScopes": [
              "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
              "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
          ]
      })
      ```
   * 平台启动已安装SDK
      1. [创建平台启动属性](https://docs.adobe.com/content/help/zh-Hans/launch/using/reference/admin/companies-and-properties.html)
      2. [添加平台启动嵌入代码](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      3. 通过从“边缘配置”下拉菜单中选择您刚刚创建的配置，安装并配置AEP Web SDK扩展。 有关扩展的有 [用文档](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html)。
         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)
      4. 创建必要的 [数据元素](https://docs.adobe.com/content/help/zh-Hans/launch/using/reference/manage-resources/data-elements.html)。 至少，您需要创建一个平台Web SDK标识映射和一个平台Web SDK XDM对象数据元素。
         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)
      5. 创建规 [则](https://docs.adobe.com/content/help/zh-Hans/launch/using/reference/manage-resources/rules.html)。
         * 添加Platform Web SDK发送事件操作，并将相 `decisionScopes` 关内容添加到该操作的配置
            ![send-事件-action-decisionScopes](./assets/send-event-action-decisionScopes.png)
      6. [创建并发布包含](https://docs.adobe.com/content/help/zh-Hans/launch/using/reference/publish/libraries.html) 您配置的所有相关规则、数据元素和扩展的库


## 示例请求和响应

### 一个 `decisionScopes` 值

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
| `identityMap` | 是 | 请参阅此 [Identity Service文档](../../identity/overview.md)。 | 每个请求一个身份。 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | 是 | 包含活动和位置ID的JSON的Base64编码字符串数组。 | 每个请求 `decisionScopes` 最多30个。 | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

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
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
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
| `scope` | 产生拟议优惠的决定范围。 | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `items.id` | 建议优惠的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 与建议的优惠关联的内容的模式。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 建议优惠的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 与建议的优惠关联的内容的格式。 | `"format": "text/html"` |
| `language` | 与建议优惠中的内容关联的语言数组。 | `"language": [ "en-US" ]` |
| `content` | 以字符串格式与建议优惠关联的内容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式与建议优惠关联的图像内容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 与JSON对象格式的建议优惠关联的特性。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### 多个 `decisionScopes` 值

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
| `identityMap` | 是 | 请参阅此 [Identity Service文档](../../identity/overview.md)。 | 每个请求一个身份。 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | 是 | 包含活动和位置ID的JSON的Base64编码字符串数组。 | 每个请求 `decisionScopes` 最多30个。 | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

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
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
              "data": {
                "id": "xcore:personalized-offer:124cc332095cfa74",
                "format": "text/html",
                "language": [
                  "en-US"
                ],
                "content": "<p style=\"color:red;\">20% Off on shipping</p>",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ==",
          "items": [
            {
              "id": "xcore:personalized-offer:235fe313094cdb75",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-text",
              "data": {
                "id": "xcore:personalized-offer:235fe313094cdb75",
                "format": "text/text",
                "language": [
                  "en-US"
                ],
                "content": "20% Off on shipping",
                "characteristics": {
                  "foo2": "bar2",
                  "foo3": "bar3"
                }
              }
            }
          ]
        }
      ],
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyYzkxMzg1Mjc2MDE4YyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMzMxZjU2MTYyYWEyZjcifQ==",
          "items": [
            {
              "id": "xcore:personalized-offer:312de312095cda65",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
              "data": {
                "id": "xcore:personalized-offer:312de312095cda65",
                "format": "image/png",
                "language": [
                  "en-US"
                ],
                "deliveryURL": "https://image.jpeg"
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
| `scope` | 产生拟议优惠的决定范围。 | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `items.id` | 建议优惠的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 与建议的优惠关联的内容的模式。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 建议优惠的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 与建议的优惠关联的内容的格式。 | `"format": "text/html"` |
| `language` | 与建议优惠中的内容关联的语言数组。 | `"language": [ "en-US" ]` |
| `content` | 以字符串格式与建议优惠关联的内容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式与建议优惠关联的图像内容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 与JSON对象格式的建议优惠关联的特性。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

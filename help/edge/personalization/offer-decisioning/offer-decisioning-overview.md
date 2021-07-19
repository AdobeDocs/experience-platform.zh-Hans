---
title: 将Offer decisioning与Platform Web SDK结合使用
description: Adobe Experience Platform Web SDK可以提供和渲染在Offer decisioning中管理的个性化选件。 您可以使用Offer decisioningUI或API创建选件和其他相关对象。
keywords: offer decisioning；决策；Web SDK;Platform Web SDK；个性化选件；提供选件；选件交付；选件个性化；
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 3%

---

# 将Offer decisioning与Platform Web SDK结合使用

>[!NOTE]
>
>目前，在Adobe Experience Platform Web SDK中使用Offer decisioning可供选定用户抢先体验。 并非所有IMS组织都能使用此功能。

Adobe Experience Platform [!DNL Web SDK]可以交付和渲染在Offer decisioning中管理的个性化选件。 您可以使用Offer decisioning用户界面(UI)或API创建选件和其他相关对象。

## 先决条件

* IMS组织已启用边缘决策
* 选件、已创建的活动
* 数据流已发布

## 术语

使用Offer decisioning时，请务必了解以下术语。 有关更多信息和查看其他术语，请访问[Offer decisioning术语表](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html)。

* **容器：** 容器是一种隔离机制，可分开不同的关注点。容器ID是所有存储库API的第一个路径元素。 所有决策对象都驻留在容器中。

* **决策范围：** 对于Offer decisioning，这些是JSON的Base64编码字符串，其中包含您希望offer decisioning服务用于建议选件的活动和版面ID。

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
   >您可以从UI的&#x200B;**活动概述**&#x200B;页面复制决策范围值。

   ![](assets/decision-scope-copy.png)

* **数据流：** 有关更多信息，请阅读 [](../../fundamentals/datastreams.md) datastreams文档。

* **身份**:有关更多信息，请阅读此文档概述 [Platform Web SDK如何利用Identity Service](../../identity/overview.md)。

## 启用Offer decisioning

要启用Offer decisioning，您需要执行以下步骤：

1. 在[datastream](../../fundamentals/datastreams.md)中启用Adobe Experience Platform，并选中“Offer decisioning”框

   ![offer-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)

1. 按照[安装SDK](../../fundamentals/installing-the-sdk.md)的说明操作(SDK可以独立安装，也可以通过[Adobe Experience Platform Launch](http://launch.adobe.com/)进行安装。 以下是[Platform launch快速入门指南](../../../tags/quick-start/quick-start.md))。
1. [配置SDK](../../fundamentals/configuring-the-sdk.md) 以Offer decisioning。下面提供了其他Offer decisioning特定步骤。

   * 独立安装的SDK

      1. 使用`decisionScopes`配置“sendEvent”操作

         ```javascript
          alloy("sendEvent", {
             ...
             "decisionScopes": [
                 "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
                 "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
             ]
          })
         ```
   * platform launch安装的SDK

      1. [创建Platform launch资产](../../../tags/ui/administration/companies-and-properties.md)
      1. [添加Platform launch嵌入代码](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      1. 使用您刚刚创建的数据流安装和配置Platform Web SDK扩展，方法是从“数据流”下拉菜单中选择配置。 请参阅关于[extensions](../../../tags/ui/managing-resources/extensions/overview.md)的文档。

         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)

      1. 创建必要的[数据元素](../../../tags/ui/managing-resources/data-elements.md)。 您至少必须创建Platform Web SDK身份映射和Platform Web SDK XDM对象数据元素。

         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)

      1. 创建[Rules](../../../tags/ui/managing-resources/rules.md)。

         * 添加Platform Web SDK发送事件操作，并将相关的`decisionScopes`添加到该操作的配置中

            ![send-event-action-decisionScopes](./assets/send-event-action-decisionScopes.png)
      1. [创建并发布包](../../../tags/ui/publishing/libraries.md) 含您配置的所有相关规则、数据元素和扩展的库



## 请求和响应示例

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
| `identityMap` | 是 | 请参阅此[Identity Service文档](../../identity/overview.md)。 | 每个请求一个标识。 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | 是 | 包含活动ID和位置ID的JSON的Base64编码字符串数组。 | 每个请求最多30个`decisionScopes`。 | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

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
| `scope` | 产生建议报价的决定范围。 | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | 选件活动的唯一ID。 | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | 选件版面的唯一ID。 | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | 建议的选件的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 与建议的选件关联的内容的架构。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 建议的选件的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 与建议的选件关联的内容格式。 | `"format": "text/html"` |
| `language` | 与建议选件中的内容关联的语言数组。 | `"language": [ "en-US" ]` |
| `content` | 与建议的选件关联的内容（以字符串格式）。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 与建议的选件关联的图像内容采用URL格式。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 与JSON对象格式的建议选件关联的特性。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

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
| `identityMap` | 是 | 请参阅此[Identity Service文档](../../identity/overview.md)。 | 每个请求一个标识。 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | 是 | 包含活动ID和位置ID的JSON的Base64编码字符串数组。 | 每个请求最多30个`decisionScopes`。 | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

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
| `scope` | 产生建议报价的决定范围。 | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | 选件活动的唯一ID。 | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | 选件版面的唯一ID。 | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | 建议的选件的ID。 | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | 与建议的选件关联的内容的架构。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | 建议的选件的ID。 | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | 与建议的选件关联的内容格式。 | `"format": "text/text"` |
| `language` | 与建议选件中的内容关联的语言数组。 | `"language": [ "en-US" ]` |
| `content` | 与建议的选件关联的内容（以字符串格式）。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 与建议的选件关联的图像内容采用URL格式。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 与JSON对象格式的建议选件关联的特性。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

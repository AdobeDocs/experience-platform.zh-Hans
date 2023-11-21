---
title: 使用Web SDK和边缘网络服务器API的混合个性化
description: 本文演示了如何将Web SDK与服务器API结合使用，在Web资产上部署混合个性化。
keywords: 个性化；混合；服务器API；服务器端；混合实现；
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: 33e69f34934b505e2ee434bc957f278486a97642
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 2%

---

# 使用Web SDK和边缘网络服务器API的混合个性化

## 概述 {#overview}

混合个性化描述使用检索服务器端个性化内容的过程。 [边缘网络服务器API](../..//server-api/overview.md)，并在客户端呈现，使用 [Web SDK](../home.md).

您可以将混合个性化与Adobe Target或Offer Decisioning等个性化解决方案一起使用，其区别在于 [!UICONTROL 服务器API] 有效负荷。

## 先决条件 {#prerequisites}

在Web资产上实施混合个性化之前，请确保满足以下条件：

* 您已决定要使用的个性化解决方案。 这将对以下内容的内容产生影响： [!UICONTROL 服务器API] 有效负荷。
* 您有权访问应用程序服务器，您可以使用该服务器来 [!UICONTROL 服务器API] 呼叫。
* 您有权访问 [边缘网络服务器API](../../server-api/authentication.md).
* 您已正确设置 [已配置和部署](../fundamentals/configuring-the-sdk.md) 要个性化的页面上的Web SDK。

## 流程图 {#flow-diagram}

以下流程图描述了实现混合个性化的步骤顺序。

![显示混合个性化步骤顺序的可视化流程图。](assets/hybrid-personalization-diagram.png)

1. 之前由浏览器存储的任何现有Cookie，前缀为 `kndctr_`，包含在浏览器请求中。
1. 客户端Web浏览器向应用程序服务器请求网页。
1. 当应用程序服务器收到页面请求时，会发出 `POST` 请求 [服务器API交互式数据收集端点](../../server-api/interactive-data-collection.md) 以获取个性化内容。 此 `POST` 请求包含 `event` 和 `query`. 上一步的Cookie（如果可用）包含在 `meta>state>entries` 数组。
1. 服务器API将个性化内容返回到应用程序服务器。
1. 应用程序服务器向客户端浏览器返回HTML响应，其中包含 [身份和集群Cookie](#cookies).
1. 在客户端页面上， [!DNL Web SDK] `applyResponse` 调用命令，传入的标头和正文 [!UICONTROL 服务器API] 上一步的响应。
1. 此 [!DNL Web SDK] 渲染页面加载 [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) 自动选件，因为 `renderDecisions` 标志设置为 `true`.
1. 基于表单 [!DNL JSON] 选件通过以下方式手动应用 `applyPersonalization` 方法，更新 [!DNL DOM] 基于个性化选件。
1. 对于基于表单的活动，必须手动发送显示事件，以指示何时显示选件。 这可以通过以下方式实现 `sendEvent` 命令。

## Cookie {#cookies}

Cookie用于保留用户标识和群集信息。  使用混合实施时，Web应用程序服务器会在请求生命周期中处理这些Cookie的存储和发送。

| Cookie | 用途 | 存储者 | 发送者 |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | 包含用户身份详细信息。 | 应用程序服务器 | 应用程序服务器 |
| `kndctr_AdobeOrg_cluster` | 指示应使用哪个Edge Network群集来完成请求。 | 应用程序服务器 | 应用程序服务器 |

## 请求投放 {#request-placement}

需要服务器API请求才能获取建议并发送显示通知。 使用混合实施时，应用程序服务器向服务器API发出这些请求。

| 请求 | 创建者 |
|---|---|
| 用于检索建议的Interact请求 | 应用程序服务器 |
| Interact请求发送显示通知 | 应用程序服务器 |

## Analytics含义 {#analytics}

实施混合个性化时，必须特别注意，以便Analytics中的页面点击不会被计数多次。

当您 [配置数据流](../../datastreams/overview.md) 对于Analytics，会自动转发事件，以便捕获页面点击。

此实施中的示例使用两个不同的数据流：

* 为Analytics配置的数据流。 此数据流用于Web SDK交互。
* 第二个不具有Analytics配置的数据流。 此数据流用于服务器API请求。 您必须使用与Analytics配置的数据流相同的目标配置来配置此数据流。

这样一来，服务器端请求就不会注册任何Analytics事件，而客户端请求会注册。 这将导致Analytics请求被准确计数。


## 服务器端请求 {#server-side-request}

以下示例请求说明了您的应用程序服务器可用于检索个性化内容的服务器API请求。

>[!IMPORTANT]
>
>此示例请求使用Adobe Target作为个性化解决方案。 您的请求可能会因您选择的个性化解决方案而异。


**API格式**

```http
POST /ee/v2/interact
```

### 请求 {#request}

```shell
curl -X POST "https://edge.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Content-Type: text/plain" 
-d '{
   "event":{
      "xdm":{
         "web":{
            "webPageDetails":{
               "URL":"http://localhost/"
            },
            "webReferrer":{
               "URL":""
            }
         },
         "identityMap":{
            "FPID":[
               {
                  "id":"xyz",
                  "authenticatedState":"ambiguous",
                  "primary":true
               }
            ]
         },
         "timestamp":"2022-06-23T22:21:00.878Z"
      },
      "data":{
         
      }
   },
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      },
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/default-content-item",
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "sample-json-offer"
         ]
      }
   },
   "meta":{
      "state":{
         "domain":"localhost",
         "cookiesEnabled":true,
         "entries":[
            {
               "key":"kndctr_XXX_AdobeOrg_identity",
               "value":"abc123"
            },
            {
               "key":"kndctr_XXX_AdobeOrg_cluster",
               "value":"or2"
            }
         ]
      }
   }
}'
```

| 参数 | 类型 | 必需 | 描述 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 可以。 | 用于将交互传递到Edge Network的数据流的ID。 请参阅 [数据流概述](../../datastreams/overview.md) 了解如何配置数据流。 |
| `requestId` | `String` | 否 | 用于关联内部服务器请求的随机ID。 如果未提供，Edge Network将生成一个，并在响应中返回它。 |

### 服务器端响应 {#server-response}

下面的示例响应显示了服务器API响应可能的外观。


```json
{
   "requestId":"5c539bd0-33bf-43b6-a054-2924ac58038b",
   "handle":[
      {
         "payload":[
            {
               "id":"XXX",
               "namespace":{
                  "code":"ECID"
               }
            }
         ],
         "type":"identity:result"
      },
      {
         "payload":[
            {
               "..."
            },
            {
               "..."
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      }
   ]
}
```

## 客户端请求 {#client-request}

在客户端页面上， [!DNL Web SDK] `applyResponse` 调用命令，传入服务器端响应的标头和正文。

```js
   alloy("applyResponse", {
      "renderDecisions": true,
      "responseHeaders": {
         "cache-control": "no-cache, no-store, max-age=0, no-transform, private",
         "connection": "close",
         "content-encoding": "deflate",
         "content-type": "application/json;charset=utf-8",
         "date": "Mon, 11 Jul 2022 19:42:01 GMT",
         "server": "jag",
         "strict-transport-security": "max-age=31536000; includeSubDomains",
         "transfer-encoding": "chunked",
         "vary": "Origin",
         "x-adobe-edge": "OR2;9",
         "x-content-type-options": "nosniff",
         "x-konductor": "22.6.78-BLACKOUTSERVERDOMAINS:7fa23f82",
         "x-rate-limit-remaining": "599",
         "x-request-id": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "x-xss-protection": "1; mode=block"
      },
      "responseBody": {
         "requestId": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "handle": [
         {
            "payload": [
               {
               "id": "XXX",
               "namespace": {
                  "code": "ECID"
               }
               }
            ],
            "type": "identity:result"
         },
         {
            "payload": [
               {...}, 
               {...}
            ],
            "type": "personalization:decisions",
            "eventIndex": 0
         }
         ]
      }
   }
   ).then(applyPersonalization("sample-json-offer"));
```

基于表单 [!DNL JSON] 选件通过以下方式手动应用 `applyPersonalization` 方法，更新 [!DNL DOM] 基于个性化选件。 对于基于表单的活动，必须手动发送显示事件，以指示何时显示选件。 这可以通过以下方式实现 `sendEvent` 命令。

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        xdm: {
            eventType: "decisioning.propositionDisplay",
            _experience: {
                decisioning: {
                    propositions: [
                        {
                            id: id,
                            scope: scope,
                            scopeDetails: scopeDetails,
                        },
                    ],
                },
            },
        },
    });
}
```

## 示例应用程序 {#sample-app}

为了帮助您试验这种类型的个性化并了解关于它的更多信息，我们提供了一个示例应用程序，您可以下载它并用于测试。 您可以从以下网站下载应用程序，以及有关如何使用该应用程序的详细说明 [GitHub存储库](https://github.com/adobe/alloy-samples).

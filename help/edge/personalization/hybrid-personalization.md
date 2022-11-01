---
title: 使用Web SDK和边缘网络服务器API进行混合个性化
description: 本文演示了如何将Web SDK与服务器API结合使用来在Web属性上部署混合个性化。
keywords: 个性化；混合；服务器api;服务器端；混合实施；
source-git-commit: f280d4cbcde434ccf36df37e95f1902cfd02c96c
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 3%

---


# 使用Web SDK和边缘网络服务器API进行混合个性化

## 概述 {#overview}

Hybdrid个性化介绍了在服务器端使用 [边缘网络服务器API](../..//server-api/overview.md)，并使用 [Web SDK](../home.md).

您可以将混合个性化与个性化解决方案(如Adobe Target或Offer Decisioning)结合使用，其中的内容是 [!UICONTROL 服务器API] 负载。

## 先决条件 {#prerequisites}

在Web资产上实施混合个性化之前，请确保满足以下条件：

* 您已决定要使用哪种个性化解决方案。 这会对 [!UICONTROL 服务器API] 负载。
* 您有权访问应用程序服务器，您可以使用该服务器将 [!UICONTROL 服务器API] 调用。
* 您有权访问 [边缘网络服务器API](../../server-api/authentication.md).
* 您已正确 [已配置和部署](../fundamentals/configuring-the-sdk.md) 要个性化的页面上的Web SDK。

## 流程图 {#flow-diagram}

以下流程图描述了为提供混合个性化而采取的步骤的顺序。

![可视化流程图显示了为提供混合个性化而采取的步骤的顺序。](assets/hybrid-personalization-diagram.png)

1. 之前由浏览器存储的任何现有Cookie，其前缀为 `kndctr_`，包含在浏览器请求中。
1. 客户端Web浏览器从您的应用程序服务器请求网页。
1. 当应用程序服务器收到页面请求时，会发出 `POST` 请求 [服务器API交互式数据收集端点](../../server-api/interactive-data-collection.md) 以获取个性化内容。 的 `POST` 请求包含 `event` 和 `query`. 上一步中的Cookie（如果可用）包含在 `meta>state>entries` 数组。
1. 服务器API会将个性化内容返回到应用程序服务器。
1. 应用程序服务器会向客户端浏览器返回HTML响应，其中包含 [标识和群集cookie](#cookies).
1. 在客户端页面上， [!DNL Web SDK] `applyResponse` 命令，传入的标头和正文 [!UICONTROL 服务器API] 上一步的响应。
1. 的 [!DNL Web SDK] 渲染页面加载 [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) 自动选件，因为 `renderDecisions` 标志设置为 `true`.
1. 基于表单 [!DNL JSON] 选件通过手动应用 `applyPersonalization` 方法，更新 [!DNL DOM] 基于个性化选件。
1. 对于基于表单的活动，必须手动发送显示事件，以指示选件何时显示。 这是通过 `sendEvent` 命令。

## Cookie {#cookies}

Cookie用于保留用户标识和群集信息。  使用混合实施时，Web应用程序服务器会在请求生命周期中处理这些Cookie的存储和发送。

| Cookie | 用途 | 存储者 | 发送者 |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | 包含用户身份详细信息。 | 应用程序服务器 | 应用程序服务器 |
| `kndctr_AdobeOrg_cluster` | 指示应使用哪个边缘网络群集来执行请求。 | 应用程序服务器 | 应用程序服务器 |

## 请求投放 {#request-placement}

需要服务器API请求才能获取建议并发送显示通知。 使用混合实施时，应用程序服务器会向服务器API发出这些请求。

| 请求 | 制作者 |
|---|---|
| 交互请求以检索主张 | 应用程序服务器 |
| 用于发送显示通知的交互请求 | 应用程序服务器 |

## Analytics的影响 {#analytics}

在实施混合个性化时，您必须特别注意，以便在Analytics中不会多次计算页面点击量。

当您 [配置数据流](../datastreams/overview.md) 对于Analytics，会自动转发事件，以便捕获页面点击量。

此实现中的示例使用两个不同的数据流：

* 为Analytics配置的数据流。 此数据流用于Web SDK交互。
* 没有Analytics配置的第二个数据流。 此数据流用于服务器API请求。

这样，服务器端请求便不会注册任何Analytics事件，但客户端请求会注册。 这会导致Analytics请求被准确计数。


## 服务器端请求 {#server-side-request}

以下示例请求说明了应用程序服务器可用于检索个性化内容的服务器API请求。

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
| `dataStreamId` | `String` | 可以。 | 用于将交互传递到边缘网络的数据流的ID。 请参阅 [数据流概述](../datastreams/overview.md) 了解如何配置数据流。 |
| `requestId` | `String` | 否 | 用于关联内部服务器请求的随机ID。 如果未提供任何内容，边缘网络将生成一个，并在响应中返回。 |

### 服务器端响应 {#server-response}

以下示例响应显示了服务器API响应的样式。


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

基于表单 [!DNL JSON] 选件通过手动应用 `applyPersonalization` 方法，更新 [!DNL DOM] 基于个性化选件。 对于基于表单的活动，必须手动发送显示事件，以指示选件何时显示。 这是通过 `sendEvent` 命令。

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

为了帮助您试验和进一步了解此类个性化，我们提供了一个示例应用程序，您可以下载并使用它进行测试。 您可以从以下页面下载应用程序以及有关如何使用该应用程序的详细说明 [GitHub存储库](https://github.com/adobe/alloy-samples).







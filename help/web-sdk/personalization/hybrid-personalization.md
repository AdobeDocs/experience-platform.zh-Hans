---
title: 使用Web SDK和Edge Network API的混合个性化
description: 本文演示了如何将Web SDK与Edge Network API结合使用来在Web资产上部署混合个性化。
keywords: 个性化；混合；服务器API；服务器端；混合实现；
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: 7b91f4f486db67d4673877477a6be8287693533a
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 2%

---

# 使用Web SDK和Edge Network API的混合个性化

## 概述 {#overview}

Hybdrid个性化描述使用[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/)在服务器端检索个性化内容，并使用[Web SDK](../home.md)在客户端呈现该内容的过程。

您可以将混合个性化与Adobe Target、Adobe Journey Optimizer或Offer Decisioning等个性化解决方案一起使用，不同之处在于[!UICONTROL Edge Network API]有效负载的内容。

## 先决条件 {#prerequisites}

在Web资产上实施混合个性化之前，请确保满足以下条件：

* 您已决定要使用的个性化解决方案。 这将影响[!UICONTROL Edge Network API]有效负载的内容。
* 您有权访问可用于进行[!UICONTROL Edge Network API]调用的应用程序服务器。
* 您有权访问[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/)。
* 您已正确[配置](/help/web-sdk/commands/configure/overview.md)并在要个性化的页面上部署了Web SDK。

## 流程图 {#flow-diagram}

以下流程图描述了实现混合个性化的步骤顺序。

![显示混合个性化步骤顺序的可视化流程图。](assets/hybrid-personalization-diagram.png)

1. 浏览器先前存储的任何带有`kndctr_`前缀的现有Cookie都将包含在浏览器请求中。
1. 客户端Web浏览器向应用程序服务器请求网页。
1. 应用程序服务器在收到页面请求时，会向[Edge Network API交互式数据收集终结点](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)发出`POST`请求以获取个性化内容。 `POST`请求包含`event`和`query`。 上一步的Cookie（如果可用）包含在`meta>state>entries`数组中。
1. Edge Network API会将个性化内容返回到应用程序服务器。
1. 应用程序服务器向客户端浏览器返回一个HTML响应，其中包含[标识和群集Cookie](#cookies)。
1. 在客户端页面上，调用[!DNL Web SDK] `applyResponse`命令，传入上一步的[!UICONTROL Edge Network API]响应的标头和正文。
1. [!DNL Web SDK]自动呈现Target [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=zh-Hans)选件和Journey Optimizer Web渠道项，因为`renderDecisions`标志设置为`true`。
1. 通过`applyProposition`方法手动应用基于Target表单的[!DNL HTML]/[!DNL JSON]选件和基于代码的Journey Optimizer体验，以根据建议中的个性化内容更新[!DNL DOM]。
1. 对于基于Target表单的[!DNL HTML]/[!DNL JSON]选件和基于代码的Journey Optimizer体验，必须手动发送显示事件，以指示何时显示返回的内容。 这是通过`sendEvent`命令完成的。

## Cookie {#cookies}

Cookie用于保留用户标识和群集信息。  使用混合实施时，Web应用程序服务器会在请求生命周期中处理这些Cookie的存储和发送。

| Cookie | 目的 | 存储者 | 发送者 |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | 包含用户身份详细信息。 | 应用程序服务器 | 应用程序服务器 |
| `kndctr_AdobeOrg_cluster` | 指示应使用哪个Edge Network群集来完成请求。 | 应用程序服务器 | 应用程序服务器 |

## 请求投放 {#request-placement}

需要Edge Network API请求才能获取建议并发送显示通知。 使用混合实施时，应用程序服务器会向Edge Network API发出这些请求。

| 请求 | 创建者 |
|---|---|
| 用于检索建议的Interact请求 | 应用程序服务器 |
| Interact请求发送显示通知 | 应用程序服务器 |


## 建立Edge Network区域主机 {#regional-host}

要建立Edge Network区域主机，请首先从`kndctr_<orgId>_AdobeOrg_cluster` Cookie中读取位置提示，它可具有以下值：

* `va6`
* `or2`
* `irl1`
* `ind1`
* `sgp3`
* `jpn3`
* `aus3`

示例：`kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_cluster: va6`

Edge Network区域主机使用以下格式： `<location_hint>.server.adobedc.net`，可以具有以下值：

* `va6.server.adobedc.net`
* `or2.server.adobedc.net`
* `irl1.server.adobedc.net`
* `ind1.server.adobedc.net`
* `sgp3.server.adobedc.net`
* `jpn3.server.adobedc.net`
* `aus3.server.adobedc.net`

通过使用这些特定主机，请求将被定向到用户之前访问过的相同Edge Network位置，并且由于存在用户数据，因此系统将能够提供最佳体验。

如果没有位置提示（即没有Cookie），请使用默认主机： `server.adobedc.net`。

>[!TIP]
>
>作为最佳实践，您应使用允许位置的列表。 这样可防止缓减位置提示，因为它是通过客户端Cookie提供的。

## Analytics含义 {#analytics}

实施混合个性化时，必须特别注意，以便Analytics中的页面点击不会被计数多次。

当您[为Analytics配置数据流](../../datastreams/overview.md)时，会自动转发事件以便捕获页面点击。

此实施中的示例使用两个不同的数据流：

* 为Analytics配置的数据流。 此数据流用于Web SDK交互。
* 第二个不具有Analytics配置的数据流。 此数据流用于Edge Network API请求。 您必须使用与Analytics配置的数据流相同的目标配置来配置此数据流。

这样一来，服务器端请求就不会注册任何Analytics事件，而客户端请求会注册。 这将导致Analytics请求被准确计数。

## 构建服务器端请求 {#server-side-request}

以下示例请求说明了您的应用程序服务器可用于检索个性化内容的Edge Network API请求。

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
         "entries": [{
           "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
           "value":"CiY0NzE0NzkwMTUyMzYzMzI4NDAxMjc3NDcwNzA2NTcxMjI3OTI1NVIRCJ_S-uCRMRABGAEqBElSTDHwAZ_S-uCRMQ=="
         }, {
           "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
           "value": "general=in"
         }, {
            "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_cluster",
            "value": "va6"
         }]
      }
   }
}'
```

| 参数 | 类型 | 必需 | 描述 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 可以。 | 用于将交互传递到Edge Network的数据流的ID。 请参阅[数据流概述](../../datastreams/overview.md)，了解如何配置数据流。 |
| `requestId` | `String` | 否 | 用于关联内部服务器请求的随机ID。 如果未提供，Edge Network将生成一个，并在响应中返回它。 |

### 代理标头 {#proxy-headers}

要正确处理请求，需要以下标头。

* `Referer`
* `X-Forwarded-For`
* `X-Forwarded-Proto`
* `X-Forwarded-Host`

请确保正确设置这些参数以指向实际的客户端信息。 例如，`X-Forwarded-For`标头应包含客户端IP，以便进行正确的地理定位。

### User-Agent标头 {#user-agent-headers}

使用以下用户代理标头可正确处理请求。

**默认值**

* `User-Agent`

**低熵（必需）：**

* `Sec-CH-UA`
* `Sec-CH-UA-Mobile`
* `Sec-CH-UA-Platform`

**高熵（可选）：**

* `Sec-CH-UA-Platform-Version`
* `Sec-CH-UA-Arch`
* `Sec-CH-UA-Model`
* `Sec-CH-UA-Bitness`
* `Sec-CH-UA-WoW64`

必须按照[Edge Network API规范](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)中的说明发送请求。 如果您的用例需要，请参阅[个性化文档](https://developer.adobe.com/data-collection-apis/docs/getting-started/personalization/)。

### 服务器端响应 {#server-response}

Edge Network响应将包含`state:store`条指令，这些指令应转换为`Set-Cookie`标头。 它们将被保存在浏览器中，Web SDK实施可以使用它们。

这些Cookie应设置在顶级域上，以便它们会与请求一起发送到服务器实施和客户端实施。 （或至少是两个实施使用的公共子域）

示例：

* 服务器端调用使用`api.example.com`
* 客户端调用使用`adobe.example.com`

应在`.example.com`上设置Cookie，以便在两种情况下共享。

服务器端响应按名为`Handles`的片段进行组织，这些片段根据数据流配置生成。 例如，实时个性化引擎返回`personalization:decisions`句柄，而实时激活引擎生成`activation:pull`句柄。

下面的示例响应显示了Edge Network API响应可能具有的外观。

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

在客户端页面上，调用[!DNL Web SDK] `applyResponse`命令，传入服务器端响应的标头和正文。

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

通过`applyPersonalization`方法手动应用基于表单的[!DNL JSON]选件，以根据个性化选件更新[!DNL DOM]。 对于基于表单的活动，必须手动发送显示事件，以指示何时显示选件。 这是通过`sendEvent`命令完成的。

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        "xdm": {
            "eventType": "decisioning.propositionDisplay",
            "_experience": {
                "decisioning": {
                    "propositions": [{
                        "id": id,
                        "scope": scope,
                        "scopeDetails": scopeDetails
                    }],
                    "propositionEventType": {
                        "display": 1
                    }
                }
            }
        }
    });
}
```

## 示例应用程序 {#sample-app}

为了帮助您试验这种类型的个性化并了解关于它的更多信息，我们提供了一个示例应用程序，您可以下载它并用于测试。 您可以从此[GitHub存储库](https://github.com/adobe/alloy-samples)下载应用程序，以及有关如何使用该应用程序的详细说明。

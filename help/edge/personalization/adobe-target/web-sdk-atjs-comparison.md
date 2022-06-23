---
title: 比较at.js与Experience PlatformWeb SDK
description: 了解at.js功能与Experience PlatformWeb SDK的异同
keywords: Target;Adobe Target;activity.id;experience.id;renderDecisions;decisionScopes；预隐藏代码片段；VEC；基于表单的体验编辑器；XDM；受众；决策；范围；架构；系统图；图
exl-id: b63fe47d-856a-4cae-9057-51917b3e58dd
source-git-commit: 7bdf4c01ad3b361b3bc53574d4da1096757c815c
workflow-type: tm+mt
source-wordcount: '2286'
ht-degree: 6%

---

# 将at.js库与Web SDK进行比较

## 概述

本文概述了 `at.js` 库和Experience Platform Web SDK。

## 安装库

### 安装at.js

我们允许客户直接从“实施”选项卡的Adobe Experience Cloud下载库。 at.js库是使用客户的如下设置自定义的：clientCode、imsOrgId等

### 安装Web SDK

预建版本可在CDN上使用。 您可以直接在页面上引用CDN上的库，或在自己的基础架构下载并托管该库。 它以缩小和未缩小的格式提供。 未缩小版本有助于进行调试。

URL结构：https://cdn1.adoberesources.net/alloy/[版本]/alloy.min.js或alloy.js（用于非缩小版本）。

例如：

* 缩小： [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js)
* 未缩小： [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js)

[了解更多](../../fundamentals/installing-the-sdk.md)

## 配置库

### 配置at.js

在每个at.js文件的末尾，您将找到一个部分，我们在其中实例化并传递设置对象。 它可自定义，下载时，我们会使用当前客户设置填充该部分。

```javascript
window.adobe.target.init(window, document, {
  "clientCode": "demo",
  "imsOrgId": "",
  "serverDomain": "localhost:5000",
  "timeout": 2000,
  "globalMboxName": "target-global-mbox",
  "version": "2.0.0",
  "defaultContentHiddenStyle": "visibility: hidden;",
  "defaultContentVisibleStyle": "visibility: visible;",
  "bodyHiddenStyle": "body {opacity: 0 !important}",
  "bodyHidingEnabled": true,
  "deviceIdLifetime": 63244800000,
  "sessionIdLifetime": 1860000,
  "selectorsPollingTimeout": 5000,
  "visitorApiTimeout": 2000,
  "overrideMboxEdgeServer": false,
  "overrideMboxEdgeServerTimeout": 1860000,
  "optoutEnabled": false,
  "optinEnabled": false,
  "secureOnly": false,
  "supplementalDataIdParamTimeout": 30,
  "authoringScriptUrl": "//cdn.tt.omtrdc.net/cdn/target-vec.js",
  "urlSizeLimit": 2048,
  "endpoint": "/rest/v1/delivery",
  "pageLoadEnabled": true,
  "viewsEnabled": true,
  "analyticsLogging": "server_side",
  "serverState": {},
  "decisioningMethod": "server-side",
  "legacyBrowserSupport":  false
});
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en)


### 配置Web SDK

SDK的配置已通过 `configure` 命令。

>[!IMPORTANT]
>
>`configure` is *always* 第一个命令名为。

示例：

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

在配置过程中可以设置许多选项。 所有选项都可在下面找到，并按类别分组。

[了解更多](../../fundamentals/configuring-the-sdk.md)


## 如何请求和自动渲染页面加载Target选件

### 使用at.js

使用at.js 2.x(如果启用了 `pageLoadEnabled`，则库将触发对Target Edge的调用 `execute -> pageLoad`. 如果所有设置都设置为默认值，则无需进行自定义编码。将at.js添加到页面并由浏览器加载后，将执行Target边缘调用。

### 使用Web SDK

在Adobe Target中创建的内容 [可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) 可由SDK自动检索和渲染。

要请求并自动渲染Target选件，请使用 `sendEvent` 命令并设置 `renderDecisions` 选项 `true`. 这样做会强制SDK自动渲染任何符合自动渲染条件的个性化内容。

示例：

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Experience PlatformWeb SDK会自动发送包含WEB SDK执行的选件的通知，以下是通知请求有效负载的外观示例：

```json
{
  "events": [{
      "xdm": {
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                "scope": "cart",
                "scopeDetails": {
                  "decisionProvider": "TGT",
                  "activity": {
                    "id": "127019"
                  },
                  "experience": {
                    "id": "0"
                  },
                  "strategies": [
                    {
                      "step": "entry",
                      "algorithmID": "0",
                      "trafficType": "0"
                    },
                    {
                      "step": "display",
                      "algorithmID": "0",
                      "trafficType": "0"
                    }
                  ],
                  "characteristics": {
                    "eventToken": "bKMxJ8dCR1XlPfDCx+2vSGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                  }
                }
              }
            ]
          }
        },
        "eventType": "display",
        "web": {
          "webPageDetails": {
            "viewName": "cart",
            "URL": "https://alloyio.com/personalizationSpa/cart"
          },
          "webReferrer": {
            "URL": ""
          }
        },
        "device": {
          "screenHeight": 800,
          "screenWidth": 1280,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1280,
            "viewportHeight": 284
          }
        },
        "placeContext": {
          "localTime": "2021-12-10T15:50:34.467+02:00",
          "localTimezoneOffset": -120
        },
        "timestamp": "2021-12-10T13:50:34.467Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy",
          "version": "2.6.2",
          "environment": "browser"
        }
      }
    }
  ]
}
```

[了解更多](../rendering-personalization-content.md)

## 如何请求和不自动渲染页面加载Target选件

### 使用at.js

有两种方法可以触发对Target Edge的调用，以获取用于页面加载的选件。

示例 1:

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox", 
   success: console.log,
   error: console.error
});
```

示例 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=en)

### 使用Web SDK

执行 `sendEvent` 具有特殊范围的命令 `decisionScopes`: `__view__`. 我们使用此范围作为信号，从Target获取所有页面加载活动并预取所有视图。 Web SDK还将尝试评估所有基于VEC视图的活动。 Web SDK当前不支持禁用视图预取。

要访问任何个性化内容，您可以提供一个回调函数，该函数将在SDK收到来自服务器的成功响应后调用。 您的回调将提供一个结果对象，该对象可能包含包含任何返回的个性化内容的命题属性。

示例：

```javascript
alloy("sendEvent", {
    xdm: {...},
    decisionScopes: ["__view__"]
  }).then(function(result) {
    if (result.propositions) {
      result.propositions.forEach(proposition => {
        proposition.items.forEach(item => {
          if (item.schema === HTML_SCHEMA) {
            // manually apply offer
            document.getElementById("form-based-offer-container").innerHTML =
              item.data.content;
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
          // manually send the display notification event, so that Target/Analytics impressions aare increased
            alloy("sendEvent",{
              "xdm": {
                "eventType": "decisioning.propositionDisplay",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          }
        });
      });
    }
  });
```

[了解更多](../rendering-personalization-content.md#manually-rendering-content)


## 如何请求特定的基于表单的Target mbox


### 使用at.js

您可以使用 `getOffer` 函数：

示例 1:

```javascript
adobe.target.getOffer({
   mbox: "hero-banner", 
   success: console.log,
   error: console.error
});
```

示例 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        mboxes: [
        {
          index: 0,
          name: "hero-banner"
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=en)


### 使用Web SDK

您可以使用 `sendEvent` 命令并在 `decisionScopes` 选项。 的 `sendEvent` 命令将返回一个通过包含所请求活动/命题的对象进行解析的promise:这就是 `propositions` 数组如下所示：

```javascript
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg=="
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

示例：

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];
        if (item.schema === HTML_SCHEMA) {
          // apply offer
          document.getElementById("form-based-offer-container").innerHTML =
            item.data.content;
          const executedPropositions = [
            {
              id: proposition.id,
              scope: proposition.scope,
              scopeDetails: proposition.scopeDetails
            }
          ];

          alloy("sendEvent", {
            "xdm": {
              "eventType": "decisioning.propositionDisplay",
              "_experience": {
                "decisioning": {
                  "propositions": executedPropositions
                }
              }
            }
          });
        }
      }
    }
  }
});
```

[了解更多](../rendering-personalization-content.md#manually-rendering-content)

## 如何应用Target活动

### 使用at.js

您可以使用 `applyOffers` 函数： `adobe.target.applyOffer(options)`

示例：

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

进一步了解 `applyOffers` 命令 [专用文档](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2.html?lang=en).


### 使用Web SDK

您可以使用 `applyPropositions` 命令。

示例：

```javascript
alloy("applyPropositions", {
    propositions: [...]
});
```

进一步了解 `applyPropositions` 命令 [专用文档](../../personalization/rendering-personalization-content.md#applypropositions).

## 如何跟踪事件

### 使用at.js

您可以使用 `trackEvent` 函数或使用 `sendNotifications`.

此函数会触发报告用户操作（如点击次数和转化）的请求。 它不会在响应中交付活动。


**示例 1**

```javascript
adobe.target.trackEvent({ 
    "type": "click",
    "mbox": "some-mbox"
});
```

**示例 2**

```javascript
adobe.target.sendNotifications({ 
    request: {
       notifications: [{
          ...,
          mbox: {
            name: "some-mbox"
          },
          type: "click",
          ...
       }]
    }
});
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html?lang=en)

### 使用Web SDK

您可以通过调用 `sendEvent` 命令，填充 `_experience.decisioning.propositions` XDM字段组，并设置 `eventType` 值2之一：

* `decisioning.propositionDisplay`:表示Target活动的呈现。
* `decisioning.propositionInteract`:表示用户与活动的交互，如鼠标单击。

的 `_experience.decisioning.propositions` XDM字段组是一个对象数组。 每个对象的属性均从 `result.propositions` 在 `sendEvent` 命令： `{ id, scope, scopeDetails }`

**示例1 — 跟踪 `decisioning.propositionDisplay` 事件**

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        var discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
      // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered.
    alloy("sendEvent", {
      xdm: {
        eventType: "decisioning.propositionDisplay",
        _experience: {
          decisioning: {
            propositions: [
              {
                id: discountProposition.id,
                scope: discountProposition.scope,
                scopeDetails: discountProposition.scopeDetails
              }
            ]
          }
        }
      }
    });
  }
});
```

**示例2 — 跟踪 `decisioning.propositionInteract` 点击量度后的事件**

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

[了解更多](../rendering-personalization-content.md#manually-rendering-content)

## 如何在单页应用程序中触发视图更改

### 使用at.js

使用 `adobe.target.triggerView` 函数。 每当加载新页面或重新渲染页面上的组件时，都可以调用此函数。应该为单页应用程序(SPA)实施adobe.target.triggerView()，以便使用可视化体验编辑器(VEC)创建A/B测试和体验定位(XT)活动。 如果未在网站上实施adobe.target.triggerView()，则无法将VEC用于SPA。

**示例**

```javascript
adobe.target.triggerView("homeView")
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-triggerview-atjs-2.html?lang=en)


### 使用Web SDK

要触发或指示单页应用程序查看更改，请设置 `web.webPageDetails.viewName` 属性 `xdm` 的 `sendEvent` 命令。 如果存在 `viewName` 指定 `sendEvent` 它将执行这些事件并发送显示通知事件。

**示例**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  xdm:{
    web:{
      webPageDetails:{
        viewName: "homeView"
      }
    }
  }
});
```

[了解更多](./spa-implementation.md#implementing-xdm-views)

## 如何利用响应令牌

从Adobe Target返回的个性化内容包括 [响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)，其中提供了有关活动、选件、体验、用户配置文件、地理信息等的详细信息。 这些详细信息可以与第三方工具共享或用于调试。 可以在Adobe Target用户界面中配置响应令牌。

### 使用at.js

使用at.js自定义事件来监听Target响应并读取响应令牌。

**示例**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)


### 使用Web SDK

>[!IMPORTANT]
>
>确保您使用的是Platform Web SDK版本2.6.0或更高版本。

响应令牌将作为 `propositions` 在 `sendEvent` 命令。 每个命题都包含一个 `items`，并且每个项目都 `meta` 对象中填充了响应令牌（如果在Target管理员UI中启用）。 [了解详情](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)

**示例**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Format of result.propositions:
      /*
        [
            {
                "id": "",
                "scope": "",
                "items": [
                    {
                        "id": "",
                        "schema": "",
                        "data": {},
                        "meta": { // RESPONSE TOKENS
                            "activity.name": ...,
                            "offer.id": ...,
                            "profile.activeActivities": ...
                        }
                    }
                ],
                "scopeDetails": {}
                "renderAttempted": false
            }
        ]
      */
    }
  });
```

[了解更多](./accessing-response-tokens.md)

## 如何管理闪烁

### 使用at.js

使用at.js，您可以通过设置 `bodyHidingEnabled: true` 以便at.js在获取并应用DOM更改之前会处理预隐藏的个性化容器。
通过覆盖at.js，可以预先隐藏包含个性化内容的页面部分 `bodyHiddenStyle`.
默认情况下 `bodyHiddenStyle` 隐藏了整个HTML `body`.
这两个设置都可以使用 `window.targetGlobalSettings`. `window.targetGlobalSettings` 应先放置，然后再加载at.js。

### 使用Web SDK

使用Web SDK，客户可以在configure命令中设置其预隐藏样式，如以下示例中所示：

```javascript
alloy("configure", {
  edgeConfigId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

异步加载Web SDK时，我们建议先在页面中插入以下代码片段，然后再插入Web SDK:

```html
<script>
  !function(e,a,n,t){
  if (a) return;
  var i=e.head;if(i){
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
  setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

## 如何处理A4T

### 使用at.js

使用at.js支持以下两种类型的A4T日志记录：

* Analytics客户端日志记录
* Analytics服务器端日志记录

#### Analytics客户端日志记录

**示例1:使用Target全局设置**

可以通过设置 `analyticsLogging: client_side` 或通过覆盖 `window.targetglobalSettings` 对象。
设置此选项时，返回的有效负载格式如下所示：

```json
{
  "analytics": {
    "payload": {
      "pe": "tnt",
      "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
    }
  }
}
```

然后，可以通过数据插入API将有效负载转发到Analytics。

示例2:在 `getOffers` 函数：

```javascript
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

响应有效负载如下所示：

```json
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

Analytics有效负载(`tnta` 令牌)应包含在使用的Analytics点击中 [数据插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

#### Analytics服务器端日志记录

可以通过设置 `analyticsLogging: server_side` 或通过覆盖 `window.targetglobalSettings` 对象。
然后，数据会按如下方式流动：

![](assets/a4t-server-side-atjs.png)

[了解详情](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html?lang=en)

### 使用Web SDK

Web SDK还支持：

* Analytics客户端日志记录
* Analytics服务器端日志记录

#### Analytics客户端日志记录

对于该DataStream配置，如果禁用了Adobe Analytics，则会启用Analytics客户端日志记录。

![](assets/analytics-disabled-datastream-config.png)

客户有权访问Analytics令牌(`tnta`) [数据插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)
通过链接 `sendEvent` 命令并迭代生成的命题数组。

**示例**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  for (var i = 0; i < results.propositions.length; i++) {
    var proposition = results.propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getAnalyticsPayload(proposition);
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // send the page view Analytics hit with collected Analytics payload using Data Insertion API
});
```

下图显示了启用Analytics客户端时数据如何流动：

![](assets/analytics-client-side-logging.png)

#### Analytics服务器端日志记录

为该数据流配置启用Analytics时，将启用Analytics服务器端日志记录。

![](assets/analytics-enabled-datastream-config.png)

启用“服务器端分析日志记录”后，将需要与Analytics共享A4T有效负载，以便Analytics报表显示正确的展示次数和转化次数在体验边缘级别进行共享，以便客户无需执行任何其他处理。

以下是启用服务器端分析日志记录后数据如何流入我们的系统：

![](assets/analytics-server-side-logging.png)

## 如何设置Target全局设置

### 使用at.js

您可以使用 `window.targetGlobalSettings` 覆盖 at.js 库中的设置，而不是在 Target Standard/Premium UI 中或通过使用 REST API 来配置设置。

应在加载at.js之前或在管理>实施>编辑at.js设置>代码设置>库标题中定义覆盖。

示例：

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en)

### 使用Web SDK

Web SDK不支持此功能。

## 如何更新Target配置文件属性

### 使用at.js

**示例 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "profile.name": "test",
     "profile.gender": "female"
   },
   success: console.log,
   error: console.error
});
```

**示例 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          profileParameters: {
            name: "test",
            gender: "female"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

### 使用Web SDK

要更新Target配置文件，请使用 `sendEvent` 命令并设置 `data.__adobe.target` 属性，使用 `profile`.

**示例**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## 如何使用Target Recommendations

### 使用at.js

**示例 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "entity.productName": "T-shirt",
     "entity.productId": "1234"
   },
   success: console.log,
   error: console.error
});
```

**示例 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          parameters: {
            "entity.productName": "T-shirt",
            "entity.productId": "1234"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html?lang=en)


### 使用Web SDK

要发送推荐数据，请使用 `sendEvent` 命令并设置 `data.__adobe.target` 属性，使用 `entity`.

**示例**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.productName": "T-shirt",
        "entity.productId": "1234"
      }
    }
  }
});
```

## 如何使用第三方ID

### 使用at.js

使用at.js可通过多种方式发送 `mbox3rdPartyId`，使用 `getOffer` 或 `getOffers`:

**示例 1**

```javascript
adobe.target.getOffer({
  mbox:"test",
  params:{
    "mbox3rdPartyId": "1234"
  },
  success: console.log,
  error: console.error
});
```

**示例 2**

```javascript
adobe.target.getOffers({
    request: {
      id:{
        thirdPartyId: "1234"
      },
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

或者有办法设置 `mbox3rdPartyId` 在 `targetPageParams` 或 `targetPageParamsAll`.
在 `targetPageParams`，则会在 `target-global-mbox` 也称为 `pag-lLoad`.
建议将使用 `targetPageParamsAll` ，因为它将在每个target请求中发送。
使用的优势 `targetPageParamsAll` 就是你可以定义 `mbox3rdPartyId` ，这将确保所有目标请求都具有 `mbox3rdPartyId`.

```javascript
window.targetPageParamsAll = function() {
      return {
        "mbox3rdPartyId": "1234"
      };
    };
```

```javascript
window.targetPageParams = function() {
  return {
    "mbox3rdPartyId": "1234"
  };
};
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html?lang=en)

### 使用Web SDK

Web SDK支持Target第三方ID。 但是，还需要执行一些步骤。 在开始研究解决方案之前，我们应该谈谈 `identityMap`.
身份映射允许客户发送多个身份。 所有身份都是同名的。 每个命名空间可以具有一个或多个标识。 特定身份可标记为主标识。
牢记这些知识后，我们可以了解设置Web sdk以使用Target第三方ID的必要步骤。

1. 在“数据流配置”视图中设置将包含Target第三方ID的命名空间：

![](assets/mbox-3-party-id-setup.png)

1. 在每个sendEvent命令中发送该身份命名空间，如下所示：

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "identityMap": {
      "TGT3PID": [
        {
          "id": "1234",
          "primary": true
        }
      ]
    }
  }
});
```

## 如何设置属性令牌

### 使用at.js

使用at.js时，可通过两种方式来设置资产令牌，即使用 `targetPageParams` 或 `targetPageParamsAll`. 使用 `targetPageParams` 将资产令牌添加到 `target-global-mbox` 调用，但使用 `targetPageParamsAll` 将令牌添加到所有target调用：

**示例 1**

```javascript
   window.targetPageParamsAll = function() {
      return {
        "at_property": "1234"
      };
    };
```

**示例 2**

```javascript
window.targetPageParams = function() {
      return {
        "at_property": "1234"
      };
    };
```

### 使用Web SDK

使用Web SDK，客户在Adobe Target命名空间下设置数据流配置时，能够在更高级别设置属性：
![](assets/at-property-setup.png)
这意味着该特定数据流配置的每个Target调用都将包含该资产令牌。

## 如何预取mbox

### 使用at.js

此功能仅在at.js 2.x中可用。at.js 2.x具有一个名为 `getOffers`. `getOffers` 允许客户预取一个或多个mbox的内容。 示例如下：

```javascript
adobe.target.getOffers({
    request: {
      prefetch: {
        mboxes: [{
          index: 0,
          name: "test-mbox",
          parameters: {
            ...
          },
          profileParameters: {
            ...
          }
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

注意：强烈建议确保 `mbox` 在 `mboxes` 数组有其自己的索引。 通常第一个mbox具有 `index=0`，下一个 `index=1`等。

### 使用Web SDK

Web SDK当前不支持此功能。

## 如何调试Target实施

### 使用at.js

At.js会公开以下调试功能：

* Mbox禁用 — 禁用Target的获取和渲染功能，以检查在没有Target交互的情况下页面是否已损坏
* Mbox调试 — at.js记录每个操作
* Target跟踪 — 在Bullseye中生成了mbox跟踪令牌，其中提供了一个跟踪对象，其中包含参与决策过程的详细信息，位于 `window.___target_trace` 对象

注意：所有这些调试功能均在 [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

### 使用Web SDK

使用Web SDK时，您有多种调试功能：

* 使用 [格里丰](https://aep-sdks.gitbook.io/docs/beta/project-griffon)
* [已启用Web SDK调试](../../../edge/fundamentals/debugging.md)
* 使用 [Web SDK监控挂接](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* 使用 [Adobe Experience Platform Debugger](../../../debugger/home.md)
* 目标跟踪

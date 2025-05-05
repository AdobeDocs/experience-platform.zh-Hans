---
title: 将at.js与Experience Platform Web SDK进行比较
description: 了解at.js功能与Experience Platform Web SDK的比较
keywords: target；adobe target；activity.id；experience.id；renderDecisions；decisionScopes；预隐藏代码片段；vec；基于表单的体验编辑器；xdm；受众；决策；范围；架构；系统图；图
exl-id: b63fe47d-856a-4cae-9057-51917b3e58dd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 2%

---

# 将at.js库与Web SDK进行比较

## 概述

本文概述了`at.js`库与Experience Platform Web SDK之间的差异。

## 安装库

### 安装at.js

我们允许我们的客户直接从Adobe Experience Cloud的“实现”选项卡下载库。 使用客户拥有的如下设置自定义at.js库： clientCode、imsOrgId等

### 安装Web SDK

预建版本在CDN上可用。 您可以在页面上直接在CDN上引用库，也可以将其下载并托管在您自己的基础架构上。 它以缩小和未缩小的格式提供。 未缩小的版本有助于进行调试。

有关详细信息，请参阅[使用JavaScript库安装Web SDK](/help/web-sdk/install/library.md)。

## 配置库

### 配置at.js

在每个at.js文件的末尾，您会找到我们实例化并传递设置对象的部分。 它可自定义，在下载时，我们使用当前客户设置填充该部分。

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

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=zh-Hans)


### 配置Web SDK

使用[`configure`](/help/web-sdk/commands/configure/overview.md)命令完成SDK的配置。 `configure`命令是首先调用的&#x200B;*始终*。

## 如何请求和自动渲染页面加载Target选件

### 使用at.js

使用at.js 2.x时，如果启用设置`pageLoadEnabled`，则库将触发通过`execute -> pageLoad`对Target Edge的调用。 如果所有设置都设置为默认值，则无需自定义编码。将at.js添加到页面并由浏览器加载后，将执行Target Edge调用。

### 使用Web SDK

SDK可以自动检索和渲染在Adobe Target的[可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=zh-Hans)中创建的内容。

要请求并自动呈现Target选件，请使用`sendEvent`命令并将`renderDecisions`选项设置为`true`。 这样做会强制SDK自动呈现任何符合自动呈现条件的个性化内容。

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

Experience Platform Web SDK会自动发送包含WEB SDK执行的选件的通知，例如，通知请求有效负载如下所示：

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

[了解详情](../rendering-personalization-content.md)

## 如何请求且不会自动渲染页面加载Target选件

### 使用at.js

我们可以通过两种方式触发对Target Edge的调用，以便获取页面加载的选件。

示例 1：

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox", 
   success: console.log,
   error: console.error
});
```

示例 2：

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

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=zh-Hans)

### 使用Web SDK

在`decisionScopes`下执行具有特殊作用域的`sendEvent`命令： `__view__`。 我们使用此范围作为信号，从Target中提取所有页面加载活动并预取所有视图。 Web SDK还将尝试评估所有基于VEC视图的活动。 Web SDK当前不支持禁用视图预取。

要访问任何个性化内容，您可以提供回调函数，在SDK收到来自服务器的成功响应后，将调用该函数。 您的回调提供了一个结果对象，该对象可能包含包含包含任何返回的个性化内容的建议属性。

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

[了解详情](../rendering-personalization-content.md#manually-rendering-content)


## 如何请求特定的基于表单的Target mbox


### 使用at.js

您可以使用`getOffer`函数获取基于表单的编辑器活动：

示例 1：

```javascript
adobe.target.getOffer({
   mbox: "hero-banner", 
   success: console.log,
   error: console.error
});
```

示例 2：

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

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=zh-Hans)


### 使用Web SDK

您可以使用`sendEvent`命令并在`decisionScopes`选项下传递mbox名称，以获取基于表单的编辑器的活动。 `sendEvent`命令将返回一个承诺，该承诺会使用包含所请求的活动/建议的对象来解析：
`propositions`数组如下所示：

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

[了解详情](../rendering-personalization-content.md#manually-rendering-content)

## 如何应用Target活动

### 使用at.js

您可以使用`applyOffers`函数应用Target活动： `adobe.target.applyOffer(options)`

示例：

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

从[专用文档](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2.html?lang=zh-Hans)了解有关`applyOffers`命令的更多信息。


### 使用Web SDK

您可以使用`applyPropositions`命令应用Target活动。

示例：

```javascript
alloy("applyPropositions", {
    propositions: [...]
});
```

从[专用文档](../../personalization/rendering-personalization-content.md#applypropositions)了解有关`applyPropositions`命令的更多信息。

## 如何跟踪事件

### 使用at.js

您可以使用`trackEvent`函数或使用`sendNotifications`跟踪事件。

此函数会触发一个请求，以报告用户操作，例如点击次数和转化次数。 它不会在响应中投放活动。


**示例1**

```javascript
adobe.target.trackEvent({ 
    "type": "click",
    "mbox": "some-mbox"
});
```

**示例2**

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

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html?lang=zh-Hans)

### 使用Web SDK

您可以通过调用`sendEvent`命令、填充`_experience.decisioning.propositions` XDM字段组并将`eventType`设置为2个值中的其中一个来跟踪事件和用户操作：

* `decisioning.propositionDisplay`：表示Target活动的渲染。
* `decisioning.propositionInteract`：表示用户与活动的交互，如鼠标单击。

`_experience.decisioning.propositions` XDM字段组是一个对象数组。 每个对象的属性派生自`sendEvent`命令中返回的`result.propositions`： `{ id, scope, scopeDetails }`

**示例1 — 呈现活动后跟踪`decisioning.propositionDisplay`事件**

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
});
```

**示例2 — 发生点击量度后跟踪`decisioning.propositionInteract`事件**

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
      for (var j = 0; j < proposition.items.length; j++) {
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

[了解详情](../rendering-personalization-content.md#manually-rendering-content)

**示例3 — 跟踪执行操作后触发的事件**

此示例跟踪在执行特定操作（如单击按钮）后触发的事件。
您可以通过`__adobe.target`数据对象添加任何其他自定义参数。

您还可以添加`commerce` XDM对象。

```js
alloy("sendEvent", {
    "xdm": {
        "_experience": {
            "decisioning": {
                "propositions": [
                    {
                        "scope": "orderConfirm" //example scope name
                    }
                ],
                "propositionEventType": {
                    "display": 1
                }
            }
        },
        "eventType": "decisioning.propositionDisplay"
    },
    "commerce": {
        "order": {
            "purchaseID": "a8g784hjq1mnp3",
            "purchaseOrderNumber": "VAU3123",
            "currencyCode": "USD",
            "priceTotal": 999.98
        }
    },
    "data": {
        "__adobe": {
            "target": {
                "pageType": "Order Confirmation",
                "user.categoryId": "Insurance"
            }
        }
    }
})
```

## 如何在单页应用程序中触发视图更改

### 使用at.js

使用`adobe.target.triggerView`函数。 每当加载新页面或重新呈现页面上的组件时，都可以调用此函数。 应该为单页应用程序(SPA)实施adobe.target.triggerView()，以便使用可视化体验编辑器(VEC)创建A/B测试和体验定位(XT)活动。 如果未在网站上实施adobe.target.triggerView()，则无法将VEC用于SPA。

**示例**

```javascript
adobe.target.triggerView("homeView")
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-triggerview-atjs-2.html?lang=zh-Hans)


### 使用Web SDK

要触发或发出单页应用程序视图更改信号，请在`sendEvent`命令的`xdm`选项下设置`web.webPageDetails.viewName`属性。 Web SDK将检查视图缓存，如果`sendEvent`中指定的`viewName`有选件，它将执行这些选件并发送显示通知事件。

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

[了解详情](./spa-implementation.md#implementing-xdm-views)

## 如何利用响应令牌

从Adobe Target返回的Personalization内容包括[响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hans)，这些令牌包含有关活动、选件、体验、用户配置文件、地理信息等的详细信息。 这些详细信息可与第三方工具共享或用于调试。 响应令牌可在Adobe Target用户界面中配置。

### 使用at.js

使用at.js自定义事件来监听Target响应并读取响应令牌。

**示例**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hans)


### 使用Web SDK

>[!IMPORTANT]
>
>确保您使用的是Experience Platform Web SDK版本2.6.0或更高版本。

响应令牌作为`propositions`的一部分返回，在`sendEvent`命令的结果中公开。 每个建议都包含一个由`items`组成的数组，并且如果在Target管理UI中启用了响应令牌，则每个项目都将有一个用响应令牌填充的`meta`对象。 [了解详情](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hans)

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

[了解详情](./accessing-response-tokens.md)

## 如何管理闪烁

### 使用at.js

使用at.js，您可以通过设置`bodyHidingEnabled: true`来管理闪烁，以便at.js可以解决此问题
在提取和应用DOM更改之前预隐藏个性化容器。
通过覆盖at.js `bodyHiddenStyle`，可以预先隐藏包含个性化内容的页面部分。
默认情况下，`bodyHiddenStyle`会隐藏整个HTML `body`。
可使用`window.targetGlobalSettings`覆盖这两个设置。 `window.targetGlobalSettings`应在加载at.js之前放置。

### 使用Web SDK

通过使用Web SDK，客户可以在configure命令中设置其预隐藏样式，如以下示例所示：

```javascript
alloy("configure", {
  datastreamId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

异步加载Web SDK时，我们建议在插入Web SDK之前在页面中插入以下代码片段：

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

使用at.js支持以下2种A4T日志记录类型：

* Analytics客户端日志记录
* Analytics服务器端日志记录

#### Analytics客户端日志记录

**示例1：使用Target全局设置**

可以通过在at.js设置中设置`analyticsLogging: client_side`或覆盖`window.targetglobalSettings`对象来启用Analytics客户端日志记录。
设置此选项后，返回的有效负载格式如下所示：

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

示例2：在每个`getOffers`函数中对其进行配置：

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

Analytics有效负载（`tnta`令牌）应包含在使用[数据插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)的Analytics点击中。

#### Analytics服务器端日志记录

可以通过在at.js设置中设置`analyticsLogging: server_side`或覆盖`window.targetglobalSettings`对象来启用Analytics服务器端日志记录。
然后，数据将按如下方式流动：

![显示Analytics服务器端日志记录工作流的图表](assets/a4t-server-side-atjs.png)

[了解详情](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html?lang=zh-Hans)

### 使用Web SDK

Web SDK还支持：

* Analytics客户端日志记录
* Analytics服务器端日志记录

#### Analytics客户端日志记录

如果对该DataStream配置禁用Adobe Analytics，则会启用Analytics客户端日志记录。

![显示Analytics客户端日志记录工作流的图表](assets/analytics-disabled-datastream-config.png)

客户有权访问需要使用[数据插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)与Analytics共享的Analytics令牌(`tnta`)
在中，方法是链接`sendEvent`命令并迭代结果建议数组。

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

下图显示了启用Analytics客户端时的数据流方式：

Analytics客户端日志记录中的![数据流图](assets/analytics-client-side-logging.png)

#### Analytics服务器端日志记录

为该DataStream配置启用Analytics时，将启用Analytics服务器端日志记录。

![显示Analytics设置的数据流UI。](assets/analytics-enabled-datastream-config.png)

启用服务器端Analytics日志记录后，需要与Analytics共享的A4T有效负载将显示Analytics报表
正确的展示和转化在Edge Network级别共享，因此客户不必进行任何额外的处理。

下面是启用服务器端Analytics日志记录时数据如何流入我们的系统：

![显示服务器端Analytics日志记录中数据流的图表](assets/analytics-server-side-logging.png)

## 如何设置Target全局设置

### 使用at.js

您可以使用`window.targetGlobalSettings`覆盖at.js库中的设置，而不是在Target Standard/Premium UI中或通过使用REST API来配置设置。

应在加载at.js之前或在“管理”>“实施”>“编辑at.js设置”>“代码设置”>“库标题”中定义覆盖。

示例：

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=zh-Hans)

### 使用Web SDK

Web SDK不支持此功能。

## 如何更新Target配置文件属性

### 使用at.js

**示例1**

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

**示例2**

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

要更新Target配置文件，请使用`sendEvent`命令并设置`data.__adobe.target`属性，并使用`profile`为键名添加前缀。

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

## 如何使用Target推荐

### 使用at.js

**示例1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "entity.name": "T-shirt",
     "entity.id": "1234"
   },
   success: console.log,
   error: console.error
});
```

**示例2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          parameters: {
            "entity.name": "T-shirt",
            "entity.id": "1234"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html?lang=zh-Hans)


### 使用Web SDK

若要发送推荐数据，请使用`sendEvent`命令并设置`data.__adobe.target`属性，并使用`entity`为键名添加前缀。

**示例**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.name": "T-shirt",
        "entity.id": "1234"
      }
    }
  }
});
```

## 如何使用第三方ID

### 使用at.js

使用at.js可通过多种方式使用`getOffer`或`getOffers`发送`mbox3rdPartyId`：

**示例1**

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

**示例2**

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

或者可以在`targetPageParams`或`targetPageParamsAll`中设置`mbox3rdPartyId`。
在`targetPageParams`中设置它时，它将在`target-global-mbox`（也称为`pag-lLoad`）的请求中发送。
推荐将使用`targetPageParamsAll`进行设置，因为它将在每个目标请求中发送。
使用`targetPageParamsAll`的优点是，您可以在页面上定义一次`mbox3rdPartyId`，这将确保所有目标请求都具有正确的`mbox3rdPartyId`。

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

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html?lang=zh-Hans)

### 使用Web SDK

Web SDK支持Target第三方ID。 但是，还需要执行几个步骤。 在深入研究解决方案之前，我们应该先谈一谈`identityMap`。
标识映射允许客户发送多个标识。 所有身份都处于命名空间中。 每个命名空间可以具有一个或多个标识。 可以将特定标识标记为主要标识。
有了这些知识，我们可以了解设置Web sdk以使用Target第三方ID的必要步骤。

1. 在数据流配置页面中设置将包含Target第三方ID的命名空间：

![数据流UI显示Target第三方ID命名空间字段](assets/mbox-3-party-id-setup.png)

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

使用at.js有两种方法可设置属性令牌，即使用`targetPageParams`或`targetPageParamsAll`。 使用`targetPageParams`可将属性令牌添加到`target-global-mbox`调用中，但使用`targetPageParamsAll`可将令牌添加到所有目标调用中：

**示例1**

```javascript
   window.targetPageParamsAll = function() {
      return {
        "at_property": "1234"
      };
    };
```

**示例2**

```javascript
window.targetPageParams = function() {
      return {
        "at_property": "1234"
      };
    };
```

### 使用Web SDK

使用Web SDK，客户在设置Adobe Target命名空间下的数据流配置时，可以在更高级别设置属性：
![显示Adobe Target设置的数据流UI。](assets/at-property-setup.png)
这意味着该特定数据流配置的每个Target调用都将包含该资产令牌。

## 如何预取mbox

### 使用at.js

此功能仅在at.js 2.x中可用。at.js 2.x具有一个名为`getOffers`的新函数。 `getOffers`允许客户预取一个或多个mbox的内容。 示例如下：

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

注意：强烈建议确保`mboxes`数组中的每个`mbox`都有自己的索引。 通常第一个mbox具有`index=0`、下一个`index=1`等。

### 使用Web SDK

Web SDK当前不支持此功能。

## 如何调试Target实施

### 使用at.js

At.js会公开以下调试功能：

* Mbox禁用 — 禁用Target的提取和渲染功能，以检查页面是否在不进行Target交互的情况下损坏
* Mbox调试 — at.js记录每个操作
* 目标跟踪 — 通过靶心中生成的mbox跟踪令牌，具有参与决策过程的详细信息的跟踪对象可在`window.___target_trace`对象下使用

注意：所有这些调试功能都可以在[Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)的增强功能中使用

### 使用Web SDK

在使用Web SDK时，您拥有多种调试功能：

* 使用[Assurance](/help/assurance/home.md)
* [已启用Web SDK debug](/help/web-sdk/use-cases/debugging.md)
* 使用[Web SDK监视挂接](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* 使用[Adobe Experience Platform Debugger](/help/debugger/home.md)
* 目标跟踪

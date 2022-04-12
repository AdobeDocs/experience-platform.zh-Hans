---
title: 平台Web SDK中A4T数据的客户端日志记录
description: 了解如何使用Experience PlatformWeb SDK为Adobe Analytics for Target(A4T)启用客户端日志记录。
seo-title: Client-side logging for A4T data in the Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: Target;A4T；日志记录；Web SDK；体验；平台
source-git-commit: a2214465001f90d19d88c0622c154e7a4ae3bb03
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 4%

---

# 平台Web SDK中A4T数据的客户端日志记录

## 概述 {#overview}

Adobe Experience Platform Web SDK允许您收集 [Adobe Analytics for Target(A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=zh-Hans) Web应用程序客户端上的数据。

客户端日志记录是指与 [!DNL Target] 数据在客户端返回，允许您收集数据并将其与Analytics共享。 如果您打算使用 [数据插入API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html).

>[!NOTE]
>
>使用执行此操作的方法 [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=zh-Hans) 目前正在开发中，将在不久的将来提供。

本文档介绍了为Web SDK设置客户端A4T日志记录的步骤，并提供了一些常见用例的实施示例。

## 先决条件 {#prerequisites}

本教程假定您熟悉与将Web SDK用于个性化相关的基本概念和流程。 如果您需要介绍，请查看以下文档：

* [配置Web SDK](../../../fundamentals/configuring-the-sdk.md)
* [发送事件](../../../fundamentals/tracking-events.md)
* [呈现个性化内容](../../rendering-personalization-content.md)

## 设置Analytics客户端日志记录 {#set-up-client-side-logging}

以下子部分概述了如何为Web SDK实施启用Analytics客户端日志记录。

### 启用Analytics客户端日志记录 {#enable-analytics-client-side-logging}

要考虑为您的实施启用Adobe Analytics客户端日志记录，您必须在 [数据流](../../../fundamentals/datastreams.md).

![Analytics数据流配置已禁用](../assets/disable-analytics-datastream.png)

### 检索 [!DNL A4T] 从SDK获取的数据并将其发送到Analytics {#a4t-to-analytics}

要使此报表方法正常工作，您必须发送 [!DNL A4T] 从检索到的相关数据 [`sendEvent`](../../../fundamentals/tracking-events.md) 命令。

当Target Edge计算命题响应时，它会检查是否启用了Analytics客户端日志记录（即，如果您的数据流中禁用了Analytics）。 如果启用了客户端日志记录，则系统会向响应中的每个建议添加一个Analytics令牌。

该流程类似于以下内容：

![客户端日志记录流](../assets/analytics-client-side-logging.png)

以下是 `interact` 启用Analytics客户端日志记录时的响应。 如果建议的活动包含Analytics报表，则该活动将具有 `scopeDetails.characteristics.analyticsToken` 属性。

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
              "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
              "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "characteristics": {
              "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
              "analyticsToken": "434689:0:0|32767"
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

基于表单的体验编辑器活动的建议可以在同一建议下同时包含内容和点击量度项目。 因此，在中不显示内容的单个分析令牌 `scopeDetails.characteristics.analyticsToken` 属性中，它们可以同时具有在 `scopeDetails.characteristics.analyticsTokens` 对象，在 `display` 和 `click` 属性，相应地。

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
              "eventTokens": {
                "display": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
                "click": "E0gb6q1+WyFW3FMbbQJmrg=="
              },
              "analyticsTokens": {
                "display": "434689:0:0|2,434689:0:0|1",
                "click": "434689:0:0|32767"
              }
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
            },
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

所有 `scopeDetails.characteristics.analyticsToken`, `scopeDetails.characteristics.analyticsTokens.display` （对于显示的内容）和 `scopeDetails.characteristics.analyticsTokens.click` （对于点击量度）是需要收集并作为 `tnta` 标记 [数据插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) 呼叫。

>[!IMPORTANT]
>
>请注意， `analyticsToken`/`analyticsTokens` 属性可以包含多个令牌，并作为一个以逗号分隔的字符串连接。
>
>在下一节中提供的实施示例中，会反复收集多个Analytics令牌。 要连接Analytics令牌数组，请使用如下类似的函数：
>
>
```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## 实施示例 {#implementation-examples}

以下子部分演示了如何为常见用例实施Analytics客户端日志记录。

### 基于表单的体验编辑器活动 {#form-based-composer}

您可以使用Web SDK控制建议的执行 [Adobe Target基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) 活动。

当您请求针对特定决策范围的建议时，返回的建议包含其适当的Analytics令牌。 最佳做法是连接平台Web SDK `sendEvent` 命令并迭代返回的命题，以在同时收集Analytics令牌时执行它们。

您可以触发 `sendEvent` 命令来访问基于表单的体验编辑器活动范围，如下所示：

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  for (var i = 0; i < results.propositions.length; i++) {
    //Execute the propositions and collect the Analytics payload
  }
});
```

从此处，您必须实施代码以执行建议并构建最终将发送到Analytics的有效负载。 这是 `results.propositions` 可能包含：

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
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
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
        "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
        "analyticsToken": "434689:0:0|32767"
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
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434688"
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
        "eventTokens": {
          "display": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "click": "Tagb6q1+WyFW3FMbbQJrtg=="
        },
        "analyticsTokens": {
          "display": "434688:0:0|2,434688:0:0|1",
          "click": "434688:0:0|32767"
        }
      }
    },
    "items": [
      {
        "id": "1184845",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434688",
          "experience.id": "0",
          "activity.name": "a4t test form based activity 1",
          "offer.id": "1184845"
        },
        "data": {
          "id": "1184845",
          "format": "text/html",
          "content": "<div> analytics impressions 1</div>"
        }
      },
      {
        "id": "434688",
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

要从包含内容项的命题中提取Analytics令牌，您可以实施类似于以下内容的函数：

```javascript
function getDisplayAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsTokens) {
    return characteristics.analyticsTokens.display;
  }
  return characteristics.analyticsToken;
}
```

建议可以具有不同类型的项目，如 `schema` 该项目的属性。 基于表单的体验编辑器活动支持四个建议项目架构：

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` 和 `JSON_SCHEMA` 是反映选件类型的架构，而 `MEASUREMENT_SCHEMA` 反映应附加到DOM元素的量度。

在访客实际单击之前显示的内容时，应收集点击量度的Analytics负载，并将其与内容项目分开发送到Analytics。

在这种情况下，以下用于获取点击量度A4T有效负载的帮助程序函数将会派上用场：

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsTokens) {
    return characteristics.analyticsTokens.click;
  }
  return characteristics.analyticsToken;
}
```

#### 实施摘要 {#implementation-summary}

总之，在使用Platform Web SDK应用基于表单的体验编辑器活动时，必须执行以下步骤：

1. 发送可获取基于表单的体验编辑器活动选件的事件；
1. 将内容更改应用到页面；
1. 发送 `decisioning.propositionDisplay` 通知事件；
1. 从SDK响应中收集Analytics显示令牌，并构建Analytics点击的有效负载；
1. 使用 [数据插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);
1. 如果已提交的建议中有任何点击量度，则应设置点击侦听器，以便在执行点击时，它会发送 `decisioning.propositionInteract` 通知事件。 的 `onBeforeEventSend` 应配置处理程序，以便在拦截 `decisioning.propositionInteract` 事件，则会执行以下操作：
   1. 从收集点击Analytics令牌 `xdm._experience.decisioning.propositions`
   1. 使用通过收集的Analytics有效负载发送点击Analytics点击 [数据插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  var analyticsPayload = new Set();
  results.propositions.forEach(function (proposition) {
    proposition.items.forEach(function (item) {
      if (item.schema === HTML_SCHEMA) {
        // 1. Apply offer
        // 2. Collect executed propositions and send the decisioning.propositionDisplay notification event
        // 3. Collect the display Analytics tokens
      }
      if (item.schema === MEASUREMENT_SCHEMA) {
        // Setup click listener, so that when clicked:
        // 1. Collect clicked propositions and send the decisioning.propositionInteract notification event
        // Note: onBeforeEventSend handler should be configured, so that when intercepting decisioning.propositionInteract events:
        //   1. Collect the click Analytics tokens from xdm._experience.decisioning.propositions
        //   2. Send the click Analytics hit with the collected Analytics payload via Data Insertion API
      }
    });
  });
  // Send the page view Analytics hit with the collected display Analytics payload via Data Insertion API
});
```

### 可视化体验编辑器活动 {#visual-experience-composer-acitivties}

Web SDK允许您处理使用创作的选件 [可视化体验编辑器(VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).

>[!NOTE]
>
>实施此用例的步骤与 [基于表单的体验编辑器活动](#form-based-composer). 有关更多详细信息，请查看上一节。

启用自动渲染后，您可以从页面上执行的建议中收集Analytics令牌。 最佳做法是连接平台Web SDK `sendEvent` 命令并迭代返回的主题，以过滤Web SDK尝试渲染的主题。

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
  
    var proposition = propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getDisplayAnalyticsPayload(proposition);
      
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // Send the page view Analytics hit with collected Analytics payload via Data Insertion API
});
```

### 使用 `onBeforeEventSend` 处理页面量度 {#using-onbeforeeventsend}

使用Adobe Target活动，您可以在页面上设置不同的量度，即手动附加到DOM，或自动附加到DOM（VEC创作的活动）。 这两种类型都是网页上延迟的最终用户交互。

为此，最佳做法是使用 `onBeforeEventSend` Adobe Experience Platform Web SDK挂接。 的 `onBeforeEventSend` 挂钩应使用 `configure` ，并将反映在通过数据流发送的所有事件中。

以下示例说明了如何 `onBeforeEventSent` 可以配置为触发Analytics点击：

```javascript
alloy("configure", {
  edgeConfigId: "datastream configuration ID",
  orgId: "adobe ORG ID",
  onBeforeEventSend: function(options) {
    const xdm = options.xdm;
    const eventType = xdm.eventType;
    if (eventType === "decisioning.propositionInteract") {
      const analyticsPayloads = new Set();
      const propositions = xdm._experience.decisioning.propositions;

      for (var i = 0; i < propositions.length; i++) {
        var proposition = propositions[i];
        analyticsPayloads.add(getClickAnalyticsPayload(proposition));
      }
      // Trigger the Analytics hit
    }
  }
});
```

## 后续步骤 {#next-steps}

本指南介绍了Web SDK中A4T数据的客户端日志记录。 请参阅 [服务器端日志记录](server-side.md) 有关如何在边缘网络上处理A4T数据的更多信息。

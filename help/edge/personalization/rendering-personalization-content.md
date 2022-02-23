---
title: 使用Adobe Experience Platform Web SDK渲染个性化内容
description: 了解如何使用Adobe Experience Platform Web SDK呈现个性化内容。
keywords: 个性化；renderDecisions;sendEvent;decisionScopes；建议；
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 6ba563db7fd31084813426ffbb0c35be9d7fe4bb
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 1%

---

# 呈现个性化内容

Adobe Experience Platform Web SDK支持从Adobe个性化解决方案中检索个性化内容，包括 [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) 和 [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=zh-Hans).

此外，Web SDK还通过Adobe Experience Platform个性化目标(例如 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自定义个性化连接](../../destinations/catalog/personalization/custom-personalization.md). 要了解如何为同一页面和下一页面个性化配置Experience Platform，请参阅 [专用指南](../../destinations/ui/configure-personalization-destinations.md).

在Adobe Target中创建的内容 [可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) 可由SDK自动检索和渲染。 在Adobe Target中创建的内容 [基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) 或Offer decisioning无法由SDK自动呈现。 您而是必须使用SDK请求此内容，然后自行手动渲染该内容。

## 自动渲染内容

向服务器发送事件时，您可以将 `renderDecisions` 选项 `true`. 这样做会强制SDK自动渲染任何符合自动渲染条件的个性化内容。

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

呈现个性化内容是异步的，因此您不应当假设特定内容将何时完成渲染。

## 手动渲染内容

要访问任何个性化内容，您可以提供一个回调函数，该函数将在SDK收到来自服务器的成功响应后调用。 您的回调函数提供了 `result` 对象，可能包含 `propositions` 属性。 以下示例用于说明在发送事件时如何提供回调函数。

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

在本例中， `result.propositions`，如果存在，则是一个数组，其中包含与事件相关的个性化建议。 默认情况下，它仅包含符合自动渲染条件的建议。

的 `propositions` 数组可能类似于以下示例：

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  }
]
```

在本例中， `renderDecisions` 选项未设置为 `true` 当 `sendEvent` 命令，因此SDK未尝试自动渲染任何内容。 但是，SDK仍会自动检索符合自动渲染条件的内容，并将其提供给您以在您愿意的情况下手动渲染。 请注意，每个命题对象都有其 `renderAttempted` 属性设置为 `false`.

如果您改为 `renderDecisions` 选项 `true` 在发送事件时，SDK会尝试渲染任何符合自动渲染条件的主张（如之前所述）。 因此，每个提案对象都将拥有 `renderAttempted` 属性设置为 `true`. 在这种情况下，无需手动呈现这些建议。

迄今为止，我们仅讨论了符合自动渲染条件的个性化内容(即在Adobe Target的可视化体验编辑器中创建的任何内容)。 检索任何个性化内容 _not_ 符合自动渲染的条件，您需要通过在 `decisionScopes` 选项。 范围是一个字符串，用于标识要从服务器检索的特定主张。

示例如下：

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

在本例中，如果在与 `salutation` 或 `discount` 范围，则会返回并包含在 `result.propositions` 数组。 请注意，符合自动渲染条件的主张将继续包含在 `propositions` 阵列，无论您如何配置 `renderDecisions` 或 `decisionScopes` 选项。 的 `propositions` 数组在本例中类似于以下示例：

```json
[
  {
    "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
    "scope": "salutation",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/json-content-item",
        "data": {
          "id": "4433221",
          "content": {
            "salutation": "Welcome, esteemed visitor!"
          }
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
      "activity": {
        "id": "384456"
      }
    },  
    "renderAttempted": false
  },
  {
    "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
    "scope": "discount",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "data": {
          "id": "4433222",
          "content": "<div>50% off your order!</div>",
          "format": "text/html"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
      "activity": {
        "id": "384457"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  }
]
```

此时，您可以根据自己的需求渲染建议内容。 在本例中，建议与 `discount` 范围是使用Adobe Target的基于表单的体验编辑器构建的HTML建议。 假定您的页面上有一个ID为 `daily-special` 并希望从 `discount` 建议 `daily-special` 元素，请执行以下操作：

1. 从 `result` 对象。
1. 回顾每个命题，寻找包含范围的命题 `discount`.
1. 如果您找到一个建议，请循环查看建议中的每个项目，并查找HTML内容的项目。 （检查好过假设。）
1. 如果您找到包含HTML内容的项目，请找到 `daily-special` 元素，并将其HTML替换为个性化内容。
1. 内容呈现后，发送 `display` 事件。

您的代码如下所示：

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['salutation', 'discount']
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

  var discountHtml;
  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a signle place to update in the HTML.
        break;  
      }
    }
      // Send a "display" event 
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


>[!TIP]
>
>如果您使用Adobe Target，则作用域与服务器上的mbox相对应，只是它们都是同时请求的，而不是单独请求。 将始终返回全局mbox。

### 管理闪烁

SDK为 [管理闪烁](../personalization/manage-flicker.md) 在个性化过程中。

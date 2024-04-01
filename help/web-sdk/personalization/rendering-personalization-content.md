---
title: 使用Adobe Experience Platform Web SDK呈现个性化内容
description: 了解如何使用Adobe Experience Platform Web SDK呈现个性化内容。
keywords: 个性化；renderDecisions；sendEvent；decisionScopes；建议；
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 6841a6f777d18845ce36e3503fbdb9698ece84bb
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# 呈现个性化内容

Adobe Experience Platform Web SDK支持从Adobe个性化解决方案中检索个性化内容，包括 [Adobe Target](https://business.adobe.com/products/target/adobe-target.html)， [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=zh-Hans) 和 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=zh-Hans).

此外，Web SDK还通过Adobe Experience Platform个性化目标(例如 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自定义个性化连接](../../destinations/catalog/personalization/custom-personalization.md). 要了解如何为同页和下一页个性化配置Experience Platform，请参阅 [专用指南](../../destinations/ui/activate-edge-personalization-destinations.md).

在Adobe Target中创建的内容 [可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) 以及Adobe Journey Optimizer的 [Web Campaign UI](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) SDK可以自动检索和渲染。 在Adobe Target中创建的内容 [基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)， Adobe Journey Optimizer的 [基于代码的体验渠道](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based) 或Offer decisioning无法由SDK自动呈现。 相反，您必须使用SDK请求此内容，然后自行手动渲染内容。

## 自动呈现内容 {#automatic}

将事件发送到服务器时，可以设置 `renderDecisions` 选项至 `true`. 这样做会强制SDK自动呈现任何符合自动呈现条件的个性化内容。

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

渲染个性化内容是异步的，因此您不应假设一段特定内容何时已完成渲染。

## 手动呈现内容 {#manual}

要访问任何个性化内容，您可以提供回调函数，SDK收到来自服务器的成功响应后将调用该函数。 为您的回调提供了 `result` 对象，其中可能包含 `propositions` 包含任何返回的个性化内容的属性。 下面是一个示例，说明在发送事件时如何提供回调函数。

```javascript
alloy("sendEvent", {
    "xdm": {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

在此示例中， `result.propositions`如果存在，则是一个数组，其中包含与事件相关的个性化建议。 默认情况下，它仅包含适于自动渲染的建议。

此 `propositions` 数组可能与以下示例类似：

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

在本例中， `renderDecisions` 选项未设置为 `true` 当 `sendEvent` 已执行命令，因此SDK不会尝试自动渲染任何内容。 但是，SDK仍会自动检索符合自动渲染条件的内容，如果您愿意，可以将其提供给您手动渲染。 请注意，每个建议对象都有其 `renderAttempted` 属性设置为 `false`.

如果您选择将 `renderDecisions` 选项至 `true` 在发送事件时，SDK会尝试呈现任何符合自动呈现条件的建议（如之前所述）。 因此，每个建议对象将具有 `renderAttempted` 属性设置为 `true`. 在这种情况下，无需手动呈现这些建议。

到目前为止，我们仅讨论了符合自动呈现条件的个性化内容(即，在Adobe Target的可视化体验编辑器或Adobe Journey Optimizer的Web Campaign UI中创建的任何内容)。 检索任何个性化内容 _非_ 符合自动渲染的条件，您需要通过填充 `decisionScopes` 选项。 范围是一个字符串，它标识您要从服务器检索的特定建议。

示例如下：

```javascript
alloy("sendEvent", {
    "xdm": {},
    "decisionScopes": ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

在本例中，如果在服务器上找到与 `salutation` 或 `discount` 范围，它们将返回并包含在 `result.propositions` 数组。 请注意，符合自动呈现条件的主张将继续包含在 `propositions` 阵列，无论您如何配置 `renderDecisions` 或 `decisionScopes` 选项。 此 `propositions` 在此例中，数组类似于以下示例：

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

此时，您可以根据需要呈现建议内容。 在此示例中，建议与 `discount` scope是使用Adobe Target的基于表单的HTML编辑器构建的体验建议。 假设您的页面上有元素，其ID为 `daily-special` 并希望呈现以下源的内容： `discount` 中的建议 `daily-special` 元素，请执行以下操作：

1. 从提取建议 `result` 对象。
1. 循环查看每个建议，寻找具有以下范围的建议 `discount`.
1. 如果您找到一个建议，请循环遍历建议中的每个项目，查找包含HTML内容的项目。 （检查总比假设要好。 ）
1. 如果找到一个包含HTML内容的项目，请找到 `daily-special` 元素，并将其HTML替换为个性化内容。
1. 呈现内容后，发送 `display` 事件。

您的代码将如下所示：

```javascript
alloy("sendEvent", {
  "xdm": {},
  "decisionScopes": ['salutation', 'discount']
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
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": discountProposition.id,
                "scope": discountProposition.scope,
                "scopeDetails": discountProposition.scopeDetails
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
>如果您使用Adobe Target，则作用域将与服务器上的mbox相对应，只不过这些作用域是同时请求的，而不是分别请求的。 始终返回全局mbox。

### 管理闪烁

SDK为以下人员提供工具 [管理闪烁](../personalization/manage-flicker.md) 在个性化过程中。

## 在单页应用程序中渲染建议而不增加量度 {#applypropositions}

此 `applyPropositions` 命令允许您从呈现或执行建议数组 [!DNL Target] 或Adobe Journey Optimizer集成到单页应用程序中，而不增加 [!DNL Analytics] 和 [!DNL Target] 量度。 这提高了报告准确性。

>[!IMPORTANT]
>
>如果建议用于 `__view__` 范围（或Web表面）在页面加载时渲染，其 `renderAttempted` 标志将设置为 `true`. 此 `applyPropositions` 命令将不会重新呈现 `__view__` 具有以下特征的范围（或Web表面）建议 `renderAttempted: true` 标志。

### 用例1：重新呈现单页应用程序视图建议

下面示例中描述的用例重新呈现之前获取和渲染的购物车视图建议，而不发送显示通知。

在以下示例中， `sendEvent` 命令在视图更改时触发，并将生成的对象保存为常量。

接下来，当视图或组件更新时， `applyPropositions` 调用命令，其中包含来自上一页的建议 `sendEvent` 命令，以重新渲染视图建议。

```js
var cartPropositions = alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
        "web": {
            "webPageDetails": {
                "viewName": "cart"
            }
        }
    }
}).then(function(result) {
    var propositions = result.propositions;

    // Collect response tokens, etc.
    return propositions;
});

// Call applyPropositions to re-render the view propositions from the previous sendEvent command.
alloy("applyPropositions", {
    "propositions": cartPropositions
});
```

### 用例2：没有选择器的渲染建议

此用例适用于使用创作的体验 [!DNL Target Form-based Experience Composer] 或Adobe Journey Optimizer的 [基于代码的体验渠道](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based).

您必须在以下位置提供选择器、操作和范围： `applyPropositions` 呼叫。

支持 `actionTypes` 为：

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
    "decisionScopes": ["salutation", "discount"]
}).then(function(result) {
    var retrievedPropositions = result.propositions;
    // Render propositions on the page by providing additional metadata

    return alloy("applyPropositions", {
        "propositions": retrievedPropositions,
        "metadata": {
            "salutation": {
                "selector": "#first-form-based-offer",
                "actionType": "setHtml"
            },
            "discount": {
                "selector": "#second-form-based-offer",
                "actionType": "replaceHtml"
            }
        }
    }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        function sendDisplayEvent(proposition) {
            const {
                id,
                scope,
                scopeDetails = {}
            } = proposition;

            alloy("sendEvent", {
                xdm: {
                    eventType: "decisioning.propositionDisplay",
                    _experience: {
                        decisioning: {
                            propositions: [{
                                id: id,
                                scope: scope,
                                scopeDetails: scopeDetails,
                            }, ],
                            propositionEventType: {
                                display: 1
                            },
                        },
                    },
                },
            });
        }
    });
});
```

如果您没有为决策范围提供元数据，则不会呈现关联的建议。

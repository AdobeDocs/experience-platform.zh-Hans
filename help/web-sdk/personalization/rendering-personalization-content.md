---
title: 使用Adobe Experience Platform Web SDK呈现个性化内容
description: 了解如何使用Adobe Experience Platform Web SDK呈现个性化内容。
keywords: 个性化；renderDecisions；sendEvent；decisionScopes；建议；
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# 呈现个性化内容

Adobe Experience Platform Web SDK支持从Adobe个性化解决方案中检索个性化内容，这些解决方案包括[Adobe Target](https://business.adobe.com/products/target/adobe-target.html)、[Offer Decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=zh-Hans)和[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=zh-Hans)。

此外，Web SDK还通过Adobe Experience Platform个性化目标(如[Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md)和[自定义个性化连接](../../destinations/catalog/personalization/custom-personalization.md))支持同页和下一页个性化功能。 要了解如何为同页和下一页个性化配置Experience Platform，请参阅[专用指南](../../destinations/ui/activate-edge-personalization-destinations.md)。

在Adobe Target的[可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=zh-Hans)和Adobe Journey Optimizer的[Web Campaign UI](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=zh-Hans)中创建的内容可由SDK自动检索和渲染。 在Adobe Target的[基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=zh-Hans)、Adobe Journey Optimizer的[基于代码的体验渠道](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/code-based-experience/get-started-code-based)或Offer Decisioning中创建的内容，无法由SDK自动呈现。 相反，您必须使用SDK请求此内容，然后自行手动渲染内容。

## 自动呈现内容 {#automatic}

将事件发送到服务器时，可以将`renderDecisions`选项设置为`true`。 这样做会强制SDK自动呈现任何符合自动呈现条件的个性化内容。

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

要访问任何个性化内容，您可以提供回调函数，在SDK收到来自服务器的成功响应后，将调用该函数。 为您的回调提供了`result`对象，该对象可能包含包含包含任何返回的个性化内容的`propositions`属性。 下面是一个示例，说明在发送事件时如何提供回调函数。

```javascript
alloy("sendEvent", {
    "xdm": {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

在此示例中，`result.propositions`（如果存在）是一个数组，其中包含与事件相关的个性化建议。 默认情况下，它仅包含适于自动渲染的建议。

`propositions`数组可能与以下示例类似：

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

在该示例中，执行`renderDecisions`命令时，`true`选项未设置为`sendEvent`，因此SDK未尝试自动呈现任何内容。 但是，SDK仍会自动检索符合自动渲染条件的内容，并在需要时为您提供该内容以手动渲染。 请注意，每个建议对象的`renderAttempted`属性均设置为`false`。

如果您在发送事件时将`renderDecisions`选项设置为`true`，则SDK会尝试呈现任何符合自动呈现条件的建议（如前所述）。 因此，每个建议对象的`renderAttempted`属性都将设置为`true`。 在这种情况下，无需手动呈现这些建议。

到目前为止，我们仅讨论了符合自动呈现条件的个性化内容(即，在Adobe Target的可视化体验编辑器或Adobe Journey Optimizer的Web Campaign UI中创建的任何内容)。 要检索任何个性化内容&#x200B;_不符合_&#x200B;的自动呈现条件，您需要在发送事件时通过填充`decisionScopes`选项来请求该内容。 范围是一个字符串，它标识您要从服务器检索的特定建议。

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

在此示例中，如果在与`salutation`或`discount`范围匹配的服务器上找到建议，则将返回这些建议并将其包含在`result.propositions`数组中。 请注意，无论如何配置`propositions`或`renderDecisions`选项，符合自动呈现条件的建议将继续包含在`decisionScopes`阵列中。 在这种情况下，`propositions`数组将与以下示例类似：

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

此时，您可以根据需要呈现建议内容。 在此示例中，与`discount`范围匹配的建议是使用HTML的基于表单的体验编辑器构建的Adobe Target建议。 假定您的页面上的ID为`daily-special`的元素并希望将`discount`建议中的内容渲染到`daily-special`元素中，请执行以下操作：

1. 从`result`对象提取建议。
1. 循环遍历每个建议，查找范围为`discount`的建议。
1. 如果您找到一个建议，请循环遍历建议中的每个项目，查找作为HTML内容的项目。 （检查总比假设要好。 ）
1. 如果找到一个包含HTML内容的项目，请在页面上找到`daily-special`元素，并将其HTML替换为个性化内容。
1. 呈现内容后，发送`display`事件。

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
    // Rather than assuming there is a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
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
            ],
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


>[!TIP]
>
>如果您使用Adobe Target，则作用域将与服务器上的mbox相对应，只不过这些作用域是同时请求的，而不是分别请求的。 始终返回全局mbox。

### 管理闪烁

SDK在个性化过程中为[管理闪烁](../personalization/manage-flicker.md)提供了便利。

## 在单页应用程序中渲染建议而不增加量度 {#applypropositions}

`applyPropositions`命令允许您将[!DNL Target]或Adobe Journey Optimizer中的建议数组渲染或执行到单页应用程序中，而不增加[!DNL Analytics]和[!DNL Target]指标。 这提高了报告准确性。

>[!IMPORTANT]
>
>如果在页面加载时呈现了`__view__`作用域（或Web表面）的建议，则其`renderAttempted`标志将设置为`true`。 `applyPropositions`命令将不会重新呈现具有`__view__`标志的`renderAttempted: true`作用域（或Web表面）建议。

### 用例1：重新呈现单页应用程序视图建议

下面示例中描述的用例重新呈现之前获取和渲染的购物车视图建议，而不发送显示通知。

在以下示例中，`sendEvent`命令在视图更改时触发，并将生成的对象保存为常量。

接下来，当视图或组件被更新时，使用上一个`applyPropositions`命令中的建议调用`sendEvent`命令以重新呈现视图建议。

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

此使用案例适用于使用[!DNL Target Form-based Experience Composer]或Adobe Journey Optimizer的[基于代码的体验渠道](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/code-based-experience/get-started-code-based)创作的体验。

必须在`applyPropositions`调用中提供选择器、操作和范围。

支持的`actionTypes`包括：

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
});
```

如果您没有为决策范围提供元数据，则不会呈现关联的建议。

---
title: 在Web SDK中管理显示事件
description: 解释什么是显示事件以及如何在Web SDK中使用它们。
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
keywords: 个性化；显示事件；sendEvent；renderDecisions；applyPropositions；建议；
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# 在Web SDK中管理显示事件

显示事件可告知个性化服务或Analytics服务，已向用户显示了特定的个性化内容。 发送显示事件有助于下游系统区分&#x200B;*请求的内容*&#x200B;和&#x200B;*实际显示的内容*，从而提高报表准确性。

## 自动发送显示事件

自动显示事件通常是最简单的选项。 它们在Web SDK从`sendEvent`响应中完成合格内容的渲染后立即发送，这可以提高报表准确性。

要自动发送显示事件，请使用将`sendEvent`设置为`renderDecisions`并将`true`设置为`personalization.sendDisplayEvent`的`true`调用（或省略，因为`true`是默认值）：

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: { }, // sendDisplayEvent defaults to true
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

>[!NOTE]
>
>自动显示事件取决于SDK管理的渲染。 如果您手动渲染内容（包括使用`applyPropositions`），则必须使用`sendEvent`显式发送显示事件。

## 在后续`sendEvent`调用中发送显示事件

当您想要附加在请求个性化时不可用的其他页面加载数据时，在稍后的`sendEvent`调用中包含显示事件会很有用。 常用于实现[顶页面事件和底页面事件](/help/collection/use-cases/personalization/top-bottom-page-events.md)。 以这种方式正确实施显示事件有助于避免Adobe Analytics中的[跳出率](https://experienceleague.adobe.com/zh-hans/docs/analytics/components/metrics/bounce-rate)出现问题。

1. 在初始`sendEvent`调用（通常在页面顶部）中，请求并渲染内容，但通过将`renderDecisions`设置为`true`并将`personalization.sendDisplayEvent`设置为`false`来禁止自动显示事件：

   ```js
   alloy("sendEvent", {
     renderDecisions: true,
     personalization: { sendDisplayEvent: false },
     xdm: {
       web: {
         webPageDetails: {
            name: "home"
         }
       }
     }
   });
   ```

1. 稍后（通常在页面底部），使用XDM有效负载调用`sendEvent`，该XDM有效负载包含自上次请求以来通过将[`personalization.includeRenderedPropositions`](/help/collection/js/commands/sendevent/personalization.md)设置为`true`而呈现的建议的显示事件：

   ```js
   alloy("sendEvent", {
     personalization: { includeRenderedPropositions: true },
     xdm: {
       // Add any additional page load telemetry you want to send here
       web: {
         webPageDetails: {
           name: "home"
         }
       }
     }
   });
   ```

>[!NOTE]
>
>使用`includeRenderedPropositions`时，只包括已隐藏显示的自动渲染建议。

## 发送手动呈现的建议的显示事件

如果您自己渲染内容（完全手动渲染或使用`applyPropositions`），则必须使用`sendEvent`命令显式发送显示事件。 使用包含以下属性的XDM有效负载调用`sendEvent`：

* `_experience.decisioning.propositions`包含渲染的建议“`id`”、`scope`和`scopeDetails`
* `_experience.decisioning.propositionEventType.display`设置为`1`

以下两个示例使用此帮助程序函数来构建显示事件XDM有效负载：

```js
function buildDisplayEventXdm(renderedPropositions) {
  return {
    eventType: "decisioning.propositionDisplay",
    _experience: {
      decisioning: {
        propositions: renderedPropositions.map(({ id, scope, scopeDetails }) => ({
          id,
          scope,
          scopeDetails
        })),
        propositionEventType: { display: 1 }
      }
    }
  };
}
```

以下示例对显示事件使用手动渲染：

```js
function renderExample(propositions) {
  // Your custom logic here. Return ONLY the propositions that were actually rendered.
  // For example: return [propositions[0]];
  return [];
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const renderedPropositions = renderExample(propositions);
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

以下示例使用带有显示事件的`applyPropositions`命令。 它将`sendEvent`、`applyPropositions`以及另一个`sendEvent`链接在一起：

```js
alloy("sendEvent", {
  personalization: { decisionScopes: ["discount", "salutation"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  });
}).then(({ propositions: renderedPropositions = [] }) => {
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

## 要避免的常见错误

* **在渲染完成之前发送显示事件**：在自动渲染完成之后、`applyPropositions`解析之后或手动渲染逻辑完成之后发送显示事件。
* **发送您未呈现的建议显示事件**：仅包括实际显示给用户的建议。
* **正在删除`scopeDetails`**：发送显示事件时从建议对象中包含`scopeDetails`。

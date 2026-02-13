---
title: 自动呈现DOM操作建议
description: 使用Web SDK自动渲染符合条件的DOM操作建议并处理常见的SPA重新渲染方案。
keywords: 个性化；renderDecisions；dom-action；sendEvent；applyPropositions；单页应用程序；
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 自动呈现DOM操作建议

当您的个性化响应包含带有架构的建议项目时，请使用此模式：

**`https://ns.adobe.com/personalization/dom-action`**

这些项目通常包括选择器和操作类型（例如，`setHtml`），启用`renderDecisions`后，Web SDK可自动应用这些类型。

## 1.管理闪烁（可选）

如果您在应用个性化内容时需要防止闪烁，请为您的实施使用推荐的闪烁管理方法。 有关可用选项，请参阅[管理闪烁](manage-flicker.md)。

## 2.请求并作出指示自动作出的决定

调用`renderDecisions`命令时将`true`设置为`sendEvent`。 如果忽略，`renderDecisions`属性将默认为false。

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

（可选）如果您需要请求特定投放位置，请包含`personalization.decisionScopes`：

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    decisionScopes: ["hero-banner", "recommendations"]
  },
  xdm: { }
});
```

有关详细信息，请参阅[`personalization`](/help/collection/js/commands/sendevent/personalization.md)命令中的[`sendEvent`](/help/collection/js/commands/sendevent/overview.md)对象。

## 3.显示事件

如果您将`renderDecisions`设置为`true`并将`personalization.sendDisplayEvent`设置为`true`或忽略它，则Web SDK会在呈现个性化后立即发送显示事件。

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    // sendDisplayEvent defaults to true when omitted
  },
  xdm: { }
});
```

请参阅[管理显示事件](display-events.md)，了解符合实施需求的备用选项，例如使用[顶页和底页事件](top-bottom-page-events.md)时。

## &#x200B;4. SPA视图更改和重新呈现

对于单页应用程序，在视图更改事件中包含`viewName`。

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```

如果您的SPA重新呈现同一视图的UI而没有新的决策获取，则您可以重新应用之前返回的建议：

```js
let lastPropositions = [];

alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: { webPageDetails: { viewName: "cart" } }
  }
}).then(({ propositions = [] }) => {
  lastPropositions = propositions;
});

// Later, after a UI re-render:
alloy("applyPropositions", {
  propositions: lastPropositions
});
```

有关详细信息，请参阅[`applyPropositions`](/help/collection/js/commands/applypropositions.md)。

>[!NOTE]
>
>`applyPropositions`命令不会自动发送显示事件。 如果需要为重新渲染方案记录“显示”，请参阅[管理显示事件](display-events.md)。

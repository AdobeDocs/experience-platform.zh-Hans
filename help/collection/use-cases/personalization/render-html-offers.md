---
title: 呈现不带选择器的HTML选件
description: 通过提供元数据到applyPropositions来呈现不包含选择器的HTML建议项，然后记录显示事件。
keywords: 个性化；applyPropositions；元数据；actionType；decisionScopes；显示事件；
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# 呈现不带选择器的HTML选件

当您的建议包含HTML内容时，请使用此模式，但您必须提供应用它的位置（选择器）以及如何应用它（操作类型）。 为此，您可以调用带有按范围键值的[`applyPropositions`](/help/collection/js/commands/applypropositions.md)对象的`metadata`。 支持的`actionType`值为`setHtml`、`replaceHtml`和`appendHtml`。

## 1.管理闪烁（可选）

如果在渲染时隐藏内容，则您负责在渲染完成后显示内容。 有关详细信息，请参阅[管理闪烁](manage-flicker.md)。

## 2.请求您打算呈现的范围的建议

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

有关详细信息，请参阅[`personalization.decisionScopes`](/help/collection/js/commands/sendevent/personalization.md)。

## 3.渲染带有`applyPropositions`元数据的选件

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: {
        selector: "#salutation",
        actionType: "setHtml"
      },
      discount: {
        selector: "#daily-special",
        actionType: "replaceHtml"
      }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return { renderedPropositions };
  });
});
```

## 4.记录呈现的建议的显示事件

在调用`applyPropositions`时，显示事件不会自动发送。 渲染完成后，使用引用渲染建议的`sendEvent`调用：

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return alloy("sendEvent", {
      xdm: {
        _experience: {
          decisioning: {
            propositions: toDisplayPayload(renderedPropositions),
            propositionEventType: { display: 1 }
          }
        }
      }
    });
  });
});
```

有关详细信息，请参阅[管理显示事件](display-events.md)。

>[!TIP]
>
>如果您使用[Top和bottom page事件](top-bottom-page-events.md)，则此“记录显示”调用通常在后`sendEvent`调用中实现。

## 5.重新呈现

如果您的实施需要稍后重新呈现（例如在单页应用程序中），请使用相同的建议和元数据再次调用`applyPropositions`：

```js
alloy("applyPropositions", {
  propositions,
  metadata: {
    discount: { selector: "#daily-special", actionType: "replaceHtml" }
  }
});
```

如果需要为重新渲染录制显示事件，请参阅[管理显示事件](display-events.md)。

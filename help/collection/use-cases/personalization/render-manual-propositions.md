---
title: 手动呈现建议
description: 使用您自己的UI逻辑(HTML、JSON或自定义架构)呈现建议内容，然后记录显示事件。
keywords: 个性化；建议；手动渲染；sendEvent；decisionScopes；显示事件；
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 手动呈现建议

当您需要完全控制建议项的应用方式时，请使用此模式。 例如，您是从JSON内容构成复杂的UI，或者您希望在呈现之前应用自定义业务规则。

## 1.请求建议

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["salutation", "discount"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

有关详细信息，请参阅[`personalization`](/help/collection/js/commands/sendevent/personalization.md)命令中的[`sendEvent`](/help/collection/js/commands/sendevent/overview.md)对象。

## 2.呈现建议项目（示例）

手动渲染建议时，它们可以采用许多不同的表单或形状。 以下是按范围查找建议，然后应用它找到的第一个HTML内容项的最小示例。

```js
function findPropositionByScope(propositions, scope) {
  return propositions.find((p) => p.scope === scope);
}

function renderHtmlInto(selector, html) {
  const el = document.querySelector(selector);
  if (!el) return;
  el.innerHTML = html;
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const discount = findPropositionByScope(propositions, "discount");
  if (!discount) return { propositions, rendered: [] };

  const htmlItem = discount.items?.find(
    (i) => i.schema === "https://ns.adobe.com/personalization/html-content-item"
  );

  if (!htmlItem) return { propositions, rendered: [] };

  renderHtmlInto("#daily-special", htmlItem.data.content);
  return { propositions, rendered: [discount] };
});
```

>[!IMPORTANT]
>
>如果您渲染HTML，请确保它对于您的环境是安全的。 将内容渲染视为安全边界（清理、可信来源和CSP注意事项）。

## 3.记录所呈现内容的显示事件

对于手动渲染的建议，显示事件通过引用渲染的建议的`sendEvent`调用进行记录。

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

// Example: record display for the propositions you actually rendered.
alloy("sendEvent", {
  xdm: {
    _experience: {
      decisioning: {
        propositions: toDisplayPayload(renderedPropositions),
        propositionEventType: { display: 1 }
      }
    }
  }
});
```

有关详细信息，请参阅[管理显示事件](display-events.md)。

## 4.重新呈现

当UI更改需要重新渲染时，请针对您缓存的建议数据重新运行手动渲染逻辑（如果需要，可再次提取）。 如果需要为重新渲染方案记录显示，请参阅[管理显示事件](display-events.md)。

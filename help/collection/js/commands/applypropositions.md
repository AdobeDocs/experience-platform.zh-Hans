---
title: applyPropositions
description: 重新呈现已使用sendEvent呈现的建议。
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# `applyPropositions`

`applyPropositions`命令允许您重新渲染已使用[`sendEvent`](sendevent/overview.md)命令渲染的建议。 此命令在处理单页应用程序时很有用，应用程序重新渲染了页面的各个部分，可能会覆盖已应用于页面的任何个性化设置。

此命令支持以下字段：

* **建议**：要重新渲染的建议对象的数组。
* **视图名称**：要呈现的视图的名称。 已缓存这些决策的显示通知，可以使用`sendEvent`选项将其包含在后续`personalization.includeRenderedPropositions`命令中。
* **Meta数据**：确定如何应用HTML选件的对象。 它包含以下属性：
   * 范围
   * 选择器
   * 操作类型

调用Web SDK的配置实例时运行`applyPropositions`命令。 包含配置选项的对象支持以下字段：

* **`propositions`**：要重新渲染的建议对象的数组。 通常不使用此对象，因为`propositionScopes`字段通常确定您要重新渲染的领域或表面。
* **`metadata`**：确定如何应用HTML选件。 这是一个映射，其中键是范围或表面，值是包含键`selector`和`actionType`的对象。
   * `selector`：一个字符串，其中包含要应用HTML的CSS选择器。
   * `actionType`：要对HTML执行的操作。 有效值包括`setHtml`、`replaceHtml`和`appendHtml`。
* **`viewName`**：要在单页应用程序中呈现的视图的名称。 已缓存这些决策的显示通知，可以使用`sendEvent`将其包含在后续`personalization.includeRenderedPropositions`命令中。

```js
alloy("applyPropositions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```

## 使用Web SDK标记扩展应用建议

与此命令等效的Web SDK标记扩展是[**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md)操作。

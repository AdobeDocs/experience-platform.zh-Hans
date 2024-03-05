---
title: applyPropositions
description: 重新呈现已使用sendEvent呈现的建议。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---


# `applyPropositions`

此 `applyPropositions` 命令允许您重新呈现已使用 [`sendEvent`](sendevent/overview.md) 命令。 此命令在处理单页应用程序时很有用，应用程序重新渲染了页面的各个部分，可能会覆盖已应用于页面的任何个性化设置。

此命令支持以下字段：

* **建议**：要重新渲染的建议对象数组。
* **视图名称**：要呈现的视图的名称。 这些决策的显示通知将被缓存，并可包含在后续中 `sendEvent` 命令使用 `personalization.includePendingDisplayNotifications` 选项。
* **元数据**：确定如何应用HTML选件的对象。 它包含以下属性：
   * 范围
   * 选择器
   * 操作类型

## 使用Web SDK标记扩展应用建议

应用建议可作为Adobe Experience Platform数据收集标记界面中规则内的操作执行。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 规则]**，然后选择所需的规则。
1. 下 [!UICONTROL 操作]，选择现有操作或创建操作。
1. 设置 [!UICONTROL 扩展名] 下拉字段至 **[!UICONTROL Adobe Experience Platform Web SDK]**，并设置 [!UICONTROL 操作类型] 到 **[!UICONTROL 应用建议]**.
1. 在右侧设置所需字段。
1. 单击 **[!UICONTROL 保留更改]**，然后运行发布工作流程。

## 使用Web SDK JavaScript库应用建议

运行 `applyPropositions` 命令。 包含配置选项的对象支持以下字段：

* **`propositions`**：要重新渲染的建议对象数组。 通常不使用此对象，因为 `propositionScopes` 字段通常确定要重新渲染的范围或表面。
* **`metadata`**：确定如何应用HTML选件。 这是一个映射，其中键是范围或曲面，值是包含键的对象 `selector` 和 `actionType`.
   * `selector`：一个字符串，其中包含应用HTML的CSS选择器。
   * `actionType`：要对HTML执行的操作。 有效值包括 `setHtml`, `replaceHtml` 和 `appendHtml`。
* **`viewName`**：要在单页应用程序中呈现的视图的名称。 这些决策的显示通知将被缓存，并可包含在后续中 `sendEvent` 命令使用 `personalization.includePendingDisplayNotifications`.

```js
alloy("applyPropositiions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```

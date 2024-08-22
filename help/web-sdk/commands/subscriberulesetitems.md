---
title: subscribeRulesetItems
description: 使用subscribeRulesetItems命令订阅特定界面的内容卡。
source-git-commit: 01cba985e22e4673fb60721c810ac9cbee287386
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---


# `subscribeRulesetItems`

`subscribeRulesetItems`命令允许您订阅由满意的规则集产生的建议。 为此，可指定要过滤的曲面和方案，并提供回调函数。

无论何时评估规则集，回调函数都会接收一个包含建议数组的`result`对象。

>[!IMPORTANT]
>
>`subscribeRulesetItems`命令是获取来自规则集的建议的唯一方法，因为它们未与[`sendEvent`](sendevent/overview.md)结果一起返回。

## 命令选项 {#command-options}

此命令接受具有以下属性的`options`对象：

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| `surfaces` | 字符串数组 | 曲面列表。 仅当建议与此处提供的某个表面匹配时，回调函数才会接收建议。 |
| `schemas` | 字符串数组 | 架构列表。 仅当建议与此处提供的某个架构匹配时，回调函数才会接收建议。 |
| `callback` | 函数 | 当建议是满足的规则集的结果时将调用的回调函数。 调用时，回调函数接收两个参数： `result`和`collectEvent`。 有关详细信息，请参阅[回调参数](#callback-parameters)。 |

### Callback参数 {#callback-parameters}

调用时，回调函数会接收下表中描述的两个参数。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `result` | 对象 | 此对象包含`propositions`数组。  这些建议是令人满意的规则集的直接结果。 `result`对象的结构与使用`then`子句的`sendEvent`返回的[结果对象](command-responses.md)相同。 |
| `collectEvent` | 函数 | 一种方便的功能，可用于发送Edge Network事件以跟踪交互、显示和其他事件。 |

### `collectEvent`函数 {#collectevent-function}

`collectEvent`函数是一个方便的功能，可用于发送Edge Network事件以跟踪交互、显示和其他事件。 它接受下表中描述的两个参数。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| 事件类型 | 字符串 | 一个字符串，指明要发出的建议事件类型。 支持的事件类型为`display`、`interact`或`dismiss`。 |
| `propositions` | 数组 | 对应于事件的建议数组。 |

## 使用Web SDK标记扩展订阅内容卡 {#tag-extension}

按照以下步骤通过Tags用户界面订阅内容卡。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 规则]**，然后选择所需的规则。
1. 在[!UICONTROL 事件]下，选择现有事件或创建新事件。
1. 将[!UICONTROL 扩展]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，并将&#x200B;**[!UICONTROL 事件类型]**&#x200B;设置为&#x200B;**[!UICONTROL 订阅规则集项]**。
1. 在屏幕右侧选择要订阅内容卡的架构和界面。
1. 选择&#x200B;**[!UICONTROL 保留更改]**，然后运行发布工作流。

## 使用Web SDK JavaScript库订阅内容卡 {#library}

以下示例代码订阅了内容卡的`web://mywebsite.com/#welcome`表面，并使用`collectEvent`便利方法为所有建议发出`display`事件。

```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://mywebsite.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```

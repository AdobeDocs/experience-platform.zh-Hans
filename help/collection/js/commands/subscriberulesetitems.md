---
title: subscribeRulesetItems
description: 使用subscribeRulesetItems命令订阅特定界面的内容卡。
exl-id: bc932ba5-a810-4fa6-82cc-998af39fdd34
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 3%

---

# `subscribeRulesetItems`

`subscribeRulesetItems`命令允许您订阅由满意的规则集产生的建议。 为此，可指定要过滤的曲面和方案，并提供回调函数。

无论何时评估规则集，回调函数都会接收一个包含建议数组的`result`对象。

>[!IMPORTANT]
>
>`subscribeRulesetItems`命令是获取来自规则集的建议的唯一方法，因为它们未与[`sendEvent`](sendevent/overview.md)结果一起返回。


```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://example.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```

上述代码订阅了内容卡的`web://example.com/#welcome`表面，并使用`collectEvent`便利方法为所有建议发出`display`事件。

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
| `result` | 对象 | 此对象包含`propositions`数组。  这些建议是令人满意的规则集的直接结果。 `result`对象的结构与使用[子句的](command-responses.md)返回的`sendEvent`结果对象`then`相同。 |
| `collectEvent` | 函数 | 一个方便使用的功能，可用于发送Edge Network事件以跟踪交互、显示和其他事件。 |

### `collectEvent`函数 {#collectevent-function}

`collectEvent`函数是一个方便使用的函数，可用于发送Edge Network事件以跟踪交互、显示和其他事件。 它接受下表中描述的两个参数。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| 事件类型 | 字符串 | 一个字符串，指明要发出的建议事件类型。 支持的事件类型为`display`、`interact`或`dismiss`。 |
| `propositions` | 数组 | 对应于事件的建议数组。 |

## 使用Web SDK标记扩展订阅内容卡

等效于命令响应的Web SDK标记扩展是订阅[**[!UICONTROL Subscribe ruleset items]**](/help/tags/extensions/client/web-sdk/event-types.md#subscribe-ruleset-items)事件的规则。 事件允许您提供所需的架构和界面。

---
title: Web擴充功能的條件型別
description: 瞭解如何為Web屬性中的標籤擴充功能定義條件型別程式庫模組。
exl-id: db504455-858b-4ac8-aa42-de516b0f1d5a
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 65%

---

# Web 扩展的条件类型

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

在規則的內容中，條件會在事件發生後進行評估。 所有条件必须返回 true，规则才会继续处理。例外情況是使用者明確將條件放入「例外」貯體，在這種情況下，貯體中的所有條件都必須傳回false，規則才能繼續處理。

例如，扩展可以提供“视区包含”条件类型， 用户可在其中指定 CSS 选择器。在客户端网站上评估条件时，扩展将能够找到与 CSS 选择器匹配的元素，并返回其中是否有任何元素包含在用户视区中。

本文介紹如何在Adobe Experience Platform中定義Web擴充功能的條件型別。

>[!NOTE]
>
>如果您正在开发 Edge 扩展，请另外参阅关于 [Edge 扩展的条件类型](../edge/condition-types.md)的指南。
>
>本檔案假設您熟悉程式庫模組，以及如何將這些模組整合在Web擴充功能中。 如果您需要查看简介，请在返回本指南之前参阅关于[库模块格式](./format.md)的概述。

條件型別通常包含下列專案：

1. A [檢視](./views.md) 顯示在Experience PlatformUI和資料收集UI中，可讓使用者修改條件的設定。
2. 在標籤執行階段程式庫內發出的程式庫模組，用於解譯設定及評估條件。

條件型別程式庫模組有一個目標：評估某條件是否成立。 具体评估的内容由您来决定。

例如，如果要评估用户是否位于主机 `example.com` 上，则您的模块可能如下所示：

```js
module.exports = function(settings) {
  return document.location.hostname === 'example.com';
};
```

现在，假定您希望可由 Adobe Experience Platform 用户配置主机名。您可以允许用户输入主机名，然后将主机名保存到设置对象。该对象可能如下所示：

```js
{
  "hostname": "example.com"
}
```

要对用户定义的主机名执行操作，您的模块需要更改为：

```js
module.exports = function(settings) {
  return document.location.hostname === settings.hostname;
};
```

## 上下文事件数据

第二个参数将传递到您的模块，其中包含与触发规则的事件相关的上下文信息。该参数在某些情况下可能会有所帮助并且可以按如下方式访问：

```js
module.exports = function(settings, event) {
  // event contains information regarding the event that fired the rule
};
```

`event` 对象必须包含以下属性：

| 属性 | 描述 |
| --- | --- |
| `$type` | 描述扩展名称和事件名称的字符串，使用句点连接。例如，`youtube.play`。 |
| `$rule` | 包含有关当前正在执行的规则的信息的对象。该对象必须包含以下子属性：<ul><li>`id`：当前正在执行的规则的 ID。</li><li>`name`：当前正在执行的规则的名称。</li></ul> |

提供触发规则的事件类型的扩展可以选择性地向此 `event` 对象添加任何其他有用信息。

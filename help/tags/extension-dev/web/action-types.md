---
title: Web擴充功能的動作型別
description: 瞭解如何為Web屬性中的標籤擴充功能定義動作型別程式庫模組。
exl-id: d4539132-a72c-40b0-84b6-50cbe3785d2d
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 50%

---

# Web 扩展的操作类型

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

在資料收集標籤的內容中，動作是在規則事件發生且所有條件都通過評估後執行的動作。

例如，扩展可以提供“显示支持聊天”操作类型，该操作类型可以显示支持聊天对话框，以帮助在注销时可能遇到困难的用户。

本文介紹如何在Adobe Experience Platform中定義Web擴充功能的動作型別。

>[!IMPORTANT]
>
>本文档介绍 Web 扩展的操作类型。如果您正在开发 Edge 扩展，请另外参阅关于 [Edge 扩展的操作类型](../edge/action-types.md)的指南。
>
>本檔案也假設您熟悉程式庫模組，以及如何將這些模組整合在Web擴充功能中。 如果您需要查看简介，请在返回本指南之前参阅关于[库模块格式](./format.md)的概述。

動作型別通常包含下列專案：

1. A [檢視](./views.md) 顯示在Experience PlatformUI和資料收集UI中，可讓使用者修改動作的設定。
2. 在標籤執行階段程式庫內發出的程式庫模組，用於解譯設定及執行動作。

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

例如，若要讓Adobe Experience Platform使用者能夠設定訊息，您可以允許使用者輸入訊息，並將其儲存至設定物件。 物件看起來像這樣：

```json
{
  "message": "Thank you for being one of our VIP members!"
}
```

要对用户定义的消息执行操作，您的模块需要更改为：

```js
module.exports = function(settings) {
  alert(settings.message);
}
```

## 上下文事件数据

接著，系統必須將第二個引數傳遞至模組，該模組包含引發規則之事件的相關內容資訊。 该参数在某些情况下可能会有所帮助并且可以按如下方式访问：

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

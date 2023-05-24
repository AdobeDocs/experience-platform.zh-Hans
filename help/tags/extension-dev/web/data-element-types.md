---
title: Web擴充功能的資料元素型別
description: 瞭解如何為Web屬性中的標籤擴充功能定義資料元素型別程式庫模組。
exl-id: 3aa79322-2237-492f-82ff-0ba4d4902f70
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 60%

---

# Web擴充功能的資料元素型別

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

在資料收集標籤中，資料元素本質上是頁面上資料片段的別名。 此資料可在查詢字串引數、Cookie、DOM元素或其他位置找到。 数据元素可以被规则引用，并充当访问这些数据段的抽象。

資料元素型別由擴充功能提供，可讓使用者設定資料元素，以特定方式存取資料片段。 例如，扩展可以提供“本地存储项”数据元素类型， 用户可在其中指定本地存储项名称。当数据元素被规则引用时，扩展将能够使用用户在配置数据元素时提供的本地存储项名称来查找本地存储项值。

本文介紹如何在Adobe Experience Platform中定義Web擴充功能的資料元素型別。

>[!IMPORTANT]
>
>如果您正在開發邊緣擴充功能，請參閱以下指南： [邊緣擴充功能的資料元素型別](../edge/data-element-types.md) 而非。
>
>本檔案也假設您熟悉程式庫模組，以及如何將這些模組整合在Web擴充功能中。 如果您需要查看简介，请在返回本指南之前参阅关于[库模块格式](./format.md)的概述。

資料元素型別通常包含下列專案：

1. A [檢視](./views.md) 顯示在Experience PlatformUI和資料收集UI中，可讓使用者修改資料元素的設定。
2. 在標籤執行階段程式庫內發出的程式庫模組，用於解譯設定及擷取資料片段。

假设您想要允许用户从名为 `productName` 的本地存储项中检索一段数据。您的模块可能如下所示：

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

如果要讓Adobe Experience Platform使用者能夠設定本機儲存體專案名稱，您可以允許使用者輸入名稱，然後將該名稱儲存至 `settings` 物件。 该对象可能如下所示：

```js
{
  itemName: "campaignId"
}
```

要对用户定义的本地存储项名称执行操作，您的模块需要更改为：

```js
module.exports = function(settings) {
  return localStorage.getItem(settings.itemName);
}
```

## 默认值支持

请注意，用户可以选择为任何数据元素配置默认值。如果您的数据元素库模块返回值 `undefined` 或 `null`，则它将被自动替换为用户为数据元素配置的默认值。

## 上下文事件数据

如果因为触发了规则而导致检索数据元素（例如数据元素在规则的条件和操作中使用），则会将第二个参数传递给您的模块，其中包含有关触发规则的事件的上下文信息。该参数在某些情况下可能会有所帮助并且可以按如下方式访问：

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

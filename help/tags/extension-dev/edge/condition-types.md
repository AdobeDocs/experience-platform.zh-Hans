---
title: 邊緣擴充功能的條件型別
description: 瞭解如何在Adobe Experience Platform中定義邊緣擴充功能的條件型別程式庫模組。
exl-id: fe13420e-ffa7-49d6-92c4-965ebd9d7390
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 50%

---

# Edge 扩展的条件类型

>[!NOTE]
>
> Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

在標籤規則中，會在事件發生後評估條件。 所有条件必须返回 true，规则才会继续处理。條件型別由擴充功能提供，會評估某條件是否成立，傳回布林值。

例如，扩展可以提供“视区包含”条件类型， 用户可在其中指定 CSS 选择器。在客户端网站上评估条件时，扩展将能够找到与 CSS 选择器匹配的元素，并返回其中是否有任何元素包含在用户视区中。

本文介紹如何在Adobe Experience Platform中定義邊緣擴充功能的條件型別。

>[!IMPORTANT]
>
>如果您正在开发 Web 扩展，请另外参阅关于 [Web 扩展的条件类型](../web/condition-types.md)的指南。
>
>本檔案也假設您熟悉程式庫模組，以及如何將這些模組整合在Edge擴充功能中。 如果您需要查看简介，请在返回本指南之前参阅关于[库模块格式](./format.md)的概述。

條件型別通常包含下列專案：

1. Experience PlatformUI和資料收集UI中顯示的檢視，可讓使用者修改條件的設定。
2. 在標籤執行階段程式庫內發出的程式庫模組，用於解譯設定及評估條件。

例如，如果您想要評估使用者是否在主機上 `example.com`，您的模組可能如下所示。

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith("adobelaunch.com");
};
```

如果您想要讓使用者能夠設定主機名稱，以允許輸入主機名稱並將其儲存到設定物件，該物件看起來可能類似於此範例。

```js
{
  "hostname": "example.com"
}
```

要对用户定义的主机名执行操作，您的模块需要更改为：

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith(settings.hostname);
};
```

## 条件结果

条件模块返回的结果可以是如下内容之一：

1. 布尔值（`true` 或 `false`）。
1. 解析后返回布尔值的 [promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)。

## 库模块上下文

所有条件模块都可以访问在调用模块时提供的 `context` 变量。您可以在[此处](./context.md)了解更多信息。

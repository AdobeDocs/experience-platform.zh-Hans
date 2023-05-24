---
title: 邊緣擴充功能的動作型別
description: 瞭解如何為Edge屬性中的標籤擴充功能定義動作型別程式庫模組。
exl-id: c0b058aa-f0fe-4fd8-a873-018482c3e4db
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 42%

---

# Edge 扩展的操作类型

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

在標籤規則中，動作是在規則條件通過評估後所執行的動作。 動作型別由擴充功能提供，其效果完全由擴充功能作者定義。

例如，扩展可以提供“显示支持聊天”操作类型，该操作类型可以显示支持聊天对话框，以帮助在注销时可能遇到困难的用户。

本文介紹如何在Adobe Experience Platform中定義Edge擴充功能的動作型別。

>[!IMPORTANT]
>
>如果您正在开发 Web 扩展，请另外参阅关于 [Web 扩展的操作类型](../web/action-types.md)的指南。
>
>本檔案也假設您熟悉程式庫模組，以及如何將這些模組整合在Edge擴充功能中。 如果您需要查看简介，请在返回本指南之前参阅关于[库模块格式](./format.md)的概述。

動作型別通常包含下列專案：

1. Experience PlatformUI和資料收集UI中顯示的檢視，可讓使用者修改動作的設定。
2. 在標籤執行階段程式庫內發出的程式庫模組，用於解譯設定及執行動作。

例如，將部分資料轉送至協力廠商端點的模組可能如下所示。

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  return fetch('http://someendpoint.com', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

如果您想要讓使用者能夠設定端點，並允許端點輸入和持續存在模組內的設定物件，則物件看起來會像這樣。

```json
{
  "endpoint": "http://someendpoint.com"
}
```

若要運用於使用者定義的端點，您的模組必須變更至以下範例。

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  const  { endpoint } = settings;
  return fetch(endpoint, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

## 操作结果

操作模块返回的结果可以是任何内容。如果该操作需要执行异步任务，您可以返回一个 [promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)，该 promise 在得到解析后会返回您所需的结果。

操作结果存储在 `ruleStash` 键中，所有模块均可通过 `context` 参数 (`context.arc.ruleStash`) 使用该键。您可以在[此处](./context.md#rulestash)了解关于 `ruleStash` 的更多信息。

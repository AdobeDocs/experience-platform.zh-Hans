---
title: 处理命令响应
description: 使用JavaScript承诺处理来自命令的响应。
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: 8abdd206f5fcff0e1cec7bb6ecd25c5eb9354286
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 处理命令响应

某些Web SDK命令可能会返回包含对您的组织潜在有用的数据的对象。 如果需要，您可以选择如何处理这些数据。 命令响应对于建议和目标非常有用，因为它们需要Edge Network数据才能有效工作。

命令响应使用JavaScript [promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)，充当创建promise时未知的值的代理。 知道该值后，将使用值“解析”promise。

使用`then`和`catch`方法确定命令成功或失败的时间。 您可以忽略`then`或`catch`（如果它们的目的对您的实施不重要）。

```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    console.log("The sendEvent command succeeded.");
  })
  .catch(function(error) {
    console.log("The sendEvent command failed.");
  });
```

从命令返回的所有承诺都使用`result`对象。 例如，您可以使用`result`命令从[`getLibraryInfo`](getlibraryinfo.md)对象获取库信息：

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

此`result`对象的内容取决于您使用的命令和用户同意的组合。 如果用户没有针对特定目的给予同意，则响应对象仅包含可以在用户同意的内容上下文中提供的信息。

## 使用Web SDK标记扩展程序的命令响应

等效于命令响应的Web SDK标记扩展是订阅[**[!UICONTROL Send event complete]**](/help/tags/extensions/client/web-sdk/event-types.md#send-event-complete)事件的规则。 然后，您可以将诸如[**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md)或[**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md)之类的操作包含到此规则中。

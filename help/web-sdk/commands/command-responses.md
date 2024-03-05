---
title: 处理命令响应
description: 使用JavaScript承诺处理来自命令的响应。
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# 处理命令响应

某些Web SDK命令可以返回包含对您的组织潜在有用的数据的对象。 如果需要，您可以选择如何处理这些数据。 命令响应对于建议和目标非常有用，因为它们需要Edge Network数据才能有效工作。

命令响应使用JavaScript [承诺](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)，充当创建promise时未知的值的代理。 知道该值后，将使用值“解析”promise。

## 使用Web SDK标记扩展处理命令响应

创建订阅 **[!UICONTROL 发送事件完成]** 事件。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 规则]**，然后选择所需的规则。
1. 下 [!UICONTROL 活动]，选择现有事件或创建事件。
1. 设置 [!UICONTROL 扩展名] 下拉字段至 **[!UICONTROL Adobe Experience Platform Web SDK]**，并设置 [!UICONTROL 事件类型] 到 **[!UICONTROL 发送事件完成]**.
1. 单击 **[!UICONTROL 保留更改]**，然后运行发布工作流程。

然后，您可以包含操作 **[!UICONTROL 应用建议]** 或 **[!UICONTROL 应用响应]** 到这个规则里。

1. 查看以上创建或编辑的规则时，选择现有操作或创建操作。
1. 设置 [!UICONTROL 扩展名] 下拉字段至 **[!UICONTROL Adobe Experience Platform Web SDK]**，并设置 [!UICONTROL 操作类型] 到 **[!UICONTROL 应用建议]** 或 **[!UICONTROL 应用响应]**，具体取决于所需的行为。
1. 设置操作的所需字段，然后单击 **[!UICONTROL 保留更改]**.

## 使用Web SDK JavaScript库处理命令响应

使用 `then` 和 `catch` 用于确定命令何时成功或失败的方法。 您可以忽略以下任一项 `then` 或 `catch` 如果它们的目的对您的实施不重要。

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

从命令返回的所有承诺都使用 `result` 对象。 例如，您可以从以下位置获取库信息 `result` 对象使用 [`getLibraryInfo`](getlibraryinfo.md) 命令：

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

此的内容 `result` 对象取决于您使用的命令和用户同意的组合。 如果用户没有针对特定目的给予同意，则响应对象仅包含可以在用户同意的内容上下文中提供的信息。

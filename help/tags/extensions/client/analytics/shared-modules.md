---
title: Adobe Analytics 扩展的共享模块
description: 了解由Adobe Experience Platform中的Adobe Analytics标记扩展提供的共享库模块。
exl-id: f1d7cb2b-0058-46f9-983c-079079e06057
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 70%

---

# Adobe Analytics 扩展的共享模块

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。 有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

[Adobe Analytics 扩展](./overview.md)提供两个不同的[共享模块](../../../extension-dev/web/shared.md)，您可以将这两个模块集成到体验应用程序中。以下各部分将对这些模块进行介绍。

## [!DNL get-tracker]

Adobe Analytics 在发送任何信标之前，必须先初始化跟踪器对象。初始化过程首先需加载 [AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=zh-Hans)，然后创建跟踪器对象。

在使用 `get-tracker` 共享模块完全初始化跟踪器对象后，您才有权访问该对象，如下所示：

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

getTracker().then(function(tracker) {
  // Use tracker in some way
});
```

### 验证是否已安装 Adobe Analytics

Adobe Analytics可能尚未安装或包含在与您的扩展相同的标记库中。 因此，强烈建议您在代码中检查有无这种情况，并做出相应处理。以下的 JavaScript 是实施此功能的方法示例：

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

if (getTracker) {
  getTracker().then(function(tracker) {
    // Use tracker in some way
  });
} else {
  turbine.logger.error("The Adobe Analytics extension is required for Extension XYZ to function properly.");
}
```

如果`getTracker`为`undefined`，则标记库中不存在Adobe Analytics扩展。 您可以自定义已记录的消息，以便准确反映未安装 Adobe Analytics 时可能丢失的功能。


## [!DNL augment-tracker]

初始化跟踪器对象后，流程中的下一步是增强。在从Adobe Analytics扩展配置应用任何变量之前，或者在发送任何信标之前，此步骤允许您的扩展使用任何必要的内容来增强跟踪器。

此外，当扩展执行其自身的任何异步任务（如从服务器中获取数据或 JavaScript）时，则有机会暂停跟踪器初始化过程。

您可以实施 `augment-tracker` 模块，如下所示：

```js
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  // Augment tracker in some way
});
```

一旦达到跟踪器初始化过程的增强阶段，将立即调用传递到 `augmentTracker()` 的函数。

如果您的扩展需要在增强跟踪器之前完成异步任务，您可以从函数中返回一个 promise，如下所示：

```js
var Promise = require('@adobe/reactor-promise');
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  return new Promise(function(resolve) {
    // Augment the tracker object, then call resolve()
  });
});
```

通过返回 promise，您的扩展将向 Adobe Analytics 发出信号，提示它应暂停跟踪器初始化过程，直到 promise 得以解决。

>[!WARNING]
>
>在暂停跟踪器初始化过程中，请务必保持谨慎，因为它可能会延迟发送信标，从而导致无法收集数据（例如，如果用户在信标发送前从页面导航离开）。

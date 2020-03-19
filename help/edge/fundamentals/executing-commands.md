---
title: 执行命令
seo-title: 执行Adobe Experience Platform Web SDK命令
description: 了解如何执行Experience Platform Web SDK命令
seo-description: 了解如何执行Experience Platform Web SDK命令
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# （测试版）执行命令

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生更改。

在您的网页上实现基本代码后，您可以开始使用SDK执行命令。 执行命令之前，您无需等待外部文件\(`alloy.js`\)从服务器加载。 如果SDK尚未完成加载，则命令将尽快排队并由SDK进行处理。

使用以下语法执行命令。

```javascript
alloy("commandName", options);
```

它 `commandName` 告诉SDK要做什么，而 `options` 您要传递到命令的参数和数据。 由于可用选项取决于命令，请查阅文档以了解有关每个命令的更多详细信息。

## 承诺的注意事项

[承诺](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) ，是SDK如何与网页上的代码通信的基础。 承诺是一种常见的编程结构，并非特定于此SDK甚至JavaScript。 承诺充当创建承诺时未知的值的代理。 一旦确定了该值，承诺即与该值“已解析”。 处理函数可以与承诺相关联，以便在承诺已解析时或在承诺解析过程中出现错误时可以通知您。 要进一步了解承诺，请阅 [读本教程](https://javascript.info/promise-basics) ，或Web上的任何其他资源。

## 处理成功或失败

每次执行命令时，都会返回承诺。 这一承诺是指最终完成指挥。 在以下示例中，您可以使用 `then` 和方 `catch` 法确定命令何时成功或失败。

```javascript
alloy("commandName", options)
  .then(function(value) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

如果知道命令何时成功对您来说并不重要，您可以删除调 `then` 用。

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

同样，如果知道命令何时失败对您来说并不重要，您也可以删除调 `catch` 用。

```javascript
alloy("commandName", options)
  .then(function(value) {
    // The command succeeded.
    // "value" will be whatever the command returned
  })
```

## 隐藏错误

如果承诺被拒绝且您尚未添加调用，则无论Adobe Experience Platform Web SDK中是否启用了日志记录，错误“冒泡”并记录在浏览器的开发人员控制台中。 `catch` 如果您担心此问题，可将配置选 `suppressErrors` 项设置为 `true` 如配置 [SDK中所述](configuring-the-sdk.md)。

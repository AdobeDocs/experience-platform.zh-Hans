---
title: 执行Adobe Experience Platform Web SDK命令
description: 了解如何执行Experience PlatformWeb SDK命令
keywords: 执行命令；commandName；Promise；getLibraryInfo；响应对象；同意；
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: ffc60e83285188bc5b0f6eb7a20fafee16d51d4d
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 执行命令


在网页上实施基础代码后，您可以开始使用SDK执行命令。 您无需等待外部文件(`alloy.js`)，以便在执行命令之前从服务器加载。 如果SDK尚未完成加载，SDK会尽快将命令排入队列并进行处理。

命令使用以下语法执行。

```javascript
alloy("commandName", options);
```

此 `commandName` 告诉SDK要执行的操作，同时 `options` 是要传递到命令中的参数和数据。 由于可用选项取决于命令，因此有关每个命令的更多详细信息，请参阅文档。

## 关于承诺的说明

[承诺](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对于SDK如何与网页上的代码进行通信至关重要。 promise是一种常见的编程结构，并非特定于此SDK甚至JavaScript。 promise充当创建promise时未知的值的代理。 知道该值后，将使用值“解析”promise。 可以将处理程序函数与承诺关联，以便在解决承诺时或解决承诺过程中发生错误时通知您。 要了解有关承诺的更多信息，请阅读 [本教程](https://javascript.info/promise-basics) 或Web上的任何其他资源。

## 处理成功或失败 {#handling-success-or-failure}

每次执行命令时，都会返回promise。 承诺表示命令的最终完成。 在下面的示例中，您可以使用 `then` 和 `catch` 用于确定命令何时成功或失败的方法。

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "result" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

如果知道命令何时成功对您来说并不重要，则可以删除 `then` 呼叫。

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

同样，如果知道命令何时失败对您来说并不重要，则可以删除 `catch` 呼叫。

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### 响应对象

从命令返回的所有承诺都使用 `result` 对象。 结果对象将包含数据，具体取决于命令和用户的同意。 例如，在下列命令中，库信息作为结果对象的属性传递。

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

### 同意

如果用户没有针对特定目的给出其同意，则承诺仍将被解析；但是，响应对象将仅包含可以在用户同意的内容上下文中提供的信息。

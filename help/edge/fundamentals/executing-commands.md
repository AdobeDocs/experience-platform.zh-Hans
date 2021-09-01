---
title: 执行Adobe Experience Platform Web SDK命令
description: 了解如何执行Experience PlatformWeb SDK命令
keywords: 执行命令；commandName;Promise;getLibraryInfo；响应对象；同意；
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: ca3ee230d510dfb9de400b6f573a612ec33c8f7a
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 2%

---

# 执行命令


在您的网页上实施基础代码后，您可以使用SDK开始执行命令。 执行命令之前，您无需等待从服务器加载外部文件(`alloy.js`)。 如果SDK尚未完成加载，则SDK会尽快排入队列并处理命令。

使用以下语法执行命令。

```javascript
alloy("commandName", options);
```

`commandName`告知SDK要执行的操作，而`options`是要传递到命令的参数和数据。 由于可用选项取决于命令，请查阅文档以了解有关每个命令的更多详细信息。

## 关于承诺的说明

[](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 承诺是SDK如何与您网页上的代码通信的基础。promise是一种常见的编程结构，并非特定于此SDK甚至JavaScript。 promise用作创建promise时未知值的代理。 一旦该值已知，promise将通过该值“解析”。 处理程序函数可以与promise关联，以便在promise已解析或在解析promise过程中出错时向您发送通知。 要了解有关promise的更多信息，请阅读[本教程](https://javascript.info/promise-basics)或Web上的任何其他资源。

## 处理成功或失败 {#handling-success-or-failure}

每次执行命令时，都会返回一个promise。 promise表示命令的最终完成。 在以下示例中，可以使用`then`和`catch`方法来确定命令何时成功或失败。

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

如果知道命令何时成功对您不重要，则可以删除`then`调用。

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

同样，如果知道命令何时失败对您来说并不重要，则可以删除`catch`调用。

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### 响应对象

从命令返回的所有promise都使用`result`对象进行解析。 结果对象将包含数据，具体取决于命令和用户的同意。 例如，库信息将作为以下命令中结果对象的属性传递。

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
  });
```

### 同意

如果用户未针对特定目的给予同意，则承诺仍将得到解决；但是，响应对象将仅包含可在用户同意的上下文中提供的信息。

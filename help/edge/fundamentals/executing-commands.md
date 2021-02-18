---
title: 执行Adobe Experience Platform Web SDK命令
description: 了解如何执行Experience Platform Web SDK命令
keywords: 执行命令；commandName;Promies;getLibraryInfo；响应对象；同意；
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 2%

---


# 执行命令

在您的网页上实现基本代码后，您可以开始使用SDK执行命令。 执行命令之前，您无需等待从服务器加载外部文件(alloy.js)。 如果SDK尚未完成加载，则命令将尽快排队并由SDK进行处理。

使用以下语法执行命令。

```javascript
alloy("commandName", options);
```

`commandName`告诉SDK要做什么，而`options`是要传递到命令的参数和数据。 由于可用选项取决于命令，请查阅文档以了解有关每个命令的详细信息。

## 关于承诺的便条

[承](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 诺是SDK如何与您网页上的代码通信的基础。承诺是一种常见的编程结构，并非特定于此SDK甚至JavaScript。 承诺充当创建承诺时未知的值的代理。 一旦知道该值，承诺就与该值“解析”。 处理函数可以与承诺关联，以便当承诺已解析或在解决承诺过程中出现错误时可以通知您。 要进一步了解承诺，请阅读[本教程](https://javascript.info/promise-basics)或Web上的任何其他资源。

## 处理成功或失败{#handling-success-or-failure}

每次执行命令时，都会返回承诺。 承诺是指最终完成指挥。 在以下示例中，可以使用`then`和`catch`方法确定命令何时成功或失败。

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

如果知道命令何时成功对您不重要，您可以删除`then`调用。

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

同样，如果知道命令何时失败对您来说并不重要，您可以删除`catch`调用。

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### 响应对象

从命令返回的所有承诺都由`result`对象解析。 结果对象将根据命令和用户同意包含数据。 例如，库信息将作为结果对象的属性在以下命令中传递。

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(results.libraryInfo.version);
  });
```

### 同意

如果用户未出于特定目的同意，承诺仍将得到解决；但是，响应对象将仅包含可在用户同意的上下文中提供的信息。

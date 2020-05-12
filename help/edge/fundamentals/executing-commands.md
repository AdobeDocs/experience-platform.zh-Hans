---
title: 执行命令
seo-title: 执行Adobe Experience Platform Web SDK命令
description: 了解如何执行Experience Platform Web SDK命令
seo-description: 了解如何执行Experience Platform Web SDK命令
translation-type: tm+mt
source-git-commit: 9bd6feb767e39911097bbe15eb2c370d61d9842a
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---


# （测试版）执行命令

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生变化。

在您的网页上实现基本代码后，您可以开始使用SDK执行命令。 您无需等待外部文件\(`alloy.js`\)从服务器加载，即可执行命令。 如果SDK尚未完成加载，SDK会尽快排队并处理命令。

使用以下语法执行命令。

```javascript
alloy("commandName", options);
```

它 `commandName` 告诉SDK要做什么，而 `options` 您要将参数和数据传递给命令。 由于可用选项取决于命令，请查阅文档以了解有关每个命令的更多详细信息。

## 承诺的便条

[承诺](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 是SDK如何与您网页上的代码通信的基础。 承诺是一种通用的编程结构，并非特定于此SDK甚至JavaScript。 承诺充当创建承诺时未知的值的代理。 一旦知道该值，承诺即与该值“解析”。 处理函数可以与承诺相关联，以便在承诺已解析或在解决承诺过程中出错时向您发送通知。 要进一步了解承诺，请阅 [读本教程](https://javascript.info/promise-basics) ，或Web上的任何其他资源。

## 处理成功或失败

每次执行命令时，都会返回承诺。 这一承诺代表了指挥最终完成。 在以下示例中，您可以使用 `then` 和方 `catch` 法确定命令何时成功或失败。

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

如果知道命令何时成功对您不重要，您可以删除调 `then` 用。

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

同样，如果知道命令何时失败对您不重要，您也可以删除调 `catch` 用。

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  })
```

### 响应对象

从命令返回的所有承诺都用一个对象 `result` 解析。 结果对象将根据命令和用户同意包含数据。 例如，库信息将作为结果对象的属性在以下命令中传递。

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(results.libraryInfo.version);
});
```

### 同意

如果用户未就特定目的给予同意，承诺仍将解决； 但是，响应对象将仅包含可在用户同意的上下文中提供的信息。

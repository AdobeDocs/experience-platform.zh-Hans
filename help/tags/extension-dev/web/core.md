---
title: Web扩展的核心库模块
description: 了解可以在Web扩展中使用的核心库模块。
exl-id: 7fb63208-aed0-4add-b6da-8e4aea063d0a
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 83%

---

# Web扩展的核心库模块

本文档提供了可在Web扩展中使用的核心库模块的列表。 您可以使用 `require('@adobe/{MODULE}')` 访问这些模块，其中 `{MODULE}` 是要使用的核心模块的名称。

## [!DNL reactor-object-assign]

`reactor-object-assign` 通过将属性从源对象复制到目标对象来模拟本机 [`Object.assign`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) 方法。

```javascript
var objectAssign = require('@adobe/reactor-object-assign');
var all = objectAssign({ a: 'a' }, { b: 'b' });
```

## [!DNL reactor-cookie]

`reactor-cookie` 对象是用于读取和写入 Cookie 的实用程序。有关更多信息，请参阅 [js-cookie npm 包](https://www.npmjs.com/package/js-cookie)。

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
console.log(cookie.get('foo'));
cookie.remove('foo');
```

### [!DNL reactor-document]

`reactor-document` 表示 [`Document`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document) 对象。当通过允许测试使用 [`inject-loader`](https://www.npmjs.com/package/inject-loader) 之类的实用程序注入模拟 `document` 对象来测试模块时，这会很有用。

```javascript
var document = require('@adobe/reactor-document');
console.log(document.location);
```

### [!DNL reactor-query-string]

`reactor-query-string` 是用于解析和序列化[查询字符串](https://developer.mozilla.org/en-US/docs/Web/API/HTMLHyperlinkElementUtils/search)的实用程序。

```javascript
var queryString = require('@adobe/reactor-query-string');
var parsed = queryString.parse(location.search);
console.log(parsed.campaign);
var obj = {
  campaign: 'Campaign A'
};
var stringified = queryString.stringify(obj);
```

该实用程序具有以下方法：

* `queryString.parse({STRING})`：将查询字符串解析为对象。查询字符串中的前导 `?`、`#` 和 `&` 字符将被忽略。
* `queryString.stringify({OBJECT})`：将对象字符串化为查询字符串。

### [!DNL reactor-load-script]

`reactor-load-script` 是一个在给定 URL 时加载脚本的函数。系统将创建一个脚本标记并将其放置在文档的 `head` 节点中。系统将返回一个 [promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)，您可以使用它来确定脚本加载的成功时间或失败时间。

```javascript
var loadScript = require('@adobe/reactor-load-script');
var url = 'http://code.jquery.com/jquery-3.1.1.js';
loadScript(url).then(function() {
  // Do something ...
})
```

### [!DNL reactor-promise]

`reactor-promise` 是一个模拟 ECMAScript 6 中本机 [Promise API](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 的构造函数。如果本机 Promise API 可用，则将返回该 API。

```javascript
var Promise = require('@adobe/reactor-promise');
new Promise(function(resolve) {
  resolve();
}, function(err) {
  console.error(err);
});
```

### [!DNL reactor-window]

`reactor-window` 表示 [`Window`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window) 对象。当通过允许测试使用 [`inject-loader`](https://www.npmjs.com/package/inject-loader) 之类的实用程序注入模拟 `Window` 对象来测试模块时，这会很有用。

```javascript
var window = require('@adobe/reactor-window');
console.log(window.document);
```

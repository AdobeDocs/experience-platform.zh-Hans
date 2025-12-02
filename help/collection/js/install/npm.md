---
title: 使用NPM包安装Web SDK
description: 使用NPM包来安装和引用Web SDK库。
exl-id: 4c70ec5d-33fd-4ef7-ba9e-5b92ff6c3e86
source-git-commit: b1574940b3afbd98cd60a079fdf7b10153e8e9d7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 使用NPM包安装Web SDK

Adobe Experience Platform Web SDK以[NPM包](https://www.npmjs.com)的形式提供。 通过安装NPM包，您可以控制Adobe Experience Platform Web SDK JavaScript库的构建过程。 NPM包会公开要在浏览器中运行的EcmaScript版本5模块或EcmaScript版本2015 (ES6)模块。

```bash
npm install @adobe/alloy
```

Adobe Experience Platform Web SDK的NPM包会公开`createInstance`函数。 传递到函数的name选项可控制日志记录中使用的前缀。 以下是使用该包的示例。

## 将软件包用作ECMAScript 2015 (ES6)模块

```js
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("configure", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>NPM包依赖于CommonJS模块；因此，在使用捆绑包时，请确保该捆绑包支持CommonJS模块。 某些捆绑包（如[Rollup](https://rollupjs.org)）需要提供CommonJS支持的[插件](https://www.npmjs.com/package/@rollup/plugin-commonjs)。

## 将软件包用作ECMAScript 5模块

```js
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("configure", { ... });
alloy("sendEvent", { ... });
```

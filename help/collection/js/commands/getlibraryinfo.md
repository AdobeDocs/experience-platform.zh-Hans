---
title: getLibraryInfo
description: 检索有关当前Web SDK库版本的信息。
exl-id: f2bc0185-71c9-4d77-b9d2-b777a41a20e5
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# `getLibraryInfo`

`getLibraryInfo`命令为您提供有关当前使用的Web SDK库版本的信息。 您可以使用此命令跟踪您部署到其他Web资产的Web SDK版本。

调用Web SDK的配置实例时运行`getLibraryInfo`命令。 此命令通常与JavaScript promise配对，用于检索它填充的对象。

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## 响应对象

如果您决定使用此命令[处理响应](command-responses.md)，则响应对象中提供了以下属性：

* **`libraryInfo.commands`**：此版本的Web SDK支持的命令数组。
* **`libraryInfo.configs`**：此版本的Web SDK支持的配置设置数组。
* **`libraryInfo.version`**： Web SDK库的版本。

## 使用Web SDK标记扩展的“库信息”

标记扩展不提供用于发送此命令的接口。 请按照JavaScript库语法使用自定义代码编辑器。

如果使用标记扩展运行此命令，则标记扩展版本和库版本都会包含在内，并以`+`符号连接。 首先列出Web SDK库版本，然后是标记扩展版本。

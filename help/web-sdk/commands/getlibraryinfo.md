---
title: getLibraryInfo
description: 检索有关当前Web SDK库版本的信息。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# `getLibraryInfo`

此 `getLibraryInfo` 命令为您提供有关当前使用的Web SDK库版本的信息。 您可以使用此命令跟踪您部署到不同Web属性的Web SDK版本。

## 使用Web SDK标记扩展的“库信息”

标记扩展不提供用于发送此命令的接口。 按照JavaScript库语法使用自定义代码编辑器。

如果使用标记扩展运行此命令，则会同时包含标记扩展版本和库版本，并以 `+` 符号。 首先列出Web SDK库版本，然后是标记扩展版本。

## 使用Web SDK JavaScript库的库信息

运行 `getLibraryInfo` 命令。 此命令通常与JavaScript promise配对，后者允许您检索它所填充的对象。

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## 响应对象

如果您决定 [处理响应](command-responses.md) 使用此命令，响应对象中提供了以下属性：

* **`libraryInfo.commands`**：此版本的Web SDK支持的命令数组。
* **`libraryInfo.configs`**：此版本的Web SDK支持的一系列配置设置。
* **`libraryInfo.version`**：Web SDK库的版本。

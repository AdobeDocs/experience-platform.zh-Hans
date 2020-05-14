---
title: 检索库信息
seo-title: 使用Adobe Experience Platform Web SDK检索库信息
description: 了解如何检索有关加载到网站上的库的信息
seo-description: 了解如何通过Adobe Experience Cloud SDK自动收集加载到网站上的库的相关信息
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# 检索库信息

访问加载到网站的库后的一些详细信息通常很有帮助。 要执行此操作，请按 `getLibraryInfo` 如下方式执行命令：

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

当前，提供的 `libraryInfo` 对象包含以下属性：

* `version` 这是加载库的版本。 例如，如果要加载的库版本为1.0.0，则该值将为 `1.0.0`。
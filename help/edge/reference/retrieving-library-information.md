---
title: 检索库信息
seo-title: 使用Adobe Experience Platform Web SDK检索库信息
description: 了解如何检索加载到网站上的库的相关信息
seo-description: 了解如何通过Adobe Experience Cloud SDK自动收集加载到网站上的库的相关信息
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# （测试版）检索库信息

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生更改。

访问加载到您网站的库后的某些详细信息通常很有帮助。 要执行此操作，请按如 `getLibraryInfo` 下方式执行命令：

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

当前，提供的对 `libraryInfo` 象包含以下属性：

* `version` 这是加载库的版本。 例如，如果加载的库版本为1.0.0，则值将为 `1.0.0`。
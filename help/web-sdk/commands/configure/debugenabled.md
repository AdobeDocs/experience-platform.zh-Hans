---
title: debugEnabled
description: 使用代码启用Web SDK中的调试功能。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

此 `debugEnabled` 属性允许您启用或禁用使用Web SDK代码进行调试。 这是启用的可用方法之一 [调试](../../use-cases/debugging.md). 在网站开发期间，当您始终希望启用调试时，在实施中启用调试会比其他方法更方便。 由于此调试方法适用于所有访客，因此不建议在生产页面中使用该方法。

请参阅 [调试](../../use-cases/debugging.md) 用例页面，以了解更多启用调试的方法。

## 使用Web SDK标记扩展启用调试

使用Web SDK标记扩展在本地没有可用的调试选项。 使用 [替代调试方法](../../use-cases/debugging.md).

## 使用Web SDK JavaScript库启用调试

设置 `debugEnabled` 布尔到 `true` 运行 `configure` 命令。 如果在配置SDK时省略此属性，则默认使用 `false`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

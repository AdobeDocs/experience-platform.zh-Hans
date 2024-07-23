---
title: debugEnabled
description: 使用代码启用Web SDK中的调试功能。
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

`debugEnabled`属性允许您启用或禁用使用Web SDK代码进行调试。 它是启用[调试](../../use-cases/debugging.md)的可用方法之一。 在网站开发期间，当您始终希望启用调试时，在实施中启用调试会比其他方法更方便。 由于此调试方法适用于所有访客，因此不建议在生产页面中使用该方法。

有关启用调试的更多方法，请参阅[调试](../../use-cases/debugging.md)用例页。

## 使用Web SDK标记扩展启用调试

使用Web SDK标记扩展在本地没有可用的调试选项。 使用[备用调试方法](../../use-cases/debugging.md)。

## 使用Web SDK JavaScript库启用调试

运行`configure`命令时，将`debugEnabled`布尔值设置为`true`。 如果在配置SDK时省略此属性，则默认设置为`false`。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```

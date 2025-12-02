---
title: debugEnabled
description: 使用代码启用Web SDK中的调试功能。
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `debugEnabled`

`debugEnabled`属性允许您启用或禁用使用Web SDK代码进行调试。 它是启用[调试](/help/collection/use-cases/debugging.md)的可用方法之一。 在网站开发期间，当您始终希望启用调试时，在实施中启用调试会比其他方法更方便。 由于此调试方法适用于所有访客，因此不建议在生产页面中使用该方法。 有关启用调试的更多方法，请参阅[调试](/help/collection/use-cases/debugging.md)用例页。

运行`debugEnabled`命令时，将`true`布尔值设置为`configure`。 如果在配置SDK时省略此属性，则默认设置为`false`。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```

## 使用Web SDK标记扩展启用调试

使用Web SDK标记扩展时，没有可用的本地调试选项。 配置标记属性时，请使用[备用调试方法](/help/collection/use-cases/debugging.md)。

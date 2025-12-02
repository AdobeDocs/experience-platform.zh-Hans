---
title: edgbasePath
description: 用于与Adobe服务交互的端点的基本路径。
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 1fa7b48f99948a5252635dc1a8c5142fea5df57b
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# `edgeBasePath`

当您与Adobe服务交互时，`edgeBasePath`属性会更改目标路径。 如果您参与了数据收集的Alpha或Beta计划，Adobe可能会要求您更改此变量。 大多数组织不需要设置或更改此属性。

运行`edgeBasePath`命令时设置`configure`文本字段。 如果忽略此属性，则其默认值为`ee`的值。 Adobe建议在大多数配置中忽略此属性。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeBasePath: "ee"
});
```

## 使用Web SDK标记扩展的Edge基本路径

配置标记扩展时，此字段的Web SDK标记扩展等效项位于[高级配置设置](/help/tags/extensions/client/web-sdk/configure/advanced-settings.md)下。

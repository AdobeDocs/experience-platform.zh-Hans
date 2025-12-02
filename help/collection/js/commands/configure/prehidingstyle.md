---
title: 预隐藏样式
description: 创建一个CSS定义，以允许加载个性化内容而不会出现闪烁。
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# `prehidingStyle`

`prehidingStyle`属性允许您定义CSS选择器以隐藏个性化内容，直到加载为止。 此属性在同步Web SDK实施中非常有用，可避免闪烁。 Adobe建议对异步Web SDK实施使用[预隐藏代码片段](/help/collection/use-cases/personalization/manage-flicker.md)。

在页面上运行第一个[`sendEvent`](../sendevent/overview.md)命令时，您在此属性中定义的CSS选择器会开始隐藏内容。 在收到来自Adobe的响应时，内容会取消隐藏，这通常包括个性化内容。 如果`sendEvent`命令失败或超时，内容也会取消隐藏。

如果在实施中同时包含`prehidingStyle`和预隐藏代码片段，则预隐藏代码片段的优先级将高于此配置属性。

运行`prehidingStyle`命令时设置`configure`字符串。 如果在配置Web SDK时省略此属性，则在页面上运行第一个`sendEvent`命令时不会隐藏任何内容。 将此值设置为同步加载的库所需的CSS选择器和声明块。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```

## 使用Web SDK标记扩展预隐藏样式

可以使用[Personalization配置设置](/help/tags/extensions/client/web-sdk/configure/personalization.md)在Web SDK标记扩展中配置这些设置。

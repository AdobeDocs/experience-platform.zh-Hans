---
title: 预隐藏样式
description: 创建一个CSS定义，以允许加载个性化内容而不会出现闪烁。
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

`prehidingStyle`属性允许您定义CSS选择器以隐藏个性化内容，直到加载为止。 此属性在同步Web SDK实施中非常有用，可避免闪烁。 Adobe建议对异步Web SDK实现使用[预隐藏代码片段](../../personalization/manage-flicker.md)。

在页面上运行第一个[`sendEvent`](../sendevent/overview.md)命令时，您在此属性中定义的CSS选择器会开始隐藏内容。 当收到来自Adobe的响应时（通常包括个性化内容），内容不会隐藏。 如果`sendEvent`命令失败或超时，内容也会取消隐藏。

如果在实施中同时包含`prehidingStyle`和预隐藏代码片段，则预隐藏代码片段的优先级将高于此配置属性。

## 使用Web SDK标记扩展的预隐藏样式

在[配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)时，选择&#x200B;**[!UICONTROL 提供预隐藏样式]**&#x200B;按钮。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 扩展]**，然后单击[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 配置]**。
1. 向下滚动到[!UICONTROL Personalization]部分，然后选择按钮&#x200B;**[!UICONTROL 提供预隐藏样式]**。
1. 此按钮将打开一个带有CSS编辑器的模式窗口。 插入所需的CSS选择器和声明块，然后单击&#x200B;**[!UICONTROL 保存]**&#x200B;以关闭模式窗口。
1. 单击扩展设置下的&#x200B;**[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库预隐藏样式

运行`configure`命令时设置`prehidingStyle`字符串。 如果在配置Web SDK时省略此属性，则在页面上运行第一个`sendEvent`命令时不会隐藏任何内容。 将此值设置为同步加载的库所需的CSS选择器和声明块。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "prehidingStyle": "#container { opacity: 0 !important }"
});
```

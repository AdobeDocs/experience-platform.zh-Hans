---
title: 预隐藏样式
description: 创建一个CSS定义，以允许加载个性化内容而不会出现闪烁。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

此 `prehidingStyle` 属性允许您定义CSS选择器，以隐藏个性化内容，直到加载为止。 此属性在同步Web SDK实施中非常有用，可避免闪烁。 Adobe建议使用 [预隐藏代码片段](../../personalization/manage-flicker.md) 用于异步Web SDK实施。

您在此属性中定义的CSS选择器将在您第一次运行时开始隐藏内容 [`sendEvent`](../sendevent/overview.md) 命令。 当收到来自Adobe的响应时（通常包括个性化内容），内容不会隐藏。 如果 `sendEvent` 命令失败或超时。

如果您同时包含两者 `prehidingStyle` 以及实施中的预隐藏代码片段，则预隐藏代码片段的优先级将高于此配置属性。

## 使用Web SDK标记扩展的预隐藏样式

选择 **[!UICONTROL 提供预隐藏样式]** 按钮时间 [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下滚动到 [!UICONTROL 个性化] 部分，然后选择按钮 **[!UICONTROL 提供预隐藏样式]**.
1. 此按钮将打开一个带有CSS编辑器的模式窗口。 插入所需的CSS选择器和声明块，然后单击 **[!UICONTROL 保存]** 以关闭模式窗口。
1. 单击 **[!UICONTROL 保存]** 在扩展设置下，然后发布更改。

## 使用Web SDK JavaScript库预隐藏样式

设置 `prehidingStyle` 字符串 `configure` 命令。 如果在配置Web SDK时省略此属性，则运行第一个 `sendEvent` 命令。 将此值设置为同步加载的库所需的CSS选择器和声明块。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "prehidingStyle": "#container { opacity: 0 !important }"
});
```

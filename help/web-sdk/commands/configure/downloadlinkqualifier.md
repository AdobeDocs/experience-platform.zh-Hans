---
title: downloadlinkqualifier
description: 帮助确定自动链接跟踪如何限定下载链接。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

如果您使用以下方式启用自动链接跟踪 [`clickCollectionEnabled`](clickcollectionenabled.md)， `downloadLinkQualifier` 属性可帮助确定将URL视为下载链接的条件。

此属性是一个正则表达式字符串。 如果点击的URL与此正则表达式匹配， `xdm.web.webInteraction.type` 设置为 `"download"`. 如果链接中包含以下链接，则也会立即将其分类为下载链接 `download` 属性HTML。 如果 `clickCollectionEnabled` 未启用，则此属性不执行任何操作。

## 使用Web SDK标记扩展下载链接限定符

启用 **[!UICONTROL 启用点击数据收集]** 复选框，然后在下面输入所需的文本 **[!UICONTROL 下载链接限定符]** 时间 [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下滚动到 [!UICONTROL 数据收集] 部分，然后选中复选框 **[!UICONTROL 启用点击数据收集]**.
1. 启用后， **[!UICONTROL 下载链接限定符]** 文本框出现。 输入所需的值。 也有按钮可用于测试正则表达式并恢复默认值。
1. 单击 **[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库下载链接限定符

设置 `downloadLinkQualifier` 字符串 `configure` 命令。 如果省略此属性，则默认使用以下值：

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

如果要使用其他标准来限定下载链接，请将此属性设置为所需的正则表达式值。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": true,
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```

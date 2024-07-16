---
title: downloadlinkqualifier
description: 帮助确定自动链接跟踪如何限定下载链接。
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

如果使用[`clickCollectionEnabled`](clickcollectionenabled.md)启用自动链接跟踪，`downloadLinkQualifier`属性可帮助确定将URL视为下载链接的条件。

此属性是一个正则表达式字符串。 如果点击的URL与此正则表达式匹配，`xdm.web.webInteraction.type`将设置为`"download"`。 如果链接包含`download`HTML属性，则也会立即将其分类为下载链接。 如果未启用`clickCollectionEnabled`，则此属性不执行任何操作。

## 使用Web SDK标记扩展下载链接限定符

启用&#x200B;**[!UICONTROL 启用“单击数据收集]**”复选框，然后在[配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)时，在&#x200B;**[!UICONTROL 下载链接限定符]**&#x200B;下输入所需的文本。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 扩展]**，然后单击[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 配置]**。
1. 向下滚动到[!UICONTROL 数据收集]部分，然后选中复选框&#x200B;**[!UICONTROL 启用“单击数据收集”]**。
1. 启用后，将显示&#x200B;**[!UICONTROL 下载链接限定符]**&#x200B;文本框。 输入所需的值。 也有按钮可用于测试正则表达式并恢复默认值。
1. 单击&#x200B;**[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库下载链接限定符

运行`configure`命令时设置`downloadLinkQualifier`字符串。 如果省略此属性，则默认使用以下值：

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

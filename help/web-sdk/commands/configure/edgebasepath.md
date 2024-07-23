---
title: edgbasePath
description: 用于与Adobe服务交互的端点的基本路径。
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

当您与Adobe服务交互时，`edgeBasePath`属性会更改目标路径。 大多数组织不需要设置或更改此属性。

## 使用Web SDK标记扩展的Edge基本路径

当[配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)时，在&#x200B;**[!UICONTROL Edge基本路径]**&#x200B;文本字段中输入所需的文本。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 扩展]**，然后单击[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 配置]**。
1. 向下滚动到[!UICONTROL 高级设置]部分，然后在&#x200B;**[!UICONTROL Edge基本路径]**&#x200B;文本字段中输入所需的值。
1. 单击&#x200B;**[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库的Edge基本路径

运行`configure`命令时设置`edgeBasePath`文本字段。 如果忽略此属性，则其默认值为`ee`的值。 Adobe建议在大多数配置中忽略此属性。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeBasePath: "ee"
});
```

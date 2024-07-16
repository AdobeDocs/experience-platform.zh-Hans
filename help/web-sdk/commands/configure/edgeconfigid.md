---
title: edgeConfigId
description: 确定要将数据发送到的数据流ID。
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# `edgeConfigId`

`edgeConfigId`属性是一个字符串，可决定您要将数据发送至Adobe Experience Platform中的哪个[数据流](../../../datastreams/overview.md)。 向Adobe发送数据时需要此属性。

要查找数据流ID，请执行以下操作：

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 数据流]**。
1. 使用搜索字段查找所需的数据流，然后选择数据流ID旁边的&#x200B;**[!UICONTROL 复制]** ![复制](../../assets/copy.png)。

您还可以选择所需的数据流名称，数据流ID将显示在右列以供您复制。

## 使用Web SDK标记扩展选择数据流ID

从可用数据流列表中进行选择，或在[配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)时直接输入数据流ID。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 扩展]**，然后单击[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 配置]**。
1. 找到[!UICONTROL 数据流]部分，然后选择确定数据流的所需方法。
   * 如果从列表中选择，请从每个相应的下拉列表中选择沙盒和数据流。
   * 如果输入值，请输入所需的数据流ID。
1. 单击&#x200B;**[!UICONTROL 保存]**，然后发布更改。

您可以将数据发送到不同的数据流以用于生产、暂存和开发标记环境。

## 使用Web SDK JavaScript库选择数据流ID

运行`configure`命令时设置`edgeConfigId`字符串属性。 所有Web SDK实施都需要此属性。 如果忽略此属性，则Web SDK不知道要将数据发送到哪个数据流，从而导致该数据永久丢失。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

如果您在单个页面上配置了Web SDK的多个实例，则必须为每个实例配置不同的`edgeConfigId`。

---
title: datastreamId
description: 确定要将数据发送到的数据流ID。
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: b9fea4833c4fe869b27c1270aafd3f7ed62d59db
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# `datastreamId`

`datastreamId`属性是一个字符串，可决定您要将数据发送至Adobe Experience Platform中的哪个[数据流](/help/datastreams/overview.md)。 向Adobe发送数据时需要此属性。 Web SDK 2.20.0或更早版本改用`edgeConfigId`。

要查找数据流ID，请执行以下操作：

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**。
1. 使用搜索字段找到所需的数据流，然后选择数据流ID旁边的&#x200B;**[!UICONTROL Copy]** ![复制](../../assets/copy.png)。

或者，您可以选择所需的数据流名称，数据流ID将显示在右列以供您复制。

## 代码示例

运行`datastreamID`命令时设置`configure`字符串属性。 所有Web SDK实施都需要此属性。 如果忽略此属性，则Web SDK不知道要将数据发送到哪个数据流，从而导致该数据永久丢失。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

>[!NOTE]
>
>如果您在单个页面上配置了Web SDK的多个实例，则必须为每个实例配置不同的`datastreamId`。

## 使用Web SDK标记扩展选择数据流ID

请参阅Web SDK标记扩展文档中的[数据流配置设置](/help/tags/extensions/client/web-sdk/configure/datastreams.md)，了解如何使用标记为每个环境设置所需的数据流。 您可以将数据发送到不同的数据流以用于生产、暂存和开发标记环境。

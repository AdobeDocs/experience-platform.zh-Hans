---
title: edgeConfigId
description: 确定要将数据发送到的数据流ID。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# `edgeConfigId`

此 `edgeConfigId` 属性是一个字符串，可确定 [数据流](../../../datastreams/overview.md) 在Adobe Experience Platform中，将数据发送到。 向Adobe发送数据时需要此属性。

要查找数据流ID，请执行以下操作：

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 数据流]**.
1. 使用搜索字段找到所需的数据流，然后选择 **[!UICONTROL 复制]** ![复制](../../assets/copy.png) 数据流ID旁边的。

您还可以选择所需的数据流名称，数据流ID将显示在右列以供您复制。

## 使用Web SDK标记扩展选择数据流ID

从可用数据流的列表中选择数据，或直接输入数据流ID [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 找到 [!UICONTROL 数据流] 部分，然后选择所需的数据流确定方法。
   * 如果从列表中选择，请从每个相应的下拉列表中选择沙盒和数据流。
   * 如果输入值，请输入所需的数据流ID。
1. 单击 **[!UICONTROL 保存]**，然后发布更改。

您可以将数据发送到不同的数据流以用于生产、暂存和开发标记环境。

## 使用Web SDK JavaScript库选择数据流ID

设置 `edgeConfigId` 字符串属性 `configure` 命令。 所有Web SDK实施都需要此属性。 如果忽略此属性，则Web SDK不知道要将数据发送到哪个数据流，从而导致该数据永久丢失。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

如果在一个页面上配置多个Web SDK实例，则必须配置其他 `edgeConfigId` 针对每个实例。

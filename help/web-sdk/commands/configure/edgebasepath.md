---
title: edgbasePath
description: 用于与Adobe服务交互的端点的基本路径。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

此 `edgeBasePath` 属性可在您与Adobe服务交互时更改目标路径。 大多数组织不需要设置或更改此属性。

## 使用Web SDK标记扩展的Edge基本路径

在中输入所需的文本 **[!UICONTROL 边缘基本路径]** 文本字段，条件 [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下滚动到 [!UICONTROL 高级设置] 部分，然后在中输入所需的值 **[!UICONTROL 边缘基本路径]** 文本字段。
1. 单击 **[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库的边缘基本路径

设置 `edgeBasePath` 文本字段 `configure` 命令。 如果忽略此属性，则其默认值为 `ee`. Adobe建议在大多数配置中忽略此属性。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeBasePath": "ee"
});
```

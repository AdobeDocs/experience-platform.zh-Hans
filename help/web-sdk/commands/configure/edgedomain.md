---
title: edgeDomain
description: 确定要将数据发送到的根域。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# `edgeDomain`

此 `edgeDomain` 属性允许您更改Web SDK发送数据的域。 此属性经常由使用它的组织使用 [第一方Cookie](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=zh-Hans). 数据会发送到组织自己的域，然后CNAME记录会将该数据转发到Adobe。

您的组织在设置时确定此属性的正确值 [第一方Cookie](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=zh-Hans). 组织通常使用专用子域来实现此目的。 例如，如果您使用域 `example.com`，您可以在上设置第一方Cookie `data.example.com`.

## 使用Web SDK标记扩展配置边缘域

设置 **[!UICONTROL 边缘域]** 文本字段，条件 [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 找到文本字段 **[!UICONTROL 边缘域]**，然后输入所需的值。
1. 单击 **[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库配置边缘域

设置 `edgeDomain` 字符串 `configure` 命令。 如果在配置SDK时省略此属性，则默认使用 `edge.adobedc.net`. 如果要覆盖Web SDK将数据发送到的域，请设置此值。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeDomain": "data.example.com"
});
```

---
title: edgeDomain
description: 确定要将数据发送到的根域。
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# `edgeDomain`

`edgeDomain`属性允许您更改Web SDK发送数据的域。 此属性经常由使用[第一方Cookie](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=zh-Hans)的组织使用。 数据会发送到组织自己的域，然后CNAME记录会将该数据转发到Adobe。

您的组织在设置[第一方Cookie](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=zh-Hans)时确定此属性的正确值。 组织通常使用专用子域来实现此目的。 例如，如果您使用域`example.com`，则可以在`data.example.com`上设置第一方Cookie。

## 使用Web SDK标记扩展配置边缘域

在[配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)时设置&#x200B;**[!UICONTROL Edge域]**&#x200B;文本字段。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 扩展]**，然后单击[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 配置]**。
1. 找到文本字段&#x200B;**[!UICONTROL Edge域]**，然后输入所需的值。
1. 单击&#x200B;**[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库配置边缘域

运行`configure`命令时设置`edgeDomain`字符串。 如果在配置SDK时省略此属性，则默认设置为`edge.adobedc.net`。 如果要覆盖Web SDK将数据发送到的域，请设置此值。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```

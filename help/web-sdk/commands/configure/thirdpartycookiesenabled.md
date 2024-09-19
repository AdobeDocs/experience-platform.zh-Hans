---
title: thirdPartyCookiesEnabled
description: 允许使用第三方Cookie来识别访客。
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: a884790aa48fb97eebe2421124fc5d5f76c8a79d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# `thirdPartyCookiesEnabled`

`thirdPartyCookiesEnabled`属性是一个布尔值，用于确定Web SDK是否会在第三方上下文中设置Cookie。 如果要识别组织拥有的子域或域之间的访客，则启用此选项非常有用。 但是，许多现代浏览器会限制第三方Cookie的设置和过期。

`thirdPartyCookiesEnabled`属性还控制能否在[`getIdentity`](../getidentity.md)调用中请求[`CORE ID`](../../identity/overview.md#tracking-coreid-web-sdk)。

启用此选项后，Web SDK将使用Adobe Audience Manager帮助识别访客。 禁用此选项后，将禁用对Audience Manager的调用。 有关详细信息，请参阅Audience Manager用户指南中的[了解Demdex域调用](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=zh-Hans)。

## 使用Web SDK标记扩展启用第三方Cookie

选中[配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)时的&#x200B;**[!UICONTROL 使用第三方Cookie]**&#x200B;复选框。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 扩展]**，然后单击[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 配置]**。
1. 向下滚动到[!UICONTROL 标识]部分，然后选中&#x200B;**[!UICONTROL 使用第三方Cookie]**&#x200B;复选框。
1. 单击&#x200B;**[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库启用第三方Cookie

运行`configure`命令时设置`thirdPartyCookiesEnabled`布尔值。 如果在配置Web SDK时省略此属性，则默认设置为`true`。 如果不希望Web SDK使用Audience Manager帮助识别访客，请将此值设置为`false`。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```

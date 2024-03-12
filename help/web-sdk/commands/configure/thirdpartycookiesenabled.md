---
title: thirdPartyCookiesEnabled
description: 允许使用第三方Cookie来识别访客。
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: bc48f45bd6b9b7f7cc446ae84d712376292718d2
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# `thirdPartyCookiesEnabled`

>[!IMPORTANT]
>
>Google [已宣布](https://developers.google.com/privacy-sandbox/3pcd/prepare/prepare-for-phaseout) 计划在2024年下半年停止支持第三方Chrome Cookie。 因此，任何主要浏览器将不再支持第三方Cookie。
>
>实施此更改后，Adobe将停止对 `demdex` Web SDK当前支持的Cookie。


此 `thirdPartyCookiesEnabled` 属性是一个布尔值，用于确定Web SDK是否会在第三方上下文中设置Cookie。 如果要识别组织拥有的子域或域之间的访客，则启用此选项非常有用。 但是，许多现代浏览器会限制第三方Cookie的设置和过期。

启用此选项后，Web SDK将使用Adobe Audience Manager帮助识别访客。 禁用此选项后，将禁用对Audience Manager的调用。 请参阅 [了解Demdex域调用](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=zh-Hans) 有关更多信息，请参阅Audience Manager用户指南。

## 使用Web SDK标记扩展启用第三方Cookie

选择 **[!UICONTROL 使用第三方Cookie]** 复选框，条件 [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下滚动到 [!UICONTROL 标识] 部分，然后选中复选框 **[!UICONTROL 使用第三方Cookie]**.
1. 单击 **[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库启用第三方Cookie

设置 `thirdPartyCookiesEnabled` 布尔值 `configure` 命令。 如果在配置Web SDK时省略此属性，则默认使用 `true`. 将此值设置为 `false` 如果您不希望Web SDK使用Audience Manager来帮助识别访客。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "thirdPartyCookiesEnabled": false
});
```

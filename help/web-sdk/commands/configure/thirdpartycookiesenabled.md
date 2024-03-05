---
title: thirdPartyCookiesEnabled
description: 允许使用第三方Cookie来识别访客。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# `thirdPartyCookiesEnabled`

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

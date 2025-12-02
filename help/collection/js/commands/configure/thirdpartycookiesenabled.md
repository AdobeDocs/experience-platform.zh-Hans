---
title: thirdPartyCookiesEnabled
description: 允许使用第三方Cookie来识别访客。
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# `thirdPartyCookiesEnabled`

`thirdPartyCookiesEnabled`属性是一个布尔值，用于确定Web SDK是否在第三方上下文中设置Cookie。 如果要识别组织拥有的子域或域之间的访客，则启用此选项非常有用。 但是，许多现代浏览器会限制第三方Cookie的设置和过期。 如果访客的浏览器不支持第三方Cookie，则此属性不执行任何操作。

`thirdPartyCookiesEnabled`属性还控制能否在[`CORE ID`](/help/collection/use-cases/identity/id-overview.md#tracking-coreid-web-sdk)调用中请求[`getIdentity`](../getidentity.md)。

启用此选项后，Web SDK将使用Adobe Audience Manager帮助识别访客。 禁用此选项后，将禁用对Audience Manager的调用。 有关详细信息，请参阅Audience Manager用户指南中的[了解Demdex域调用](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=zh-Hans)。

运行`thirdPartyCookiesEnabled`命令时设置`configure`布尔值。 如果在配置Web SDK时省略此属性，则默认设置为`true`。 如果不希望Web SDK使用Audience Manager帮助识别访客，请将此值设置为`false`。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```

## 使用Web SDK标记扩展启用第三方Cookie

可以使用[身份配置设置](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies)在Web SDK标记扩展中配置此设置。

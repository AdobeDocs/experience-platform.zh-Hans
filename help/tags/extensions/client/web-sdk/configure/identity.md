---
title: 身份配置设置
description: 定义标记扩展如何识别访客。
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 2%

---

# 身份配置设置

通过此配置部分，可定义Web SDK在处理用户标识时的行为。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Extensions]**，然后在&#x200B;**[!UICONTROL Configure]**&#x200B;信息卡上选择[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下滚动到&#x200B;**[!UICONTROL Identity]**&#x200B;部分。

![在标记UI中显示Web SDK标记扩展的标识设置的图像](../assets/web-sdk-ext-identity.png)

可以使用以下选项：

## [!UICONTROL Migrate ECID from VisitorAPI]

一个复选框，允许Web SDK读取`AMCV`和`s_ecid` Cookie并设置`AMCV`使用的`Visitor.js` Cookie。 在从使用`VisitorAPI.js`的库迁移到Web SDK时，此功能很重要，因为某些页面可能仍在使用`Visitor.js`。 此选项允许SDK继续使用相同的ECID，这样用户就不会被标识为两个不同的用户。 与此复选框等效的JavaScript库为[`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md)。

## [!UICONTROL Use third-party cookies]

启用此选项后，Web SDK会尝试将用户标识符存储在第三方Cookie中。 如果成功，则在用户跨多个域导航时将用户标识为单个用户，而不是在每个域上将用户标识为单独的用户。 如果启用了此选项，则如果SDK不支持第三方Cookie或用户将其配置为不允许第三方Cookie，则浏览器仍可能无法将用户标识符存储在第三方Cookie中。 在这种情况下，SDK只将标识符存储在第一方域中。 与此复选框等效的JavaScript库为[`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md)。

>[!IMPORTANT]
>
>第三方Cookie与Web SDK中的[第一方设备ID](/help/collection/use-cases/identity/first-party-device-ids.md)功能不兼容。 您可以使用第一方设备ID，也可以使用第三方Cookie；您不能同时使用这两项功能。

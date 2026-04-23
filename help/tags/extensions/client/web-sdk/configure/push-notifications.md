---
title: 推送通知设置
description: 为Web SDK标记扩展配置推送通知设置。
exl-id: 96ab7ea8-7180-46bb-9c15-eecba2009c52
source-git-commit: d38cfb7d2ace7c1bb45dcb584a2cdf10063da06a
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 10%

---

# 推送通知设置 {#push-notifications}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_pushnotifications"
>title="推送通知"
>abstract="设置用于推送通知身份验证的 VAPID 公钥。"

此配置部分允许您为推送通知身份验证设置VAPID公钥。

>[!NOTE]
>
>必须首先使用[自定义生成组件](custom-build-components.md)启用此功能；默认情况下禁用此功能。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Extensions]**，然后单击&#x200B;**[!UICONTROL Configure]**&#x200B;信息卡上的[!UICONTROL Adobe Experience Platform Web SDK]。
1. 展开&#x200B;**[!UICONTROL Custom build components]**，然后启用&#x200B;**[!UICONTROL Push notifications]**。
1. 在[!UICONTROL SDK instances]下，向下滚动以找到[!UICONTROL Push Notifications]部分。
1. 在&#x200B;**[!UICONTROL VAPID Public Key]**&#x200B;字段中输入您的VAPID公钥。

![显示使用Web SDK标记扩展的推送通知设置的图像](../assets/push-notifications.png)

以下字段可用：

## [!UICONTROL VAPID public key]

用于推送订阅的VAPID公钥。 它是Base64编码的字符串。

## [!UICONTROL Application ID]

与VAPID公钥关联的应用程序ID。

## [!UICONTROL Tracking dataset ID]

用于推送通知跟踪和分析的数据集ID。

## 使用JavaScript库推送通知

在配置JavaScript库时，此部分的标记等效于[`pushNotifications`](/help/collection/js/commands/configure/pushnotifications.md)。 链接的页面还提供了有关先决条件和生成VAPID公钥的信息。

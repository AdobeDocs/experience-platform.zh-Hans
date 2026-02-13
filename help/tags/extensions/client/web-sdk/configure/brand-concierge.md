---
title: Brand Concierge配置设置
description: 为Brand Concierge Chat配置会话持久性和流超时。
exl-id: d5c0bdf7-563d-4e0e-9b1b-71e2fa783e29
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 5%

---

# Brand Concierge配置设置 {#brand-concierge}

>[!AVAILABILITY]
>
>适用于Web SDK的Brand Concierge当前处于&#x200B;**测试版**&#x200B;中。 功能和文档可能会发生更改。

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_brandconcierge"
>title="Brand Concierge"
>abstract="在资产上使用Brand Concierge时的配置设置。"

通过&#x200B;**[!UICONTROL Brand Concierge]**&#x200B;部分，您可以控制Brand Concierge聊天会话在Web SDK标记扩展中的行为。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Extensions]**，然后在&#x200B;**[!UICONTROL Configure]**&#x200B;信息卡上选择[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下滚动到&#x200B;**[!UICONTROL Brand Concierge]**&#x200B;部分。

可以使用以下选项：

## [!UICONTROL Sticky conversation session]

一个复选框，它使用会话Cookie跨页面加载保留Brand Concierge会话。 此选项默认处于禁用状态。 有关设置此值的指导，请参阅JavaScript库文档中的[`conversation`](/help/collection/js/commands/configure/conversation.md)。

## [!UICONTROL Stream timeout (seconds)]

触发超时错误之前等待会话流块的最长时间（以秒为单位）。 默认值为`10`秒。

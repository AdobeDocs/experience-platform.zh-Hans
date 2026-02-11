---
title: 自定义生成组件
description: 创建自定义Web SDK内部版本，该内部版本会禁用相关功能以减小内部版本大小。
exl-id: 853e0a6c-0953-4e08-9a7d-334aab022583
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# 自定义生成组件

Web SDK库包含多个模块，用于提供各种功能，如个性化、身份识别、链接跟踪等。 根据您的用例，您可能只需要特定功能，而无需整个库。 通过禁用生成组件，您可以仅使用所需的模块，从而减小库大小并提高性能。

禁用某个组件后，无法再编辑该组件的设置。 如果您使用多个Web SDK实例，则选定的生成组件将应用于所有实例。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Extensions]**，然后在&#x200B;**[!UICONTROL Configure]**&#x200B;信息卡上选择[!UICONTROL Adobe Experience Platform Web SDK]。
1. 展开顶部的&#x200B;**[!UICONTROL Custom build components]**&#x200B;折叠面板。

>[!WARNING]
>
>错误地修改这些设置可能会导致意外的结果，包括数据丢失。 先在开发环境中彻底测试您的实施，然后再将这些更改发布到生产环境。

Adobe提供禁用以下Web SDK构建组件的功能：

| 生成组件 | 描述 | 从属特征 |
| --- | --- | --- |
| **[!UICONTROL Activity collector]** | 允许自动链接收集和Activity Map跟踪。 | |
| **[!UICONTROL Advertising]** | 启用Adobe Advertising与Customer Journey Analytics的集成。 | |
| **[!UICONTROL Audiences]** | 支持与Adobe Audience Manager的集成，例如ID同步。 | |
| **[!UICONTROL Brand concierge]** | 支持与Brand Concierge集成。 |
| **[!UICONTROL Consent]** | 允许使用同意功能。 | [[!UICONTROL Set consent]](../actions/set-consent.md)操作 |
| **[!UICONTROL Event merge]** | 已弃用。 | [[!UICONTROL Event merge ID]](../data-element-types.md)数据元素（已弃用）<br>[[!UICONTROL Reset event merge ID]](../actions/reset-event-merge-id.md)操作（已弃用） |
| **[!UICONTROL Media Analytics bridge]** | 支持与旧版Media Analytics的集成。 | [[!UICONTROL Get media analytics tracker]](../actions/get-media-analytics-tracker.md)操作 |
| **[!UICONTROL Personalization]** | 支持与Adobe Target和Adobe Journey Optimizer的集成。 | [[!UICONTROL Apply propositions]](../actions/apply-propositions.md)操作 |
| **[!UICONTROL Push notifications]** | 为Adobe Journey Optimizer启用Web推送通知。 | [[!UICONTROL Send push subscription]](../actions/send-push-subscription.md)操作 |
| **[!UICONTROL Rules engine]** | 通过Adobe Journey Optimizer启用设备决策。 | [[!UICONTROL Evaluate rulsets]](../actions/evaluate-rulesets.md)操作<br> [[!UICONTROL Subscribe ruleset items]](../event-types.md#subscribe-ruleset-items)事件 |
| **[!UICONTROL Streaming media]** | 支持与流媒体收藏集集成。 | [[!UICONTROL Send media event]](../actions/send-media-event.md)操作 |

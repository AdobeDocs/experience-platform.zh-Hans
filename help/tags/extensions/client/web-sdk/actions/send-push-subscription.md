---
title: 发送推送订阅
description: 注册、发送和收集浏览器推送订阅的数据。
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 2%

---

# 发送推送订阅

>[!AVAILABILITY]
>
>Web SDK的推送通知当前处于&#x200B;**测试版**&#x200B;中。 功能和文档可能会发生更改。

**[!UICONTROL Send push subscription]**&#x200B;操作向Adobe Experience Platform注册推送通知订阅。 它处理从浏览器检索推送订阅详细信息并将它们发送到您配置的数据流。 它在Web SDK扩展版本2.32.0或更高版本中可用。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Rules]**，然后选择所需的规则。
1. 在[!UICONTROL Actions]下，选择现有操作或创建操作。
1. 将[!UICONTROL Extension]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**&#x200B;并将[!UICONTROL Action Type]设置为&#x200B;**[!UICONTROL Send push subscription]**。

除了选择SDK实例之外，该操作没有任何配置设置。

使用此命令之前，请确保在配置扩展时设置有效的[VAPID公钥](../configure/push-notifications.md)。

此操作是等效于[`sendPushSubscription`](/help/collection/js/commands/sendpushsubscription.md)命令的标记扩展。 有关先决条件、建议的执行频率、命令工作方式和错误处理的信息，请参阅链接的页面。

>[!MORELIKETHIS]
>
>* [配置推送通知](../configure/push-notifications.md)
>* [Web推送API规范](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)

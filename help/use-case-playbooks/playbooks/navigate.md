---
solution: Experience Platform
title: 导航到用例行动手册
description: 了解如何在行动手册库中导航并开始使用启发性的沙盒。
role: User
exl-id: 1f5dae75-1136-4be3-9132-01d36a4066ca
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---

# 导航到用例行动手册

所有Adobe Experience Platform客户均可免费获得用例行动手册。 要在Experience Platform UI中访问丰富的用例行动手册，请从左侧导航中选择&#x200B;**[!UICONTROL 行动手册]**。

![用例剧本库。](/help/use-case-playbooks/assets/playbooks/discover/playbooks-gallery.png)

![直接访问左侧导航栏中的用例行动手册。](/help/use-case-playbooks/assets/playbooks/discover/left-nav-playbooks.png)

选择任意行动手册以转到详细信息页面，然后选择&#x200B;**[!UICONTROL 转到励志沙盒]**。 此时将显示确认模式窗口。 选择&#x200B;**确认**&#x200B;以转到启发性的沙盒，您可以在其中探索和试验不同的用例。

如果您没有创建沙盒的权限，请联系管理员以获取有关创建启发型沙盒的帮助。

>[!TIP]
>
>启发性的沙盒是Adobe Experience Platform中的开发沙盒，您可以在其中创建、测试和试验各种用例，然后再在实时生产环境中实施它们。

![转到励志沙盒。](/help/use-case-playbooks/assets/playbooks/discover/inspirational-sandbox.png)

如果您尚未设置任何启发性的沙盒，请选择&#x200B;**[!UICONTROL 创建启发性的沙盒]**。 此时将显示一个模式窗口。 在必填字段框中输入&#x200B;**名称**&#x200B;和&#x200B;**标题**，然后选择&#x200B;**创建**。 创建启发性的沙盒后，请确保在[定义权限](/help/access-control/home.md)之后再导航回用例行动手册详细信息页面以创建实例。

![创建启发性的沙盒。](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox.png)

![输入名称和标题以创建启发性的沙盒。](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox-modal.png)

如果您从启发性的沙盒之外选择用例剧本，您将无法创建实例。 在详细信息页面上，选择&#x200B;**转到启发沙盒**&#x200B;以转到现有的启发沙盒，然后选择&#x200B;**[!UICONTROL 创建实例]**。

如果您没有创建沙盒的权限，请联系管理员以获取有关创建启发型沙盒的帮助。

![没有创建沙盒的权限。](/help/use-case-playbooks/assets/playbooks/discover/no-permissions-to-create-sandbox.png)

如果您已达到已分配给您的沙盒数量限制，则会显示一条消息，要求您联系组织管理员以增加限制，或者停用或删除一些活动沙盒。 一旦调整了沙盒限制或减少了活动沙盒数，您就可以继续创建启发性的沙盒。

已达到![沙盒限制。](/help/use-case-playbooks/assets/playbooks/discover/sandbox-limit-reached.png)

请注意，在创建启发性的沙盒时，不会自动设置电子邮件、推送和短信通知的渠道界面。 请联系您的IT管理员以手动配置它们，否则实例创建可能会失败。

![配置渠道预设。](/help/use-case-playbooks/assets/playbooks/discover/configure-channel-presets.png)

## 在Journey Optimizer中配置沙盒和渠道表面 {#configure-channel-surfaces}

如果您的组织获得[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=zh-Hans)的许可，并且您打算使用针对Journey Optimizer设计的行动手册，则需要在沙盒中配置渠道预设，这些预设可定义消息所需的技术参数。 [了解如何在 Adobe Journey Optimizer 中设置渠道界面。](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=zh-Hans)

要在Journey Optimizer中创建行动手册的实例，您需要为电子邮件、推送和短信通知配置渠道平面。

### 电子邮件渠道表面

在Journey Optimizer界面中转到`Channels`。 为营销电子邮件和事务性消息配置单独的子域和IP池（如果尚未配置）。 这些是确保事务型消息（如订单确认电子邮件）传递给客户的最佳实践。 输入姓名、电子邮件地址和其他设置。 选择页面右上角的&#x200B;**提交**&#x200B;以创建营销渠道表面。 阅读有关[如何设置电子邮件渠道界面](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html?lang=zh-Hans)的文档。

### SMS渠道表面

要创建SMS渠道表面，请首先创建SMS API凭据，然后选择首选供应商（例如Sinch）。 命名短信渠道表面（例如，短信营销），选择配置，然后输入发送者号码。 选择页面右上角的&#x200B;**提交**&#x200B;以保存短信渠道表面。 阅读有关[如何设置短信渠道界面](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=zh-Hans#message-preset-sms)的文档。

此外，为包含订单确认等事务性消息的行动手册配置渠道。

### 推送渠道表面

确认已从Experience Platform或数据收集界面配置渠道配置。 渠道配置在数据收集环境中的外观如下。

## 后续步骤 {#next-steps}

现在您已阅读本文档，您应该知道如何设置启发性的沙盒，并熟悉访问Experience Platform中的用例行动手册的各种方式。 接下来，阅读如何[选择](/help/use-case-playbooks/playbooks/choose.md)正确的剧本。

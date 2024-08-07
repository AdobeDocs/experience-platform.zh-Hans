---
solution: Experience Platform
title: 用例行动手册入门
description: 了解如何开始使用用例战术手册功能。
role: Admin
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: 1781aa552107b6ca1fed357c053a4f892960dc55
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 14%

---


# 快速入门

了解如何为用例行动手册设置您的帐户，这些行动手册专为未自动设置的Real-time Customer Data Platform和Adobe Journey Optimizer设计。 三个主要配置步骤为：

* 创建沙盒
* 配置用户权限
* 为电子邮件、推送和短信通知配置Journey Optimizer渠道界面(如果您计划使用Journey Optimizer行动手册)

要在Experience PlatformUI中访问丰富的用例行动手册，请从左侧导航中选择&#x200B;**[!UICONTROL 行动手册]**。 阅读有关如何[导航用例行动手册](../playbooks/navigate.md)并开始使用[启发型沙盒](../playbooks/navigate.md)的文档。

## 配置用例行动手册 — 视频演练 {#video}

观看本视频，了解在Journey Optimizer中创建沙盒、配置权限和配置电子邮件、推送和短信通知的渠道界面所需的步骤。

>[!VIDEO](https://video.tv.adobe.com/v/3426987?learn=on)

## 创建开发沙盒 {#create-development-sandbox}

用例行动手册使用特殊类型的开发沙盒。 要开始使用并访问[[!UICONTROL 使用用例战术手册]](/help/use-case-playbooks/playbooks/overview.md)功能性，[创建一个新的开发沙盒](/help/sandboxes/ui/user-guide.md#create)（确保您没有选择生产沙盒），其名称（而不是标题）后缀中包含 `-ucp` 或者 `-UCP`，如下所示。

>[!IMPORTANT]
>
>创建新的开发沙盒时，请确保名称在后缀中包含`-ucp`或`-UCP`。


![为用例战术手册创建开发沙盒](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

现在，您应该会在左边栏中的[!UICONTROL 用例行动手册]下看到[!UICONTROL 行动手册]。

![创建沙盒后，UI 中的用例战术手册。](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

如果您在左栏中没有看到如上图所示的[!UICONTROL 战术手册]，请使用此链接`https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates`直接导航到那里。在链接中，`<YOUR_ORG>` 是您的组织的名称，而 `<YOUR_SANDBOX_NAME>` 是您创建的开发沙盒的名称。

## 授予您的团队所需的访问权限 {#grant-access-permissions}

要开始使用[!UICONTROL 用例行动手册]，您的营销团队成员需要正确的权限，以便他们可以查看已创建的行动手册的列表或自行创建行动手册。

**所需权限**

若要添加所需权限，请在权限UI中，将新的用例行动手册沙盒包含在您已配置的[角色中](/help/access-control/abac/ui/permissions.md#managing-sandboxes-for-role)，包括用于其他开发沙盒的角色。

![角色的Playbook沙盒已配置](/help/use-case-playbooks/assets/playbooks/get-started/permissions-to-existing-roles.png)

**为行动手册设置角色：**

或者，您也可以考虑添加具有[所需权限](/help/access-control/home.md#sandboxes-and-permissions)的新角色。

[设置具有基本行动手册任务必要权限的新角色](/help/access-control/abac/ui/permissions.md)。 创建一个角色并向其添加新沙盒，如下所示。

![创建角色并将其添加到沙盒](/help/use-case-playbooks/assets/playbooks/get-started/create-new-role.png)

行动手册实例的&#x200B;**权限**

作为用例剧本的一部分，您将创建各种资源，如架构、受众、目标和历程。 您和其他用户需要正确的权限才能创建这些对象。

架构的&#x200B;**权限**

若要创建和管理架构，请利用数据建模权限；**[!UICONTROL 管理架构]**、**[!UICONTROL 查看架构]**、**[!UICONTROL 管理关系]**、**[!UICONTROL 管理身份元数据]**

目标的&#x200B;**权限**

要创建和管理目标，请使用目标权限；**[!UICONTROL 管理]**、**[!UICONTROL 目标]**、**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 激活不含映射的区段]**、**[!UICONTROL 管理和激活数据集目标]**、**[!UICONTROL 目标创作]**。

历程的&#x200B;**权限**

要创建和管理历程，请使用历程权限；**[!UICONTROL 管理历程]**、**[!UICONTROL 查看历程]**、**[!UICONTROL 查看历程报告]**、**[!UICONTROL 管理历程]**、**[!UICONTROL 事件]**、**[!UICONTROL 数据源和操作]**、**[!UICONTROL 查看历程]**、**[!UICONTROL 事件]**、**[!UICONTROL 数据源和操作、{Publish历程]**。

下图显示了用户查看、创建和管理行动手册以及行动手册生成的资产的建议权限快照。

![创建行动手册的所有实例所需的所有权限项的快照](/help/use-case-playbooks/assets/playbooks/get-started/permission-snapshot.png)

**将用户添加到角色**

在您[创建了如上所述的新角色](/help/access-control/abac/ui/permissions.md#managing-users-for-role)后，请将您自己作为用户添加到该角色中。 如果您为另一组具有仅查看访问权限的用户创建具有有限访问权限的角色，则仅包括与这些权限关联的必需查看项目。

## 在Journey Optimizer中配置沙盒和渠道表面 {#configure-channel-surfaces}

如果您的组织获得[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=zh-Hans)的许可，并且您打算使用针对Journey Optimizer设计的行动手册，则需要在沙盒中配置渠道预设，这些预设可定义消息所需的技术参数。 [了解如何在 Adobe Journey Optimizer 中设置渠道界面。](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html)

要在Journey Optimizer中创建行动手册的实例，您需要为电子邮件、推送和短信通知配置渠道平面。

### 电子邮件渠道表面

在Journey Optimizer界面中转到`Channels`。 为营销电子邮件和事务性消息配置单独的子域和IP池（如果尚未配置）。 这些是确保事务型消息（如订单确认电子邮件）传递给客户的最佳实践。 输入姓名、电子邮件地址和其他设置。 选择页面右上角的&#x200B;**提交**&#x200B;以创建营销渠道表面。 阅读有关[如何设置电子邮件渠道界面](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html)的文档。

### SMS渠道表面

要创建SMS渠道表面，请首先创建SMS API凭据，然后选择首选供应商（例如Sinch）。 命名短信渠道表面（例如，短信营销），选择配置，然后输入发送者号码。 选择页面右上角的&#x200B;**提交**&#x200B;以保存短信渠道表面。 阅读有关[如何设置短信渠道界面](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=zh-Hans#message-preset-sms)的文档。

此外，为包含订单确认等事务性消息的行动手册配置渠道。

### 推送渠道表面

确认已在Experience Platform或数据收藏集界面中配置应用程序表面。 这就是应用程序表面在数据收集环境中的外观。

<!-- ![App surfaces in Data collections](/help/use-case-playbooks/assets/playbooks/get-started/.png) -->

接下来，选择您在应用程序表面配置中查看的渠道、平台和应用程序。 选择&#x200B;**提交**&#x200B;以创建推送渠道表面。

阅读有关[如何设置推送渠道界面](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html)的文档。

## 后续步骤 {#next-steps}

现在，您已执行本文档中的所有步骤，您应该已使用可在左侧导航栏中找到的用例行动手册创建了一个开发沙盒。 您现在还知道如何授予团队成员查看和管理行动手册以及生成资产所需的权限。 接下来，阅读如何[为您选择正确的行动手册](/help/use-case-playbooks/playbooks/choose.md)，然后[从中创建实例](/help/use-case-playbooks/playbooks/create-share-reuse.md)。

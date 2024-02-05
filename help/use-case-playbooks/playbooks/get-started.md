---
solution: Experience Platform
title: 快速入门
description: 了解如何开始使用用例战术手册功能。
role: Admin
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: 785e32b27372cef9d23761f648bcbaa431448ce7
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 14%

---


# 快速入门

了解如何为针对Real-time Customer Data Platform和Adobe Journey Optimizer设计的用例行动手册设置您的帐户。 三个主要配置步骤为：

* 创建沙盒
* 配置用户权限
* 为电子邮件、推送和短信通知配置Journey Optimizer渠道界面(如果您计划使用Journey Optimizer行动手册)

## 配置用例行动手册 — 视频演练 {#video}

观看本视频，了解在Journey Optimizer中创建沙盒、配置权限和配置电子邮件、推送和短信通知的渠道界面所需的步骤。

>[!VIDEO](https://video.tv.adobe.com/v/3426987?learn=on)

## 创建开发沙盒 {#create-development-sandbox}

用例行动手册使用特殊类型的开发沙盒。 要开始使用并访问[[!UICONTROL 使用用例战术手册]](/help/use-case-playbooks/playbooks/overview.md)功能性，[创建一个新的开发沙盒](/help/sandboxes/ui/user-guide.md#create)（确保您没有选择生产沙盒），其名称（而不是标题）后缀中包含 `-ucp` 或者 `-UCP`，如下所示。

>[!IMPORTANT]
>
>创建新的开发沙盒时，请确保名称包含 `-ucp` 或 `-UCP` 在后缀中。


![为用例战术手册创建开发沙盒](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

您现在应该看到 [!UICONTROL 行动手册] 在左边栏中的 [!UICONTROL 用例行动手册].

![创建沙盒后，UI 中的用例战术手册。](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

如果您在左栏中没有看到如上图所示的[!UICONTROL 战术手册]，请使用此链接`https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates`直接导航到那里。在链接中，`<YOUR_ORG>` 是您的组织的名称，而 `<YOUR_SANDBOX_NAME>` 是您创建的开发沙盒的名称。

## 授予您的团队所需的访问权限 {#grant-access-permissions}

开始使用 [!UICONTROL 用例行动手册]，您的营销团队成员需要正确的权限，以便他们可以查看已创建的行动手册的列表或自行创建行动手册。

**所需权限**

要添加所需的权限，请在权限UI中，将新的用例剧本沙盒包含在 [您已配置的角色](/help/access-control/abac/ui/permissions.md#managing-sandboxes-for-role)，包括用于其他开发沙盒的沙盒。

![角色的Playbook沙盒已配置](/help/use-case-playbooks/assets/playbooks/get-started/permissions-to-existing-roles.png)

**为行动手册设置一个角色：**

或者，您也可以考虑通过 [所需的权限](/help/access-control/home.md#sandboxes-and-permissions).

[设置新角色](/help/access-control/abac/ui/permissions.md) 提供必要的权限，以执行基本行动手册任务。 创建一个角色并向其添加新沙盒，如下所示。

![创建角色并将其添加到沙盒](/help/use-case-playbooks/assets/playbooks/get-started/create-new-role.png)

**剧本实例的权限**

作为用例剧本的一部分，您将创建各种资源，如架构、受众、目标和历程。 您和其他用户需要正确的权限才能创建这些对象。

**架构权限**

创建和管理模式，利用数据建模权限； **[!UICONTROL 管理架构]**， **[!UICONTROL 查看架构]**， **[!UICONTROL 管理关系]**， **[!UICONTROL 管理身份元数据]**

**目标的权限**

要创建和管理目标，请使用目标权限； **[!UICONTROL 管理]**， **[!UICONTROL 目标]**， **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 激活没有映射的区段]**， **[!UICONTROL 管理和激活数据集目标]**， **[!UICONTROL 目标创作]**.

**历程的权限**

要创建和管理历程，请使用历程权限； **[!UICONTROL 管理历程]**， **[!UICONTROL 查看历程]**， **[!UICONTROL 查看历程报表]**， **[!UICONTROL 管理历程]**， **[!UICONTROL 活动]**， **[!UICONTROL 数据源和操作]**， **[!UICONTROL 查看历程]**， **[!UICONTROL 活动]**， **[!UICONTROL 数据源和操作，发布历程]**.

下图显示了用户查看、创建和管理行动手册以及行动手册生成的资产的建议权限快照。

![创建行动手册的所有实例所需的所有权限项的快照](/help/use-case-playbooks/assets/playbooks/get-started/permission-snapshot.png)

**将用户添加到角色**

一旦 [已创建新角色](/help/access-control/abac/ui/permissions.md#managing-users-for-role) 如上所述，请将您自己作为用户添加到其中。 如果您为另一组具有仅查看访问权限的用户创建具有有限访问权限的角色，则仅包括与这些权限关联的必需查看项目。

## 在Journey Optimizer中配置沙盒和渠道表面 {#configure-channel-surfaces}

如果您的组织获得许可 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)，并且您正在寻求使用针对Journey Optimizer设计的行动手册，您需要在沙盒中配置渠道预设，这会定义消息所需的技术参数。 [了解如何在 Adobe Journey Optimizer 中设置渠道界面。](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html)

要在Journey Optimizer中创建行动手册的实例，您需要为电子邮件、推送和短信通知配置渠道平面。

### 电子邮件渠道表面

转到 `Channels` 在Journey Optimizer界面中。 为营销电子邮件和事务性消息配置单独的子域和IP池（如果尚未配置）。 这些是确保事务型消息（如订单确认电子邮件）传递给客户的最佳实践。 输入姓名、电子邮件地址和其他设置。 选择 **提交** 创建营销渠道界面。 请阅读相关文档 [如何设置电子邮件渠道界面](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### SMS渠道表面

要创建SMS渠道表面，请首先创建SMS API凭据，然后选择首选供应商（例如Sinch）。 命名短信渠道表面（例如，短信营销），选择配置，然后输入发送者号码。 选择 **提交** ，以保存短信渠道界面。 请阅读相关文档 [如何设置短信渠道平面](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=zh-Hans#message-preset-sms).

此外，为包含订单确认等事务性消息的行动手册配置渠道。

### 推送渠道表面

确认已在Experience Platform或数据收藏集界面中配置应用程序表面。 这就是应用程序表面在数据收集环境中的外观。

<!-- ![App surfaces in Data collections](/help/use-case-playbooks/assets/playbooks/get-started/.png) -->

接下来，选择您在应用程序表面配置中查看的渠道、平台和应用程序。 选择 **提交** 创建推送渠道平面。

请阅读相关文档 [如何设置推送渠道平面](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html).

## 后续步骤 {#next-steps}

现在，您已执行本文档中的所有步骤，您应该已使用可在左侧导航栏中找到的用例行动手册创建了一个开发沙盒。 您现在还知道如何授予团队成员查看和管理行动手册以及生成资产所需的权限。 接下来，阅读如何 [了解正确的行动手册](/help/use-case-playbooks/playbooks/discover.md) 对于您和 [从中创建实例](/help/use-case-playbooks/playbooks/create-share-reuse.md).
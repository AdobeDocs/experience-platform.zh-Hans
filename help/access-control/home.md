---
keywords: Experience Platform；主页；热门主题；访问控制；adobe admin console
solution: Experience Platform
title: 访问控制概述
description: Adobe Experience Platform的访问控制是通过Adobe Admin Console提供的。 此功能利用Admin Console中的产品配置文件，它将用户与权限和沙盒关联起来。
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 5d5c57dfb9e4abda6b1bca96147a95d063bc17c6
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 1%

---

# 访问控制概述

Adobe Experience Platform的访问控制是通过[Adobe Experience Cloud](https://experience.adobe.com/)中的&#x200B;**[!UICONTROL 权限]**&#x200B;提供的。 此功能利用角色和策略，将用户与权限和沙盒关联起来。

## 访问控制层级和工作流

要为Experience Platform配置访问控制，您必须对拥有Experience Platform产品的组织具有系统或产品管理员权限。 可以授予或撤销权限的最低角色是产品管理员。 可以管理权限的其他管理员角色是系统管理员（无限制）。 有关详细信息，请参阅有关[管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html)的Adobe Help Center文章。

>[!NOTE]
>
>从此刻起，本文档中对“管理员”的任何提及均指产品管理员或更高版本（如上所述）。

用于获取和分配访问权限的高级工作流可概括如下：

- 在许可Adobe Experience Platform或使用Experience Platform的应用程序/应用程序服务后，会向在许可期间指定的管理员发送一封电子邮件。
- 管理员登录到[Adobe Admin Console](#adobe-admin-console)，并从概述页面的产品列表中选择&#x200B;**Adobe Experience Platform**。
- 要授予对Experience Platform的访问权限，建议管理员将用户添加到默认产品配置文件： `AEP-Default-All-Users`。
- 在“Experience Platform权限”中，管理员可以创建新角色，或编辑任何现有角色的权限和用户。
- 创建或编辑角色时，管理员使用&#x200B;**[!UICONTROL 用户]**&#x200B;选项卡将用户添加到该角色，并通过编辑该角色的权限授予这些用户（如“[!UICONTROL 读取数据集]”或“[!UICONTROL 管理架构]”）的权限。 同样，管理员可以使用相同的编辑选项为沙盒分配访问权限。
- 当用户登录Experience Platform用户界面时，他们对各种Experience Platform功能的访问权限由上一步中授予的权限驱动。 例如，如果用户没有[!UICONTROL 查看数据集]权限，则该用户看不到侧菜单中的&#x200B;**[!UICONTROL 数据集]**&#x200B;选项卡。

有关如何管理Experience Platform中的访问权限的详细步骤，请参阅[访问控制用户指南](./ui/overview.md)。

所有对Experience PlatformAPI的调用都会验证权限，如果在当前用户上下文中未找到相应的权限，则将返回错误。 在UI中，将根据授予当前用户的权限，隐藏或更改元素。

## 权限 {#platform-permissions}

[!UICONTROL 权限]提供了一个中心位置，用于管理组织的Experience Platform访问权限。 通过[!UICONTROL 权限]，您可以授予用户组访问各种Experience Platform功能的权限，例如[!UICONTROL 管理数据集]、[!UICONTROL 查看数据集]或[!UICONTROL 管理配置文件]。

### 角色

在[!UICONTROL 角色]部分中，权限是通过使用角色分配给用户的。 角色允许您向一个或多个用户授予权限，并且还包含他们对通过角色分配给他们的沙盒范围的访问权限。 可以将用户分配给属于您组织的一个或多个角色。

### 默认角色

Experience Platform附带两个预配置的默认角色。 下表概述了每个默认配置文件中提供的内容，包括它们授予访问权限的沙盒以及它们在该沙盒范围内授予的权限。

| 角色 | 沙盒访问 | 权限 |
| --- | --- | --- |
| 默认的生产所有访问权限 | 生产 | 所有适用于Experience Platform的权限，“沙盒管理”权限除外。 |
| 沙盒管理员 | 不适用 | 仅提供对沙盒管理权限的访问。 |

## 沙盒和权限

非生产沙盒是一种数据虚拟化形式，允许您将数据与其他沙盒隔离，通常用于开发实验、测试或试用。 角色的权限允许角色的用户访问他们在被授予访问权限的沙盒环境中的Experience Platform功能。 默认Experience Platform许可证授予您5个沙盒（一个生产沙盒和4个非生产沙盒）。 您可以添加包含10个非生产沙盒的包，最多总共75个沙盒。 有关更多详细信息，请联系贵组织的管理员或您的Adobe销售代表。

有关Experience Platform中沙盒的更多信息，请参阅[沙盒概述](../sandboxes/home.md)。

### 沙盒访问权限

沙盒的访问通过角色进行管理。 有关如何为角色启用对沙盒访问的详细步骤，请参阅[基于属性的访问控制角色指南](./abac/ui/roles.md)。

可以授予用户访问角色中一个或多个沙盒的权限。 如果两个或更多角色中包含一个用户，则该用户将有权访问这些角色中包含的所有沙盒。

“沙盒管理”权限允许用户管理、查看或重置沙盒。

### 资源权限 {#permissions}

角色中的资源[!UICONTROL 权限]选项卡显示对该角色活动的沙盒和权限：

![权限概述](./images/permissions.png)

通过资源权限授予的权限按类别排序，有些权限授予对多个低级功能的访问权限。

下表概述了Experience Platform在角色中可用的权限，并说明了他们授予访问权限的特定Experience Platform功能。 有关如何向角色添加权限的详细步骤，请参阅[基于属性的访问控制角色指南](./abac/ui/roles.md)。

| 类别 | 权限 | 描述 |
| --- | --- | --- |
| [!DNL AI Assistant] | [!UICONTROL 启用AI助手] | 能够向[AI助手](../ai-assistant/access.md)提问。 |
| [!DNL AI Assistant] | [!UICONTROL 查看运营分析] | 访问以获取对[操作分析](../ai-assistant/home.md##operational-insights)查询的响应。 |
| [!DNL Alerts] | [!UICONTROL 查看警报历史记录] | 对警报历史记录的只读访问权限。 |
| [!DNL Alerts] | [!UICONTROL 解决警报] | 有权读取、编辑和删除警报。 |
| [!DNL Alerts] | [!UICONTROL 查看警报] | 警报的只读访问权限。 |
| [!DNL Alerts] | [!UICONTROL 管理警报] | 有权读取、创建、编辑和删除警报历史记录。 |
| [!DNL Computed Attributes] | [!UICONTROL 查看计算属性] | 对计算属性选项卡、库存和详细信息的只读访问权限。 |
| [!DNL Computed Attributes] | [!UICONTROL 管理计算属性] | 有权读取、创建、删除草稿和停用计算属性。 |
| [!DNL Dashboards] | [!UICONTROL 查看许可证使用情况仪表板] | 查看许可证使用情况仪表板的只读访问权限。 |
| [!DNL Dashboards] | [!UICONTROL 管理标准仪表板] | 添加数据仓库中尚未存在的自定义属性。 |
| [!DNL Data Governance] | [!UICONTROL 管理使用标签] | 有权读取、创建和删除使用标签。 |
| [!DNL Data Governance] | [!UICONTROL 管理数据使用策略] | 有权读取、创建、编辑和删除数据使用策略。 |
| [!DNL Data Governance] | [!UICONTROL 查看数据使用策略] | 对属于您组织的数据使用策略的只读访问权限。 |
| [!DNL Data Governance] | [!UICONTROL 查看用户活动日志] | 只读访问权限，用于查看平台活动中记录的[审核日志](../landing/governance-privacy-security/audit-logs/overview.md)。 |
| [!DNL Data Ingestion] | [!UICONTROL 管理源] | 有权读取、创建、编辑和禁用源。 |
| [!DNL Data Ingestion] | [!UICONTROL 查看源] | 对&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡中的可用源以及&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中的已验证源的只读访问权限。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | 创建、接受和拒绝伙伴握手以连接两个组织并启用[!DNL Segment Match]流的访问权限。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | 有权读取、创建、编辑和发布[!DNL Segment Match]活动伙伴信息源。 |
| [!DNL Data Lifecycle] | [!UICONTROL 查看数据生命周期] | 数据生命周期的只读访问。 |
| [!DNL Data Lifecycle] | [!UICONTROL 管理数据生命周期] | 有权读取、创建、编辑和删除数据生命周期。 |
| [!DNL Data Modeling] | [!UICONTROL 管理架构] | 有权读取、创建、编辑和删除架构和相关资源。 |
| [!DNL Data Modeling] | [!UICONTROL 查看架构] | 对架构和相关资源的只读访问权限。 |
| [!DNL Data Modeling] | [!UICONTROL 管理关系] | 有权读取、创建、编辑和删除架构关系。 |
| [!DNL Data Modeling] | [!UICONTROL 管理身份元数据] | 有权读取、创建、编辑和删除架构的身份元数据。 |
| [!DNL Data Management] | [!UICONTROL 管理数据集] | 有权读取、创建、编辑和删除数据集。 架构的只读访问权限。 |
| [!DNL Data Management] | [!UICONTROL 查看数据集] | 对数据集和架构的只读访问权限。 |
| [!DNL Data Management] | [!UICONTROL 数据监视] | 对监控数据集和流的只读访问权限。 |
| [!DNL Data Science Workspace] | [!UICONTROL 管理数据科学Workspace] | 在[!DNL Data Science Workspace]中读取、创建、编辑和删除的权限。 |
| [!DNL Destinations] | [!UICONTROL 查看目标] | 只读访问权限，可查看&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡中的可用目标和&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中的已验证目标。 |
| [!DNL Destinations] | [!UICONTROL 管理目标] | 读取、创建和删除目标连接和目标帐户的权限。 |
| [!DNL Destinations] | [!UICONTROL 激活目标] | 允许用户将区段激活到现有目标。 在激活工作流中启用映射步骤。 此权限还要求向将数据激活到目标的用户授予[!UICONTROL 查看目标]权限。 |
| [!DNL Destinations] | [!UICONTROL 激活没有映射的区段] | 允许用户将区段激活到现有目标，而不显示[映射步骤](../destinations/ui/activate-batch-profile-destinations.md#mapping)。 用户可以在激活工作流中添加和删除区段，但无法添加或删除映射的属性或标识。 此权限还要求向将数据激活到目标的用户授予[!UICONTROL 查看目标]权限。 |
| [!DNL Destinations] | [!UICONTROL 管理和激活数据集目标] | 能够读取、创建、编辑和禁用数据集导出流。 还能将数据激活到已创建的活动数据集。 此权限还要求向将数据激活到目标的用户授予[!UICONTROL 查看目标]权限。 |
| [!DNL Destinations] | [!UICONTROL 目标创作] | 能够使用[Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md)创作目标。 |
| [!DNL Identity Management] | [!UICONTROL 管理身份命名空间] | 读取、创建、编辑和删除身份命名空间的权限。 |
| [!DNL Identity Management] | [!UICONTROL 查看身份命名空间] | 对身份命名空间的只读访问。 |
| [!DNL Identity Management] | [!UICONTROL 查看身份图] | 对标识图的只读访问。 |
| [!DNL Intelligent Services] | [!UICONTROL 查看Attribution AI] | 对Attribution AI设置和分析的只读访问权限。 |
| [!DNL Intelligent Services] | [!UICONTROL 管理Attribution AI] | 有权读取、创建、编辑和删除Attribution AI模型。 |
| [!DNL Intelligent Services] | [!UICONTROL 查看客户人工智能] | 访问读取或查看客户AI模型。 |
| [!DNL Intelligent Services] | [!UICONTROL 管理客户人工智能] | 有权创建、更新、删除、启用或禁用Customer AI模型。 |
| [!DNL Profile Management] | [!UICONTROL 管理配置文件] | 从多个来源摄取数据，为个别客户构建强大的配置文件，并将启用配置文件的数据存储在Data Lake和Real-Time Customer Profile数据存储中。 |
| [!DNL Profile Management] | [!UICONTROL 查看配置文件] | 对可用配置文件的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 管理区段] | 有权读取、创建、编辑和删除区段。 |
| [!DNL Profile Management] | [!UICONTROL 查看区段] | 对可用区段的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 管理合并策略] | 有权读取、创建、编辑和删除合并策略。 |
| [!DNL Profile Management] | [!UICONTROL 查看合并策略] | 对可用合并策略的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 导入受众] | 有权读取、创建、编辑和删除导入的受众。 |
| [!DNL Profile Management] | [!UICONTROL 导出区段的受众] | 能够将评估的受众区段导出到数据集。 |
| [!DNL Profile Management] | [!UICONTROL 评估受众的区段] | 能够通过评估区段定义为受众生成配置文件。 |
| [!DNL Profile Management] | [!UICONTROL 查看B2B AI] | 对所有B2B AI/ML服务的设置和配置的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 管理B2B AI] | 有权读取、创建、编辑和删除所有B2B AI/ML服务的设置和配置。 |
| [!DNL Profile Management] | [!UICONTROL 查看B2B配置文件] | 对B2B实体配置文件（如Account、Opportunity等）、所有B2B AI/ML服务的设置和配置以及B2B仪表板小部件的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 管理B2B配置文件] | 有权读取、创建、编辑和删除B2B实体配置文件（如Account 、 Opportunity等）。 对所有B2B AI/ML服务和B2B仪表板小组件的设置和配置的只读访问权限。 |
| [!DNL Query Service] | [!UICONTROL 管理查询] | 访问Platform数据的读取、创建、编辑和删除结构化SQL查询。 |
| [!DNL Query Service] | [!UICONTROL 管理查询服务集成] | 访问创建、更新和删除未过期的凭据以访问查询服务。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理沙盒] | 访问读取、创建、编辑和删除沙箱。 |
| [!DNL Sandbox Administration] | [!UICONTROL 查看沙盒] | 对属于您组织的沙盒具有只读访问权限。 |
| [!DNL Sandbox Administration] | [!UICONTROL 重置沙盒] | 能够重置沙盒。 |

## 后续步骤

通过阅读本指南，您已经了解了Experience Platform中访问控制的主要原则。 现在，您可以继续阅读[基于属性的访问控制用户指南](./abac/overview.md)，以了解有关如何使用Experience Cloud创建Experience Platform和分配角色的权限的详细步骤。

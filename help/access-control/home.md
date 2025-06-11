---
keywords: Experience Platform；主页；热门主题；访问控制；adobe admin console
solution: Experience Platform
title: 访问控制概述
description: Adobe Experience Platform的访问控制是通过Adobe Admin Console提供的。 此功能利用Admin Console中的产品配置文件，它将用户与权限和沙盒关联起来。
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 6a466770495b226f890ab67b21c5cb027fd46e02
workflow-type: tm+mt
source-wordcount: '3851'
ht-degree: 0%

---

# 访问控制概述

Adobe Experience Platform的访问控制是通过[Adobe Experience Cloud](https://experience.adobe.com/)中的&#x200B;**[!UICONTROL 权限]**&#x200B;提供的。 此功能利用角色和策略，将用户与权限和沙盒关联起来。

## 访问控制层级和工作流

要配置Experience Platform的访问控制，您必须对拥有Experience Platform产品的组织具有系统或产品管理员权限。 可以授予或撤销权限的最低角色是产品管理员。 可以管理权限的其他管理员角色是系统管理员（无限制）。 有关详细信息，请参阅有关[管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html)的Adobe帮助中心文章。

>[!NOTE]
>
>从此刻起，本文档中对“管理员”的任何提及均指产品管理员或更高版本（如上所述）。

用于获取和分配访问权限的高级工作流可概括如下：

- 在许可Adobe Experience Platform或使用Experience Platform的应用程序/应用程序服务后，会向在许可期间指定的管理员发送一封电子邮件。
- 管理员登录到[Adobe Admin Console](#adobe-admin-console)，并从概述页面的产品列表中选择&#x200B;**Adobe Experience Platform**。
- 要授予对Experience Platform的访问权限，建议管理员将用户添加到默认产品配置文件： `AEP-Default-All-Users`。
- 在Experience Platform权限中，管理员可以创建新角色，或编辑任何现有角色的权限和用户。
- 创建或编辑角色时，管理员使用&#x200B;**[!UICONTROL 用户]**&#x200B;选项卡将用户添加到该角色，并通过编辑该角色的权限授予这些用户（如“[!UICONTROL 读取数据集]”或“[!UICONTROL 管理架构]”）的权限。 同样，管理员可以使用相同的编辑选项为沙盒分配访问权限。
- 当用户登录Experience Platform用户界面时，他们对该Experience Platform功能的访问权限由上一步中授予的权限驱动。 例如，如果用户没有[!UICONTROL 查看数据集]权限，则该用户看不到侧菜单中的&#x200B;**[!UICONTROL 数据集]**&#x200B;选项卡。

有关如何在Experience Platform中管理访问权限控制的更多详细步骤，请参阅[访问控制用户指南](./ui/overview.md)。

对Experience Platform API的所有调用均会验证权限，如果在当前用户上下文中未找到相应的权限，则将返回错误。 在UI中，将根据授予当前用户的权限，隐藏或更改元素。

## 权限 {#platform-permissions}

[!UICONTROL 权限]提供了一个中央位置，用于管理贵组织的Experience Platform访问权限。 通过[!UICONTROL 权限]，您可以授予用户组访问各种Experience Platform功能的权限，例如[!UICONTROL 管理数据集]、[!UICONTROL 查看数据集]或[!UICONTROL 管理配置文件]。

### 角色

在[!UICONTROL 角色]部分中，权限是通过使用角色分配给用户的。 角色允许您向一个或多个用户授予权限，并且还包含他们对通过角色分配给他们的沙盒范围的访问权限。 可以将用户分配给属于您组织的一个或多个角色。

### 默认角色

Experience Platform附带两个预配置的默认角色。 下表概述了每个默认配置文件中提供的内容，包括它们授予访问权限的沙盒以及它们在该沙盒范围内授予的权限。

| 角色 | 沙盒访问 | 权限 |
| --- | --- | --- |
| 默认的生产所有访问权限 | Prod | 所有适用于Experience Platform的权限，“沙盒管理”权限除外。 |
| 沙盒管理员 | 不适用 | 提供对`Prod`沙盒的访问权限和沙盒管理权限。 |

## 沙盒和权限

非生产沙盒是一种数据虚拟化形式，允许您将数据与其他沙盒隔离，通常用于开发实验、测试或试用。 角色的权限允许角色的用户在有权访问的沙盒环境中访问Experience Platform功能。 默认的Experience Platform许可证授予您5个沙盒（一个生产沙盒和四个非生产沙盒）。 您可以添加包含10个非生产沙盒的包，最多总共75个沙盒。 有关更多详细信息，请联系贵组织的管理员或Adobe销售代表。

有关Experience Platform中沙盒的更多信息，请参阅[沙盒概述](../sandboxes/home.md)。

### 沙盒访问权限

沙盒的访问通过角色进行管理。 有关如何为角色启用对沙盒访问的详细步骤，请参阅[基于属性的访问控制角色指南](./abac/ui/roles.md)。

可以授予用户访问角色中一个或多个沙盒的权限。 如果两个或更多角色中包含一个用户，则该用户将有权访问这些角色中包含的所有沙盒。

“沙盒管理”权限允许用户管理、查看或重置沙盒。

### 资源权限 {#permissions}

资源权限授予对特定Experience Platform功能的访问权限。 资源分为多个类别，其中包含一组可单独分配给角色的相关权限。

在[!UICONTROL 权限]中，角色的资源工作区显示对该角色有效的沙盒和权限：

![具有选定类别和权限列表的角色的资源工作区。](./images/permissions.png)

下表概述了通过“权限”管理的Experience Platform和应用程序的可用资源类别：

| 类别 | 描述 |
| --- | --- |
| [!DNL Adobe Mix Modeler] | 配置、管理和查看[!DNL Adobe Mix Modeler]的权限。 |
| [!DNL AI Assistant] | 配置[!DNL AI Assistant]的权限。 |
| [!DNL Alerts] | 配置管理、解决和查看警报和警报历史记录的权限。 |
| [!DNL B2B Account Lists] | 配置B2B帐户列表的管理、查看和发布权限，包括从帐户列表中添加、删除、导入和删除帐户等操作。 |
| [!DNL B2B Admin Configurations] | 配置管理和查看B2B管理配置的权限，包括数字资产管理连接、资产存储库和事件。 |
| [!DNL B2B Assets] | 配置B2B资产的管理和查看权限，包括电子邮件、短信、登陆页面、片段、模板和图像。 |
| [!DNL B2B Buying Groups] | 配置B2B购买群组的管理和查看权限，包括解决方案兴趣、角色模板和购买群组状态等功能。 |
| [!DNL B2B Channel Configurations] | 配置B2B渠道配置的管理和查看权限，包括通信限制、API凭据和安全设置等设置。 |
| [!DNL B2B Dashboards] | 配置B2B仪表板的查看权限，包括帐户参与度、购买团体阶段、激增帐户和联系范围等功能。 |
| [!DNL B2B Journeys] | 配置B2B历程的管理、查看和发布权限，包括帐户和人员操作、事件侦听器以及拆分路径等功能。 |
| [!DNL Campaigns] | 在Journey Optimizer中配置营销活动的管理、发布和查看权限。 |
| [!DNL Channel Configurations] | 配置管理、查看和导出渠道配置功能，如子域、IP池、消息预设、PTR记录、禁止列表、登陆页面设置、短信设置和文件路由。 |
| [!DNL Collaborations] | 配置管理和查看对Real-time Customer Data Profile Collaboration功能的权限。 |
| [!DNL Computed Attributes] | 配置对草稿或发布的计算属性的管理和查看权限。 |
| [!DNL Customer Managed Keys] | 配置对客户管理的密钥的管理权限。 |
| [!DNL Dashboards] | 配置对标准、自定义和许可仪表板的管理和查看权限。 |
| [!DNL Data Collection] | 配置管理和查看数据流的权限。 |
| [!DNL Data Governance] | 配置管理、应用和查看数据管理功能（如标签、策略和活动日志）的权限。 |
| [!DNL Data Ingestion] | 配置管理和查看对数据源和受众共享等数据摄取功能的权限。 |
| [!DNL Data Lifecycle] | 配置管理和查看数据卫生功能的权限。 |
| [!DNL Data Management] | 配置管理和查看数据管理功能（如数据集以及监控数据集和流）的权限。 |
| [!DNL Data Modeling] | 配置管理和查看对数据建模功能（如架构、关系和身份元数据）的权限。 |
| [!DNL Data Science Workspace] | 配置[!DNL Data Science Workspace]的管理权限。 |
| [!DNL Decision Management] | 在决策管理中配置管理和查看决策、优惠和排名策略功能的权限。 |
| [!DNL Destinations] | 配置管理和查看目标的权限，包括激活和创作目标SDK等功能。 |
| [!DNL Federated Data] | 配置管理和查看对联合数据功能的权限。 |
| [!DNL Identity Management] | 配置管理和查看对Identity Service功能（如身份命名空间和身份图）的权限。 |
| [!DNL Intelligent Service] | 在智能服务中配置对归因人工智能和客户人工智能的管理和查看权限。 |
| [!DNL IP Warmup Configurations] | 配置管理和查看IP预热计划的权限以及查看IP预热报告的权限。 |
| [!DNL Journey Optimizer Library] | 配置对Adobe Journey Optimizer中的库项目的管理权限。 |
| [!DNL Journey Optimizer Rules] | 在Adobe Journey Optimizer中配置管理和查看频率规则的权限。 |
| [!DNL Journeys] | 配置管理、发布和查看历程的权限，包括历程报告、事件、数据源和操作等功能。 |
| [!DNL Messages] | 配置管理、发布和查看消息的权限，包括消息预览和测试等功能。 |
| [!DNL Privacy Service] | 配置对Privacy Service功能的管理和查看权限。 |
| [!DNL Profile Management] | 配置对配置文件服务功能（如受众、配置文件和合并策略）的管理、查看、导出和评估权限。 |
| [!DNL Prospects] | 配置对潜在客户架构、用户档案和受众的管理和查看权限，包括查看潜在客户折叠面板等功能。 |
| [!DNL Query Service] | 配置管理权限以查询服务功能，如未过期的凭据和结构化SQL查询。 |
| [!DNL Reports] | 配置渠道报表的查看权限。 |
| [!DNL Sandbox Administration] | 管理沙盒时配置管理、查看和重置权限。 |
| [!DNL Traits Configuration] | 通过计算属性UI配置管理和查看特征。 |
| [!DNL Translation Services] | 为项目、任务、审核、内部、设置和提供商配置管理和查看翻译服务的权限。 |

下表概述了Experience Platform在角色中可用的权限，以及这些权限授予访问权限的特定Experience Platform功能的说明。 有关如何向角色添加权限的详细步骤，请参阅[基于属性的访问控制角色指南](./abac/ui/roles.md)。

| 类别 | 权限 | 描述 |
| --- | --- | --- |
| [!DNL Adobe Mix Modeler] | [!UICONTROL 管理Adobe Mix Modeler协调数据] | 查看和修改协调数据的能力。 |
| [!DNL Adobe Mix Modeler] | [!UICONTROL 查看Adobe Mix Modeler协调数据] | 对协调数据的只读访问。 |
| [!DNL Adobe Mix Modeler] | [!UICONTROL 管理Adobe Mix Modeler模型配置] | 查看和修改模型配置的功能。 |
| [!DNL Adobe Mix Modeler] | [!UICONTROL 查看Adobe Mix Modeler模型配置] | 对模型配置的只读访问权限。 |
| [!DNL Adobe Mix Modeler] | [!UICONTROL 管理Adobe Mix Modeler模型计划配置] | 查看和修改计划配置的功能。 |
| [!DNL Adobe Mix Modeler] | [!UICONTROL 查看Adobe Mix Modeler模型计划配置] | 对计划配置的只读访问权限。 |
| [!DNL AI Assistant] | [!UICONTROL 启用AI助手] | 能够询问[[!DNL [AI assistant]]](../ai-assistant/access.md)问题。 |
| [!DNL AI Assistant] | [!UICONTROL 查看运营分析] | 访问以获取对[操作分析](../ai-assistant/home.md##operational-insights)查询的响应。 |
| [!DNL AI Assistant] | [!UICONTROL 生成内容] | 允许用户使用[!DNL AI Assistant]生成内容。 |
| [!DNL AI Assistant] | [!UICONTROL 管理品牌套件] | 允许用户使用[!DNL AI Assistant]创建品牌指南。 |
| [!DNL Alerts] | [!UICONTROL 查看警报历史记录] | 对警报历史记录的只读访问权限。 |
| [!DNL Alerts] | [!UICONTROL 解决警报] | 有权读取、编辑和删除警报。 |
| [!DNL Alerts] | [!UICONTROL 查看警报] | 警报的只读访问权限。 |
| [!DNL Alerts] | [!UICONTROL 管理警报] | 有权读取、创建、编辑和删除警报。 |
| [!DNL B2B Account Lists] | [!UICONTROL 管理B2B帐户列表] | 在左侧导航中查看和访问&#x200B;**[!UICONTROL 帐户列表]**。 有权访问&#x200B;**[!UICONTROL 帐户列表]**&#x200B;的用户应有权访问所有帐户列表CRUD功能： `/accounts-list`。 |
| [!DNL B2B Admin Configurations] | [!UICONTROL 管理B2B管理配置] | 能够在左侧导航中查看和访问&#x200B;**[!UICONTROL B2B管理配置]**。 有权访问&#x200B;**[!UICONTROL B2B管理配置]**&#x200B;的用户应该有权访问所有SMS API凭据CRUD功能： `/admin-configs`。 |
| [!DNL B2B Assets] | [!UICONTROL 管理B2B Assets] | 能够在左侧导航中查看和访问&#x200B;**[!UICONTROL Assets]**。 有权访问&#x200B;**[!UICONTROL Assets]**&#x200B;的用户应有权访问所有Assets CRUD功能： `/assets-listing`。 |
| [!DNL B2B Assets] | [!UICONTROL 管理B2B模板] | 能够在左侧导航中查看和访问&#x200B;**[!UICONTROL 模板]**。 有权访问&#x200B;**[!UICONTROL 模板]**&#x200B;的用户应有权访问所有模板CRUD功能： `/b2b-content-templates`。 |
| [!DNL B2B Assets] | [!UICONTROL 管理B2B片段] | 能够在左侧导航中查看和访问&#x200B;**[!UICONTROL 片段]**。 有权访问&#x200B;**[!UICONTROL 片段]**&#x200B;的用户应有权访问所有片段CRUD函数： `/fragments`。 |
| [!DNL B2B Buying Groups] | [!UICONTROL 管理B2B购买组] | 可在左侧导航栏中查看和访问&#x200B;**[!UICONTROL 购买组]**。 有权访问&#x200B;**[!UICONTROL 购买组]**&#x200B;的用户应有权访问所有购买组CRUD功能： `/buying-groups`。 |
| [!DNL B2B Dashboards] | [!UICONTROL 管理B2B参与仪表板] | 能够在左侧导航中查看和访问&#x200B;**[!UICONTROL 仪表板]**。 有权访问&#x200B;**[!UICONTROL 功能板]**&#x200B;的用户应有权访问所有功能板CRUD功能： `/insights-dashboard`。 |
| [!DNL B2B Channel Configurations] | [!UICONTROL 管理B2B渠道配置] | 能够在左侧导航中查看和访问&#x200B;**[!UICONTROL 通道]**。 有权访问&#x200B;**[!UICONTROL 渠道]**&#x200B;的用户应有权访问所有渠道CRUD功能： `/channels-config`。 |
| [!DNL B2B Journeys] | [!UICONTROL 管理B2B帐户历程] | 能够在左侧导航中查看和访问&#x200B;**[!UICONTROL 帐户历程]**。 有权访问&#x200B;**[!UICONTROL 帐户历程]**&#x200B;的用户应有权访问所有帐户历程CRUD功能： `/account-journeys`。 |
| [!DNL Campaigns] | [!UICONTROL 管理营销活动] | 有权读取、创建、编辑和删除营销活动。 |
| [!DNL Campaigns] | [!UICONTROL 批准和发布营销活动] | 批准和发布活动的功能。 |
| [!DNL Campaigns] | [!UICONTROL 发布营销活动] | 能够发布营销活动。 |
| [!DNL Campaigns] | [!UICONTROL 查看营销活动] | 对营销活动的只读访问权限。 |
| [!DNL Campaigns] | [!UICONTROL 查看营销活动报告] | 对营销活动报表的只读访问权限。 |
| [!DNL Channel Configurations] | [!UICONTROL 查看邮件常规设置] | 对消息常规设置的只读访问权限。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理子域委派] | 有权读取、创建、编辑和删除子域委派。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理IP池] | 有权读取、创建和编辑IP池。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理邮件常规设置] | 访问读取、创建、编辑和删除消息的一般设置。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理邮件预设] | 访问读取、创建、编辑和删除消息预设。 |
| [!DNL Channel Configurations] | [!UICONTROL 查看邮件预设] | 对消息预设的只读访问权限。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理PTR记录] | 读取和编辑PTR记录的权限。 |
| [!DNL Channel Configurations] | [!UICONTROL 查看PTR记录] | 对PTR记录的只读访问权限。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理禁止显示] | 有权读取、创建、编辑和删除禁止显示规则。 |
| [!DNL Channel Configurations] | [!UICONTROL 查看禁止显示列表] | 对禁止显示列表的只读访问权限。 |
| [!DNL Channel Configurations] | [!UICONTROL 导出禁止显示列表] | 将禁止列表导出为CSV文件的权限。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理登陆页面设置] | 有权读取、创建、编辑和删除登陆页面设置。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理短信设置] | 有权读取、创建、编辑和删除短信设置。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理SMS子域] | 访问读取、创建、编辑和删除短信子域。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理文件路由] | 有权读取、创建、编辑和删除文件工艺路线。 |
| [!DNL Channel Configurations] | [!UICONTROL 查看文件路由] | 对文件路由的只读访问权限。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理种子列表] | 创建和编辑Seedlist的功能。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理语言设置] | 创建和编辑语言设置的功能。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理Web子域] | 创建和编辑CJM Web子域的功能。 |
| [!DNL Channel Configurations] | [!UICONTROL 管理推送凭据] | 创建、编辑和删除推送凭据的功能。 |
| [!DNL Collaborations] | [!UICONTROL 管理Collaboration实例] | 查看、创建、更新和删除组织的协作实例。 发现其他组织的协作实例。 |
| [!DNL Collaborations] | [!UICONTROL 读取Collaboration实例] | 读取组织的协作实例并发现其他组织的协作实例。 |
| [!DNL Collaborations] | [!UICONTROL 管理连接邀请] | 查看、创建和删除您的组织发起的连接邀请。 接受和拒绝其他组织发起的连接邀请。 |
| [!DNL Collaborations] | [!UICONTROL 读取连接邀请] | 对连接邀请的只读访问权限。 |
| [!DNL Collaborations] | [!UICONTROL 管理Collaboration连接] | 广告商可以查看、创建和更新设置，以及提交和删除连接。 发布者可以查看、接受或拒绝连接。 |
| [!DNL Collaborations] | [!UICONTROL 读取Collaboration连接] | 对连接的只读访问权限。 |
| [!DNL Collaborations] | [!UICONTROL 管理受众数据] | 载入和发现受众。 更新公共、私有和自定义受众，并管理受众清单元数据设置。 |
| [!DNL Collaborations] | [!UICONTROL 读取受众数据] | 阅读和发现受众。 |
| [!DNL Collaborations] | [!UICONTROL 管理测量数据] | 载入、更新和删除测量数据。 |
| [!DNL Collaborations] | [!UICONTROL 读取测量数据] | 对测量数据的只读访问权限。 |
| [!DNL Collaborations] | [!UICONTROL 管理项目] | 查看、创建、更新和删除任何发现、共享、激活和测量活动的项目。 |
| [!DNL Collaborations] | [!UICONTROL 读取项目] | 查看任何发现、共享、激活和测量活动的项目。 |
| [!DNL Collaborations] | [!UICONTROL 读取用户活动] | 对用户活动的只读访问权限。 |
| [!DNL Collaborations] | [!UICONTROL 导出用户活动] | 导出用户活动。 |
| [!DNL Collaborations] | [!UICONTROL 读取Collaboration信用监控] | 组织和实例层的信用监控。 |
| [!DNL Computed Attributes] | [!UICONTROL 查看计算属性] | 对计算属性选项卡、库存和详细信息的只读访问权限。 |
| [!DNL Computed Attributes] | [!UICONTROL 管理计算属性] | 有权读取、创建、删除草稿和停用计算属性。 |
| [!DNL Customer Managed Keys] | [!UICONTROL 管理客户管理的密钥] | 查看和配置客户管理的密钥的访问权限。 |
| [!DNL Dashboards] | [!UICONTROL 查看许可证使用情况仪表板] | 查看许可证使用情况仪表板的只读访问权限。 |
| [!DNL Dashboards] | [!UICONTROL 管理标准仪表板] | 添加数据仓库中尚未存在的自定义属性。 |
| [!DNL Dashboards] | [!UICONTROL 查看标准仪表板] | 对“配置文件”、“目标”和“区段”功能板的只读访问权限。 还支持在左侧导航和“功能板清单和集成”选项卡中访问功能板。 |
| [!DNL Dashboards] | [!UICONTROL 管理自定义仪表板] | 创建或编辑功能板的权限。 |
| [!DNL Dashboards] | [!UICONTROL 查看自定义仪表板] | 对用户定义仪表板的只读访问权限。 |
| [!DNL Dashboards] | [!UICONTROL 管理报告计划] | 能够创建时间表。 |
| [!DNL Dashboards] | [!UICONTROL 导出仪表板数据] | 控制用户从查询专业模式仪表板导出表格数据的能力。 |
| [!DNL Data Collection] | [!UICONTROL 管理数据流] | 访问读取、创建和编辑数据流。 |
| [!DNL Data Collection] | [!UICONTROL 查看数据流] | 对数据流的只读访问权限。 |
| [!DNL Data Governance] | [!UICONTROL 管理使用标签] | 有权读取、创建和删除使用标签。 |
| [!DNL Data Governance] | [!UICONTROL 管理数据使用策略] | 有权读取、创建、编辑和删除数据使用策略。 |
| [!DNL Data Governance] | [!UICONTROL 查看数据使用策略] | 对属于您组织的数据使用策略的只读访问权限。 |
| [!DNL Data Governance] | [!UICONTROL 查看用户活动日志] | 只读访问权限，可查看Experience Platform活动中记录的[审核日志](../landing/governance-privacy-security/audit-logs/overview.md)。 |
| [!DNL Data Governance] | [!UICONTROL 查看隐私控制台] | 对隐私控制台的只读访问权限。 |
| [!DNL Data Ingestion] | [!UICONTROL 管理源] | 有权读取、创建、编辑和禁用源。 |
| [!DNL Data Ingestion] | [!UICONTROL 查看源] | 对&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡中的可用源以及&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中的已验证源的只读访问权限。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | 创建、接受和拒绝合作伙伴共享以连接两个组织并启用[!DNL Segment Match]流的权限。 |
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
| [!DNL Decision Management] | [!UICONTROL 管理Experience Decisioning] | 能够管理Experience Decisioning实体。 |
| [!DNL Decision Management] | [!UICONTROL 查看Experience Decisioning] | 对Experience Decisioning实体的只读访问权限。 |
| [!DNL Decision Management] | [!UICONTROL 管理决策] | 有权读取、创建、编辑和删除决策实体。 |
| [!DNL Decisions Management] | [!UICONTROL 查看决策] | 对决策实体的只读访问权限。 |
| [!DNL Decision Management] | [!UICONTROL 管理优惠] | 有权读取、创建、编辑和删除所有选件和组件。 对决策和收藏集的只读访问权限。 |
| [!DNL Decsion Management] | [!UICONTROL 管理排名策略] | 有权读取、创建、编辑和删除自定义报告并使用操作功能。 |
| [!DNL Destinations] | [!UICONTROL 查看目标] | 只读访问权限，可查看&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡中的可用目标和&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中的已验证目标。 |
| [!DNL Destinations] | [!UICONTROL 管理目标] | 有权读取、创建和删除目标连接和目标帐户。 |
| [!DNL Destinations] | [!UICONTROL 激活目标] | 能够将数据激活到已创建的活动目标。 此权限还要求将[!UICONTROL 查看目标]或[!UICONTROL 管理目标]授予将激活目标的用户。 |
| [!DNL Destinations] | [!UICONTROL 激活没有映射的区段] | 能够将受众激活到现有目标，而不显示[映射步骤](../destinations/ui/activate-batch-profile-destinations.md#mapping)。 用户可以在激活工作流中添加和删除受众，但无法添加或删除映射的属性或身份。 此权限还要求向将数据激活到目标的用户授予[!UICONTROL 查看目标]权限。 |
| [!DNL Destinations] | [!UICONTROL 管理和激活数据集目标] | 能够读取、创建、编辑和禁用数据集导出流。 还能将数据激活到已创建的活动数据集。 此权限还要求向将数据激活到目标的用户授予[!UICONTROL 查看目标]权限。 |
| [!DNL Destinations] | [!UICONTROL 目标创作] | 能够使用[Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md)创作目标。 |
| [!DNL Federated Data] | [!UICONTROL 管理联合数据] | 访问所有联合数据功能（如创建架构、模型和组合）的能力。 |
| [!DNL Identity Management] | [!UICONTROL 管理身份命名空间] | 读取、创建、编辑和删除身份命名空间的权限。 |
| [!DNL Identity Management] | [!UICONTROL 查看身份命名空间] | 对身份命名空间的只读访问。 |
| [!DNL Identity Management] | [!UICONTROL 查看身份图] | 对标识图的只读访问。 |
| [!DNL Identity Management] | [!UICONTROL 管理身份设置] | 访问读取、创建和编辑身份设置。 |
| [!DNL Identity Management] | [!UICONTROL 查看身份设置] | 对身份设置的只读访问权限。 |
| [!DNL Intelligent Services] | [!UICONTROL 查看归因人工智能] | 对Attribution AI设置和分析的只读访问权限。 |
| [!DNL Intelligent Services] | [!UICONTROL 管理归因人工智能] | 有权读取、创建、编辑和删除归因人工智能模型。 |
| [!DNL Intelligent Services] | [!UICONTROL 查看客户人工智能] | 访问读取或查看客户AI模型。 |
| [!DNL Intelligent Services] | [!UICONTROL 管理客户人工智能] | 有权创建、更新、删除、启用或禁用Customer AI模型。 |
| [!DNL IP Warmup Configurations] | [!UICONTROL 查看IP预热计划] | 对IP预热计划的只读访问权限。 |
| [!DNL IP Warmup Configurations] | [!UICONTROL 管理IP预热计划] | 能够管理IP预热计划。 |
| [!DNL IP Warmup Configurations] | [!UICONTROL 查看IP预热报告] | 对IP预热报告的只读访问权限。 |
| [!DNL Journeys] | [!UICONTROL 管理历程] | 有权读取、创建、编辑和删除历程。 |
| [!DNL Journeys] | [!UICONTROL 查看历程] | 对历程的只读访问权限。 |
| [!DNL Journeys] | [!UICONTROL 查看历程报表] | 对历程报告的只读访问权限。 |
| [!DNL Journeys] | [!UICONTROL 管理历程事件、数据源和操作] | 有权读取、创建、编辑和删除事件、数据源或操作。 |
| [!DNL Journeys] | [!UICONTROL 查看历程事件、数据源和操作] | 对事件、数据源或操作的只读访问权限。 |
| [!DNL Journeys] | [!UICONTROL 批准和发布历程] | 在应用策略时批准和发布历程的功能。 |
| [!DNL Journeys] | [!UICONTROL 发布历程] | 发布历程的功能。 |
| [!DNL Journey Optimizer Library] | [!UICONTROL 管理库项目] | 添加和删除已保存表达式的功能。 |
| [!DNL Journey Optimizer Library] | [!UICONTROL 发布片段] | 发布内容片段的功能。 |
| [!DNL Journey Optimizer Library] | [!UICONTROL 模拟内容] | 访问用于预览和校样的模拟内容选项。 |
| [!DNL Journey Optimizer Rules] | [!UICONTROL 查看频率规则] | 对频率规则的只读访问权限。 |
| [!DNL Journey Optimizer Rules] | [!UICONTROL 管理频率规则] | 有权读取、创建、编辑或删除频率规则。 |
| [!DNL Messages] | [!UICONTROL 管理邮件] | 读取、创建、编辑和删除消息的权限。 |
| [!DNL Messages] | [!UICONTROL 查看邮件] | 对消息的只读访问权限。 |
| [!DNL Messages] | [!UICONTROL 查看邮件报告] | 具有读取和编辑消息报表的权限。 |
| [!DNL Messages] | [!UICONTROL 发布消息] | 能够发布消息。 |
| [!DNL Messages] | [!UICONTROL 管理邮件预览和测试] | 在应用策略时批准和发布消息的功能。 |
| [!DNL Privacy Service] | [!UICONTROL 管理Privacy Service] | 访问读取和写入隐私工作流。 |
| [!DNL Privacy Service] | [!UICONTROL 查看Privacy Service] | 对隐私工作流的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 管理配置文件] | 有权读取、创建、编辑和删除用于客户配置文件的数据集。 对可用配置文件的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 查看配置文件] | 对可用配置文件的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 管理区段] | 有权读取、创建、编辑和删除受众。 |
| [!DNL Profile Management] | [!UICONTROL 查看区段] | 对可用受众的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 管理合并策略] | 有权读取、创建、编辑和删除合并策略。 |
| [!DNL Profile Management] | [!UICONTROL 查看合并策略] | 对可用合并策略的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 导入受众] | 能够使用CSV上传工作流导入新受众。 |
| [!DNL Profile Management] | [!UICONTROL 导出受众区段] | 能够将计算的受众导出到数据集。 |
| [!DNL Profile Management] | [!UICONTROL 评估受众的区段] | 能够通过评估区段定义为受众生成配置文件。 |
| [!DNL Profile Management] | [!UICONTROL 查看B2B AI] | 对所有B2B AI/ML服务的设置和配置的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 管理B2B AI] | 有权读取、创建、编辑和删除所有B2B AI/ML服务的设置和配置。 |
| [!DNL Profile Management] | [!UICONTROL 查看B2B配置文件] | 对B2B实体配置文件（如Account、Opportunity等）、所有B2B AI/ML服务的设置和配置以及B2B仪表板小部件的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 管理B2B配置文件] | 有权读取、创建、编辑和删除B2B实体配置文件（如Account 、 Opportunity等）。 对所有B2B AI/ML服务和B2B仪表板小组件的设置和配置的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 管理Lookalikes] | 能够创建或删除相似受众。 |
| [!DNL Profile Management] | [!UICONTROL 查看B2B体验] | 能够查看B2B配置文件和属性。 |
| [!DNL Profile Management] | [!UICONTROL 查看配置文件设置] | 对所有配置文件设置的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 管理配置文件设置] | 有权读取和编辑所有配置文件设置。 |
| [!DNL Prospects] | [!UICONTROL 查看潜在客户] | 对潜在客户架构、用户档案、受众和潜在客户折叠面板的只读访问权限。 |
| [!DNL Prospects] | [!UICONTROL 管理潜在客户] | 能够创建和管理潜在客户架构、用户档案和受众。 对潜在客户折叠的只读访问权限。 |
| [!DNL Query Service] | [!UICONTROL 管理查询] | 有权读取、创建、编辑和删除Experience Platform数据的结构化SQL查询。 |
| [!DNL Query Service] | [!UICONTROL 管理查询服务集成] | 访问创建、更新和删除未过期的凭据以访问查询服务。 |
| [!DNL Query Service] | [!UICONTROL 管理查询会话] | 能够逐出现有会议。 |
| [!DNL Query Service] | [!UICONTROL 管理允许列表] | 能够管理组织的IP限制。 |
| [!DNL Reports] | [!UICONTROL 查看渠道报表] | 查看和修改渠道报表的功能。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理沙盒] | 访问读取、创建、编辑和删除沙箱。 |
| [!DNL Sandbox Administration] | [!UICONTROL 查看沙盒] | 对属于您组织的沙盒具有只读访问权限。 |
| [!DNL Sandbox Administration] | [!UICONTROL 重置沙盒] | 能够重置沙盒。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理包] | 创建、导入或导出资源包的权限。 |
| [!DNL Sandbox Administration] | [!UICONTROL 共享包] | 跨不同组织共享包的访问权限。 |
| [!DNL Traits Configurations] | [!UICONTROL 查看特征] | 特征的只读访问权限。 |
| [!DNL Traits Configurations] | [!UICONTROL 管理特征] | 管理特征的访问权限。 |
| [!DNL Translation Service] | [!UICONTROL 管理翻译项目] | 管理翻译项目的功能。 |
| [!DNL Translation Service] | [!UICONTROL 查看翻译项目] | 对翻译项目的只读访问权限。 |
| [!DNL Translation Service] | [!UICONTROL 管理翻译任务] | 管理翻译任务的能力。 |
| [!DNL Translation Service] | [!UICONTROL 查看翻译任务] | 对翻译任务的只读访问权限。 |
| [!DNL Translation Service] | [!UICONTROL 管理翻译评论] | 管理翻译审阅的功能。 |
| [!DNL Translation Service] | [!UICONTROL 查看翻译评论] | 对翻译审阅的只读访问权限。 |
| [!DNL Translation Service] | [!UICONTROL 内部管理翻译] | 能够在内部管理翻译。 |
| [!DNL Translation Service] | [!UICONTROL 查看内部翻译] | 内部翻译的只读访问权限。 |
| [!DNL Translation Service] | [!UICONTROL 管理翻译设置] | 管理员管理翻译设置的功能。 |
| [!DNL Translation Service] | [!UICONTROL 管理翻译提供商] | 能够管理翻译提供商。 |

## 后续步骤

通过阅读本指南，您已了解Experience Platform中的访问控制的主要原则。 您现在可以继续阅读[基于属性的访问控制用户指南](./abac/overview.md)，以了解有关如何使用Experience Cloud为Experience Platform创建角色和分配权限的详细步骤。

---
keywords: Experience Platform；主页；热门主题；访问控制；adobe admin console
solution: Experience Platform
title: 访问控制概述
description: Adobe Experience Platform的访问控制是通过Adobe Admin Console提供的。 此功能利用Admin Console中的产品配置文件，它将用户与权限和沙盒关联起来。
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '3279'
ht-degree: 0%

---

# 访问控制概述

Adobe Experience Platform的访问控制是通过&#x200B;**[!UICONTROL Permissions]** Adobe Experience Cloud[中的](https://experience.adobe.com/)提供的。 此功能利用角色和策略，将用户与权限和沙盒关联起来。

## 访问控制层级和工作流

要配置Experience Platform的访问控制，您必须对拥有Experience Platform产品的组织具有系统或产品管理员权限。 可以授予或撤销权限的最低角色是产品管理员。 可以管理权限的其他管理员角色是系统管理员（无限制）。 有关详细信息，请参阅有关[管理角色](https://helpx.adobe.com/cn/enterprise/using/admin-roles.html)的Adobe帮助中心文章。

>[!NOTE]
>
>从此刻起，本文档中对“管理员”的任何提及均指产品管理员或更高版本（如上所述）。

用于获取和分配访问权限的高级工作流可概括如下：

- 在许可Adobe Experience Platform或使用Experience Platform的应用程序/应用程序服务后，会向在许可期间指定的管理员发送一封电子邮件。
- 管理员登录到[Adobe Admin Console](#adobe-admin-console)，并从概述页面的产品列表中选择&#x200B;**Adobe Experience Platform**。
- 要授予对Experience Platform的访问权限，建议管理员将用户添加到默认产品配置文件： `AEP-Default-All-Users`。
- 在Experience Platform权限中，管理员可以创建新角色，或编辑任何现有角色的权限和用户。
- 创建或编辑角色时，管理员使用&#x200B;**[!UICONTROL users]**&#x200B;选项卡将用户添加到角色，并通过编辑角色的权限授予这些用户（如“[!UICONTROL Read Datasets]”或“[!UICONTROL Manage Schemas]”）的权限。 同样，管理员可以使用相同的编辑选项为沙盒分配访问权限。
- 当用户登录Experience Platform用户界面时，他们对该Experience Platform功能的访问权限由上一步中授予的权限驱动。 例如，如果用户没有[!UICONTROL View Datasets]权限，则该用户看不到侧菜单中的&#x200B;**[!UICONTROL Datasets]**&#x200B;选项卡。

有关如何在Experience Platform中管理访问权限控制的更多详细步骤，请参阅[访问控制用户指南](./ui/overview.md)。

对Experience Platform API的所有调用均会验证权限，如果在当前用户上下文中未找到相应的权限，则将返回错误。 在UI中，将根据授予当前用户的权限，隐藏或更改元素。

## 权限 {#platform-permissions}

[!UICONTROL Permissions]提供了一个中心位置，用于管理贵组织的Experience Platform访问权限。 通过[!UICONTROL Permissions]，您可以授予用户组对各种Experience Platform功能（如[!UICONTROL Manage Datasets]、[!UICONTROL View Datasets]或[!UICONTROL Manage Profiles]）的访问权限。

### 角色

在[!UICONTROL Roles]部分中，权限是通过使用角色分配给用户的。 角色允许您向一个或多个用户授予权限，并且还包含他们对通过角色分配给他们的沙盒范围的访问权限。 可以将用户分配给属于您组织的一个或多个角色。

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

在[!UICONTROL Permissions]中，角色的资源工作区显示对该角色有效的沙盒和权限：

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
| [!DNL Run and Operate] | 为运行和操作功能（如运行状况检查和作业计划）配置查看权限。 |
| [!DNL Sandbox Administration] | 管理沙盒时配置管理、查看和重置权限。 |
| [!DNL Traits Configuration] | 通过计算属性UI配置管理和查看特征。 |
| [!DNL Translation Services] | 为项目、任务、审核、内部、设置和提供商配置管理和查看翻译服务的权限。 |

下表概述了Experience Platform在角色中可用的权限，以及这些权限授予访问权限的特定Experience Platform功能的说明。 有关如何向角色添加权限的详细步骤，请参阅[基于属性的访问控制角色指南](./abac/ui/roles.md)。

| 类别 | 权限 | 描述 |
| --- | --- | --- |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Harmonized Data] | 查看和修改协调数据的能力。 |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Harmonized Data] | 对协调数据的只读访问。 |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Models Configurations] | 查看和修改模型配置的功能。 |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Models Configurations] | 对模型配置的只读访问权限。 |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Models Plans Configurations] | 查看和修改计划配置的功能。 |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Models Plans Configurations] | 对计划配置的只读访问权限。 |
| [!DNL AI Assistant] | [!UICONTROL Enable AI Assistant] | 能够询问[[!DNL [AI assistant]]](../ai-assistant/access.md)问题。 |
| [!DNL AI Assistant] | [!UICONTROL View Operational Insights] | 访问以获取对[操作分析](../ai-assistant/home.md##operational-insights)查询的响应。 |
| [!DNL AI Assistant] | [!UICONTROL Generate Content] | 允许用户使用[!DNL AI Assistant]生成内容。 |
| [!DNL AI Assistant] | [!UICONTROL Manage Brand Kit] | 允许用户使用[!DNL AI Assistant]创建品牌指南。 |
| [!DNL Alerts] | [!UICONTROL View Alerts History] | 对警报历史记录的只读访问权限。 |
| [!DNL Alerts] | [!UICONTROL Resolve Alerts] | 有权读取、编辑和删除警报。 |
| [!DNL Alerts] | [!UICONTROL View Alerts] | 警报的只读访问权限。 |
| [!DNL Alerts] | [!UICONTROL Manage Alerts] | 有权读取、创建、编辑和删除警报。 |
| [!DNL B2B Account Lists] | [!UICONTROL Manage B2B Account Lists] | 能够在左侧导航中查看和访问&#x200B;**[!UICONTROL Account Lists]**。 有权访问&#x200B;**[!UICONTROL Account Lists]**&#x200B;的用户应有权访问所有帐户列表CRUD功能： `/accounts-list`。 |
| [!DNL B2B Admin Configurations] | [!UICONTROL Manage B2B Admin Configurations] | 能够在左侧导航中查看和访问&#x200B;**[!UICONTROL B2B Admin Configurations]**。 有权访问&#x200B;**[!UICONTROL B2B Admin Configurations]**&#x200B;的用户应有权访问所有SMS API凭据CRUD功能： `/admin-configs`。 |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Assets] | 能够在左侧导航中查看和访问&#x200B;**[!UICONTROL Assets]**。 有权访问&#x200B;**[!UICONTROL Assets]**&#x200B;的用户应有权访问所有Assets CRUD功能： `/assets-listing`。 |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Templates] | 能够在左侧导航中查看和访问&#x200B;**[!UICONTROL Templates]**。 有权访问&#x200B;**[!UICONTROL Templates]**&#x200B;的用户应有权访问所有模板CRUD功能： `/b2b-content-templates`。 |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Fragments] | 能够在左侧导航中查看和访问&#x200B;**[!UICONTROL Fragments]**。 有权访问&#x200B;**[!UICONTROL Fragments]**&#x200B;的用户应有权访问所有片段CRUD函数： `/fragments`。 |
| [!DNL B2B Buying Groups] | [!UICONTROL Manage B2B Buying Groups] | 能够在左侧导航中查看和访问&#x200B;**[!UICONTROL Buying Groups]**。 有权访问&#x200B;**[!UICONTROL Buying Groups]**&#x200B;的用户应有权访问所有购买组CRUD功能： `/buying-groups`。 |
| [!DNL B2B Dashboards] | [!UICONTROL Manage B2B Engagement Dashboards] | 能够在左侧导航中查看和访问&#x200B;**[!UICONTROL Dashboard]**。 有权访问&#x200B;**[!UICONTROL Dashboards]**&#x200B;的用户应有权访问所有功能板CRUD功能： `/insights-dashboard`。 |
| [!DNL B2B Channel Configurations] | [!UICONTROL Manage B2B Channels Configurations] | 能够在左侧导航中查看和访问&#x200B;**[!UICONTROL Channels]**。 有权访问&#x200B;**[!UICONTROL Channels]**&#x200B;的用户应有权访问所有渠道CRUD功能： `/channels-config`。 |
| [!DNL B2B Journeys] | [!UICONTROL Manage B2B Account Journeys] | 能够在左侧导航中查看和访问&#x200B;**[!UICONTROL Account Journeys]**。 有权访问&#x200B;**[!UICONTROL Account Journeys]**&#x200B;的用户应有权访问所有帐户历程CRUD功能： `/account-journeys`。 |
| [!DNL Campaigns] | [!UICONTROL Manage Campaigns] | 有权读取、创建、编辑和删除营销活动。 |
| [!DNL Campaigns] | [!UICONTROL Approve and Publish Campaigns] | 批准和发布活动的功能。 |
| [!DNL Campaigns] | [!UICONTROL Publish Campaigns] | 能够发布营销活动。 |
| [!DNL Campaigns] | [!UICONTROL View Campaigns] | 对营销活动的只读访问权限。 |
| [!DNL Campaigns] | [!UICONTROL View Campaigns Report] | 对营销活动报表的只读访问权限。 |
| [!DNL Channel Configurations] | [!UICONTROL View Messages General Settings] | 对消息常规设置的只读访问权限。 |
| [!DNL Channel Configurations] | [!UICONTROL Manage Subdomains Delegations] | 有权读取、创建、编辑和删除子域委派。 |
| [!DNL Channel Configurations] | [!UICONTROL Manage IP Pools] | 有权读取、创建和编辑IP池。 |
| [!DNL Channel Configurations] | [!UICONTROL Manage Messages General Settings] | 访问读取、创建、编辑和删除消息的一般设置。 |
| [!DNL Channel Configurations] | [!UICONTROL Manage Messages Presets] | 访问读取、创建、编辑和删除消息预设。 |
| [!DNL Channel Configurations] | [!UICONTROL View Messages Presets] | 对消息预设的只读访问权限。 |
| [!DNL Channel Configurations] | [!UICONTROL Manage PTR Records] | 读取和编辑PTR记录的权限。 |
| [!DNL Channel Configurations] | [!UICONTROL View PTR Records] | 对PTR记录的只读访问权限。 |
| [!DNL Channel Configurations] | [!UICONTROL Manage Suppression] | 有权读取、创建、编辑和删除禁止显示规则。 |
| [!DNL Channel Configurations] | [!UICONTROL View Suppression List] | 对禁止显示列表的只读访问权限。 |
| [!DNL Channel Configurations] | [!UICONTROL Export Suppression List] | 将禁止列表导出为CSV文件的权限。 |
| [!DNL Channel Configurations] | [!UICONTROL Manage Landing Page Settings] | 有权读取、创建、编辑和删除登陆页面设置。 |
| [!DNL Channel Configurations] | [!UICONTROL Manage SMS Settings] | 有权读取、创建、编辑和删除短信设置。 |
| [!DNL Channel Configurations] | [!UICONTROL Manage SMS Subdomains] | 访问读取、创建、编辑和删除短信子域。 |
| [!DNL Channel Configurations] | [!UICONTROL Manage File Routing] | 有权读取、创建、编辑和删除文件工艺路线。 |
| [!DNL Channel Configurations] | [!UICONTROL View File Routing] | 对文件路由的只读访问权限。 |
| [!DNL Channel Configurations] | [!UICONTROL Manage Seedlist] | 创建和编辑Seedlist的功能。 |
| [!DNL Channel Configurations] | [!UICONTROL Manage Language Settings] | 创建和编辑语言设置的功能。 |
| [!DNL Channel Configurations] | [!UICONTROL Manage Web Subdomains] | 创建和编辑CJM Web子域的功能。 |
| [!DNL Channel Configurations] | [!UICONTROL Manage Push Credentials] | 创建、编辑和删除推送凭据的功能。 |
| [!DNL Collaborations] | [!UICONTROL Manage Collaboration Instances] | 查看、创建、更新和删除组织的协作实例。 发现其他组织的协作实例。 |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Instances] | 读取组织的协作实例并发现其他组织的协作实例。 |
| [!DNL Collaborations] | [!UICONTROL Manage Connection Invites] | 查看、创建和删除您的组织发起的连接邀请。 接受和拒绝其他组织发起的连接邀请。 |
| [!DNL Collaborations] | [!UICONTROL Read Connection Invites] | 对连接邀请的只读访问权限。 |
| [!DNL Collaborations] | [!UICONTROL Manage Collaboration Connections] | 广告商可以查看、创建和更新设置，以及提交和删除连接。 发布者可以查看、接受或拒绝连接。 |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Connections] | 对连接的只读访问权限。 |
| [!DNL Collaborations] | [!UICONTROL Manage Audience Data] | 载入和发现受众。 更新公共、私有和自定义受众，并管理受众清单元数据设置。 |
| [!DNL Collaborations] | [!UICONTROL Read Audience Data] | 阅读和发现受众。 |
| [!DNL Collaborations] | [!UICONTROL Manage Measurement Data] | 载入、更新和删除测量数据。 |
| [!DNL Collaborations] | [!UICONTROL Read Measurement Data] | 对测量数据的只读访问权限。 |
| [!DNL Collaborations] | [!UICONTROL Manage Projects] | 查看、创建、更新和删除任何发现、共享、激活和测量活动的项目。 |
| [!DNL Collaborations] | [!UICONTROL Read Projects] | 查看任何发现、共享、激活和测量活动的项目。 |
| [!DNL Collaborations] | [!UICONTROL Read User Activities] | 对用户活动的只读访问权限。 |
| [!DNL Collaborations] | [!UICONTROL Export User Activities] | 导出用户活动。 |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Credit Monitoring] | 组织和实例层的信用监控。 |
| [!DNL Computed Attributes] | [!UICONTROL View Computed attributes] | 对计算属性选项卡、库存和详细信息的只读访问权限。 |
| [!DNL Computed Attributes] | [!UICONTROL Manage Computed attributes] | 有权读取、创建、删除草稿和停用计算属性。 |
| [!DNL Customer Managed Keys] | [!UICONTROL Manage Customer Managed Keys] | 查看和配置客户管理的密钥的访问权限。 |
| [!DNL Dashboards] | [!UICONTROL View License Usage Dashboard] | 查看许可证使用情况仪表板的只读访问权限。 |
| [!DNL Dashboards] | [!UICONTROL Manage Standard Dashboards] | 添加数据仓库中尚未存在的自定义属性。 |
| [!DNL Dashboards] | [!UICONTROL View Standard Dashboards] | 对“配置文件”、“目标”和“区段”功能板的只读访问权限。 还支持在左侧导航和“功能板清单和集成”选项卡中访问功能板。 |
| [!DNL Dashboards] | [!UICONTROL Manage Custom Dashboards] | 创建或编辑功能板的权限。 |
| [!DNL Dashboards] | [!UICONTROL View Custom Dashboards] | 对用户定义仪表板的只读访问权限。 |
| [!DNL Dashboards] | [!UICONTROL Manage Report Schedules] | 能够创建时间表。 |
| [!DNL Dashboards] | [!UICONTROL Export Dashboard Data] | 控制用户从查询专业模式仪表板导出表格数据的能力。 |
| [!DNL Data Collection] | [!UICONTROL Manage Datastreams] | 访问读取、创建和编辑数据流。 |
| [!DNL Data Collection] | [!UICONTROL View Datastreams] | 对数据流的只读访问权限。 |
| [!DNL Data Governance] | [!UICONTROL Manage Usage Labels] | 有权读取、创建和删除使用标签。 |
| [!DNL Data Governance] | [!UICONTROL Manage Data Usage Policies] | 有权读取、创建、编辑和删除数据使用策略。 |
| [!DNL Data Governance] | [!UICONTROL View Data Usage Policies] | 对属于您组织的数据使用策略的只读访问权限。 |
| [!DNL Data Governance] | [!UICONTROL View User Activity Log] | 只读访问权限，可查看Experience Platform活动中记录的[审核日志](../landing/governance-privacy-security/audit-logs/overview.md)。 |
| [!DNL Data Governance] | [!UICONTROL View Privacy Console] | 对隐私控制台的只读访问权限。 |
| [!DNL Data Ingestion] | [!UICONTROL Manage Sources] | 有权读取、创建、编辑和禁用源。 |
| [!DNL Data Ingestion] | [!UICONTROL View Sources] | 对&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡中的可用源和&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡中的已验证源的只读访问权限。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | 创建、接受和拒绝合作伙伴共享以连接两个组织并启用[!DNL Segment Match]流的权限。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | 有权读取、创建、编辑和发布[!DNL Segment Match]活动伙伴信息源。 |
| [!DNL Data Lifecycle] | [!UICONTROL View Data Lifecycle] | 数据生命周期的只读访问。 |
| [!DNL Data Lifecycle] | [!UICONTROL Manage Data Lifecycle] | 有权读取、创建、编辑和删除数据生命周期。 |
| [!DNL Data Modeling] | [!UICONTROL Manage Schemas] | 有权读取、创建、编辑和删除架构和相关资源。 |
| [!DNL Data Modeling] | [!UICONTROL View Schemas] | 对架构和相关资源的只读访问权限。 |
| [!DNL Data Modeling] | [!UICONTROL Manage Relationships] | 有权读取、创建、编辑和删除架构关系。 |
| [!DNL Data Modeling] | [!UICONTROL Manage Identity Metadata] | 有权读取、创建、编辑和删除架构的身份元数据。 |
| [!DNL Data Management] | [!UICONTROL Manage Datasets] | 有权读取、创建、编辑和删除数据集。 架构的只读访问权限。 |
| [!DNL Data Management] | [!UICONTROL View Datasets] | 对数据集和架构的只读访问权限。 |
| [!DNL Data Management] | [!UICONTROL Data Monitoring] | 对监控数据集和流的只读访问权限。 |
| [!DNL Data Science Workspace] | [!UICONTROL Manage Data Science Workspace] | 在[!DNL Data Science Workspace]中读取、创建、编辑和删除的权限。 |
| [!DNL Decision Management] | [!UICONTROL Manage Experience Decisioning] | 能够管理Experience Decisioning实体。 |
| [!DNL Decision Management] | [!UICONTROL View Experience Decisioning] | 对Experience Decisioning实体的只读访问权限。 |
| [!DNL Decision Management] | [!UICONTROL Manage Decisions] | 有权读取、创建、编辑和删除决策实体。 |
| [!DNL Decisions Management] | [!UICONTROL View Decisions] | 对决策实体的只读访问权限。 |
| [!DNL Decision Management] | [!UICONTROL Manage Offers] | 有权读取、创建、编辑和删除所有选件和组件。 对决策和收藏集的只读访问权限。 |
| [!DNL Decsion Management] | [!UICONTROL Manage Ranking Strategies] | 有权读取、创建、编辑和删除自定义报告并使用操作功能。 |
| [!DNL Destinations] | [!UICONTROL View Destinations] | 只读访问权限，可查看&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡中的可用目标和&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡中的已验证目标。 |
| [!DNL Destinations] | [!UICONTROL Manage Destinations] | 有权读取、创建和删除目标连接和目标帐户。 |
| [!DNL Destinations] | [!UICONTROL Activate Destinations] | 能够将数据激活到已创建的活动目标。 此权限还要求将[!UICONTROL View Destinations]或[!UICONTROL Manage Destinations]授予将激活目标的用户。 |
| [!DNL Destinations] | [!UICONTROL Activate Segment without Mapping] | 能够将受众激活到现有目标，而不显示[映射步骤](../destinations/ui/activate-batch-profile-destinations.md#mapping)。 用户可以在激活工作流中添加和删除受众，但无法添加或删除映射的属性或身份。 此权限还要求向将数据激活到目标的用户授予[!UICONTROL View Destinations]权限。 |
| [!DNL Destinations] | [!UICONTROL Manage and Activate Dataset Destinations] | 能够读取、创建、编辑和禁用数据集导出流。 还能将数据激活到已创建的活动数据集。 此权限还要求向将数据激活到目标的用户授予[!UICONTROL View Destinations]权限。 |
| [!DNL Destinations] | [!UICONTROL Destination Authoring] | 能够使用[Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md)创作目标。 |
| [!DNL Federated Data] | [!UICONTROL Manage Federated Data] | 访问所有联合数据功能（如创建架构、模型和组合）的能力。 |
| [!DNL Identity Management] | [!UICONTROL Manage Identity Namespaces] | 读取、创建、编辑和删除身份命名空间的权限。 |
| [!DNL Identity Management] | [!UICONTROL View Identity Namespaces] | 对身份命名空间的只读访问。 |
| [!DNL Identity Management] | [!UICONTROL View Identity Graph] | 对标识图的只读访问。 |
| [!DNL Identity Management] | [!UICONTROL Manage Identity Settings] | 访问读取、创建和编辑身份设置。 |
| [!DNL Identity Management] | [!UICONTROL View Identity Settings] | 对身份设置的只读访问权限。 |
| [!DNL Intelligent Services] | [!UICONTROL View Attribution AI] | 对Attribution AI设置和分析的只读访问权限。 |
| [!DNL Intelligent Services] | [!UICONTROL Manage Attribution AI] | 有权读取、创建、编辑和删除归因人工智能模型。 |
| [!DNL Intelligent Services] | [!UICONTROL View Customer AI] | 访问读取或查看客户AI模型。 |
| [!DNL Intelligent Services] | [!UICONTROL Manage Customer AI] | 有权创建、更新、删除、启用或禁用Customer AI模型。 |
| [!DNL IP Warmup Configurations] | [!UICONTROL View IP Warmup Plans] | 对IP预热计划的只读访问权限。 |
| [!DNL IP Warmup Configurations] | [!UICONTROL Manage IP Warmup Plans] | 能够管理IP预热计划。 |
| [!DNL IP Warmup Configurations] | [!UICONTROL View IP Warmup Reports] | 对IP预热报告的只读访问权限。 |
| [!DNL Journeys] | [!UICONTROL Manage Journeys] | 有权读取、创建、编辑和删除历程。 |
| [!DNL Journeys] | [!UICONTROL View Journeys] | 对历程的只读访问权限。 |
| [!DNL Journeys] | [!UICONTROL View Journeys Report] | 对历程报告的只读访问权限。 |
| [!DNL Journeys] | [!UICONTROL Manage Journeys Events, Data Sources and Actions] | 有权读取、创建、编辑和删除事件、数据源或操作。 |
| [!DNL Journeys] | [!UICONTROL View Journeys Events, Data Sources and Actions] | 对事件、数据源或操作的只读访问权限。 |
| [!DNL Journeys] | [!UICONTROL Approve and Publish Journeys] | 在应用策略时批准和发布历程的功能。 |
| [!DNL Journeys] | [!UICONTROL Publish Journeys] | 发布历程的功能。 |
| [!DNL Journey Optimizer Library] | [!UICONTROL Manage Library Items] | 添加和删除已保存表达式的功能。 |
| [!DNL Journey Optimizer Library] | [!UICONTROL Publish Fragments] | 发布内容片段的功能。 |
| [!DNL Journey Optimizer Library] | [!UICONTROL Simulate Content] | 访问用于预览和校样的模拟内容选项。 |
| [!DNL Journey Optimizer Rules] | [!UICONTROL View Frequency Rules] | 对频率规则的只读访问权限。 |
| [!DNL Journey Optimizer Rules] | [!UICONTROL Manage Frequency Rules] | 有权读取、创建、编辑或删除频率规则。 |
| [!DNL Messages] | [!UICONTROL Manage Messages] | 读取、创建、编辑和删除消息的权限。 |
| [!DNL Messages] | [!UICONTROL View Messages] | 对消息的只读访问权限。 |
| [!DNL Messages] | [!UICONTROL View Messages Report] | 具有读取和编辑消息报表的权限。 |
| [!DNL Messages] | [!UICONTROL Publish Messages] | 能够发布消息。 |
| [!DNL Messages] | [!UICONTROL Manage Messages Preview and Test] | 在应用策略时批准和发布消息的功能。 |
| [!DNL Privacy Service] | [!UICONTROL Manage Privacy Service] | 访问读取和写入隐私工作流。 |
| [!DNL Privacy Service] | [!UICONTROL View Privacy Service] | 对隐私工作流的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL Manage Profiles] | 有权读取、创建、编辑和删除用于客户配置文件的数据集。 对可用配置文件的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL View Profiles] | 对可用配置文件的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL Manage Segments] | 有权读取、创建、编辑和删除受众。 |
| [!DNL Profile Management] | [!UICONTROL View Segments] | 对可用受众的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL Manage Merge Policies] | 有权读取、创建、编辑和删除合并策略。 |
| [!DNL Profile Management] | [!UICONTROL View Merge Policies] | 对可用合并策略的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL Import Audiences] | 能够使用CSV上传工作流导入新受众。 |
| [!DNL Profile Management] | [!UICONTROL Export Audience Segment] | 能够将计算的受众导出到数据集。 |
| [!DNL Profile Management] | [!UICONTROL Evaluate a Segment to an Audience] | 能够通过评估区段定义为受众生成配置文件。 |
| [!DNL Profile Management] | [!UICONTROL View B2B AI] | 对所有B2B AI/ML服务的设置和配置的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL Manage B2B AI] | 有权读取、创建、编辑和删除所有B2B AI/ML服务的设置和配置。 |
| [!DNL Profile Management] | [!UICONTROL View B2B Profile] | 对B2B实体配置文件（如Account、Opportunity等）、所有B2B AI/ML服务的设置和配置以及B2B仪表板小部件的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL Manage B2B Profile] | 有权读取、创建、编辑和删除B2B实体配置文件（如Account 、 Opportunity等）。 对所有B2B AI/ML服务和B2B仪表板小组件的设置和配置的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL Manage Lookalikes] | 能够创建或删除相似受众。 |
| [!DNL Profile Management] | [!UICONTROL View B2B Experience] | 能够查看B2B配置文件和属性。 |
| [!DNL Profile Management] | [!UICONTROL View Profile Settings] | 对所有配置文件设置的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL Manage Profile Settings] | 有权读取和编辑所有配置文件设置。 |
| [!DNL Prospects] | [!UICONTROL View Prospects] | 对潜在客户架构、用户档案、受众和潜在客户折叠面板的只读访问权限。 |
| [!DNL Prospects] | [!UICONTROL Manage Prospects] | 能够创建和管理潜在客户架构、用户档案和受众。 对潜在客户折叠的只读访问权限。 |
| [!DNL Query Service] | [!UICONTROL Manage Queries] | 有权读取、创建、编辑和删除Experience Platform数据的结构化SQL查询。 |
| [!DNL Query Service] | [!UICONTROL Manage Query Service Integration] | 访问创建、更新和删除未过期的凭据以访问查询服务。 |
| [!DNL Query Service] | [!UICONTROL Manage Query Sessions] | 能够逐出现有会议。 |
| [!DNL Query Service] | [!UICONTROL Manage Allow List] | 能够管理组织的IP限制。 |
| [!DNL Reports] | [!UICONTROL View Channel Reports] | 查看和修改渠道报表的功能。 |
| [!DNL Run and Operate] | [!UICONTROL View Health Checks] | 对运行状况检查的只读访问权限。 |
| [!DNL Run and Operate] | [!UICONTROL View Job Schedules] | 对作业计划的只读访问权限。 |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Sandboxes] | 访问读取、创建、编辑和删除沙箱。 |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes] | 对属于您组织的沙盒具有只读访问权限。 |
| [!DNL Sandbox Administration] | [!UICONTROL Reset a Sandbox] | 能够重置沙盒。 |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Packages] | 创建、导入或导出资源包的权限。 |
| [!DNL Sandbox Administration] | [!UICONTROL Share Packages] | 跨不同组织共享包的访问权限。 |
| [!DNL Traits Configurations] | [!UICONTROL View Traits] | 特征的只读访问权限。 |
| [!DNL Traits Configurations] | [!UICONTROL Manage Traits] | 管理特征的访问权限。 |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Projects] | 管理翻译项目的功能。 |
| [!DNL Translation Service] | [!UICONTROL View Translation Projects] | 对翻译项目的只读访问权限。 |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Tasks] | 管理翻译任务的能力。 |
| [!DNL Translation Service] | [!UICONTROL View Translation Tasks] | 对翻译任务的只读访问权限。 |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Reviews] | 管理翻译审阅的功能。 |
| [!DNL Translation Service] | [!UICONTROL View Translation Reviews] | 对翻译审阅的只读访问权限。 |
| [!DNL Translation Service] | [!UICONTROL Manage Translation In-house] | 能够在内部管理翻译。 |
| [!DNL Translation Service] | [!UICONTROL View Translation In-house] | 内部翻译的只读访问权限。 |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Settings] | 管理员管理翻译设置的功能。 |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Providers] | 能够管理翻译提供商。 |

## 后续步骤

通过阅读本指南，您已了解Experience Platform中的访问控制的主要原则。 您现在可以继续阅读[基于属性的访问控制用户指南](./abac/overview.md)，以了解有关如何使用Experience Cloud为Experience Platform创建角色和分配权限的详细步骤。

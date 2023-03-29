---
keywords: Experience Platform；主页；热门主题；访问控制；Adobe Admin Console
solution: Experience Platform
title: 访问控制概述
description: 通过Adobe Experience Platform提供对Adobe Admin Console的访问控制。 此功能可利用Admin Console中的产品配置文件，将用户与权限和沙箱相关联。
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 546758c419670746cf55de35cbb33131d4457cb9
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 3%

---

# 访问控制概述

的访问控制 [!DNL Experience Platform] 通过 [Adobe Admin Console](https://adminconsole.adobe.com). 此功能可利用 [!DNL Admin Console]，用于将用户与权限和沙箱关联。

## 访问控制层次结构和工作流

为配置 [!DNL Experience Platform]，则您必须具有具有 [!DNL Experience Platform] 产品集成。 授予或撤销权限的最低角色是产品配置文件管理员。 其他可以管理权限的管理员角色包括产品管理员（可以管理产品中的所有配置文件）和系统管理员（无限制）。 请参阅Adobe Help Center上的 [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 以了解更多信息。

>[!NOTE]
>
>此后，本文档中任何对“管理员”的提及均指产品用户档案管理员或更高级别（如上所述）。

用于获取和分配访问权限的高级工作流可概括如下：

- 授权Adobe Experience Platform或使用Experience Platform的应用程序/应用程序服务后，会向授权期间指定的管理员发送电子邮件。
- 管理员登录到 [Adobe Admin Console](#adobe-admin-console) 选择 **Adobe Experience Platform** 从“概述”页面的产品列表中。
- 管理员可以查看默认 [产品配置文件](#product-profiles) 或根据需要创建新的客户产品配置文件。
- 管理员可以编辑任何现有产品配置文件的权限和用户。
- 创建或编辑产品配置文件时，管理员会使用 **[!UICONTROL 用户]** 选项卡，并向这些用户授予权限(例如“[!UICONTROL 读取数据集]&quot;或&quot;[!UICONTROL 管理架构]“) **[!UICONTROL 权限]** 选项卡。 同样，管理员也可以使用相同的权限选项卡为沙箱分配访问权限。
- 当用户登录到 [!DNL Experience Platform] 用户界面，他们对 [!DNL Platform] 功能由步骤2中授予他们的权限驱动。 例如，如果用户没有[!UICONTROL 查看数据集]“权限， **[!UICONTROL 数据集]** 选项卡。

有关如何在中管理访问控制的更详细步骤 [!DNL Experience Platform]，请参阅 [访问控制用户指南](./ui/overview.md).

所有对 [!DNL Experience Platform] API将验证是否具有权限，如果在当前用户上下文中未找到相应的权限，则会返回错误。 在UI中，元素将被隐藏或更改，具体取决于授予当前用户的权限。

## Adobe Admin Console

Adobe Admin Console提供了一个中心位置，用于管理Adobe产品权利和贵组织的访问权限。 通过控制台，您可以向用户组授予各种 [!DNL Platform] 功能，如“[!UICONTROL 管理数据集]&quot;, &quot;[!UICONTROL 查看数据集]&quot;或&quot;[!UICONTROL 管理配置文件]&quot;

### 产品配置文件

在 [!DNL Admin Console]，则会通过使用产品配置文件向用户分配权限。 产品配置文件允许您向一个或多个用户授予权限，并且还包含用户对通过产品配置文件分配给他们的沙箱范围的访问权限。 可以将用户分配到属于您组织的一个或多个产品配置文件。

### 默认产品配置文件

[!DNL Experience Platform] 附带两个预配置的默认产品配置文件。 下表概述了每个默认用户档案中提供的内容，包括授予访问权限的沙盒以及在该沙盒范围内授予的权限。

| 产品配置文件 | 沙盒访问 | 权限 |
| --- | --- | --- |
| 默认生产所有访问权限 | 生产 | 适用于 [!DNL Experience Platform]，沙盒管理权限除外。 |
| 沙盒管理员 | 不适用 | 仅提供对“沙盒管理”权限的访问权限。 |

## 沙箱和权限

非生产沙箱是数据虚拟化的一种形式，它允许您将数据与其他沙箱隔离，并通常用于开发实验、测试或试验。 产品配置文件的权限授予该配置文件的用户访问 [!DNL Platform] 功能。 默认的Experience Platform许可证会授予您五个沙箱（一个生产，四个非生产）。 您最多可以添加10个非生产沙箱，最多可添加75个沙箱。 有关更多详细信息，请联系您的IMS组织管理员或Adobe销售代表。

有关 [!DNL Experience Platform]，请参阅 [沙箱概述](../sandboxes/home.md).

### 访问沙箱

沙箱的访问权限通过产品配置文件进行管理。 有关如何启用对产品用户档案沙盒的访问权限的详细步骤，请参阅 [访问控制用户指南](./ui/overview.md).

可以向用户授予对产品配置文件中一个或多个沙箱的访问权限。 如果两个或多个产品配置文件中包含一个用户，则该用户将有权访问这些配置文件中包含的所有沙箱。

“沙盒管理”权限允许用户管理、查看或重置沙箱。

### 权限 {#permissions}

产品配置文件中的权限选项卡会显示该配置文件处于活动状态的沙箱和权限：

![permissions-overview](./images/permissions.png)

通过 [!DNL Admin Console] 按类别排序，其中有些权限授予对若干低级功能的访问权限。

下表概述了 [!DNL Experience Platform] 在 [!DNL Admin Console]，以及 [!DNL Platform] 授予访问权限的功能。 有关如何向产品配置文件添加权限的详细步骤，请参阅 [访问控制用户指南](./ui/overview.md).

| 类别 | 权限 | 描述 |
| --- | --- | --- |
| [!DNL Alerts] | [!UICONTROL 查看警报历史记录] | 警报历史记录的只读访问权限。 |
| [!DNL Alerts] | [!UICONTROL 解决警报] | 访问读取、编辑和删除警报。 |
| [!DNL Alerts] | [!UICONTROL 查看警报] | 警报的只读访问权限。 |
| [!DNL Alerts] | [!UICONTROL 管理警报] | 有权读取、创建、编辑和删除警报历史记录。 |
| [!DNL Data Hygiene] | [!UICONTROL 查看数据卫生] | 用于数据卫生的只读访问。 |
| [!DNL Data Hygiene] | [!UICONTROL 管理数据卫生] | 访问读取、创建、编辑和删除数据卫生。 |
| [!DNL Data Modeling] | [!UICONTROL 管理架构] | 访问读取、创建、编辑和删除架构及相关资源。 |
| [!DNL Data Modeling] | [!UICONTROL 查看架构] | 对架构和相关资源的只读访问。 |
| [!DNL Data Modeling] | [!UICONTROL 管理关系] | 访问读取、创建、编辑和删除架构关系。 |
| [!DNL Data Modeling] | [!UICONTROL 管理身份元数据] | 有权读取、创建、编辑和删除架构的标识元数据。 |
| [!DNL Data Management] | [!UICONTROL 管理数据集] | 访问读取、创建、编辑和删除数据集。 模式的只读访问。 |
| [!DNL Data Management] | [!UICONTROL 查看数据集] | 数据集和架构的只读访问权限。 |
| [!DNL Data Management] | [!UICONTROL 数据监控] | 对监控数据集和流的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 管理配置文件] | 有权读取、创建、编辑和删除用于客户配置文件的数据集。 对可用配置文件的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 查看配置文件] | 对可用配置文件的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 管理区段] | 访问读取、创建、编辑和删除区段。 |
| [!DNL Profile Management] | [!UICONTROL 查看区段] | 对可用区段的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 管理合并策略] | 访问读取、创建、编辑和删除合并策略。 |
| [!DNL Profile Management] | [!UICONTROL 查看合并策略] | 对可用合并策略的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 导出区段的受众] | 能够将评估的受众区段导出到数据集。 |
| [!DNL Profile Management] | [!UICONTROL 对受众评估区段] | 能够通过评估区段定义为受众生成用户档案。 |
| [!DNL Identity Management] | [!UICONTROL 管理身份命名空间] | 有权读取、创建、编辑和删除身份命名空间。 |
| [!DNL Identity Management] | [!UICONTROL 查看标识命名空间] | 身份命名空间的只读访问权限。 |
| [!DNL Identity Management] | [!UICONTROL 查看身份图] | 身份图的只读访问权限。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理沙箱] | 有权读取、创建、编辑和删除沙箱。 |
| [!DNL Sandbox Administration] | [!UICONTROL 查看沙盒] | 对属于贵组织的沙箱的只读访问权限。 |
| [!DNL Sandbox Administration] | [!UICONTROL 重置沙盒] | 能够重置沙盒。 |
| [!DNL Destinations] | [!UICONTROL 管理目标] | 对读取、创建和删除目标激活流和目标帐户的访问权限。 |
| [!DNL Destinations] | [!UICONTROL 查看目标] | 对 **[!UICONTROL 目录]** 选项卡和已验证的目标 **[!UICONTROL 浏览]** 选项卡。 |
| [!DNL Destinations] | [!UICONTROL 激活目标] | 允许用户将区段激活到现有目标。 在激活工作流中启用映射步骤。 此权限需要 [!UICONTROL 查看目标] 或 [!UICONTROL 管理目标] 授予将数据激活到目标的用户。 |
| [!DNL Destinations] | [!UICONTROL 在无映射的情况下激活区段] | 允许用户将区段激活到现有目标，而不显示 [映射步骤](../destinations/ui/activate-batch-profile-destinations.md#mapping). 用户可以在激活工作流中添加和删除区段，但无法添加或删除映射的属性或标识。 此权限需要 [!UICONTROL 激活目标] 授予将数据激活到目标的用户的权限。 |
| [!DNL Destinations] | [!UICONTROL 管理和激活数据集目标] | 能够读取、创建、编辑和禁用数据集导出流。 还能够将数据激活到已创建的活动数据集。 |
| [!DNL Destinations] | [!UICONTROL 目标创作] | 能够使用 [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL 管理源] | 对读取、创建、编辑和禁用源的访问权限。 |
| [!DNL Data Ingestion] | [!UICONTROL 查看源] | 对 **[!UICONTROL 目录]** 选项卡和已验证的源 **[!UICONTROL 浏览]** 选项卡。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | 访问创建、接受和拒绝合作伙伴握手，以连接两个IMS组织并启用 [!DNL Segment Match] 流量。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | 对读取、创建、编辑和发布的访问权限 [!DNL Segment Match] 与活跃的合作伙伴提供信息源。 |
| [!DNL Data Science Workspace] | [!UICONTROL 管理数据科学工作区] | 在 [!DNL Data Science Workspace]. |
| 数据治理 | [!UICONTROL 应用数据使用情况标签] | 访问读取、创建和删除使用情况标签。 |
| 数据治理 | [!UICONTROL 管理数据使用策略] | 访问读取、创建、编辑和删除数据使用策略。 |
| 数据治理 | [!UICONTROL 查看数据使用策略] | 对属于贵组织的数据使用策略的只读访问权限。 |
| 数据治理 | [!UICONTROL 查看用户活动日志] | 对记录的查看的只读访问权限 [审核日志](../landing/governance-privacy-security/audit-logs/overview.md) 平台活动。 |
| [!DNL Dashboards] | [!UICONTROL 查看许可证使用情况功能板] | 以只读方式访问许可证使用功能板。 |
| [!DNL Dashboards] | [!UICONTROL 管理标准功能板] | 添加data warehouse中尚未包含的自定义属性。 |
| [!DNL Query Service] | [!UICONTROL 管理查询] | 访问读取、创建、编辑和删除Platform数据的结构化SQL查询。 |
| [!DNL Query Service] | [!UICONTROL 管理查询服务集成] | 有权创建、更新和删除查询服务访问权限的未过期凭据。 |

## 后续步骤

通过阅读本指南，您已介绍中访问控制的主要原则 [!DNL Experience Platform]. 您现在可以继续 [访问控制用户指南](./ui/overview.md) 以了解有关如何使用的详细步骤 [!DNL Admin Console] 创建产品配置文件并为 [!DNL Platform].

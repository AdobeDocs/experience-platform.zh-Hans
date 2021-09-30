---
keywords: Experience Platform；主页；热门主题；访问控制；Adobe Admin Console
solution: Experience Platform
topic-legacy: overview
title: 访问控制概述
description: 通过Adobe Experience Platform提供对Adobe Admin Console的访问控制。 此功能可利用Admin Console中的产品配置文件，将用户与权限和沙箱相关联。
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 584461d3da5c5c39b9702b5d1dc1d1319568f695
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 2%

---

# 访问控制概述

[!DNL Experience Platform]的访问控制通过[Adobe Admin Console](https://adminconsole.adobe.com)提供。 此功能可利用[!DNL Admin Console]中的产品配置文件，该配置文件将用户与权限和沙箱相关联。

## 访问控制层次结构和工作流

要配置[!DNL Experience Platform]的访问控制，您必须拥有具有[!DNL Experience Platform]产品集成的组织的管理员权限。 授予或撤销权限的最低角色是产品配置文件管理员。 其他可以管理权限的管理员角色包括产品管理员（可以管理产品中的所有配置文件）和系统管理员（无限制）。 有关更多信息，请参阅Adobe Help Center关于[管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html)的文章。

>[!NOTE]
>
>此后，本文档中任何对“管理员”的提及均指产品用户档案管理员或更高级别（如上所述）。

用于获取和分配访问权限的高级工作流可概括如下：

- 授权Adobe Experience Platform或使用Experience Platform的应用程序/应用程序服务后，会向授权期间指定的管理员发送电子邮件。
- 管理员登录到[Adobe Admin Console](#adobe-admin-console)，并从概述页面的产品列表中选择&#x200B;**Adobe Experience Platform**。
- 管理员可以查看默认的[产品配置文件](#product-profiles)或根据需要创建新的客户产品配置文件。
- 管理员可以编辑任何现有产品配置文件的权限和用户。
- 创建或编辑产品配置文件时，管理员使用&#x200B;**[!UICONTROL users]**&#x200B;选项卡将用户添加到配置文件，并通过访问&#x200B;**[!UICONTROL 权限]**&#x200B;选项卡，向这些用户授予权限（例如“[!UICONTROL 读取数据集]”或“[!UICONTROL 管理架构]”）。 同样，管理员也可以使用相同的权限选项卡为沙箱分配访问权限。
- 当用户登录到[!DNL Experience Platform]用户界面时，他们对[!DNL Platform]功能的访问权限取决于步骤2中向他们授予的权限。 例如，如果用户没有“[!UICONTROL 查看数据集]”权限，则侧面菜单中的&#x200B;**[!UICONTROL 数据集]**&#x200B;选项卡将对该用户不可见。

有关如何在[!DNL Experience Platform]中管理访问控制的更多详细步骤，请参阅[访问控制用户指南](./ui/overview.md)。

所有对[!DNL Experience Platform] API的调用均已验证权限，如果在当前用户上下文中找不到相应的权限，则会返回错误。 在UI中，元素将被隐藏或更改，具体取决于授予当前用户的权限。

## Adobe Admin Console

Adobe Admin Console提供了一个中心位置，用于管理Adobe产品权利和贵组织的访问权限。 通过控制台，您可以为用户组授予各种[!DNL Platform]功能的访问权限，这些功能包括“[!UICONTROL 管理数据集]”、“[!UICONTROL 查看数据集]”或“[!UICONTROL 管理配置文件]”。

### 产品配置文件

在[!DNL Admin Console]中，会通过使用产品配置文件向用户分配权限。 产品配置文件允许您向一个或多个用户授予权限，并且还包含用户对通过产品配置文件分配给他们的沙箱范围的访问权限。 可以将用户分配到属于您组织的一个或多个产品配置文件。

### 默认产品配置文件

[!DNL Experience Platform] 附带两个预配置的默认产品配置文件。下表概述了每个默认用户档案中提供的内容，包括授予访问权限的沙盒以及在该沙盒范围内授予的权限。

| 产品配置文件 | 沙盒访问 | 权限 |
| --- | --- | --- |
| 默认生产所有访问权限 | 生产 | 适用于[!DNL Experience Platform]的所有权限，“沙盒管理”权限除外。 |
| 沙盒管理员 | 不适用 | 仅提供对“沙盒管理”权限的访问权限。 |

## 沙箱和权限

非生产沙箱是数据虚拟化的一种形式，它允许您将数据与其他沙箱隔离，并通常用于开发实验、测试或试验。 产品用户档案的权限为用户授予他们访问沙盒环境中的[!DNL Platform]功能的权限。 默认的Experience Platform许可证会授予您五个沙箱（一个生产，四个非生产）。 您最多可以添加10个非生产沙箱，最多可添加75个沙箱。 有关更多详细信息，请联系您的IMS组织管理员或Adobe销售代表。

有关[!DNL Experience Platform]中沙箱的详细信息，请参阅[沙箱概述](../sandboxes/home.md)。

### 访问沙箱

沙箱的访问权限通过产品配置文件进行管理。 有关如何启用对产品用户档案沙盒的访问的详细步骤，请参阅[访问控制用户指南](./ui/overview.md)。

可以向用户授予对产品配置文件中一个或多个沙箱的访问权限。 如果两个或多个产品配置文件中包含一个用户，则该用户将有权访问这些配置文件中包含的所有沙箱。

“沙盒管理”权限允许用户管理、查看或重置沙箱。

### 权限 {#permissions}

产品配置文件中的权限选项卡会显示该配置文件处于活动状态的沙箱和权限：

![permissions-overview](./images/permissions.png)

通过[!DNL Admin Console]授予的权限按类别排序，其中有些权限授予对若干低级功能的访问权限。

下表概述了[!DNL Admin Console]中[!DNL Experience Platform]的可用权限，以及它们授予访问权限的特定[!DNL Platform]功能的描述。 有关如何向产品配置文件添加权限的详细步骤，请参阅[访问控制用户指南](./ui/overview.md)。

| 类别 | 权限 | 描述 |
| --- | --- | --- |
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
| [!DNL Identities] | [!UICONTROL 管理身份命名空间] | 有权读取、创建、编辑和删除身份命名空间。 |
| [!DNL Identities] | [!UICONTROL 查看身份命名空间] | 身份命名空间的只读访问权限。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理沙箱] | 有权读取、创建、编辑和删除沙箱。 |
| [!DNL Sandbox Administration] | [!UICONTROL 查看沙盒] | 对属于贵组织的沙箱的只读访问权限。 |
| [!DNL Sandbox Administration] | [!UICONTROL 重置沙盒] | 能够重置沙盒。 |
| [!DNL Destinations] | [!UICONTROL 管理目标] | 访问读取、创建、编辑和禁用目标。 |
| [!DNL Destinations] | [!UICONTROL 查看目标] | 对&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡中可用目标以及&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中已验证目标的只读访问权限。 |
| [!DNL Destinations] | [!UICONTROL 激活目标] | 能够将数据激活到已创建的活动目标。 此权限要求将“查看目标”或“管理[!UICONTROL 目标”]授予将激活目标的用户。 |
| [!DNL Destinations] | [!UICONTROL 目标创作] | 能够使用[Adobe Experience Platform目标SDK](../destinations/destination-sdk/overview.md)创作目标。 |
| [!DNL Data Ingestion] | [!UICONTROL 管理源] | 对读取、创建、编辑和禁用源的访问权限。 |
| [!DNL Data Ingestion] | [!UICONTROL 查看源] | 对&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡中可用源的只读访问，对&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中的已验证源的只读访问。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | 访问创建、接受和拒绝合作伙伴握手，以连接两个IMS组织并启用[!DNL Segment Match]流。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | 与活动合作伙伴一起读取、创建、编辑和发布[!DNL Segment Match]信息源。 |
| [!DNL Data Science Workspace] | [!UICONTROL 管理数据科学工作区] | 在[!DNL Data Science Workspace]中访问读取、创建、编辑和删除操作。 |
| [!DNL Data Governance] | [!UICONTROL 应用数据使用情况标签] | 访问读取、创建和删除使用情况标签。 |
| [!DNL Data Governance] | [!UICONTROL 管理数据使用策略] | 访问读取、创建、编辑和删除数据使用策略。 |
| [!DNL Data Governance] | [!UICONTROL 查看数据使用策略] | 对属于贵组织的数据使用策略的只读访问权限。 |
| [!DNL Data Governance] | [!UICONTROL 查看审核日志] | 对查看记录的平台活动[审核日志](../landing/governance-privacy-security/audit-logs/overview.md)的只读访问权限。 |
| [!DNL Dashboards] | [!UICONTROL 查看许可证使用情况功能板] | 以只读方式访问许可证使用功能板。 |
| [!DNL Dashboards] | [!UICONTROL 管理标准功能板] | 添加data warehouse中尚未包含的自定义属性。 |
| [!DNL Query Service] | [!UICONTROL 管理查询] | 访问读取、创建、编辑和删除Platform数据的结构化SQL查询。 |
| [!DNL Query Service] | [!UICONTROL 管理查询服务集成] | 有权创建、更新和删除查询服务访问权限的未过期凭据。 |

## 后续步骤

通过阅读本指南，您了解了[!DNL Experience Platform]中访问控制的主要原则。 现在，您可以继续阅读[访问控制用户指南](./ui/overview.md) ，以详细了解如何使用[!DNL Admin Console]创建产品配置文件和分配[!DNL Platform]的权限。

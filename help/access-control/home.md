---
keywords: Experience Platform；主页；热门主题；访问控制;adobe admin console
solution: Experience Platform
topic: overview
title: 访问控制概述
description: Adobe Experience Platform的访问控制通过Adobe Admin Console提供。 此功能利用Admin Console中的产品用户档案，将用户与权限和沙箱关联起来。
translation-type: tm+mt
source-git-commit: c277caabe851c81f66b822c07a25f4b94466eef0
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 2%

---


# 访问控制概述

[!DNL Experience Platform]的访问控制通过[Adobe Admin Console](https://adminconsole.adobe.com)提供。 此功能利用[!DNL Admin Console]中的产品用户档案，该产品用户链接用户的权限和沙箱。

## 访问控制层次结构和工作流

要为[!DNL Experience Platform]配置访问控制，您必须对具有[!DNL Experience Platform]产品集成的组织具有管理员权限。 授予或撤销权限的最低角色是产品用户档案管理员。 其他可以管理权限的管理员角色包括产品管理员(可以管理产品中的所有用户档案)和系统管理员（无限制）。 有关详细信息，请参阅Adobe Help Center关于[管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html)的文章。

>[!NOTE]
>
>此后，本文档中提及的“管理员”指的是产品用户档案管理员或更高级别（如上所述）。

获取和分配访问权限的高级工作流可概括如下：

- 授权Adobe Experience Platform或使用Experience Platform的应用程序／应用程序服务后，将向授权过程中指定的管理员发送电子邮件。
- 管理员登录到[Adobe Admin Console](#adobe-admin-console)，并从概述页上的产品列表中选择&#x200B;**Adobe Experience Platform**。
- 管理员可以视图默认的[产品用户档案](#product-profiles)，或根据需要创建新的客户产品用户档案。
- 管理员可以编辑任何现有产品用户档案的权限和用户。
- 在创建或编辑产品用户档案时，管理员使用&#x200B;**[!UICONTROL users]**&#x200B;选项卡将用户添加到用户档案，并通过访问&#x200B;**[!UICONTROL 权限]**&#x200B;选项卡授予这些用户权限(如“[!UICONTROL 读取数据集]”或“[!UICONTROL 管理模式]”)。 同样，管理员也可以使用相同的权限选项卡将访问权限分配给沙箱。
- 当用户登录到[!DNL Experience Platform]用户界面时，他们对[!DNL Platform]功能的访问由步骤2授予他们的权限驱动。 例如，如果用户没有“[!UICONTROL 视图数据集]”权限，则侧面菜单中的&#x200B;**[!UICONTROL 数据集]**&#x200B;选项卡对该用户将不可见。

有关如何在[!DNL Experience Platform]中管理访问控制的更详细步骤，请参阅[访问控制用户指南](./ui/overview.md)。

所有对[!DNL Experience Platform] API的调用均经过验证以获得权限，如果在当前用户上下文中找不到相应的权限，则将返回错误。 在UI中，元素将被隐藏或更改，具体取决于授予当前用户的权限。

## Adobe Admin Console

Adobe Admin Console为管理Adobe产品授权和访问您的组织提供了一个中心位置。 通过控制台，您可以授予用户组对各种[!DNL Platform]功能(如“[!UICONTROL 管理数据集]”、“[!UICONTROL 视图数据集]”或“[!UICONTROL 管理用户档案]”)的访问权限。

### 产品用户档案

在[!DNL Admin Console]中，权限通过产品用户档案的使用分配给用户。 产品用户档案允许您向一个或多个用户授予权限，还可以包含他们对通过产品用户档案分配给他们的沙箱范围的访问权限。 可以将用户分配给属于您组织的一个或多个产品用户档案。

### 默认产品用户档案

[!DNL Experience Platform] 附带两个预配置的默认产品用户档案。下表概述了每个默认用户档案中提供的内容，包括它们授予访问权限的沙箱以及它们在该沙箱的范围内授予的权限。

| 产品配置文件 | 沙箱访问 | 权限 |
| --- | --- | --- |
| 默认的全部生产访问 | 生产 | 除“沙箱管理”权限外，适用于[!DNL Experience Platform]的所有权限。 |
| 沙箱管理员 | 不适用 | 仅提供对“沙箱管理”权限的访问。 |

## 沙箱和权限

非生产沙箱是数据虚拟化的一种形式，它允许您将数据与其他沙箱隔离，并通常用于开发实验、测试或试用。 产品用户档案的权限使用户档案的用户有权访问他们已被授予访问权限的沙箱环境中的[!DNL Platform]功能。 默认Experience Platform许可证会授予您五个沙箱（一个生产箱和四个非生产箱）。 您最多可以添加十个非生产沙箱，最多共添加75个沙箱。 有关详细信息，请与IMS组织管理员或Adobe销售代表联系。

有关[!DNL Experience Platform]中沙箱的详细信息，请参阅[沙箱概述](../sandboxes/home.md)。

### 访问沙箱

对沙箱的访问通过产品用户档案进行管理。 有关如何为产品用户档案启用沙箱访问的详细步骤，请参阅[访问控制用户指南](./ui/overview.md)。

可以向用户授予对产品用户档案中一个或多个沙箱的访问权限。 如果一个用户包含在两个或多个产品用户档案中，该用户将有权访问这些用户档案中包含的所有沙箱。

“沙箱管理”权限允许用户管理、视图或重置沙箱。

### 权限

产品用户档案中的权限选项卡显示该用户档案处于活动状态的沙箱和权限：

![权限概述](./images/permissions-overview.png)

通过[!DNL Admin Console]授予的权限按类别排序，其中一些权限授予对几个低级功能的访问权限。

下表概述了[!DNL Admin Console]中[!DNL Experience Platform]的可用权限，以及它们授予访问权限的特定[!DNL Platform]功能的说明。 有关如何向产品用户档案添加权限的详细步骤，请参阅[访问控制用户指南](./ui/overview.md)。

| 类别 | 权限 | 描述 |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL 管理架构] | 访问读取、创建、编辑和删除模式及相关资源。 |
| [!DNL Data Modeling] | [!UICONTROL 查看架构] | 对模式和相关资源的只读访问。 |
| [!DNL Data Modeling] | [!UICONTROL 管理关系] | 访问读取、创建、编辑和删除模式关系。 |
| [!DNL Data Modeling] | [!UICONTROL 管理标识元数据] | 访问读取、创建、编辑和删除模式的标识元数据。 |
| [!DNL Data Management] | [!UICONTROL 管理数据集] | 访问读取、创建、编辑和删除数据集。 模式的只读访问。 |
| [!DNL Data Management] | [!UICONTROL 查看数据集] | 数据集和模式的只读访问。 |
| [!DNL Data Management] | [!UICONTROL 数据监控] | 对监视数据集和流的只读访问。 |
| [!DNL Profile Management] | [!UICONTROL 管理用户档案] | 访问用于客户用户档案的读取、创建、编辑和删除数据集。 对可用用户档案的只读访问。 |
| [!DNL Profile Management] | [!UICONTROL 视图用户档案] | 对可用用户档案的只读访问。 |
| [!DNL Profile Management] | [!UICONTROL 管理区段] | 访问读取、创建、编辑和删除区段。 |
| [!DNL Profile Management] | [!UICONTROL 视图细分] | 对可用区段的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 管理合并策略] | 访问读取、创建、编辑和删除合并策略。 |
| [!DNL Profile Management] | [!UICONTROL 视图合并策略] | 对可用合并策略的只读访问权限。 |
| [!DNL Profile Management] | [!UICONTROL 导出区段受众] | 能够将评估的受众段导出到数据集。 |
| [!DNL Profile Management] | [!UICONTROL 将区段评估为受众] | 能够通过评估区段定义为受众生成用户档案。 |
| [!DNL Identities] | [!UICONTROL 管理身份命名空间] | 访问读取、创建、编辑和删除身份命名空间。 |
| [!DNL Identities] | [!UICONTROL 查看身份命名空间] | 身份命名空间的只读访问。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理沙箱] | 访问读取、创建、编辑和删除沙箱。 |
| [!DNL Sandbox Administration] | [!UICONTROL 查看沙盒] | 对属于您组织的沙箱的只读访问权限。 |
| [!DNL Sandbox Administration] | [!UICONTROL 重置沙箱] | 能够重置沙箱。 |
| [!DNL Destinations] | [!UICONTROL 管理目标] | 访问读取、创建、编辑和禁用目标。 |
| [!DNL Destinations] | [!UICONTROL 视图目标] | 对&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡中的可用目标和对&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中的已验证目标进行只读访问。 |
| [!DNL Destinations] | [!UICONTROL 激活目标] | 能够将数据激活到已创建的活动目标。 此权限要求向将激活目标的用户授予“视图目标”或“管理[!UICONTROL 目标”]。 |
| [!DNL Data Ingestion] | [!UICONTROL 管理源] | 访问读取、创建、编辑和禁用源。 |
| [!DNL Data Ingestion] | [!UICONTROL 视图源] | 对&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡中的可用源和对&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中经过身份验证的源进行只读访问。 |
| [!DNL Data Science Workspace] | [!UICONTROL 管理数据科学工作区] | 访问在[!DNL Data Science Workspace]中读取、创建、编辑和删除。 |
| [!DNL Data Governance] | [!UICONTROL 应用数据使用标签] | 访问读取、创建和删除使用标签。 |
| [!DNL Data Governance] | [!UICONTROL 管理数据使用策略] | 访问读取、创建、编辑和删除数据使用策略。 |
| [!DNL Data Governance] | [!UICONTROL 视图数据使用策略] | 对属于您组织的数据使用策略的只读访问。 |
| [!DNL Query Service] | [!UICONTROL 管理查询] | 访问读取、创建、编辑和删除平台查询的结构化SQL数据。 |

## 后续步骤

阅读本指南，您将了解[!DNL Experience Platform]中访问控制的主要原则。 现在，您可以继续阅读[访问控制用户指南](./ui/overview.md)，详细了解如何使用[!DNL Admin Console]创建产品用户档案并为[!DNL Platform]分配权限。
---
keywords: Experience Platform;home;popular topics;access control;adobe admin console
solution: Experience Platform
topic: overview
title: 访问控制概述
description: Adobe Experience Platform的访问控制通过Adobe Admin Console提供。 此功能利用Admin Console中的产品用户档案，将用户与权限和沙箱关联起来。
translation-type: tm+mt
source-git-commit: 397f08efa276f7885e099a0a8d9dc6d23fe0e8cc
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 2%

---


# 访问控制概述

访问控制 [!DNL Experience Platform] 通过Adobe Admin Console [提供](https://adminconsole.adobe.com)。 此功能利用中的产品用户档案, [!DNL Admin Console]将用户与权限和沙箱关联起来。

## 访问控制层次结构和工作流

要配置访问控制, [!DNL Experience Platform]您必须对具有产品集成的组织具有管 [!DNL Experience Platform] 理员权限。 授予或撤销权限的最低角色是产品 **[!UICONTROL 用户档案管理员]**。 其他可以管理权限的管理员角色 **[!UICONTROL 包括产品管理员]** (可以管理产品中的所有用户档案 **[!UICONTROL )和系统管]** 理员（无限制）。 有关更多信息，请参 [阅Adobe Help Center](https://helpx.adobe.com/enterprise/using/admin-roles.html) 《行政角色》一文。

>[!NOTE]
>
>此后，本文档中提及的“管理员”指的是产品用户档案管理员或更高级别（如上所述）。

获取和分配访问权限的高级工作流可概括如下：

- 授权Adobe Experience Platform或使用Experience Platform的应用程序／应用程序服务后，将向授权过程中指定的管理员发送电子邮件。
- 管理员登录到 [Adobe Admin Console](#adobe-admin-console) ，并从 **概述页** 面上的产品列表中选择Adobe Experience Platform。
- 管理员可以视图默 [认产品用户档案](#product-profiles) ，或根据需要创建新的客户产品用户档案。
- 管理员可以编辑任何现有产品用户档案的权限和用户。
- 在创建或编辑产品用户档案时，管理员使用“用户”选项卡将用户添加到用户档案 **[!UICONTROL 中]** ，并通过访问“permissions[!UICONTROL adets]”选项卡，向这些用户(如“Read Datasets[!UICONTROL ”或“]Manage模式 **[!UICONTROL ”)授予]** 权限。 同样，管理员也可以使用相同的权限选项卡将访问权限分配给沙箱。
- 当用户登录到用 [!DNL Experience Platform] 户界面时，其 [!DNL Platform] 权能的访问权限由步骤2授予的权限驱动。 例如，如果用户没有“[!UICONTROL 视图集]”权限，则侧面菜单中的 **[!UICONTROL Datasets]** 选项卡对该用户将不可见。

有关如何在中管理访问控制的更详细步 [!DNL Experience Platform]骤，请参阅 [访问控制用户指南](./ui/overview.md)。

对API的所 [!DNL Experience Platform] 有调用都经过验证以获得权限，如果在当前用户上下文中找不到相应的权限，则将返回错误。 在UI中，元素将被隐藏或更改，具体取决于授予当前用户的权限。

## Adobe Admin Console

Adobe Admin Console为管理Adobe产品授权和访问您的组织提供了一个中心位置。 通过控制台，您可以授予用户组对各种功能(如“管 [!DNL Platform] 理数据集[!UICONTROL ”、]“视图数据集[!UICONTROL ”或“管理]用户档案[!UICONTROL ”)的访]问权限。

### 产品用户档案

在中， [!DNL Admin Console]通过使用产品用户档案将权限分配给 **[!UICONTROL 用户]**。 产品用户档案允许您向一个或多个用户授予权限，还可以包含他们对通过产品用户档案分配给他们的沙箱范围的访问权限。 可以将用户分配给属于您组织的一个或多个产品用户档案。

### 默认产品用户档案

[!DNL Experience Platform] 附带两个预配置的默认产品用户档案。 下表概述了每个默认用户档案中提供的内容，包括它们授予访问权限的沙箱以及它们在该沙箱的范围内授予的权限。

| 产品配置文件 | 沙箱访问 | 权限 |
| --- | --- | --- |
| 默认生产——全部访问 | 生产 | 除“沙箱管理”权 [!DNL Experience Platform]限外，所有适用的权限。 |
| 默认沙箱管理 | 不适用 | 仅提供对“沙箱管理”权限的访问。 |

## 沙箱和权限

非生产沙箱是数据虚拟化的一种形式，它允许您将数据与其他沙箱隔离，并通常用于开发实验、测试或试用。 产品用户档案 **[!UICONTROL 的权限]** ，使用户档案的用户能够访 [!DNL Platform] 问沙箱环境中授予他们访问权限的功能。 默认Experience Platform许可证会授予您五个沙箱（一个生产箱和四个非生产箱）。 您最多可以添加十个非生产沙箱，最多共添加75个沙箱。 有关详细信息，请与IMS组织管理员或Adobe销售代表联系。

有关中沙箱的详 [!DNL Experience Platform]细信息，请参阅沙 [箱概述](../sandboxes/home.md)。

### 访问沙箱

对沙箱的访问通过产品用户档案进行管理。 有关如何启用对产品用户档案的沙箱访问的详细步骤，请参阅 [访问控制用户指南](./ui/overview.md)。

可以向用户授予对产品用户档案中一个或多个沙箱的访问权限。 如果一个用户包含在两个或多个产品用户档案中，该用户将有权访问这些用户档案中包含的所有沙箱。

“沙箱管理”权限允许用户管理、视图或重置沙箱。

### 权限

产 **品用户档案** 中的“权限”选项卡显示该用户档案处于活动状态的沙箱和权限：

![](./images/permissions-overview.png)

通过类别授予的权 [!DNL Admin Console] 限按排序，并授予对几个低级功能的访问权限。

下表概述了中的可用权 [!DNL Experience Platform] 限， [!DNL Admin Console]以及这些权限授予的 [!DNL Platform] 特定权能的说明。 有关如何向产品用户档案添加权限的详细步骤，请参阅 [访问控制用户指南](./ui/overview.md)。

| 类别 | 权限 | 描述 |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL 管理模式] | 访问读取、创建、编辑和删除模式及相关资源。 |
| [!DNL Data Modeling] | [!UICONTROL 查看架构] | 对模式和相关资源的只读访问。 |
| [!DNL Data Management] | [!UICONTROL 管理数据集] | 访问读取、创建、编辑和删除数据集。 模式的只读访问。 |
| [!DNL Data Management] | [!UICONTROL 查看数据集] | 数据集和模式的只读访问。 |
| [!DNL Data Management] | [!UICONTROL 数据监控] | 对监视数据集和流的只读访问。 |
| [!DNL Profile Management] | [!UICONTROL 管理用户档案] | 访问用于客户用户档案的读取、创建、编辑和删除数据集。 对可用用户档案的只读访问。 |
| [!DNL Profile Management] | [!UICONTROL 视图用户档案] | 对可用用户档案的只读访问。 |
| [!DNL Profile Management] | [!UICONTROL 导出区段受众] | 能够将评估的受众段导出到数据集。 |
| [!DNL Identities] | [!UICONTROL 管理身份命名空间] | 访问读取、创建、编辑和删除身份命名空间。 |
| [!DNL Identities] | [!UICONTROL 视图身份命名空间] | 身份命名空间的只读访问。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理沙箱] | 访问读取、创建、编辑和删除沙箱。 |
| [!DNL Sandbox Administration] | [!UICONTROL 查看沙盒] | 对属于您组织的沙箱的只读访问权限。 |
| [!DNL Sandbox Administration] | [!UICONTROL 重置沙箱] | 能够重置沙箱。 |
| [!DNL Destinations] | [!UICONTROL 管理目标] | 访问读取、创建、编辑和禁用目标。* |
| [!DNL Destinations] | [!UICONTROL 视图目标] | 对“目录”选项卡中可用目标和“浏 **[!UICONTROL 览]** ”选项卡中已验证目标的只 **[!UICONTROL 读访问]** 。* |
| [!DNL Destinations] | [!UICONTROL 激活目标] | 能够将数据激活到已创建的活动目标。 此权限要求向将激活目标 [!UICONTROL 的用户] 授予“视图目标”或“管理目标”。* |
| [!DNL Data Ingestion] | [!UICONTROL 管理源] | 访问读取、创建、编辑和禁用源。 |
| [!DNL Data Ingestion] | [!UICONTROL 视图源] | 对“目录”选项卡中的可用源和“浏览” **[!UICONTROL 选项卡中]** 经过身份验证的源进行只 **[!UICONTROL 读访问]** 。 |
| [!DNL Data Science Workspace] | [!UICONTROL 管理数据科学工作区] | 在中访问读取、创建、编辑和删除 [!DNL Data Science Workspace]。 |

_(*)本许可要求对此作出规定[!DNL Real-time Customer Data Platform]。 有关实时CDP的详细信息，请首先阅读实[时CDP概述](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/overview.html)。_

## 后续步骤

阅读本指南，您便了解了访问控制的主要原则 [!DNL Experience Platform]。 您现在可以继续阅读 [访问控制用户指南](./ui/overview.md) ，详细了解如何使用 [!DNL Admin Console] 创建产品用户档案和为其分配权限 [!DNL Platform]。
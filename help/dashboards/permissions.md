---
solution: Experience Platform
title: 如何获取和授予Experience Platform仪表板的访问权限
type: Documentation
description: 允许用户使用Adobe Admin Console查看、编辑和更新Experience Platform功能板。
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 6%

---

# 仪表板的访问权限

要授予用户查看、编辑和更新功能板的能力，您必须首先启用权限。 在Adobe Experience Platform中，访问控制是通过 [Adobe Admin Console](https://adminconsole.adobe.com/). 用户通过中的产品配置文件与权限和沙盒关联。 [!DNL Admin Console].

本文档概述了功能板的可用权限，包括这些功能板授予访问权限的功能及其启用的用户功能。 有关获取和分配访问权限的详细信息，请首先阅读 [访问控制概述](../access-control/home.md).

## 先决条件

为了配置访问控制 [!DNL Experience Platform]时，您必须对拥有 [!DNL Experience Platform] 产品集成。 请参阅Adobe Help Center文章，网址为 [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 了解更多信息。

## 可用的仪表板权限 {#available-permissions}

此 [!DNL Dashboards] 服务提供三种权限，在组合使用时，可提供对的完全访问 [!UICONTROL 配置文件]， [!UICONTROL 区段]， [!UICONTROL 目标]、和 [!UICONTROL 许可证使用情况] Adobe Experience Platform中的功能板。 这些权限包括：

| 权限 | 描述 |
|---|---|
| **管理标准功能板** | 此权限是 **全局读写权限**. 它允许您 [创建自定义构件](./customize/custom-widgets.md) 和 [编辑构件架构](./customize/edit-schema.md) 通过 [!UICONTROL 构件库]. |
| **查看标准仪表板** | 这提供了 **只读** 的功能 [!UICONTROL 配置文件]， [!UICONTROL 目标]、和 [!UICONTROL 区段] 功能板，并允许通过Platform的左侧导航访问它们。 报告还补充说 [!UICONTROL 仪表板] 左侧导航并访问 [!UICONTROL 仪表板] 清点与集成选项卡。 |
| **查看许可证使用情况仪表板** | 此权限允许用户执行以下操作 **只读** 访问 [许可证使用情况仪表板](./guides/license-usage.md) 在Experience PlatformUI中。 |

有五个权限未包含在 [!DNL Dashboard] 根据您的需求可能需要的类别。 下表概述了它们在Admin Console中的类别位置：

>[!IMPORTANT]
>
>两者都是 **[!DNL Manage Standard Dashboards]** 和 **[!DNL View Standard Dashboards]** 权限 **需要** 来自的“查看”或“管理”权限 [!DNL Profile Management] 或 [!DNL Destinations] Admin Console类别，以激活Platform UI中的相关部分。

| 权限 | Admin Console类别位置 |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## 访问控制矩阵

以下访问控制矩阵提供了哪些权限是必需的，以及这些权限提供了哪些功能用于访问不同的仪表板功能。 权限在顶部水平行中列出，Platform UI工作区在左栏中列出。

|  | [!UICONTROL 查看标准功能板] 或 [!UICONTROL 管理标准功能板] | [!UICONTROL 查看配置文件]，<br/>[!UICONTROL 查看区段]，<br/> [!UICONTROL 查看目标] | [!UICONTROL 管理查询] 和 [!UICONTROL 管理沙盒] | [!UICONTROL 查看许可证使用情况仪表板] |
|---|---|---|---|---|
| [!DNL Profiles]，<br/>[!DNL Segments]，<br/>[!DNL Destinations] 左侧导航栏中。 | 不适用 | **需要“查看”或“管理”权限** 每个仪表板的。 | 不适用 | 不适用 |
| [!DNL Dashboards] 左侧导航栏中。 | 已启用 | **至少需要一个**. | 不适用 | 不适用 |
| [!DNL Dashboards] [!DNL Inventory] <br/>（浏览选项卡） | 已启用 | 不适用 | 不适用 | 不适用 |
| [!DNL Dashboards] [!DNL Integrations] 选项卡 <br/>(用于安装Power BI) | 已启用 | **至少需要一个** | 不适用 | 不适用 |
| “安装”Power BI和工作流程 | 已启用 | 不适用 | **必需** | 不适用 |
| [!DNL Profiles]，<br/>[!DNL Segments]，<br/>[!DNL Destinations] 功能板。<br/>能够编辑构件架构并为构件自定义添加新属性 | **需要Manage-standard-dashboard** | **必需（对于每个仪表板）** | 不适用 | 不适用 |
| [!DNL License Usage Dashboard] | 不适用 | 不适用 | 不适用 | 已启用 |

{style="table-layout:auto"}

## 将权限添加到您的产品配置文件

使用上面提供的信息向产品配置文件添加适当的权限。 有关以下内容的完整说明，请参阅文档 [如何通过访问控制用户界面添加权限](../access-control/ui/permissions.md).

有关权限的描述，请参阅 [可用权限](#available-permissions) 章节。

>[!NOTE]
>
>您不必为所有用户启用所有权限。 根据贵组织的结构，您可能希望为某些用户创建单独的产品配置文件并授予有限访问权限（例如只读）。 请参阅有关管理产品配置文件的用户文档，了解更多信息 [如何为特定用户分配权限](../access-control/ui/users.md).

添加必要的访问权限后，组织内的用户可以开始在Experience PlatformUI中查看功能板，并根据您分配的权限执行其他操作。

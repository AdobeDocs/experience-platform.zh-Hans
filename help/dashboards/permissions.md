---
solution: Experience Platform
title: 如何获取和授予Experience Platform功能板的访问权限
type: Documentation
description: 允许用户使用Adobe Admin Console查看、编辑和更新Experience Platform功能板。
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 6%

---

# 仪表板的访问权限

要授予用户查看、编辑和更新功能板的能力，您必须首先启用权限。 在Adobe Experience Platform中，通过[Adobe Admin Console](https://adminconsole.adobe.com/)提供访问控制。 用户通过[!DNL Admin Console]中的产品配置文件与权限和沙盒相关联。

本文档总结了功能板的可用权限，包括它们授予访问权限的功能以及它们启用的用户功能。 有关获取和分配访问权限的详细信息，请先阅读[访问控制概述](../access-control/home.md)。

## 先决条件

为了配置[!DNL Experience Platform]的访问控制，您必须对具有[!DNL Experience Platform]产品集成的组织具有管理员权限。 有关详细信息，请参阅有关[管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html)的Adobe帮助中心文章。

## 可用的仪表板权限 {#available-permissions}

[!DNL Dashboards]服务提供了三种权限，组合这些权限后，它们可提供对Adobe Experience Platform中[!UICONTROL 用户档案]、[!UICONTROL 区段]、[!UICONTROL 目标]和[!UICONTROL 许可证使用情况]仪表板的完全访问权限。 这些权限包括：

| 权限 | 描述 |
|---|---|
| **管理标准仪表板** | 此权限是&#x200B;**全局读写权限**。 它允许您[创建自定义构件](./customize/custom-widgets.md)和通过[!UICONTROL 构件库]编辑构件架构[&#128279;](./customize/edit-schema.md)。 |
| **查看标准仪表板** | 这为[!UICONTROL 配置文件]、[!UICONTROL 目标]和[!UICONTROL 区段]仪表板提供&#x200B;**只读**&#x200B;功能，并允许通过Experience Platform的左侧导航访问它们。 它还将[!UICONTROL 仪表板]添加到左侧导航并访问[!UICONTROL 仪表板]清单和集成选项卡。 |
| **查看许可证使用情况仪表板** | 此权限允许用户在Experience Platform UI中&#x200B;**只读**&#x200B;访问[许可证使用情况仪表板](./guides/license-usage.md)。 |

根据您的需求，[!DNL Dashboard]类别中可能未包含五个权限。 下表概述了它们在Admin Console中的类别位置：

>[!IMPORTANT]
>
>**[!DNL Manage Standard Dashboards]**&#x200B;和&#x200B;**[!DNL View Standard Dashboards]**&#x200B;权限&#x200B;**都需要**&#x200B;来自Admin Console中[!DNL Profile Management]或[!DNL Destinations]类别的“查看”或“管理”权限，才能激活Experience Platform UI中的相关部分。

| 权限 | Admin Console类别位置 |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## 访问控制矩阵

以下访问控制矩阵提供了哪些权限是必需的，以及它们提供的有关访问不同功能板功能的功能的功能划分。 权限在水平顶行中列出，Experience Platform UI工作区在左栏中列出。

|   | [!UICONTROL 查看标准仪表板]或[!UICONTROL 管理标准仪表板] | [!UICONTROL 查看配置文件]，<br/>[!UICONTROL 查看区段]，<br/> [!UICONTROL 查看目标] | [!UICONTROL 管理查询]和[!UICONTROL 管理沙盒] | [!UICONTROL 查看许可证使用情况仪表板] |
|---|---|---|---|---|
| 左侧导航栏中的[!DNL Profiles]，<br/>[!DNL Segments]，<br/>[!DNL Destinations]。 | 不适用 | **每个仪表板都需要**&#x200B;的“查看”或“管理”权限。 | 不适用 | 不适用 |
| 左侧导航中的[!DNL Dashboards]。 | 已启用 | **至少需要一个**。 | 不适用 | 不适用 |
| [!DNL Dashboards] [!DNL Inventory] <br/>（浏览选项卡） | 已启用 | 不适用 | 不适用 | 不适用 |
| [!DNL Dashboards] [!DNL Integrations]选项卡<br/>(用于安装Power BI) | 已启用 | **至少需要一个** | 不适用 | 不适用 |
| Power BI安装按钮和工作流程 | 已启用 | 不适用 | **必需** | 不适用 |
| [!DNL Profiles]，<br/>[!DNL Segments]，<br/>[!DNL Destinations]仪表板。<br/>能够编辑构件架构和添加用于构件自定义的新属性 | **需要Manage-standard-dashboard** | **必需（对于每个仪表板）** | 不适用 | 不适用 |
| [!DNL License Usage Dashboard] | 不适用 | 不适用 | 不适用 | 已启用 |

{style="table-layout:auto"}

## 向产品配置文件添加权限

使用上面提供的信息向产品配置文件添加适当的权限。 有关[如何通过访问控制UI](../access-control/ui/permissions.md)添加权限的完整说明，请参阅文档。

有关权限的描述，请参阅本文档前面的[可用权限](#available-permissions)部分。

>[!NOTE]
>
>您不必为所有用户启用所有权限。 根据您组织的结构，您可能希望为某些用户创建单独的产品配置文件并授予有限访问权限（例如只读）。 请参阅有关管理产品配置文件的用户的文档，以了解[如何为特定用户分配权限](../access-control/ui/users.md)。

添加必要的访问权限后，贵组织中的用户可以开始在Experience Platform UI中查看功能板，并根据您分配的权限执行其他操作。

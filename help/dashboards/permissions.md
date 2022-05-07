---
solution: Experience Platform
title: 如何获取和授予Experience Platform功能板的访问权限
type: Documentation
description: 授予用户使用Adobe Admin Console查看、编辑和更新Experience Platform功能板的功能。
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: 052e365c6127961363b7b5333cb0f4f82ab5479a
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 6%

---

# 功能板的访问权限

要授予用户查看、编辑和更新功能板的功能，您必须首先启用权限。 在Adobe Experience Platform中，访问控制通过 [Adobe Admin Console](https://adminconsole.adobe.com/). 用户可通过 [!DNL Admin Console].

本文档概要介绍了功能板的可用权限，包括功能板授予的访问权限以及用户启用的功能。 有关获取和分配访问权限的详细信息，请首先阅读 [访问控制概述](../access-control/home.md).

## 先决条件

为配置 [!DNL Experience Platform]，则您必须具有具有 [!DNL Experience Platform] 产品集成。 请参阅Adobe Help Center上的 [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 以了解更多信息。

## 可用的功能板权限 {#available-permissions}

的 [!DNL Dashboards] 服务提供了三个权限，这些权限在组合后可提供对 [!UICONTROL 用户档案], [!UICONTROL 区段], [!UICONTROL 目标]和 [!UICONTROL 许可证使用情况] Adobe Experience Platform中的功能板。 这些权限包括：

| 权限 | 描述 |
|---|---|
| **管理标准功能板** | 此权限是 **全局读取和写入权限**. 它允许您 [创建自定义小组件](./customize/custom-widgets.md) 和 [编辑小组件架构](./customize/edit-schema.md) 到 [!UICONTROL 构件库]. |
| **查看标准功能板** | 这提供了 **只读** 功能 [!UICONTROL 用户档案], [!UICONTROL 目标]和 [!UICONTROL 区段] 功能板，并允许通过平台的左侧导航访问这些功能板。 它还补充说 [!UICONTROL 功能板] ，并访问 [!UICONTROL 功能板] “清单和集成”选项卡。 |
| **查看许可证使用情况功能板** | 此权限允许用户 **只读** 访问 [许可证使用仪表板](./guides/license-usage.md) Experience PlatformUI中。 |

有五个权限未包含在 [!DNL Dashboard] 类别。 下表概述了它们在Admin Console中的类别位置：

>[!IMPORTANT]
>
>和 **[!DNL Manage Standard Dashboards]** 和 **[!DNL View Standard Dashboards]** 权限 **要求** “查看”或“管理”权限 [!DNL Profile Management] 或 [!DNL Destinations] 类别来激活平台UI中的相关部分。

| 权限 | Admin Console类别位置 |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## 访问控制矩阵

下面的访问控制矩阵提供了需要哪些权限以及这些权限提供了哪些功能来访问不同的功能板功能的细分。 权限列在顶部水平行中，平台UI工作区列在左列。

|  | [!UICONTROL 查看标准功能板] 或 [!UICONTROL 管理标准功能板] | [!UICONTROL 查看配置文件],<br/>[!UICONTROL 查看区段],<br/> [!UICONTROL 查看目标] | [!UICONTROL 管理查询] &amp; [!UICONTROL 管理沙箱] | [!UICONTROL 查看许可证使用情况功能板] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] 中。 | 不适用 | **需要“查看”或“管理”权限** 各个功能板。 | 不适用 | 不适用 |
| [!DNL Dashboards] 中。 | 已启用 | **至少需要一个**. | 不适用 | 不适用 |
| [!DNL Dashboards] [!DNL Inventory] <br/>（“浏览”选项卡） | 已启用 | 不适用 | 不适用 | 不适用 |
| [!DNL Dashboards] [!DNL Integrations] 选项卡 <br/>(用于安装Power BI) | 已启用 | **至少需要一个** | 不适用 | 不适用 |
| Power BI安装按钮和工作流 | 已启用 | 不适用 | **必需** | 不适用 |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] 功能板。<br/>能够编辑小组件架构并添加新属性以进行小组件自定义 | **需要管理标准功能板** | **必需（对于每个功能板）** | 不适用 | 不适用 |
| [!DNL License Usage Dashboard] | 不适用 | 不适用 | 不适用 | 已启用 |

{style=&quot;table-layout:auto&quot;}

## 向产品配置文件添加权限

使用上面提供的信息，向产品用户档案添加相应的权限。 有关 [如何通过访问控制UI添加权限](../access-control/ui/permissions.md).

有关权限的描述，请参阅 [可用权限](#available-permissions) 部分。

>[!NOTE]
>
>您不必为所有用户启用所有权限。 根据贵组织的结构，您可能希望为某些用户创建单独的产品配置文件并授予有限的访问权限（例如只读）。 请参阅有关管理产品配置文件用户的文档，以了解 [如何为特定用户分配权限](../access-control/ui/users.md).

添加必要的访问权限后，您组织内的用户可以开始在Experience PlatformUI中查看功能板，并根据您分配的权限执行其他操作。

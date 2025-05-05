---
title: 基于属性的访问控制权限管理器
description: 了解如何使用Adobe Experience Platform中的权限管理器来生成报表和验证访问权限。
exl-id: 4c2b8b8e-ac4f-4c6e-a23f-66f658bb6e24
source-git-commit: 7e65e88bc49ea28d567e8204db877d22ddb8d9a6
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 7%

---

# 权限管理器

>[!NOTE]
>
>要访问[!UICONTROL 权限管理器]，您必须是产品管理员。 如果您没有管理员权限，请联系您的系统管理员以获取访问权限。

在[!UICONTROL 权限管理器]中使用简单查询来创建简洁的报告，这些报告将帮助您了解访问管理，并节省验证多个工作流和粒度级别的访问权限的时间。 您可以利用[!UICONTROL 权限管理器]查找属于用户组并具有指定访问权限的用户以及具有特定标签的角色。

## 搜索指定用户组中的用户 {#search-users}

>[!CONTEXTUALHELP]
>id="platform_permission_manager"
>title="权限管理器"
>abstract="使用页面上的下拉选择器来获取用户和角色的不同粒度的访问级别报告。"
<!-- >additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-manager/permissions.html?lang=zh-Hans" text="Permission manager" -->

使用下拉列表选择属性&#x200B;**[!UICONTROL 用户]**。

![突出显示用户的属性下拉列表。](../../images/permission-manager/users-select.png)

接下来，使用下拉列表选择要搜索的&#x200B;**[!UICONTROL 用户组]**。

>[!INFO]
>
>[!UICONTROL 用户组]不是必填字段。 您只能为每个报表选择一个用户组。

![用户组下拉列表突出显示。](../../images/permission-manager/user-group-select.png)

对于更细粒度的报告，您可以在特定沙盒中通过操作指定资源。 使用下拉菜单选择&#x200B;**[!UICONTROL 资源]**、**[!UICONTROL 操作]**&#x200B;和&#x200B;**[!UICONTROL 沙盒]**，然后选择&#x200B;**[!UICONTROL 显示结果]**。

>[!INFO]
>
>[!UICONTROL 资源]、[!UICONTROL 操作]和[!UICONTROL 沙盒]不是必填字段。 在添加操作或沙盒后，通过选择要删除的选择旁边的&#x200B;**&#39;x&#39;**，可以删除该操作或沙盒。

![资源、操作、沙盒下拉列表和显示突出显示的结果](../../images/permission-manager/users-additional-attributes-select.png)

系统会根据所选标准报告用户及其电子邮件地址的列表。 使用左侧的过滤器菜单更新属性和结果。 有关特定用户的详细信息，请从列表中选择用户名。

![基于所选突出显示的属性生成的报表](../../images/permission-manager/users-report.png)

## 搜索具有特定标签的角色 {#search-roles}

使用下拉列表选择属性&#x200B;**[!UICONTROL 角色]**。

>[!INFO]
>
>[!UICONTROL 标签]不是必填字段。 您可以选择多个标签，选中后，这些标签将列在此下拉列表下方。 添加标签后，通过选择操作旁边的&#x200B;**&#39;x&#39;**&#x200B;可以删除标签。

![突出显示角色的属性下拉列表。](../../images/permission-manager/roles-select.png)

接下来，使用下拉列表选择要搜索的&#x200B;**[!UICONTROL 标签]**。

![标签下拉列表突出显示。](../../images/permission-manager/roles-labels-select.png)

对于更细粒度的报告，您可以在特定沙盒中通过操作指定资源。 使用下拉菜单选择&#x200B;**[!UICONTROL 资源]**、**[!UICONTROL 操作]**&#x200B;和&#x200B;**[!UICONTROL 沙盒]**，然后选择&#x200B;**[!UICONTROL 显示结果]**。

>[!INFO]
>
>[!UICONTROL 资源]、[!UICONTROL 操作]和[!UICONTROL 沙盒]不是必填字段。 每个报表只能选择一个[!UICONTROL 资源]。 在添加操作或沙盒后，通过选择要删除的选择旁边的&#x200B;**&#39;x&#39;**，可以删除该操作或沙盒。

![资源、操作、沙盒下拉列表和显示突出显示的结果](../../images/permission-manager/roles-additional-attributes-select.png)

系统会根据所选标准报告角色列表。 使用左侧的过滤器菜单更新属性和结果。 有关特定角色的详细信息，请从列表中选择该角色。

对于符合条件的每个角色，将显示以下信息：

| 属性 | 描述 |
| --- | --- |
| 描述 | 对角色的简短描述。 |
| 标记 | 与角色关联的标签列表。 |
| 沙盒 | 包含此角色的Sanbox列表。 |
| 修改时间 | 上次更新角色的日期和时间戳。 |
| 创建于 | 创建角色的日期和时间戳。 |
| 创建者 | 角色创建者的详细信息。 |

![基于所选突出显示的属性生成的报表](../../images/permission-manager/roles-report.png)

## 后续步骤

您现在已经了解如何为用户和角色生成报告。 要了解有关基于属性的访问控制的详细信息，请参阅[基于属性的访问控制概述](../overview.md)。

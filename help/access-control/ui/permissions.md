---
keywords: Experience Platform；主页；热门主题；产品配置文件；管理权限
solution: Experience Platform
title: 管理产品配置文件的权限
description: Adobe Experience Platform中的访问控制允许您使用Adobe Admin Console管理各种Platform功能的角色和权限。 本文档提供了有关如何管理Platform产品配置文件的权限的指南。
exl-id: ca403bef-6d62-4ca9-bba6-d1280ac63171
source-git-commit: 1812af74e82f3071963177356b3cd4b23ea567f5
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# 管理产品配置文件的权限

紧跟在 [创建新的产品配置文件](#create-a-new-product-profile)，则系统会提示您配置该配置文件的权限。 如果您正在编辑现有配置文件的权限，请从 **[!UICONTROL 产品配置文件]** 选项卡以打开用户档案的详细信息页面，然后选择 **[!UICONTROL 权限]**.

![权限](../images/permissions.png)

权限分为不同的类别，并在此页面上列出。 该列表显示类别名称、包含的权限数（以及活动的权限数）及其描述。 请参阅中的表。 [资源权限](/help/access-control/home.md#permissions) 以了解每个角色的可用权限划分。

选择列表上的任意类别以打开 **[!UICONTROL 编辑权限]** 页面。

![edit-permissions](../images/edit-permissions.png)

此 **[!UICONTROL 编辑权限]** 页面提供了一个工作区，用于在所选产品配置文件中添加和删除权限。 屏幕左侧显示权限类别的列表。 选择类别会更改下显示的权限 **[!UICONTROL 可用的权限项目]**.

例如，要更新数据建模的权限，请选择 **[!UICONTROL 数据建模]**.

![配置文件管理](../images/profile-management.png)

要添加权限，请选择加号 **(+)** 图标（在权限名称旁）。 或者，您可以选择 **[!UICONTROL 全部添加]** 以将当前类别下的所有权限添加到配置文件。 添加的权限显示在下 **[!UICONTROL 包含的权限项]**.

![add-permission](../images/add-permission.png)

>[!NOTE]
>
>此 **[!UICONTROL 包含的权限项目]** 列表仅显示当前选定类别中已添加的权限。

要删除权限，请选择 **X** 图标，或选择 **[!UICONTROL 全部移除]** 以删除当前类别下的所有权限。 已删除的权限会重新显示在下 **[!UICONTROL 可用的权限项]**.

继续浏览可用类别并添加任何所需的权限。 完成后，选择 **[!UICONTROL 保存]**.

![remove-permisson](../images/remove-permission.png)

此 **[!UICONTROL 权限]** 此时，产品配置文件的选项卡会重新出现，并显示选定的权限现在处于活动状态。

![权限已更新](../images/permissions-updated.png)

## 后续步骤

建立权限后，您可以继续下一步以 [管理产品配置文件的详细信息和服务](details-and-services.md)

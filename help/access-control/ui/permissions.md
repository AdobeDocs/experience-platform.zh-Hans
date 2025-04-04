---
keywords: Experience Platform；主页；热门主题；产品配置文件；管理权限
solution: Experience Platform
title: 管理产品配置文件的权限
description: Adobe Experience Platform中的访问控制允许您使用Adobe Admin Console管理各种Experience Platform功能的角色和权限。 本文档提供了如何管理Experience Platform产品配置文件的权限指南。
exl-id: ca403bef-6d62-4ca9-bba6-d1280ac63171
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# 管理产品配置文件的权限

在[创建新的产品配置文件](#create-a-new-product-profile)之后，系统会立即提示您配置配置文件的权限。 如果您正在编辑现有配置文件的权限，请从&#x200B;**[!UICONTROL 产品配置文件]**&#x200B;选项卡中选择该配置文件以打开配置文件的详细信息页面，然后选择&#x200B;**[!UICONTROL 权限]**。

![权限](../images/permissions.png)

权限分为不同的类别，并在此页面上列出。 该列表显示类别名称、包含的权限数（以及活动的权限数）及其描述。 请参阅[资源权限](/help/access-control/home.md#permissions)中的表，了解每个角色的可用权限划分。

选择列表上的任意类别以打开&#x200B;**[!UICONTROL 编辑权限]**&#x200B;页面。

![编辑权限](../images/edit-permissions.png)

**[!UICONTROL 编辑权限]**&#x200B;页面提供了一个工作区，用于添加和删除所选产品配置文件的权限。 屏幕左侧显示权限类别的列表。 选择类别会更改&#x200B;**[!UICONTROL 可用权限项]**&#x200B;下显示的权限。

例如，要更新数据建模的权限，请选择&#x200B;**[!UICONTROL 数据建模]**。

![配置文件管理](../images/profile-management.png)

要添加权限，请选择该权限名称旁边的加号&#x200B;**(+)**&#x200B;图标。 或者，您也可以选择&#x200B;**[!UICONTROL 全部添加]**&#x200B;以将当前类别下的所有权限添加到配置文件。 添加的权限显示在&#x200B;**[!UICONTROL 包含的权限项]**&#x200B;下。

![添加权限](../images/add-permission.png)

>[!NOTE]
>
>**[!UICONTROL 包含的权限项]**&#x200B;列表仅显示当前选定类别中已添加的权限。

要删除权限，请选择该权限名称旁边的&#x200B;**X**&#x200B;图标，或选择&#x200B;**[!UICONTROL 全部删除]**&#x200B;以删除当前类别下的所有权限。 已删除的权限重新出现在&#x200B;**[!UICONTROL 可用权限项]**&#x200B;下。

继续浏览可用类别并添加任何所需的权限。 完成后，选择&#x200B;**[!UICONTROL 保存]**。

![删除权限](../images/remove-permission.png)

产品配置文件的&#x200B;**[!UICONTROL 权限]**&#x200B;选项卡会重新出现，并显示选定的权限现在处于活动状态。

![权限已更新](../images/permissions-updated.png)

## 后续步骤

建立权限后，您可以继续下一步以[管理产品配置文件的详细信息和服务](details-and-services.md)

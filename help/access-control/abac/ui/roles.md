---
keywords: Experience Platform；主页；热门主题；访问控制；基于属性的访问控制；ABAC
title: 基于属性的访问控制创建角色
description: 通过Adobe Experience Cloud中的“权限”界面管理角色。
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: b665d0edce713f1b252e07125aabab79d52a9cba
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 13%

---

# 管理角色

<!-- UPDATE ROLES WITH A MORE COMPREHENSIVE EXPLANATION -->

要开始管理角色，请在&#x200B;**[!UICONTROL Permissions]** Adobe Experience Cloud[中导航到](https://experience.adobe.com/){target="_blank"}，然后在左侧面板中选择&#x200B;**[!UICONTROL Roles]**。

![权限中的角色工作区。](../../images/ui/roles/roles-overview.png)

## 创建新角色 {#create-new-role}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="创建新角色"
>abstract="创建新角色以更好地对与您的 Experience Platform 实例交互的用户进行分类。例如，可为内部营销团队创建一个角色，并将受监管的健康数据 (RHD) 标签应用于该角色，使您的内部营销团队可访问受保护的健康信息 (PHI)。或者，还可为外部机构创建一个角色，并通过不将 RHD 标签应用于该角色而拒绝该角色访问 PHI 数据。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=zh-Hans" text="管理角色"
>additional-url="https://experienceleague.adobe.com/zh-hans/docs/experience-platform/access-control/abac/end-to-end-guide#label-roles" text="将标签应用于角色"

要创建新角色，请选择&#x200B;**[!UICONTROL Create role]**。

>[!TIP]
>
>只读角色是现成可用的。 只读角色是一种角色，它允许用户查看数据、配置和UI功能，而无需更改系统状态。 管理员无法编辑这些角色，但可以将用户关联到角色。

![突出显示了“创建角色”选项的角色的工作区。](../../images/ui/roles/roles-create-role.png)

出现&#x200B;**[!UICONTROL Create new role]**&#x200B;对话框。 输入角色的&#x200B;**[!UICONTROL Name]**，也可以输入&#x200B;**[!UICONTROL Description]**，然后选择&#x200B;**[!UICONTROL Confirm]**。

![已填写名称和描述并突出显示“确认”选项的“创建新角色”对话框。](../../images/ui/roles/roles-create-new-role.png)

出现&#x200B;**[!UICONTROL Resources]**&#x200B;工作区。 通过滚动或在左侧面板的搜索栏中输入资源名称来查找所需的资源。 通过选择资源名称旁边的![加号图标](/help/images/icons/plus.png)来添加资源。

![突出显示单个资源的“添加”选项的资源工作区。](../../images/ui/roles/roles-resources.png)

<!-- ADD IN NOTE ABOUT THE DEFAULT SANDBOX - THIS SHOULD BE MENTIONED IN THE HIGHER LEVEL DOCS, WE MAY BE ABLE TO LINK TO IT -->

资源将添加到主工作区。 选择资源名称旁边的下拉列表，然后选择要添加到角色的权限。 您可以单独选择这些权限，选择&#x200B;**[!UICONTROL Add all]**，或者通过在搜索栏中输入权限名称来查找特定权限。

![扩展并突出显示带有单个资源的下拉菜单的资源工作区。](../../images/ui/roles/roles-resources-permissions.png)

继续选择要添加到角色的所有资源和权限。 完成后，选择&#x200B;**[!UICONTROL Save]**。

![突出显示了“保存”选项的资源工作区。](../../images/ui/roles/roles-resources-permissions-save.png)

您将收到一个警报，表明已成功保存角色。 选择&#x200B;**[!UICONTROL Close]**&#x200B;以返回到&#x200B;**[!UICONTROL Roles]**&#x200B;工作区。

![资源工作区中成功警报和“关闭”选项突出显示。](../../images/ui/roles/roles-resources-permissions-close.png)

已成功创建新角色，并且您被重定向到&#x200B;**[!UICONTROL Roles]**&#x200B;页面，您将看到新创建的角色显示在列表中。

<!-- The following video is intended to support your understanding of creating a new role and managing users for that role.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on) -->

## 复制角色

复制角色将会复制详细信息、权限、标签和沙盒。 用户、用户组和API凭据&#x200B;**未复制**，需要手动将其添加到该角色。

要复制现有角色，请在&#x200B;**[!UICONTROL Roles]**&#x200B;选项卡中查找要复制的角色。 选择角色名称旁边的![更多图标](/help/images/icons/more.png)，然后从下拉菜单中选择&#x200B;**[!UICONTROL Duplicate]**。

![角色的工作区中扩展了角色的下拉菜单，并突出显示了“复制”选项。](../../images/ui/roles/role-duplicate.png)

将显示复制确认对话框。 选择&#x200B;**[!UICONTROL Confirm]**&#x200B;以完成角色复制。 新角色将保存在相同的名称下，并将`_Copy`添加为后缀。

![突出显示带有“确认”选项的重复确认对话框。](../../images/ui/roles/role-duplicate-confirm.png)

或者，您可以从单个角色的工作区中复制角色。 从&#x200B;**[!UICONTROL Roles]**&#x200B;工作区中选择要复制的角色，然后选择&#x200B;**[!UICONTROL Duplicate]**。

![突出显示了“重复”选项的单个角色的工作区。](../../images/ui/roles/role-duplicate-alt.png)

将显示复制确认对话框。 选择&#x200B;**[!UICONTROL Confirm]**&#x200B;以完成角色复制。 您将被重定向到新角色。

![突出显示带有“确认”选项的重复确认对话框。](../../images/ui/roles/role-duplicate-alt-confirm.png)

## 删除角色

要删除角色，请在&#x200B;**[!UICONTROL Roles]**&#x200B;选项卡中查找要删除的角色。 选择角色名称旁边的![更多图标](/help/images/icons/more.png)，然后从下拉菜单中选择&#x200B;**[!UICONTROL Delete]**。

![角色的工作区中扩展了角色的下拉菜单，并突出显示了“复制”选项。](../../images/ui/roles/role-delete.png)

此时将显示删除确认对话框。 选择&#x200B;**[!UICONTROL Confirm]**&#x200B;以完成删除角色。

![突出显示带有“确认”选项的重复确认对话框。](../../images/ui/roles/role-duplicate-confirm.png)

或者，您可以从单个角色的工作区中删除角色。 从&#x200B;**[!UICONTROL Roles]**&#x200B;工作区中选择要删除的角色，然后选择&#x200B;**[!UICONTROL Delete]**。

![突出显示删除选项的单个角色的工作区。](../../images/ui/roles/role-delete-alt.png)

此时将显示删除确认对话框。 选择&#x200B;**[!UICONTROL Confirm]**&#x200B;以完成删除角色。

![突出显示带有“确认”选项的删除确认对话框。](../../images/ui/roles/role-delete-alt-confirm.png)

<!-- ADD PERMISSIONS TO THIS PAGE -->

## 后续步骤

创建新角色后，您可以继续下一步以[管理角色](permissions.md)的权限。

---
keywords: Experience Platform；主页；热门主题；访问控制；基于属性的访问控制；ABAC
title: 基于属性的访问控制管理用户
description: 通过Adobe Experience Cloud中的“权限”界面管理用户和用户组。
exl-id: 16450867-040a-4be1-a6c0-f03d0a1b90ba
source-git-commit: b665d0edce713f1b252e07125aabab79d52a9cba
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 4%

---

# 管理用户和添加用户组 {#manage-users}

>[!CONTEXTUALHELP]
>id="platform_permissions_users_about"
>title="什么是用户？"
>abstract="用户是有权访问 Experience Platform 的个人。个人用户对组织资源的访问权限通过角色进行管理。"
>additional-url="https://experienceleague.adobe.com/zh-hans/docs/experience-platform/access-control/abac/permissions-ui/roles" text="管理角色"

用户是有权访问Adobe Experience Platform的个人。 单个用户对组织资源的访问权限通过[角色](./roles.md){target="_blank"}进行管理。 组织还可以创建[用户组](#user-groups)，以便同时为多个用户提供无缝访问。 用户在Admin Console中进行管理，与Adobe Experience Platform产品卡关联的用户会显示为Experience Platform用户列表的一部分。

## 管理用户

<!-- ADD LINKS INTO IMPORTANT NOTE BELOW
>[!IMPORTANT]
>
>[!UICONTROL Permissions] manages access control for existing Experience Platform users. To add users to Experience Platform, navigate to Adobe Admin Console through the **[!UICONTROL Edit in admin console]** option. To learn how to add users through the Admin Console, follow the [adding users to Experience Platform](...){#target="_blank"} guide.
-->

要查看您组织的用户，请在&#x200B;**[!UICONTROL Permissions]** Adobe Experience Cloud[中导航到](https://experience.adobe.com/){target="_blank"}。 在左侧面板中选择&#x200B;**[!UICONTROL Users]**。

![权限内的用户工作区。](../../images/ui/users/users-overview.png){zoomable="yes"}

此时将显示一个用户列表。 从列表中选择要查看的用户。 或者，使用搜索栏通过输入用户的姓名或电子邮件地址来搜索用户。

**[!UICONTROL Details]**&#x200B;选项卡提供用户的概述。 概述显示用户的&#x200B;**[!UICONTROL Name]**、**[!UICONTROL Preferred languages]**、**[!UICONTROL Account Type]**、**[!UICONTROL Authentication ID]**、**[!UICONTROL Email]**、**[!UICONTROL Email verified]**&#x200B;状态、**[!UICONTROL Country code]**&#x200B;和&#x200B;**[!UICONTROL Phone number]**。

![用户的详细信息工作区。](../../images/ui/users/user-details.png){zoomable="yes"}

选择&#x200B;**[!UICONTROL Roles]**&#x200B;选项卡以查看用户被分配到的角色。

![用户的角色工作区。](../../images/ui/users/user-roles.png){zoomable="yes"}

### 向用户添加角色 {#add-user-role}

要向用户添加角色，请选择&#x200B;**[!UICONTROL Add Roles]**。

![突出显示了“添加角色”选项的用户角色的工作区。](../../images/ui/users/user-add-roles.png){zoomable="yes"}

出现&#x200B;**[!UICONTROL Add Roles]**&#x200B;对话框。 选择要添加到用户的角色，然后选择&#x200B;**[!UICONTROL Save]**。

![添加角色对话框，其中选定了角色，并突出显示了“保存”选项。](../../images/ui/users/user-roles-add-roles-confirm.png){zoomable="yes"}

### 从用户中删除角色 {#remove-user-role}

要从用户中删除角色，请选择该角色名称旁边的&#x200B;**X**。

<!-- ADD LINKS INTO IMPORTANT NOTE BELOW

>[!NOTE]
>
>Role's that have been added to a user through a user group cannot be removed through the user's role workspace. Role's that have been added through a user group will have an [!Info icon](/help/images/icons/info.png) beside the **X** containing information about the associated user group. To remove the role, the role would need to be [removed from the user group](#remove-user-group-role).
-->

![突出显示角色删除选项的用户角色工作区。](../../images/ui/users/user-roles-remove.png){zoomable="yes"}

将显示确认对话框。 选择&#x200B;**[!UICONTROL Confirm]**&#x200B;以完成删除角色。

![用于删除角色且突出显示“确认”选项的确认对话框。](../../images/ui/users/user-roles-remove.png){zoomable="yes"}

## 管理用户组 {#user-groups}

用户组是多个已分组在一起的用户，并且有权执行相同的功能。

<!-- ADD LINKS INTO IMPORTANT NOTE BELOW
>[!IMPORTANT]
>
>[!UICONTROL Permissions] manages access control for existing Experience Platform user groups. To add user groups to Experience Platform, navigate to Admin Console through the **[!UICONTROL Edit in admin console]** option. To learn how to add user groups in the Admin Console, follow the [adding user groups to Experience Platform](...){#target="_blank"} guide.
 -->

要查看您组织的用户，请在&#x200B;**[!UICONTROL Permissions]** Adobe Experience Cloud[中导航到](https://experience.adobe.com/){target="_blank"}。从左侧面板的&#x200B;**[!UICONTROL Groups]**&#x200B;部分中选择&#x200B;**[!UICONTROL Users]**。

![权限中的用户组工作区。](../../images/ui/users/user-groups-overview.png){zoomable="yes"}

此时将显示用户组列表。 从列表中选择要查看的组。

**[!UICONTROL Details]**&#x200B;选项卡提供用户组的概述。 该概述显示组的&#x200B;**[!UICONTROL Name]**、**[!UICONTROL Description]**、**[!UICONTROL User Count]**&#x200B;和&#x200B;**[!UICONTROL Admin count]**。

![用户组的详细信息工作区。](../../images/ui/users/user-group-details.png){zoomable="yes"}

选择&#x200B;**[!UICONTROL Users]**&#x200B;选项卡以查看分配给该组的用户列表。

![用户组的用户工作区。](../../images/ui/users/user-group-users.png){zoomable="yes"}

选择&#x200B;**[!UICONTROL Roles]**&#x200B;选项卡以查看当前分配给该组的角色列表。

![用户组的角色工作区。](../../images/ui/users/user-group-roles.png){zoomable="yes"}

### 向用户组添加角色 {#add-user-group-role}

要向组添加新角色，请选择&#x200B;**[!UICONTROL Add Roles]**。

![突出显示了“添加角色”选项的用户组的“角色”工作区。](../../images/ui/users/user-group-add-roles.png){zoomable="yes"}

出现&#x200B;**[!UICONTROL Add Roles]**&#x200B;对话框。 选择要添加的角色，然后选择&#x200B;**[!UICONTROL Save]**。 将为属于该用户组的所有用户添加角色。

![选定角色并突出显示“保存”选项的“添加角色”对话框。](../../images/ui/users/user-group-add-roles-select.png){zoomable="yes"}

### 从用户组中删除角色 {#remove-user-group-role}

要从用户组中删除角色，请选择该角色名称旁边的&#x200B;**X**。

![突出显示具有角色删除选项的用户组的角色工作区。](../../images/ui/users/user-group-remove-role.png){zoomable="yes"}

将显示确认对话框。 选择&#x200B;**[!UICONTROL Confirm]**&#x200B;以完成删除角色。

![用于删除角色且突出显示“确认”选项的确认对话框。](../../images/ui/users/user-group-remove-role-confirm.png){zoomable="yes"}

## API凭据

>[!IMPORTANT]
>
>只有系统管理员才能在“权限”中查看和管理API凭据。

要以用户或开发人员身份使用Experience Platform API，系统管理员需要在角色的给定权限集之外添加API凭据。 权限允许您向角色分配之前创建并分配给Experience Platform产品的API凭据。 有关创建和分配API凭据以及所需权限的完整指南，请参阅[身份验证和访问Experience Platform API](/help/landing/api-authentication.md){target="_blank"}中的分步教程。

要查看与Experience Platform关联的组织API凭据，请在&#x200B;**[!UICONTROL Permissions]** Adobe Experience Cloud[中导航到](https://experience.adobe.com/){target="_blank"}。 从左侧面板的&#x200B;**[!UICONTROL API Credentials]**&#x200B;部分中选择&#x200B;**[!UICONTROL Users]**。

![权限内的API凭据工作区。](../../images/ui/users/api-credentials-overview.png){zoomable="yes"}

>[!NOTE]
>
> 要查看您组织中所有产品的API凭据，或有关凭据的更多信息，请选择&#x200B;**[!UICONTROL Edit in admin console]**。

此时将显示API凭据列表。 从列表中选择要查看的API凭据。

**[!UICONTROL Details]**&#x200B;选项卡提供了API凭据的概述。 概述显示凭据的&#x200B;**[!UICONTROL Name]**、**[!UICONTROL Modified]**&#x200B;日期、**[!UICONTROL Modified By]**&#x200B;属性、**[!UICONTROL Created]**&#x200B;日期、**[!UICONTROL Created by]**&#x200B;属性、**[!UICONTROL API key]**、**[!UICONTROL Technical ID]**&#x200B;和&#x200B;**[!UICONTROL Email]**。

![API凭据的详细信息工作区。](../../images/ui/users/api-credential-details.png){zoomable="yes"}

选择 **[!UICONTROL Roles]** 选项卡。将显示与API凭据关联的角色列表。

![API凭据的角色工作区。](../../images/ui/users/api-credential-roles.png){zoomable="yes"}

### 向API凭据添加角色 {#add-api-credential-role}

要将角色添加到API凭据，请选择&#x200B;**[!UICONTROL Add Roles]**。

![突出显示了“添加角色”选项的API凭据的工作区。](../../images/ui/users/api-credential-add-roles.png){zoomable="yes"}

出现&#x200B;**[!UICONTROL Add Roles]**&#x200B;对话框。 选择要添加到用户的角色，然后选择&#x200B;**[!UICONTROL Save]**。

![添加角色对话框，其中选定了角色，并突出显示了“保存”选项。](../../images/ui/users/api-credential-add-roles-select.png){zoomable="yes"}

### 从API凭据中删除角色 {#remove-api-credential-role}

要从API凭据中删除角色，请选择API凭据名称旁边的&#x200B;**X**。

![突出显示角色删除选项的API凭据的角色工作区。](../../images/ui/users/api-credential-remove-role.png){zoomable="yes"}

将显示确认对话框。 选择&#x200B;**[!UICONTROL Confirm]**&#x200B;以完成删除角色。

![用于删除角色且突出显示“确认”选项的确认对话框。](../../images/ui/users/api-credential-remove-role-confirm.png){zoomable="yes"}

## 后续步骤

您现在知道如何查看用户、用户组和API凭据的详细信息和角色。 要了解有关基于属性的访问控制的详细信息，请参阅[基于属性的访问控制概述](../overview.md)。

<!--
The following video is intended to support your understanding of developer and API credentials.

>[!VIDEO](https://video.tv.adobe.com/v/3446408/?captions=chi_hans&learn=on)
-->
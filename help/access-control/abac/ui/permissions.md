---
keywords: Experience Platform；主页；热门主题；访问控制；基于属性的访问控制；ABAC
title: 基于属性的访问控制管理角色权限
description: 本文档提供了有关通过Adobe Experience Cloud中的“权限”界面为角色配置权限的信息
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 2%

---

# 管理角色的权限

>[!IMPORTANT]
>
>访问控制使用用户ID（分配给用户的内部唯一ID）来授予权限。 当组织从Adobe ID迁移到Business ID时，为其用户设置的所有权限将丢失，因为用户ID发生更改，访问控制将使用新生成的用户ID。 如果贵组织迁移到Business ID，请联系您的Adobe代表以将用户ID从Adobe ID迁移到Business ID。

权限是Experience Cloud的区域，管理员可以在其中定义用户角色和访问策略，以管理产品应用程序中功能和对象的访问权限。

通过权限，您可以创建和管理角色，并为这些角色分配所需的资源权限。 权限还允许您管理与特定角色关联的标签、沙盒和用户。

在[创建新角色](#create-a-new-role)之后，您立即返回到&#x200B;**[!UICONTROL 角色]**&#x200B;选项卡。 如果您正在编辑现有角色的权限，请从&#x200B;**[!UICONTROL 角色]**&#x200B;选项卡中选择该角色。 或者，使用筛选器选项筛选结果以查找角色。

## 筛选器角色

选择漏斗图标（![筛选器图标](/help/images/icons/filter.png)）以显示筛选器控件列表，帮助缩小结果范围。

![flac-filters](../../images/flac-ui/flac-filters.png)

以下过滤器可用于UI中的角色：

| 筛选条件 | 描述 |
| --- | --- |
| [!UICONTROL 创建时间介于]之间 | 选择开始日期和/或结束日期，以定义筛选结果的日期范围。 |
| [!UICONTROL 创建者] | 通过从下拉菜单中选择用户，按角色创建者过滤。 |
| [!UICONTROL 修改时间介于]之间 | 选择开始日期和/或结束日期，以定义筛选结果的日期范围。 |
| [!UICONTROL 修改者] | 通过从下拉列表中选择用户，按角色修饰符筛选。 |

要移除过滤器，请选择相关过滤器的药丸图标上的“X”，或选择&#x200B;**[!UICONTROL 全部清除]**&#x200B;以移除所有过滤器。

![flac-clear-filters](../../images/flac-ui/flac-clear-filters.png)

## 角色详细信息

从&#x200B;**[!UICONTROL 角色]**&#x200B;选项卡中选择角色，这将打开角色的详细信息页面。

![flac-details](../../images/flac-ui/flac-details.png)

详细信息选项卡提供了角色的概述。 该概述显示了角色名称、角色说明、创建和修改角色的用户的名称、创建和修改角色的时间以及附加到角色的权限。 如果需要，可以修改角色名称和角色描述。

## 管理角色的标签

选择&#x200B;**[!UICONTROL 标签]**&#x200B;选项卡以打开角色标签页，然后选择&#x200B;**[!UICONTROL 添加标签]**&#x200B;以将标签分配给角色。

![flac-labels](../../images/flac-ui/flac-labels.png)

此页面上列出了标签。 该列表显示标签名称、友好名称、类别及其说明。

从列表中选择要添加到角色的标签，然后选择&#x200B;**[!UICONTROL 保存]**

![flac-add-labels](../../images/flac-ui/flac-add-labels.png)

添加的标签显示在&#x200B;**[!UICONTROL 标签]**&#x200B;选项卡下。

![flac添加的标签](../../images/flac-ui/flac-added-labels.png)

要从角色中删除标签，请选择标签名称旁边的&#x200B;**X**&#x200B;图标。

![flac-delete-labels](../../images/flac-ui/flac-delete-labels.png)

## 管理角色的沙盒

选择&#x200B;**[!UICONTROL 沙盒]**&#x200B;选项卡以打开角色沙盒页面。 在这里，您可以看到添加到角色的沙盒列表。

![flac-sandboxes](../../images/flac-ui/flac-sandboxes.png)

要向角色添加更多沙盒，请选择&#x200B;**[!UICONTROL 编辑]**。

![flac-add-sandboxes](../../images/flac-ui/flac-add-sandboxes.png)

下一个屏幕提示您使用下拉菜单选择要包含在角色中的沙盒中存在的资源权限。 完成后，选择&#x200B;**[!UICONTROL 保存并退出]**。

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

## 管理角色的用户

选择&#x200B;**[!UICONTROL 用户]**&#x200B;选项卡以打开“角色用户”页面，然后选择&#x200B;**[!UICONTROL 添加用户]**&#x200B;以将用户分配给角色。

![flac用户](../../images/flac-ui/flac-users.png)

从列表中选择要添加到角色的用户。 或者，使用搜索栏输入用户的姓名或电子邮件地址来搜索用户，然后选择&#x200B;**[!UICONTROL 保存]**

![flac-add-users](../../images/flac-ui/flac-add-users.png)

添加的用户显示在&#x200B;**[!UICONTROL 用户]**&#x200B;选项卡下。

![flac-added-users](../../images/flac-ui/flac-added-users.png)

要从角色中删除用户，请选择用户名旁边的&#x200B;**X**&#x200B;图标。

![flac-remove-users](../../images/flac-ui/flac-remove-users.png)

以下视频旨在支持您了解如何创建新角色以及如何管理该角色的用户。

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## 管理角色的API凭据 {#manage-api-credentials-for-role}

选择&#x200B;**[!UICONTROL API凭据]**&#x200B;选项卡以打开角色API凭据页面，然后选择&#x200B;**[!UICONTROL 添加API凭据]**&#x200B;以将API凭据分配给角色。

![flac-api-credentials](../../images/flac-ui/flac-api-credentials.png)

从列表中选择要添加到角色的API凭据，然后选择&#x200B;**[!UICONTROL 保存]**

![flac-add-api-credentials](../../images/flac-ui/flac-add-api-credentials.png)

添加的API凭据显示在&#x200B;**[!UICONTROL API凭据]**&#x200B;选项卡下。

![flac-added-api-credentials](../../images/flac-ui/flac-added-api-credentials.png)

要从角色中移除API凭据，请选择API凭据名称旁边的&#x200B;**X**&#x200B;图标。

![flac-remove-api-credentials](../../images/flac-ui/flac-remove-api-credentials.png)

出现&#x200B;**[!UICONTROL 删除API凭据]**&#x200B;对话框，提示您确认删除。

![flac-confirm-api-credentials-delete](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

您将返回&#x200B;**[!UICONTROL API凭据]**&#x200B;选项卡。

## 管理角色的用户组

用户组是多个已分组在一起的用户，并且有权执行相同的功能。

选择&#x200B;**[!UICONTROL 用户组]**&#x200B;选项卡以打开角色用户组页面，然后选择&#x200B;**[!UICONTROL 添加组]**&#x200B;以将用户组分配给角色。

![flac-user-groups](../../images/flac-ui/flac-user-groups.png)

从列表中选择要添加到角色的用户组。 或者，使用搜索栏通过输入用户组的名称来搜索该用户组，然后选择&#x200B;**[!UICONTROL 保存]**

![flac-add-user-groups](../../images/flac-ui/flac-add-user-groups.png)

添加的用户组显示在&#x200B;**[!UICONTROL 用户组]**&#x200B;选项卡下。

![flac-added-user-group](../../images/flac-ui/flac-added-user-groups.png)

要从角色中删除用户组，请选择用户组名称旁边的&#x200B;**X**&#x200B;图标。

![flac-remove-user-groups](../../images/flac-ui/flac-remove-user-groups.png)

出现&#x200B;**[!UICONTROL 删除用户组]**&#x200B;对话框，提示您确认删除。

![flac-confirm-user-groups-delete](../../images/flac-ui/flac-confirm-user-groups-delete.png)

您将返回&#x200B;**[!UICONTROL 用户组]**&#x200B;选项卡。

## 通过角色将用户添加到Experience Platform

要将用户添加到角色，请登录该Admin Console并选择&#x200B;**[!UICONTROL 添加用户]**

![product-profile-add-users](../../images/flac-ui/product-profile-add-users.png)

出现&#x200B;**[!UICONTROL 将用户添加到团队]**&#x200B;对话框。 输入用户的电子邮件地址、名字（可选）和姓氏（可选）。

选择铅笔图标以选择产品和用户组，选择&#x200B;**[!UICONTROL Adobe Experience Platform]**，选择&#x200B;**[!UICONTROL AEP-Default-All-Users]**，然后选择&#x200B;**[!UICONTROL 保存]**。

![产品配置文件](../../images/flac-ui/product-profile.png)

## 后续步骤

建立权限后，您可以继续下一步以[管理用户](users.md)。

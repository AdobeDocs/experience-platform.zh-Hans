---
keywords: Experience Platform；主页；热门主题；访问控制；基于属性的访问控制；ABAC
title: 基于属性的访问控制创建角色
description: 本文档提供了有关通过Adobe Experience Cloud中的权限界面管理角色的信息
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: d8f72bb5ae56daf5a41c763f821ca6306514bc48
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 7%

---

# 管理角色

角色定义了管理员、专家或最终用户对组织中资源的访问权限。 在基于角色的访问控制环境中，用户访问设置是通过共同的责任和需求进行分组的。 一个角色具有一组给定的权限，可将您组织的成员分配给一个或多个角色，具体取决于他们需要的查看或写入访问权限的范围。

## 创建新角色

要创建新角色，请选择 **[!UICONTROL 角色]** 选项卡，然后选择 **[!UICONTROL 创建角色]**.

![flac-new-role](../../images/flac-ui/flac-new-role.png)

此 **[!UICONTROL 创建新角色]** 对话框出现，提示您输入名称和可选说明。

完成后，选择 **[!UICONTROL 确认]**.

![flac-create-new-role](../../images/flac-ui/flac-create-new-role.png)

接下来，使用下拉菜单选择要包含在角色中的资源权限。

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

要添加其他资源，请选择 **[!UICONTROL Adobe Experience Platform]** 左侧导航面板，其中显示资源列表。 或者，在左侧导航面板的搜索栏中输入资源名称。

![flac-add-additional-resources](../../images/flac-ui/flac-add-additional-resources.png)

单击并将相关资源拖放到主面板中。

![flac-additional-resources-added](../../images/flac-ui/flac-additional-resources-added.png)

使用下拉菜单选择要包含在角色中的资源权限。 对要包含到角色的所有资源重复此操作。 完成后，选择 **[!UICONTROL 保存并退出]**.

![flac-save-resources](../../images/flac-ui/flac-save-resources.png)

新角色创建成功，您将被重定向至 **[!UICONTROL 角色]** 页面，您将在其中看到新创建的角色显示在列表中。

![flac-role-saved](../../images/flac-ui/flac-role-saved.png)

请参阅以下部分 [管理角色的权限](#manage-permissions-for-a-role) 有关如何在创建角色权限后管理角色权限的更多详细信息。

以下视频旨在支持您了解如何创建新角色以及如何管理该角色的用户。

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## 复制角色

要复制现有角色，请从中选择角色 **[!UICONTROL 角色]** 选项卡。 或者，使用筛选器选项筛选结果以查找要复制的角色。

![flac-duplicate-role](../../images/flac-ui/flac-duplicate-role.png)

接下来，选择 **[!UICONTROL 复制]** 从屏幕的右上角。

![flac-duplicate](../../images/flac-ui/flac-duplicate.png)

此 **[!UICONTROL 复制角色]** 对话框出现，提示您确认复制。

![flac-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

接下来，您将转到角色的详细信息页面，您可以在其中更改角色的名称和权限。 详细信息、标签和沙盒与上一个角色重复。 需要通过“用户”选项卡添加用户。 您可以查看 [管理角色的权限](permissions.md) 文档，了解有关将详细信息、标签、沙盒和用户添加到角色的更多信息。

单击左箭头返回 **[!UICONTROL 角色]** 选项卡。

![flac-return-to-roles](../../images/flac-ui/flac-return-to-roles.png)

新角色将显示在 **[!UICONTROL 角色]** 页面。

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## 删除角色

选择省略号(`…`)，此时下拉菜单会显示用于编辑、删除或复制角色的控件。 从下拉菜单中选择删除。

![flac-role-delete](../../images/flac-ui/flac-role-delete.png)

此 **[!UICONTROL 删除用户角色]** 对话框出现，提示您确认删除。

![flac-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

您将被返回到 **[!UICONTROL 角色]** 选项卡。

## 后续步骤

创建新角色后，您可以继续下一步以 [管理角色的权限](permissions.md).

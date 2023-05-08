---
keywords: Experience Platform；主页；热门主题；访问控制；基于属性的访问控制；ABAC
title: 基于属性的访问控制管理角色权限
description: 本文档提供了有关通过Adobe Experience Cloud中的“权限”界面配置角色权限的信息
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: 9515527f5a2c250b0a9057aa37769431e3b6fa07
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 4%

---

# 管理角色的权限

>[!IMPORTANT]
>
>访问控制使用用户ID（分配给用户的内部唯一ID）来授予权限。 将组织从Adobe ID迁移到业务ID后，为其用户设置的所有权限都将丢失，因为用户ID会发生更改，而访问控制将使用新生成的用户ID。 如果贵组织已迁移到业务ID，请联系您的Adobe代表，将您的用户ID从Adobe ID迁移到业务ID。

权限是Experience Cloud区域，管理员可以在其中定义用户角色和访问策略，以管理产品应用程序中功能和对象的访问权限。

通过 权限，您可以创建和管理角色，并为这些角色分配所需的资源权限。权限还允许您管理与特定角色关联的标签、沙盒和用户。

紧接之后 [创建新角色](#create-a-new-role)，则会返回到 **[!UICONTROL 角色]** 选项卡。 如果您正在编辑现有角色的权限，请从 **[!UICONTROL 角色]** 选项卡。 或者，使用筛选器选项筛选结果以查找角色。

## 筛选角色

选择漏斗图标(![“过滤器”图标](../../images/icon.png))以显示筛选器控件列表，以帮助缩小结果范围。

![flac-filters](../../images/flac-ui/flac-filters.png)

以下过滤器可用于UI中的角色：

| 过滤器 | 描述 |
| --- | --- |
| [!UICONTROL 创建于] | 选择开始日期和/或结束日期，以定义日期范围以按过滤结果。 |
| [!UICONTROL 创建者] | 通过从下拉菜单中选择用户，按角色创建者进行筛选。 |
| [!UICONTROL 修改时间] | 选择开始日期和/或结束日期，以定义日期范围以按过滤结果。 |
| [!UICONTROL 修改者] | 通过从下拉菜单中选择用户，按角色修改量进行筛选。 |

要删除过滤器，请在相关过滤器的“药丸”图标上选择“X”，或选择 **[!UICONTROL 全部清除]** 删除所有过滤器。

![flac-clear-filters](../../images/flac-ui/flac-clear-filters.png)

## 角色详细信息

从 **[!UICONTROL 角色]** 选项卡，以打开角色的详细信息页面。

![flac-details](../../images/flac-ui/flac-details.png)

“详细信息”选项卡提供了角色的概述。 该概述显示角色名称、角色描述、创建和修改角色的用户名称、创建和修改角色时的用户名称以及附加到角色的权限。 如果需要，可以修改角色名称和角色描述。

## 管理角色的标签

选择 **[!UICONTROL 标签]** 选项卡打开“角色标签”页面，然后选择 **[!UICONTROL 添加标签]** 为角色分配标签。

![flac标签](../../images/flac-ui/flac-labels.png)

此页面上列出了标签。 该列表显示标签名称、友好名称、类别及其说明。

从列表中选择要添加到角色的标签，然后选择 **[!UICONTROL 保存]**

![flac-add-labels](../../images/flac-ui/flac-add-labels.png)

添加的标签显示在 **[!UICONTROL 标签]** 选项卡。

![flac-added-labels](../../images/flac-ui/flac-added-labels.png)

要从角色中删除标签，请选择 **X** 图标。

![flac-delete-labels](../../images/flac-ui/flac-delete-labels.png)

## 管理角色沙箱

选择 **[!UICONTROL 沙箱]** 选项卡打开“角色”沙箱页面。 在这里，您可以看到添加到角色的沙箱列表。

![沙箱](../../images/flac-ui/flac-sandboxes.png)

要向角色添加更多沙箱，请选择 **[!UICONTROL 编辑]**.

![flac-add-sandboxes](../../images/flac-ui/flac-add-sandboxes.png)

下一个屏幕会提示您使用下拉菜单选择要包含在角色中的沙箱中的资源权限。 完成后，选择 **[!UICONTROL 保存并退出]**.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

## 管理角色的用户

选择 **[!UICONTROL 用户]** 选项卡以打开“用户”页面，然后选择 **[!UICONTROL 添加用户]** 为用户分配角色。

![flac用户](../../images/flac-ui/flac-users.png)

从列表中选择要添加到角色的用户。 或者，使用搜索栏通过输入用户姓名或电子邮件地址来搜索用户，然后选择 **[!UICONTROL 保存]**

![flac-add-users](../../images/flac-ui/flac-add-users.png)

添加的用户显示在 **[!UICONTROL 用户]** 选项卡。

![flac-added-users](../../images/flac-ui/flac-added-users.png)

要从角色中删除用户，请选择 **X** 图标。

![flac-remove-users](../../images/flac-ui/flac-remove-users.png)

## 管理角色的API凭据

选择 **[!UICONTROL API凭据]** 选项卡以打开“角色API凭据”页面，然后选择 **[!UICONTROL 添加API凭据]** 为角色分配API凭据。

![flac-api-credentials](../../images/flac-ui/flac-api-credentials.png)

从要添加到角色的列表中选择API凭据，然后选择 **[!UICONTROL 保存]**

![flac-add-api-credentials](../../images/flac-ui/flac-add-api-credentials.png)

添加的API凭据显示在 **[!UICONTROL API凭据]** 选项卡。

![flac-added-api-credentials](../../images/flac-ui/flac-added-api-credentials.png)

要从角色中删除API凭据，请选择 **X** 图标。

![flac-remove-api-credentials](../../images/flac-ui/flac-remove-api-credentials.png)

的 **[!UICONTROL 删除API凭据]** 对话框，提示您确认删除。

![flac-confirm-api-credentials-delete](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

您将返回到 **[!UICONTROL API凭据]** 选项卡。

## 管理角色的用户组

用户组是多个已分组在一起并有权执行相同功能的用户。

选择 **[!UICONTROL 用户组]** 选项卡打开“角色用户组”页面，然后选择 **[!UICONTROL 添加群组]** 为角色分配用户组。

![flac-user-groups](../../images/flac-ui/flac-user-groups.png)

从列表中选择要添加到角色的用户组。 或者，使用搜索栏通过输入用户组名称来搜索用户组，然后选择 **[!UICONTROL 保存]**

![flac-add-user-groups](../../images/flac-ui/flac-add-user-groups.png)

添加的用户组显示在 **[!UICONTROL 用户组]** 选项卡。

![flac-added-user-groups](../../images/flac-ui/flac-added-user-groups.png)

要从角色中删除用户组，请选择 **X** 图标。

![flac-remove-user-groups](../../images/flac-ui/flac-remove-user-groups.png)

的 **[!UICONTROL 删除用户组]** 对话框，提示您确认删除。

![flac-confirm-user-groups-delete](../../images/flac-ui/flac-confirm-user-groups-delete.png)

您将返回到 **[!UICONTROL 用户组]** 选项卡。

## 通过产品配置文件将用户添加到Experience Platform

要将用户添加到产品配置文件，请登录Admin Console并选择 **[!UICONTROL 添加用户]**

![product-profile-add-users](../../images/flac-ui/product-profile-add-users.png)

的 **[!UICONTROL 将用户添加到您的团队]** 对话框。 输入用户电子邮件地址、名字（可选）和姓氏（可选）。

选择铅笔图标以选择产品和用户组，选择 **[!UICONTROL Adobe Experience Platform]**，然后选择 **[!UICONTROL AEP-Default-All-Users]**，然后选择  **[!UICONTROL 保存]**.

![product-profile](../../images/flac-ui/product-profile.png)

## 后续步骤

已建立权限后，您可以继续执行 [管理用户](users.md).

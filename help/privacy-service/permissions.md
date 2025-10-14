---
title: 管理 Privacy Service 权限
description: 了解如何使用 Adobe Admin Console 管理 Adobe Experience Platform Privacy Service 的用户权限。
exl-id: 6aa81850-48d7-4fff-95d1-53b769090649
source-git-commit: 20a737cf36bf08415a15db78599f36659207ace1
workflow-type: tm+mt
source-wordcount: '1481'
ht-degree: 95%

---

# 管理 Privacy Service 权限

对 [Adobe Experience Platform Privacy Service](./home.md) 的访问权限在 Adobe Admin Console 中通过基于角色的细化权限进行控制。通过创建可为用户组分配权限的产品配置文件，您可以决定谁有权访问 Privacy Service [UI](./ui/overview.md) 和 [API](./api/overview.md) 中的哪些功能。

>[!NOTE]
>
>为 Privacy Service API 创建集成时，您必须选择现有产品配置文件，以确定该集成有权执行哪些功能或操作。请参阅[&#x200B; Privacy Service API 入门](./api/getting-started.md)指南，了解更多信息。

本指南向您展示如何管理 Privacy Service 的权限。

## 快速入门

为了配置 Privacy Service 的访问控制，您必须拥有产品与 Adobe Experience Platform Privacy Service 集成的组织的管理员权限。可以授予或撤回权限的最低角色是&#x200B;**产品配置文件管理员**。其他可以管理权限的管理员角色是&#x200B;**产品管理员**（可以管理产品内的所有配置文件）和&#x200B;**系统管理员**（无限制）。有关更多信息，请参阅 Adobe Enterprise 管理指南中关于[管理角色](https://helpx.adobe.com/cn/enterprise/using/admin-roles.html)的文章。

本指南假设您熟悉基本的 Admin Console 概念，例如产品配置文件以及它们如何向单个用户和用户组授予产品权限。有关详细信息，请参阅 [Admin Console 用户指南](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)。

## 可用权限

下表概述了 Privacy Service 的可用权限，并描述了它们授予访问权限的特定功能：

>[!NOTE]
>
>所有 Privacy Service 和[!UICONTROL 选择退出销售]权限是不同的并且彼此独立，其功能不存在重叠。这种情况是可能的，因为 Privacy Service API 被认为是幂等的。

| 类别 | 权限 | 描述 |
| --- | --- | --- |
| [!UICONTROL Privacy Service 权限] | [!UICONTROL 隐私读取权限] | 确定用户是否可以查看现有访问和删除请求及其详细信息。 |
| [!UICONTROL Privacy Service 权限] | [!UICONTROL 隐私写入权限] | 确定用户是否可以创建新的访问和删除请求。 |
| [!UICONTROL Privacy Service 权限] | [!UICONTROL 读取（访问）内容传送权限] | 当 Privacy Service 处理访问请求时，该客户会收到包含客户数据的 ZIP 文件。当查找访问请求的详细信息时，此种权限可决定用户是否可以访问请求的 ZIP 文件的下载链接。 |
| [!UICONTROL 选择退出销售权限] | [!UICONTROL 读取权限 - 选择退出销售] | 确定用户是否可以查看现有选择退出销售请求及其详细信息。 |
| [!UICONTROL 选择退出销售权限] | [!UICONTROL 写入权限 - 选择退出销售] | 确定用户是否可以创建新的选择退出销售请求。 |

{style="table-layout:auto"}

## 管理权限 {#manage}

要管理 Privacy Service 权限，请登录到 [Admin Console](https://adminconsole.adobe.com/)，并从顶部导航中选择&#x200B;**[!UICONTROL 产品]**。从此处选择 **[!UICONTROL Adobe Experience Platform Privacy Service]**。

![高亮显示Privacy Service产品卡的Admin Console。](./images/permissions/privacy-service-card.png)

### 选择或创建产品配置文件

下一个屏幕显示您组织下的 Privacy Service 的可用产品配置文件列表。如果不存在产品配置文件，请选择&#x200B;**[!UICONTROL 新的配置文件]**&#x200B;来创建一个。如果您的组织中有多个角色或用户组需要不同级别的访问权限，则应为每个角色或用户组创建单独的产品配置文件。

![Privacy Service产品配置文件突出显示的Admin Console。](./images/permissions/select-or-create-profile.png)

选择某个产品配置文件后，可使用&#x200B;**[!UICONTROL 权限]**&#x200B;选项卡开始为该配置文件[编辑权限](#edit-permissions)，或选择&#x200B;**[!UICONTROL 用户]**&#x200B;选项卡以开始[将用户分配](#assign-users)给该配置文件。

![产品配置文件Admin Console的“权限”选项卡。](./images/permissions/users-permissions-tabs.png)

### 编辑配置文件的权限 {#edit-permissions}

在&#x200B;**[!UICONTROL 权限]**&#x200B;选项卡中，选择所显示的任何权限类别，以访问权限编辑视图。

在编辑配置文件的权限时，可用权限将在左列中列出，而配置文件中包含的权限将在右列中列出。选择列出的权限，以在任一列之间移动它们。

![可用和包含的权限列。](./images/permissions/edit-permissions.png)

权限会按类别进行组织。要在类别之间切换，请从左侧导航中选择所需的类别。

![权限下的[!UICONTROL 选择退出销售]部分。](./images/permissions/switch-category.png)

配置完权限后，选择&#x200B;**[!UICONTROL 保存]**。

![突出显示“保存”的产品配置文件的权限配置。](./images/permissions/save-permissions.png)

产品配置文件视图将重新出现，并会反映添加的权限。

![为产品配置文件添加的权限。](./images/permissions/permissions-added.png)

### 将用户分配给配置文件 {#assign-users}

要将用户分配给产品配置文件（并授予其为该配置文件配置的权限），请选择&#x200B;**[!UICONTROL 用户]**&#x200B;选项卡，然后选择&#x200B;**[!UICONTROL 添加用户]**。

![Admin Console中产品配置文件的“用户”选项卡。](./images/permissions/manage-users.png)

有关为产品配置文件管理用户的详细信息，请参阅 [Admin Console 文档](https://helpx.adobe.com/cn/enterprise/using/manage-product-profiles.html)。

### 将旧的 API 凭据迁移到配置文件 {#migrate-tech-accounts}

>[!NOTE]
>
>本部分仅适用于在将 Privacy Service 权限集成到 Adobe Admin Console 之前创建的现有 API 凭据。对于新凭据，产品配置文件（及其权限）会通过[Adobe Developer Console 项目](https://developer.adobe.com/developer-console/docs/guides/projects/)分配。<br><br>有关更多信息，请参阅《Privacy Service API 入门指南》中关于[为项目分配产品配置文件](./api/getting-started.md#product-profiles)的部分。

以前，技术帐户不需要产品配置文件即可进行集成和获得权限。但是，由于最近对 Privacy Service 权限进行了改进，现在需要将旧的 API 凭据迁移到产品配置文件。此更新允许向技术帐户持有者授予细化权限。请按照下面提供的步骤更新 Privacy Service 的技术帐户权限。

#### 更新技术帐户权限 {#update-tech-account-permissions}

为您的技术帐户分配权限集的第一步是导航到[Adobe Admin Console](https://adminconsole.adobe.com/)，并为 Privacy Service 创建新的产品配置文件。

在 Admin Console UI 中，选择导航栏中的&#x200B;**产品**，然后选择左侧边栏中的 **[!UICONTROL Experience Cloud]** 和 **[!UICONTROL Adobe Experience Platform Privacy Service]**。[!UICONTROL 产品配置文件]选项卡出现。选择&#x200B;**新的配置文件**，为 Privacy Service 创建新的产品配置文件。

![Adobe Admin Console 中的 Experience Platform Privacy Service 产品配置文件选项卡中突出显示新配置文件。](./images/permissions/create-product-profile.png)

[!UICONTROL 创建新的产品配置文件]对话框出现。有关如何创建产品配置文件的完整说明可以在[创建配置文件的 UI 指南](../access-control/ui/create-profile.md)中找到。

保存新产品配置文件后，导航至 [Adobe Developer Console](https://developer.adobe.com/console/home) 并登录该产品或该项目。选择顶部导航中的&#x200B;**[!UICONTROL 项目]**，然后选择您的项目的信息卡。

>[!NOTE]
>
>您可能需要清除缓存和/或等待一段时间，新项目才会出现在 Developer Console 项目的列表中。

登录项目后，选择左侧边栏中的 **[!UICONTROL Privacy Service API]** 集成。

![Adobe Developer Console 的“项目”选项卡突出显示了“项目和 Privacy Service API”。](./images/permissions/login-to-dev-console-project.png)

Privacy Service API 集成仪表板出现。在此仪表板中，您可以编辑与该项目关联的产品配置文件。选择&#x200B;**[!UICONTROL 编辑产品配置文件]**，开始编辑。[!UICONTROL 配置 API] 对话框出现。

![Adobe Developer Console 中的 Privacy Service API 集成仪表板中突出显示“编辑产品配置文件”](./images/permissions/edit-product-profiles.png)

[!UICONTROL 配置 API] 对话框显示该服务中当前存在的可用产品配置文件。它们与在 Admin Console 中创建的产品配置文件相关联。从可用产品配置文件列表中，选中您在 Admin Console 中为技术帐户创建的新产品配置文件的复选框。这会自动将此技术帐户与所选产品配置文件中的权限关联起来。选择&#x200B;**[!UICONTROL 保存配置 API]** 确认您的设置。

>[!NOTE]
>
>如果技术帐户已与产品配置文件关联，则已选中可用产品配置文件列表中的一个复选框。

![Adobe Developer Console 中的配置 API 对话框中突出显示了产品配置文件复选框和保存配置的 API。](./images/permissions/select-profile-for-tech-account.png)

#### 确认您的设置已应用 {#confirm-applied-settings}

若要确认您的设置已应用到该帐户。返回到[&#x200B; Admin Console &#x200B;](https://adminconsole.adobe.com/)并导航至您新创建的产品配置文件。选择&#x200B;**[!UICONTROL API 凭据]**&#x200B;选项卡，查看关联项目的列表。将产品配置文件分配给技术帐户的 Developer Console 中使用的项目显示在凭据列表中。每个 API 凭据的名称均由项目名称和末尾带有后缀的随机生成的数字组成。选择一个凭据来打开[!UICONTROL 详细信息]面板。

![Admin Console 中的产品配置文件，其中突出显示了 API 凭据选项卡和一行项目凭据。](./images/permissions/confirm-credentials-in-admin-console.png)

[!UICONTROL 详细信息]面板包含有关 API 凭据的信息，其中包括关联的技术 ID、API 密钥、创建日期和上次修改日期以及关联的 Adobe 产品。

![Admin Console 中突出显示的 API 凭据的详细信息面板。](./images/permissions/admin-console-details-panel.png)

## 后续步骤

本指南介绍了 Privacy Service 的可用权限以及如何通过 Admin Console 管理它们。

有关如何在设置产品配置文件后创建新的 API 集成的步骤，请参阅[&#x200B; Privacy Service API 入门指南](./api/getting-started.md)。有关为其他 Adobe Experience Platform 功能管理权限的详细信息，请参阅[访问控制文档](../access-control/home.md)。

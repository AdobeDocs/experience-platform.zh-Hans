---
title: 管理Privacy Service权限
description: 了解如何使用Adobe Admin Console管理Adobe Experience Platform Privacy Service的用户权限。
exl-id: 6aa81850-48d7-4fff-95d1-53b769090649
source-git-commit: 1e164166f58540cbaaa4ad789b10cdfc40fa8a70
workflow-type: tm+mt
source-wordcount: '1634'
ht-degree: 1%

---

# 管理Privacy Service权限

>[!IMPORTANT]
>
>Adobe Experience Platform Privacy Service的权限已得到改进，可提高其粒度级别。 通过这些更改，组织管理员可以授予更多用户使用所需的角色和权限级别的访问权限。 技术帐户用户必须更新其Privacy Service权限，因为此即将进行的更新对他们而言是一次重大更改。 此权限更改的实施将在 **2023年4月13日**. 请参阅 [迁移旧版API凭据](#migrate-tech-accounts) 以获取有关解决此问题的指导。
>
>技术帐户可供企业客户使用，并通过Adobe开发人员控制台创建。 技术帐户持有人的Adobe ID结束于 `@techacct.adobe.com`. 如果您不确定自己是否是技术帐户持有者，请联系您的组织管理员。

访问 [Adobe Experience Platform Privacy Service](./home.md) 可通过Adobe Admin Console中基于角色的细粒度权限进行控制。 通过创建产品配置文件以将权限分配给用户组，可以确定谁有权访问Privacy Service中的哪些功能 [UI](./ui/overview.md) 和 [API](./api/overview.md).

>[!NOTE]
>
>在为Privacy ServiceAPI创建集成时，必须选择现有的产品配置文件，才能确定集成具有权限的功能或操作。 请参阅 [开始使用Privacy ServiceAPI](./api/getting-started.md) 以了解更多信息。

本指南向您展示如何管理Privacy Service权限。

## 快速入门

要配置Privacy Service的访问控制，您必须拥有与Adobe Experience Platform Privacy Service产品集成的组织的管理员权限。 可授予或撤回权限的最低角色是 **产品配置文件管理员**. 其他可以管理权限的管理员角色包括 **产品管理员** （可以管理产品中的所有配置文件）和 **系统管理员** （无限制）。 请参阅 [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 有关详细信息，请参阅Adobe企业管理指南。

本指南假定您熟悉产品配置文件等基本Admin Console概念，以及它们如何向个人用户和组授予产品权限。 有关更多信息，请参阅 [Admin Console用户指南](https://helpx.adobe.com/cn/enterprise/using/admin-console.html).

## 可用权限

下表概述了Privacy Service的可用权限，并介绍了授予访问权限的特定功能：

>[!NOTE]
>
>所有Privacy Service和 [!UICONTROL 选择退出销售] 权限是不同的，并且相互之间不存在功能重叠。 这是可能的，因为Privacy ServiceAPI被视为幂等。

| 类别 | 权限 | 描述 |
| --- | --- | --- |
| [!UICONTROL Privacy Service权限] | [!UICONTROL 隐私读取权限] | 确定用户是否可以查看现有访问和删除请求及其详细信息。 |
| [!UICONTROL Privacy Service权限] | [!UICONTROL 隐私写入权限] | 确定用户是否可以创建新的访问和删除请求。 |
| [!UICONTROL Privacy Service权限] | [!UICONTROL “读取（访问）内容交付”权限] | 当Privacy Service处理访问请求时，将向该客户发送包含客户数据的ZIP文件。 在查找访问请求的详细信息时，此权限决定用户是否可以访问请求ZIP文件的下载链接。 |
| [!UICONTROL 选择退出销售权限] | [!UICONTROL 阅读权限 — 选择退出销售] | 确定用户是否可以查看现有的选择退出销售请求及其详细信息。 |
| [!UICONTROL 选择退出销售权限] | [!UICONTROL 写入权限 — 选择退出销售] | 确定用户是否可以创建新的选择退出销售请求。 |

{style="table-layout:auto"}

## 管理权限 {#manage}

要管理Privacy Service权限，请登录 [Admin Console](https://adminconsole.adobe.com/) 选择 **[!UICONTROL 产品]** 中。 从此处选择 **[!UICONTROL Adobe Experience Platform Privacy Service]**.

![显示Privacy Service产品卡的Admin Console](./images/permissions/privacy-service-card.png)

### 选择或创建产品配置文件

下一个屏幕显示贵组织下可供Privacy Service的可用产品配置文件列表。 如果不存在产品配置文件，请选择 **[!UICONTROL 新建用户档案]** 创建一个。 如果贵组织中有多个角色或用户组需要不同级别的访问权限，则应为每个角色或用户组创建单独的产品配置文件。

![显示产品配置文件以在Admin Console中Privacy Service的图像](./images/permissions/select-or-create-profile.png)

选择产品配置文件后，您可以使用 **[!UICONTROL 权限]** 选项卡开始 [编辑权限](#edit-permissions) ，或选择 **[!UICONTROL 用户]** 选项卡开始 [分配用户](#assign-users) 到用户档案。

![显示产品配置文件Admin Console权限选项卡的图像](./images/permissions/users-permissions-tabs.png)

### 编辑配置文件的权限 {#edit-permissions}

在 **[!UICONTROL 权限]** 选项卡，选择显示的任何权限类别以访问权限编辑视图。

编辑配置文件的权限时，可用权限会列在左列，而配置文件中包含的可用权限会列在右列。 选择列出的权限，以在任一列之间移动它们。

![显示可用和包含的权限列的图像](./images/permissions/edit-permissions.png)

权限分为几类。 要在类别之间切换，请从左侧导航中选择所需的类别。

![显示 [!UICONTROL 选择退出销售] 权限部分](./images/permissions/switch-category.png)

选择 **[!UICONTROL 保存]** 权限配置完成后。

![显示为产品配置文件保存的权限配置的图像](./images/permissions/save-permissions.png)

此时将重新显示产品配置文件视图，并反映添加的权限。

![显示产品配置文件已添加权限的图像](./images/permissions/permissions-added.png)

### 将用户分配到配置文件 {#assign-users}

要将用户分配到产品配置文件（并向他们授予配置文件的配置权限），请选择 **[!UICONTROL 用户]** 选项卡，后跟 **[!UICONTROL 添加用户]**.

![显示产品配置文件的“用户”选项卡的图像，Admin Console](./images/permissions/manage-users.png)

有关管理产品配置文件用户的更多信息，请参阅 [Admin Console文档](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

### 将旧版API凭据迁移到配置文件 {#migrate-tech-accounts}

>[!NOTE]
>
>此部分仅适用于在将Privacy Service权限集成到Adobe Admin Console之前创建的现有API凭据。 对于新凭据，将通过 [Adobe Developer控制台项目](https://developer.adobe.com/developer-console/docs/guides/projects/) 中。<br><br>请参阅 [将产品配置文件分配给项目](./api/getting-started.md#product-profiles) Privacy ServiceAPI快速入门指南以了解更多信息。

以前，技术帐户不需要产品配置文件来获取集成和权限。 但是，由于最近Privacy Service权限有了改进，现在需要将旧版API凭据迁移到产品配置文件。 此更新允许向技术帐户持有人授予粒度权限。 请按照以下提供的步骤更新技术帐户权限以进行Privacy Service。

#### 更新技术帐户权限 {#update-tech-account-permissions}

为技术帐户分配权限集的第一步是导航到 [Adobe Admin Console](https://adminconsole.adobe.com/) 并创建新的产品配置文件以进行Privacy Service。

从Admin ConsoleUI中，选择 **产品** ，然后 **[!UICONTROL Experience Cloud]** 和 **[!UICONTROL Adobe Experience Platform Privacy Service]** 中。 的 [!UICONTROL 产品配置文件] 选项卡。 选择 **新建用户档案** 创建新的产品配置文件以进行Privacy Service。

![在Adobe Admin Console中Experience PlatformPrivacy Service产品配置文件选项卡，并突出显示新配置文件。](./images/permissions/create-product-profile.png)

的 [!UICONTROL 创建新的产品用户档案] 对话框。 有关如何创建产品配置文件的完整说明，请参阅 [创建用户档案的UI指南](../access-control/ui/create-profile.md).

保存新的产品配置文件后，导航到 [Adobe Developer控制台](https://developer.adobe.com/console/home) 然后登录该产品或该项目。 选择 **[!UICONTROL 项目]** ，然后是项目的卡。

>[!NOTE]
>
>您可能需要清除缓存和/或等待一段时间，才能在开发人员控制台项目列表中显示新项目。

登录项目后，选择 **[!UICONTROL Privacy ServiceAPI]** 集成。

![Adobe Developer控制台的“项目”选项卡突出显示了项目和Privacy ServiceAPI。](./images/permissions/login-to-dev-console-project.png)

此时会显示Privacy ServiceAPI集成功能板。 在此功能板中，您可以编辑与该项目关联的产品配置文件。 选择 **[!UICONTROL 编辑产品配置文件]** 开始这个过程。 的 [!UICONTROL 配置API] 对话框。

![Adobe Developer控制台中的Privacy ServiceAPI集成功能板，其中突出显示了“编辑产品配置文件”](./images/permissions/edit-product-profiles.png)

的 [!UICONTROL 配置API] 对话框显示服务中当前存在的可用产品配置文件。 它们与在管理控制台中创建的产品用户档案相关联。 从可用产品配置文件列表中，选中您在管理控制台中为技术帐户创建的新产品配置文件的复选框。 这会自动将此技术帐户与选定产品配置文件中的权限相关联。 选择 **[!UICONTROL 保存配置的API]** 以确认您的设置。

>[!NOTE]
>
>如果技术帐户已与产品配置文件关联，则将已选中可用产品配置文件列表中的某个复选框。

![在Adobe Developer控制台中，使用产品配置文件选中配置API对话框，并突出显示保存配置的API。](./images/permissions/select-profile-for-tech-account.png)

#### 确认已应用您的设置 {#confirm-applied-settings}

确认您的设置已应用于帐户。 返回到 [Admin Console](https://adminconsole.adobe.com/) ，然后导航到新创建的产品用户档案。 选择 **[!UICONTROL API凭据]** 选项卡，以查看关联的项目列表。 在开发人员控制台中使用的项目，您将产品配置文件分配给技术帐户的项目将显示在凭据列表中。 每个API凭据的名称都由项目名称组成，其后面有一个随机生成的编号，该编号的后缀为。 选择凭据以打开 [!UICONTROL 详细信息] 的上界。

![Admin Console中的产品用户档案，其中突出显示了API凭据选项卡和一行项目凭据。](./images/permissions/confirm-credentials-in-admin-console.png)

的 [!UICONTROL 详细信息] 面板包含有关API凭据的信息，包括关联的技术ID、API密钥、创建日期和上次修改日期，以及关联的Adobe产品。

![Admin Console中API凭据突出显示的详细信息面板。](./images/permissions/admin-console-details-panel.png)

## 后续步骤

本指南介绍了Privacy Service的可用权限以及如何通过Admin Console管理这些权限。

有关如何在设置产品配置文件后创建新API集成的步骤，请参阅 [Privacy ServiceAPI快速入门指南](./api/getting-started.md). 有关管理其他Adobe Experience Platform功能的权限的更多信息，请参阅 [访问控制文档](../access-control/home.md).

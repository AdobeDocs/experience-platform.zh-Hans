---
title: 管理Privacy Service的权限
description: 了解如何使用Adobe Admin Console管理Adobe Experience Platform Privacy Service的用户权限。
exl-id: 6aa81850-48d7-4fff-95d1-53b769090649
source-git-commit: 1e164166f58540cbaaa4ad789b10cdfc40fa8a70
workflow-type: tm+mt
source-wordcount: '1634'
ht-degree: 1%

---

# 管理Privacy Service的权限

>[!IMPORTANT]
>
>Adobe Experience Platform Privacy Service的权限已得到改进，以提高其粒度级别。 这些更改使组织管理员能够通过所需的角色和权限级别授予更多用户访问权限。 技术帐户用户必须更新其Privacy Service权限，因为此即将进行的更新对他们来说是一项重大更改。 此权限更改的实施将发生在 **2023年4月13日**. 请参阅相关文档 [迁移旧版API凭据](#migrate-tech-accounts) 以获取有关解决此问题的指导。
>
>企业客户可以使用技术帐户，这些帐户是通过Adobe开发人员控制台创建的。 技术帐户持有人的Adobe ID结束于 `@techacct.adobe.com`. 如果您不确定您是否是技术帐户所有者，请联系您的组织管理员。

访问 [Adobe Experience Platform Privacy Service](./home.md) 通过Adobe Admin Console中基于角色的细粒度权限进行控制。 通过创建为用户组分配权限的产品配置文件，您可以确定谁有权访问Privacy Service中的哪些功能 [UI](./ui/overview.md) 和 [API](./api/overview.md).

>[!NOTE]
>
>为Privacy ServiceAPI创建集成时，您必须选择现有的产品配置文件，以确定集成具有哪些功能或操作权限。 请参阅指南，网址为 [Privacy ServiceAPI快速入门](./api/getting-started.md) 了解更多信息。

本指南向您说明如何管理Privacy Service的权限。

## 快速入门

要为Privacy Service配置访问控制，您必须对与Adobe Experience Platform Privacy Service产品集成的组织具有管理员权限。 可以授予或撤销权限的最小角色为 **产品配置文件管理员**. 可以管理权限的其他管理员角色包括 **产品管理员** （可以管理产品中的所有配置文件）和 **系统管理员** （无限制）。 请参阅以下文章： [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 有关更多信息，请参阅Adobe企业管理指南。

本指南假定您熟悉产品配置文件等基本Admin Console概念，并熟悉它们如何将产品权限授予各个用户和组。 欲了解更多信息，请参见 [Admin Console用户指南](https://helpx.adobe.com/cn/enterprise/using/admin-console.html).

## 可用权限

下表概述了Privacy Service可用的权限，并说明了他们授予访问权限的特定功能：

>[!NOTE]
>
>所有Privacy Service和 [!UICONTROL 选择退出销售] 权限是不同的，彼此分开，没有功能重叠。 这是可能的，因为Privacy ServiceAPI被视为幂等。

| 类别 | 权限 | 描述 |
| --- | --- | --- |
| [!UICONTROL Privacy Service权限] | [!UICONTROL 隐私读取权限] | 确定用户是否可以查看现有的访问和删除请求及其详细信息。 |
| [!UICONTROL Privacy Service权限] | [!UICONTROL 隐私写入权限] | 确定用户是否可以创建新访问和删除请求。 |
| [!UICONTROL Privacy Service权限] | [!UICONTROL 读取（访问）内容交付权限] | 当Privacy Service处理访问请求时，会将包含客户数据的ZIP文件发送给该客户。 在查找访问请求的详细信息时，此权限确定用户是否可以访问请求ZIP文件的下载链接。 |
| [!UICONTROL 选择退出销售权限] | [!UICONTROL 读取权限 — 选择退出销售] | 确定用户是否可以查看现有的选择退出销售请求及其详细信息。 |
| [!UICONTROL 选择退出销售权限] | [!UICONTROL 写入权限 — 选择退出销售] | 确定用户是否可以创建新的选择退出销售请求。 |

{style="table-layout:auto"}

## 管理权限 {#manage}

要管理Privacy Service权限，请登录 [Admin Console](https://adminconsole.adobe.com/) 并选择 **[!UICONTROL 产品]** 从顶部导航中。 从此处选择 **[!UICONTROL Adobe Experience Platform Privacy Service]**.

![显示Admin Console中Privacy Service产品卡的图像](./images/permissions/privacy-service-card.png)

### 选择或创建产品配置文件

下一个屏幕显示可用于在您的组织下Privacy Service的产品配置文件列表。 如果不存在任何产品配置文件，请选择 **[!UICONTROL 新建配置文件]** 创建一个。 如果您的组织中有多个需要不同级别访问权限的角色或用户组，则应为每个角色或用户组创建单独的产品配置文件。

![显示用于Admin Console中Privacy Service的产品配置文件的图像](./images/permissions/select-or-create-profile.png)

选择产品配置文件后，您可以使用 **[!UICONTROL 权限]** 制表符开始 [编辑权限](#edit-permissions) ，或选择 **[!UICONTROL 用户]** 制表符开始 [分配用户](#assign-users) 到个人资料。

![显示产品配置文件Admin Console的“权限”选项卡的图像](./images/permissions/users-permissions-tabs.png)

### 编辑配置文件的权限 {#edit-permissions}

在 **[!UICONTROL 权限]** 选项卡中，选择显示的任何权限类别以访问权限编辑视图。

编辑配置文件的权限时，可用权限将列在左列，而配置文件中包含的权限将列在右列。 选择列出的权限可在任一列之间移动它们。

![显示可用和包含的权限列的图像](./images/permissions/edit-permissions.png)

权限可划分为不同的类别。 要在类别之间切换，请从左侧导航中选择所需的类别。

![图像显示 [!UICONTROL 选择退出销售] 权限下的部分](./images/permissions/switch-category.png)

选择 **[!UICONTROL 保存]** 配置完权限后。

![该图像显示了正在为产品配置文件保存的权限配置](./images/permissions/save-permissions.png)

产品配置文件视图会重新显示，并反映添加的权限。

![显示产品配置文件已添加权限的图像](./images/permissions/permissions-added.png)

### 将用户分配给配置文件 {#assign-users}

要将用户分配给产品配置文件（并授予他们配置文件配置的权限），请选择 **[!UICONTROL 用户]** 选项卡，然后 **[!UICONTROL 添加用户]**.

![该图像显示了用户选项卡中Admin Console的产品配置文件](./images/permissions/manage-users.png)

有关管理产品配置文件的用户的更多信息，请参阅 [Admin Console文档](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

### 将旧版API凭据迁移至配置文件 {#migrate-tech-accounts}

>[!NOTE]
>
>此部分仅适用于在Privacy Service权限集成到Adobe Admin Console之前创建的现有API凭据。 对于新凭据，产品配置文件（及其权限）将通过进行分配 [Adobe Developer控制台项目](https://developer.adobe.com/developer-console/docs/guides/projects/) 而是。<br><br>请参阅以下部分： [将产品配置文件分配给项目](./api/getting-started.md#product-profiles) 有关更多信息，请参阅Privacy ServiceAPI快速入门指南。

以前，技术帐户不需要产品配置文件即可进行集成和授予权限。 但是，由于Privacy Service权限最近有了改进，现在必须将旧版API凭据迁移到产品配置文件。 此更新允许向技术帐户持有人授予粒度权限。 按照下面提供的步骤更新Privacy Service的技术帐户权限。

#### 更新技术帐户权限 {#update-tech-account-permissions}

为您的技术帐户分配权限集的第一步是导航到 [Adobe Admin Console](https://adminconsole.adobe.com/) 和创建新的产品配置文件以进行Privacy Service。

从Admin ConsoleUI中，选择 **产品** 导航栏中，后面是 **[!UICONTROL Experience Cloud]** 和 **[!UICONTROL Adobe Experience Platform Privacy Service]** 在左侧边栏中。 此 [!UICONTROL 产品配置文件] 选项卡。 选择 **新建配置文件** 以创建新的产品配置文件进行Privacy Service。

![突出显示新配置文件的Adobe Admin Console中的“Experience PlatformPrivacy Service产品配置文件”选项卡。](./images/permissions/create-product-profile.png)

此 [!UICONTROL 创建新的产品配置文件] 对话框。 有关如何创建产品配置文件的完整说明，请参阅 [创建配置文件的UI指南](../access-control/ui/create-profile.md).

保存新的产品配置文件后，导航到 [Adobe Developer控制台](https://developer.adobe.com/console/home) 并登录该产品或该项目。 选择 **[!UICONTROL 项目]** 在顶部导航中，依次显示项目的卡。

>[!NOTE]
>
>您可能需要清除缓存和/或等待一段时间，新项目才会显示在开发人员控制台项目的列表中。

登录项目后，选择 **[!UICONTROL PRIVACY SERVICEAPI]** 从左侧边栏进行集成。

![突出显示了“项目”和“Privacy ServiceAPI”的Adobe Developer控制台的“项目”选项卡。](./images/permissions/login-to-dev-console-project.png)

此时将显示Privacy ServiceAPI集成仪表板。 从该功能板，您可以编辑与该项目关联的产品配置文件。 选择 **[!UICONTROL 编辑产品配置文件]** 以开始该过程。 此 [!UICONTROL 配置API] 对话框。

![Adobe Developer Console中的Privacy ServiceAPI集成仪表板，突出显示编辑产品配置文件](./images/permissions/edit-product-profiles.png)

此 [!UICONTROL 配置API] 对话框显示服务中当前存在的可用产品配置文件。 它们与在管理控制台中创建的产品配置文件相关联。 从可用产品配置文件列表中，选中在管理控制台中为技术帐户创建的新产品配置文件对应的复选框。 这会自动将此技术帐户与所选产品配置文件中的权限关联。 选择 **[!UICONTROL 保存配置的API]** 以确认您的设置。

>[!NOTE]
>
>如果技术帐户已与产品配置文件关联，则已选中可用产品配置文件列表中的复选框之一。

![选中Adobe Developer Console中的“使用产品配置文件配置API”复选框并选中“保存配置的API”。](./images/permissions/select-profile-for-tech-account.png)

#### 确认已应用您的设置 {#confirm-applied-settings}

确认您的设置已应用于帐户。 返回到 [Admin Console](https://adminconsole.adobe.com/) 并导航到新创建的产品配置文件。 选择 **[!UICONTROL API凭据]** 选项卡以查看关联项目的列表。 在开发人员控制台中使用的项目（您将产品配置文件分配给技术帐户）会显示在凭据列表中。 每个API凭据的名称由项目名称组成，项目名称的后缀为随机生成的编号。 选择凭据以打开 [!UICONTROL 详细信息] 面板。

![Admin Console中突出显示API凭据选项卡和一行项目凭据的产品配置文件。](./images/permissions/confirm-credentials-in-admin-console.png)

此 [!UICONTROL 详细信息] 面板包含有关API凭据的信息，包括关联的技术ID、API密钥、创建和上次修改日期以及关联的Adobe产品。

![Admin Console中API凭据的高亮显示详细信息面板。](./images/permissions/admin-console-details-panel.png)

## 后续步骤

本指南介绍了Privacy Service可用的权限以及如何通过Admin Console管理这些权限。

有关如何在设置产品配置文件后创建新的API集成的步骤，请参阅 [Privacy ServiceAPI快速入门指南](./api/getting-started.md). 有关管理其他Adobe Experience Platform功能的权限的更多信息，请参阅 [访问控制文档](../access-control/home.md).

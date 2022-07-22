---
title: Experience Platform中数据收集的权限管理
description: 简要概述如何管理权限并控制对Real-time Customer Data Platform(RTCDP)连接中各项功能的访问。
source-git-commit: e0be090bfce602c7a6e22a1e4be187d4abdfd600
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 6%

---

# Experience Platform中数据收集的权限管理

[在Adobe Experience Platform中收集数据](./home.md) 由多种不同的技术组成，这些技术可协同工作来收集和传输您的数据。 这些技术的访问权限通过Adobe Admin Console中基于角色的细分权限进行控制。

本指南向您展示如何管理数据收集功能的权限。

## 快速入门

要配置数据收集的访问控制，您必须对具有与Adobe Experience Platform数据收集产品集成的组织具有管理员权限。 可以授予或撤销权限的最低角色是产品配置文件管理员。 其他可以管理权限的管理员角色包括产品管理员（可以管理产品中的所有配置文件）和系统管理员（无限制）。 请参阅 [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 有关详细信息，请参阅Adobe企业管理指南。

本指南假定您熟悉产品配置文件等基本Admin Console概念，以及它们如何向个人用户和组授予产品权限。 有关更多信息，请参阅 [Admin Console用户指南](https://helpx.adobe.com/cn/enterprise/using/admin-console.html).

## 可用权限

数据收集的相关权限通过Admin Console中的两个产品名称提供： **Adobe Experience Platform** 和 **Adobe Experience Platform数据收集**. 以下各节概述了每个产品下提供的权限，以及这些权限授予访问权限的特定功能的描述。

### Adobe Experience Platform权限

Adobe Experience Platform下的权限包括访问数据流、身份、模式和沙箱。 有关如何配置Adobe Experience Platform权限的步骤，请参阅 [访问控制用户指南](../access-control/ui/overview.md).

| 类别 | 权限 | 描述 |
| --- | --- | --- |
| 沙盒 | (不适用) | 根据 [沙箱](../sandboxes/home.md) 您组织下创建的所有权限，您可以在Admin Console中通过此权限类别控制对每个权限的访问权限。 |
| 数据建模 | 管理架构 | 授予查看、创建和编辑 [体验数据模型(XDM)架构](../xdm/home.md). |
| 数据建模 | 查看架构 | 授予对架构的只读访问权限。 |
| 身份管理 | 管理身份命名空间 | 授予查看、创建和编辑 [身份命名空间](../identity-service/namespaces.md). |
| 身份管理 | 查看标识命名空间 | 授予对身份命名空间的只读访问权限。 |
| 数据收集 | 管理数据流 | 授予查看、创建和编辑 [数据流](../edge/datastreams/overview.md). |
| 数据收集 | 查看数据流 | 授予对数据流的只读访问权限。 |

{style=&quot;table-layout:auto&quot;}

<!-- (Feature not yet available?)
| Dashboards | Manage Custom Dashboards | |
| Dashboards | View Custom Dashboards | |
-->

### Adobe Experience Platform数据收集权限

Adobe Experience Platform数据收集下的权限控制对标记和事件转发功能（包括属性、扩展和环境）的访问。 有关如何配置Adobe Experience Platform数据收集权限的步骤，请参阅 [下方](#manage).

| 类别 | 权限 | 描述 |
| --- | --- | --- |
| 平台 | Web | 授予访问 [Web属性](../tags/ui/administration/companies-and-properties.md) 与其他资产权限结合使用时，不会将其与其他资产权限结合使用。 |
| 平台 | 移动设备 | 授予访问 [移动属性](../tags/ui/administration/companies-and-properties.md) 与其他资产权限结合使用时，不会将其与其他资产权限结合使用。 |
| 属性 | (不适用) | 根据在您的组织下创建的资产，您可以通过Admin Console中的此权限类别控制对每个资产的访问权限。<br><br>用户分配的资产权限仅适用于他们通过此权限类别获得访问权限的资产。 |
| 资产权限 | 批准 | 授予批准库内部版本作为 [发布流程](../tags/ui/publishing/publishing-flow.md). |
| 资产权限 | 开发 | 授予在 [发布流程](../tags/ui/publishing/publishing-flow.md). |
| 资产权限 | 编辑属性 | 授予编辑用户有权访问的属性的基本配置的功能。 |
| 资产权限 | 管理环境 | 授予管理 [环境](../tags/ui/publishing/environments.md) 对于用户有权访问的属性。 |
| 资产权限 | 管理扩展 | 授予管理 [扩展](../tags/ui/managing-resources/extensions/overview.md) 对于用户有权访问的属性。 |
| 资产权限 | 发布 | 授予将库内部版本作为 [发布流程](../tags/ui/publishing/publishing-flow.md). |
| 公司权限 | 开发扩展 | 允许创建和修改您的组织拥有的扩展包，包括私有版本和公共发布请求。 |
| 公司权限 | 管理扩展 | 仅当您拥有Adobe Journey Optimizer或其他授予移动设备应用程序内消息和推送消息访问权限的解决方案的许可证时，此权限才适用。 这允许您管理Adobe Experience Cloud了解的应用程序以及与Firebase Cloud Messaging服务和Apple推送通知服务通信所需的推送凭据。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>有关这些权限如何影响标记中功能（包括常见方案的管理策略）的更多信息，请参阅 [用户权限](../tags/ui/administration/user-permissions.md).

## 管理Adobe Experience Platform数据收集的权限 {#manage}

>[!IMPORTANT]
>
>此部分仅介绍如何在Admin Console中管理Adobe Experience Platform数据收集产品的权限。 但是，管理Adobe Experience Platform产品下权限的步骤类似。
>
>请参阅 [访问控制UI指南](../access-control/ui/overview.md) 以了解有关管理平台权限的详细说明。 根据贵组织有权访问的产品SKU，您可能并非拥有所有可用的权限。

要管理数据收集的权限，请登录 [Admin Console](https://adminconsole.adobe.com/) 选择 **[!UICONTROL 产品]** 中。 从此处，选择 **[!UICONTROL Adobe Experience Platform数据收集]**.

![在Admin Console中显示数据收集产品卡的图像](./images/permissions/data-collection-card.png)

### 选择或创建产品配置文件

下一个屏幕显示您组织下数据收集的可用产品配置文件列表，默认配置文件为 **[!DNL Default Data Collection All Access]**. 您可以根据需要选择编辑默认的产品配置文件，也可以选择 **[!UICONTROL 新建用户档案]** 创建一个。 如果贵组织中有多个角色或用户组需要不同级别的访问权限，则应为每个角色或用户组创建单独的产品配置文件。

![显示用于数据收集的产品配置文件的图像Admin Console](./images/permissions/new-profile.png)

选择或创建产品配置文件后，您可以使用 **[!UICONTROL 编辑]** 图标开始 [编辑权限](#edit-permissions) ，或选择 **[!UICONTROL 用户]** 选项卡开始 [分配用户](#assign-users) 到用户档案。

![显示产品配置文件Admin Console权限选项卡的图像](./images/permissions/edit-permission-categories.png)

### 编辑产品配置文件的权限 {#edit-permissions}

编辑配置文件的权限时，可用权限会列在左列，而配置文件中包含的可用权限会列在右列。 选择列出的权限，以在任一列之间移动它们。

![显示在“已包括”列下添加的权限的图像](./images/permissions/added-permissions.png)

权限分为几类。 要在类别之间切换，请从左侧导航中选择所需的类别。

![显示权限下公司权限部分的图像](./images/permissions/switch-category.png)

选择 **[!UICONTROL 保存]** 权限配置完成后。

![显示为产品配置文件保存的权限配置的图像](./images/permissions/save-permissions.png)

此时将重新显示产品配置文件视图，并反映添加的权限。

![显示产品配置文件已添加权限的图像](./images/permissions/permissions-added.png)

### 将用户分配到产品配置文件 {#assign-users}

要将用户分配到产品配置文件（并向他们授予配置文件的配置权限），请选择 **[!UICONTROL 用户]** 选项卡，后跟 **[!UICONTROL 添加用户]**.

![显示产品配置文件的“用户”选项卡的图像，Admin Console](./images/permissions/manage-users.png)

有关管理产品配置文件用户的更多信息，请参阅 [Admin Console文档](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

## 后续步骤

本指南介绍了数据收集UI的可用权限以及如何通过Admin Console管理这些权限。 有关管理其他Adobe Experience Platform功能的权限的更多信息，请参阅 [访问控制文档](../access-control/home.md).

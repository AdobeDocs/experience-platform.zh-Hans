---
title: Experience Platform 中数据收集的权限管理
description: 有关如何在Adobe Experience Platform中管理权限和控制对数据收集功能的访问权限的高级概述。
exl-id: 8426d54b-ec1d-475a-a769-f45a8c924fe7
source-git-commit: 88995c933bf067fe3d077d1be8b92b076e461707
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 26%

---

# Experience Platform 中数据收集的权限管理 {#permission-management}

>[!CONTEXTUALHELP]
>id="platform_tags_permissions"
>title="权限"
>abstract="了解在 Adobe Experience Platform 中使用数据流、模式、身份标识和沙盒所需的关键权限。"

Adobe Experience Platform[中的](home.md)数据收集由多种不同的技术组成，这些技术可共同收集和传输您的数据。 在Adobe Admin Console中，可通过基于角色的细粒度权限来控制对这些技术的访问。

本指南向您说明如何管理数据收集功能的权限。

## 快速入门

要为数据收集配置访问控制，您必须对与Adobe Experience Platform数据收集集成了产品的组织具有管理员权限。 可以授予或撤回权限的最低角色是&#x200B;**产品轮廓管理员**。其他可以管理权限的管理员角色是&#x200B;**产品管理员**（可以管理产品内的所有轮廓）和&#x200B;**系统管理员**（无限制）。有关更多信息，请参阅 Adobe Enterprise 管理指南中关于[管理角色](https://helpx.adobe.com/cn/enterprise/using/admin-roles.html)的文章。

本指南假设您熟悉基本的 Admin Console 概念，例如产品轮廓以及它们如何向单个用户和用户组授予产品权限。有关详细信息，请参阅 [Admin Console 用户指南](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)。

## 可用权限

数据收集的相关权限通过Admin Console中的两个产品名称提供： **Adobe Experience Platform**&#x200B;和&#x200B;**Adobe Experience Platform数据收集**。 以下各节概述了每个产品下提供的权限，以及这些产品授予访问权限的特定功能的描述。

### Adobe Experience Platform权限

Adobe Experience Platform下的权限包括访问数据流、身份、架构和沙盒。 有关如何配置Adobe Experience Platform权限的步骤，请参阅[访问控制用户指南](../access-control/ui/overview.md)。

| 类别 | 权限 | 描述 |
| --- | --- | --- |
| 沙盒 | （不适用） | 根据在您的组织下创建的[沙盒](../sandboxes/home.md)，您可以在Admin Console中通过此权限类别控制对每个沙盒的访问权限。 |
| 数据建模 | 管理架构 | 允许查看、创建和编辑[体验数据模型(XDM)架构](../xdm/home.md)。 |
| 数据建模 | 查看架构 | 授予对架构的只读访问权限。 |
| Identity Management | 管理身份命名空间 | 允许查看、创建和编辑[身份命名空间](../identity-service/features/namespaces.md)。 |
| Identity Management | 查看身份命名空间 | 授予对身份命名空间的只读访问权限。 |
| 数据收集 | 管理数据流 | 授予查看、创建和编辑[数据流](../datastreams/overview.md)的能力。 |
| 数据收集 | 查看数据流 | 授予对数据流的只读访问权限。 |

{style="table-layout:auto"}

### Adobe Experience Platform数据收集权限

Adobe Experience Platform数据收集下的权限可控制对标记和事件转发功能（包括属性、扩展和环境）的访问权限。 有关如何配置Adobe Experience Platform数据收集权限的步骤，请参阅下面的[部分](#manage)。

| 类别 | 权限 | 描述 |
| --- | --- | --- |
| 平台 | Web | 在与其他属性权限结合使用时，授予对[Web属性](../tags/ui/administration/companies-and-properties.md)的访问权限。 |
| 平台 | 移动设备 | 在与其他属性权限结合使用时，授予对[移动属性](../tags/ui/administration/companies-and-properties.md)的访问权限。 |
| 平台 | Edge | 在与其他属性权限结合使用时，授予对[Event Forwarding Edge属性](../tags/ui/event-forwarding/getting-started.md)的访问权限。 |
| 属性 | （不适用） | 根据在您的组织下创建的属性，您可以在Admin Console中通过此权限类别控制对其中每个属性的访问。<br><br>用户分配的属性权限仅适用于他们通过此权限类别被授予访问权限的属性。 |
| 资产权限 | 审批 | 允许将库生成批准为[发布流](../tags/ui/publishing/publishing-flow.md)的一部分。 |
| 资产权限 | 开发 | 允许将库生成开发为[发布流](../tags/ui/publishing/publishing-flow.md)的一部分。 |
| 资产权限 | 编辑属性 | 允许编辑用户有权访问的属性的基本配置。 |
| 资产权限 | 管理环境 | 授予管理用户有权访问的属性的[环境](../tags/ui/publishing/environments.md)的能力。 |
| 资产权限 | 管理扩展 | 授予管理用户有权访问的属性的[扩展](../tags/ui/managing-resources/extensions/overview.md)的能力。 |
| 资产权限 | 发布 | 允许将库内部版本发布为[发布流](../tags/ui/publishing/publishing-flow.md)的一部分。 |
| 公司权限 | 开发扩展 | 允许创建和修改组织拥有的扩展包，包括私有版本和公共发布请求。 |
| 公司权限 | 管理应用程序配置 | 此权限仅适用于您拥有Adobe Journey Optimizer或其他解决方案的许可证，且该许可证授予对移动应用程序内消息和推送消息的访问权限。 这允许您管理Adobe Experience Cloud知道的应用程序，以及与Firebase Cloud Messaging服务和Apple推送通知服务通信所需的推送凭据。 |
| 公司权限 | 管理资产 | 允许您创建和管理标记（Web属性）、事件转发（Edge属性）和移动属性。 |

{style="table-layout:auto"}

>[!NOTE]
>
>有关这些权限如何影响标记中功能（包括常见方案的管理策略）的更多信息，请参阅有关[用户权限](../tags/ui/administration/user-permissions.md)的标记文档。

## 管理权限 {#manage}

数据收集的权限通过两种产品名称进行管理： **Adobe Experience Platform**&#x200B;和&#x200B;**Adobe Experience Platform数据收集**。

有关如何管理Admin Console中每个产品下的相关权限的步骤，请参阅以下子部分：

* [Adobe Experience Platform权限](#manage-platform)
* [Adobe Experience Platform数据收集权限](#manage-collection)

### 在Adobe Experience Platform下管理权限 {#manage-platform}

>[!NOTE]
>
>要管理角色的权限，您需要管理员权限。 如果您没有管理员权限，请联系您的系统管理员。

Experience Cloud的&#x200B;**[!UICONTROL Permissions]**&#x200B;部分允许您定义用户角色和策略，以管理对产品应用程序中功能和对象的访问。

通过[!UICONTROL Permissions]，您可以创建和管理角色，并为这些角色分配所需的资源权限。

![Adobe Experience Cloud高亮显示权限产品。](assets/permissions/permissions-product.png)

要访问数据收集功能，必须启用&#x200B;**[!UICONTROL Sandboxes]**、**[!UICONTROL Data Modeling]**、**[!UICONTROL Identity Management]**&#x200B;和&#x200B;**[!UICONTROL Data Collection]**&#x200B;类别中的所有权限。

![显示Admin Console中的数据收集产品卡的图像](assets/permissions/platform-permission-card.png)

有关管理Experience Platform权限的详细说明，请参阅[访问控制UI指南](../access-control/ui/overview.md)。

>[!NOTE]
>
>根据您的组织有权访问的产品SKU，您可能没有每个Experience Platform权限可供您使用。

### 在Adobe Experience Platform数据收集下管理权限 {#manage-collection}

要管理这些权限，请登录到Admin Console并从顶部导航中选择&#x200B;**[!UICONTROL Products]**，然后选择&#x200B;**[!UICONTROL Adobe Experience Platform Data Collection]**。

![显示Admin Console中的数据收集产品卡的图像](assets/permissions/data-collection-card.png)

#### 选择或创建产品轮廓

下一个屏幕显示贵组织下数据收集的可用产品配置文件列表，默认配置文件为&#x200B;**[!DNL Default Data Collection All Access]**。 您可以根据需要选择编辑默认的产品配置文件，也可以选择&#x200B;**[!UICONTROL New Profile]**&#x200B;创建产品配置文件。 如果您的组织中有多个角色或用户组需要不同级别的访问权限，则应为每个角色或用户组创建单独的产品轮廓。

![显示Admin Console中数据收集的产品配置文件的图像](assets/permissions/new-profile.png)

选择或创建产品配置文件后，您可以使用&#x200B;**[!UICONTROL Edit]**&#x200B;图标来启动配置文件的[编辑权限](#edit-permissions)，或选择&#x200B;**[!UICONTROL Users]**&#x200B;选项卡以启动[将用户分配给配置文件](#assign-users)。

![显示产品轮廓 Admin Console 的权限选项卡的图像](assets/permissions/edit-permission-categories.png)

#### 编辑产品配置文件的权限 {#edit-permissions}

在编辑轮廓的权限时，可用权限将在左列中列出，而轮廓中包含的权限将在右列中列出。选择列出的权限，以在任一列之间移动它们。

![显示添加在所包含列](assets/permissions/added-permissions.png)下的权限的图像

权限会按类别进行组织。要在类别之间切换，请从左侧导航中选择所需的类别。

![图像显示权限下的“公司权限”部分](assets/permissions/switch-category.png)

配置完权限后，选择&#x200B;**[!UICONTROL Save]**。

![显示为产品轮廓保存的权限配置的图像](assets/permissions/save-permissions.png)

产品轮廓视图将重新出现，并会反映添加的权限。

![显示为产品轮廓添加的权限的图像](assets/permissions/permissions-added.png)

#### 将用户分配给产品配置文件 {#assign-users}

要将用户分配给产品配置文件（并授予他们配置文件配置的权限），请选择&#x200B;**[!UICONTROL Users]**&#x200B;选项卡，然后选择&#x200B;**[!UICONTROL Add user]**。

![显示 Admin Console 中产品轮廓的用户选项卡的图像](assets/permissions/manage-users.png)

有关为产品轮廓管理用户的详细信息，请参阅 [Admin Console 文档](https://helpx.adobe.com/cn/enterprise/using/manage-product-profiles.html)。

## 后续步骤

本指南介绍了数据收集可用的权限以及如何通过Admin Console管理这些权限。 有关为其他 Adobe Experience Platform 功能管理权限的详细信息，请参阅[访问控制文档](../access-control/home.md)。

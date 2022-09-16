---
keywords: Experience Platform；主页；热门主题；访问控制；基于属性的访问控制；
title: 基于属性的访问控制端到端指南
description: 本文档提供了有关Adobe Experience Platform中基于属性的访问控制的端到端指南
hide: true
hidefromtoc: true
source-git-commit: 440176ea1f21db3c7c4b3572fb52771dc70c80a0
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 基于属性的访问控制端到端指南

基于属性的访问控制是一项Adobe Experience Platform功能，它为具有隐私意识的品牌提供了更大的灵活性来管理用户访问权限。 可以将单个对象（如架构字段和区段）分配给用户角色。 此功能允许您为组织中的特定Platform用户授予或撤消对单个对象的访问权限。

利用此功能，可使用定义组织或数据使用范围的标签对架构字段、区段等进行分类。 在Adobe Journey Optimizer中，您可以将这些相同的标签应用于历程和选件。 同时，管理员可以定义围绕XDM架构字段的访问策略，并更好地管理哪些用户或组（内部、外部或第三方用户）可以访问这些字段。

## 快速入门

本教程需要对以下平台组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md):中的分段引擎 [!DNL Platform] 用于根据客户行为和属性从客户配置文件创建受众区段。

### 用例概述

本指南使用限制对敏感数据的访问的示例用例来演示工作流。 您将完成一个基于属性的访问控制工作流示例，在该工作流中，您将创建并分配角色、标签和策略，以配置用户是否可以访问组织中的特定资源。 下面概述了此用例：

您是医疗保健提供商，并且希望配置对组织中资源的访问权限。

* 您的内部营销团队应能够 **[!UICONTROL PHI/受管健康数据]** 数据。
* 外部机构应该无法访问 **[!UICONTROL PHI/受管健康数据]** 数据。

为此，您必须配置角色、资源和策略。

您将：

* [为用户设置角色标签]{#label-roles}:使用其营销组与外部代理合作的医疗保健提供商(ACME Business Group)的示例。
* [为资源设置标签（架构字段和区段）]{#label-resources}:分配 **[!UICONTROL PHI/受管健康数据]** 为架构资源和区段设置标签。
* [创建策略以将它们链接在一起]{#policy}:创建策略以将资源上的标签链接到角色中的标签，以拒绝访问架构字段和区段。 这将拒绝对没有匹配标签的用户访问架构字段并在所有沙箱中划分区段。

## 权限

[!UICONTROL 权限] 是Experience Cloud区域，管理员可以在其中定义用户角色和访问策略，以管理产品应用程序中功能和对象的访问权限。

到达 [!UICONTROL 权限]，您可以创建和管理角色，并为这些角色分配所需的资源权限。 [!UICONTROL 权限] 还允许您管理与特定角色关联的标签、沙箱和用户。

如果您没有管理员权限，请联系系统管理员以获取访问权限。

拥有管理员权限后，请转到 [Adobe Experience Cloud](https://experience.adobe.com/) 并使用您的Adobe凭据登录。 登录后， **[!UICONTROL 概述]** 会为您的组织显示页面。 本页显示贵组织订阅的产品，以及向整个组织添加用户和管理员的其他控件。 选择 **[!UICONTROL 权限]** 以打开用于Platform集成的工作区。

![显示在Adobe Experience Cloud中选择的权限产品的图像](../images/flac-ui/flac-select-product.png)

此时会显示平台UI的“权限”工作区，该工作区在 **[!UICONTROL 角色]** 页面。

## 将标签应用于角色 {#label-roles}

角色是对与您的Platform实例进行交互的用户类型进行分类的方法，这些用户是访问控制策略的构建基块。 角色具有一组给定的权限，并且可以根据角色需要的访问权限范围，将您组织的成员分配给一个或多个角色。

要开始配置，请选择 **[!UICONTROL ACME Business Group]** 从 **[!UICONTROL 角色]** 页面。

![显示在“职责”中选择的ACME业务职责的图像](../images/abac-end-to-end-user-guide/abac-select-role.png)

接下来，选择 **[!UICONTROL 标签]** 然后选择 **[!UICONTROL 添加标签]**.

![显示在“标签”选项卡上选择“添加标签”的图像](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

此时会显示组织中所有标签的列表。 选择 **[!UICONTROL RHD]** 为添加标签 **[!UICONTROL PHI/受管制的健康数据]**. 允许在标签旁边显示一些蓝色复选标记，然后选择 **[!UICONTROL 保存]**.

![显示正在选择和保存的RHD标签的图像](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

## 将标签应用于架构字段 {#label-resources}

现在，您已使用 [!UICONTROL RHD] 标签，下一步是将相同的标签添加到您要控制的该角色的资源中。

选择 **[!UICONTROL 模式]** 从左侧导航中，然后选择 **[!UICONTROL ACME Healthcare]** 从显示的架构列表中。

![显示从“架构”选项卡中选择的ACME医疗保健架构的图像](../images/abac-end-to-end-user-guide/abac-select-schema.png)

接下来，选择 **[!UICONTROL 标签]** 以查看显示与您的架构关联的字段的列表。 从此处，您可以一次为一个或多个字段分配标签。 选择 **[!UICONTROL 血糖]** 和 **[!UICONTROL 胰岛素水平]** 字段，然后选择 **[!UICONTROL 编辑管理标签]**.

![显示正在选择的血糖和胰岛素水平以及正在选择的管理标签的图像](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

的 **[!UICONTROL 编辑标签]** 对话框，允许您选择要应用于架构字段的标签。 对于此用例，请选择 **[!UICONTROL PHI/受管健康数据]** 标签，然后选择 **[!UICONTROL 保存]**.

![显示正在选择和保存的RHD标签的图像](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>将标签添加到字段后，该标签将应用于该字段的父资源（类或字段组）。 如果父类或字段组由其他架构使用，则这些架构将继承相同的标签。

## 将标签应用于区段

完成架构字段的标签设置后，您现在可以开始为区段添加标签。

选择 **[!UICONTROL 区段]** 的上界。 此时会显示组织中可用的区段列表。 在本例中，以下两个区段将进行标记，因为它们包含敏感的运行状况数据：

* 血糖>100
* 胰岛素&lt;50

选择 **[!UICONTROL 血糖>100]** 以开始标记区段。

![显示从“区段”选项卡中选择的血糖超过100的图像](../images/abac-end-to-end-user-guide/abac-select-segment.png)

区段 **[!UICONTROL 详细信息]** 屏幕。 选择 **[!UICONTROL 管理访问权限]**.

![显示“管理访问”选择的图像](../images/abac-end-to-end-user-guide/abac-segment-fields-manage-access.png)

的 **[!UICONTROL 编辑标签]** 对话框，允许您选择要应用于区段的标签。 对于此用例，请选择 **[!UICONTROL PHI/受管健康数据]** 标签，然后选择 **[!UICONTROL 保存]**.

![显示RHD标签选择和保存选择的图像](../images/abac-end-to-end-user-guide/abac-select-segment-labels.png)

使用 **[!UICONTROL 胰岛素&lt;50]**.

## 创建访问控制策略 {#policy}

访问控制策略利用标签来定义哪些用户角色有权访问特定的平台资源。 策略可以是本地策略，也可以是全局策略，并且可以覆盖其他策略。 在此示例中，对于在架构字段中没有相应标签的用户，将拒绝在所有沙箱中访问架构字段和区段。

要创建访问控制策略，请选择 **[!UICONTROL 权限]** 从左侧导航中，然后选择 **[!UICONTROL 策略]**. 接下来，选择 **[!UICONTROL 创建策略]**.

![显示正在权限中选择创建策略的图像](../images/abac-end-to-end-user-guide/abac-create-policy.png)

的 **[!UICONTROL 创建新策略]** 对话框，提示您输入名称和可选描述。 选择 **[!UICONTROL 确认]** 完成。

![显示创建新策略对话框并选择确认的图像](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

要拒绝访问架构字段，请使用下拉箭头并选择 **[!UICONTROL 拒绝访问]** 然后选择 **[!UICONTROL 未选择任何资源]**. 接下来，选择 **[!UICONTROL 架构字段]** 然后选择 **[!UICONTROL 全部]**.

![显示拒绝访问和选定资源的图像](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

下表显示了创建策略时可用的条件：

| 条件 | 描述 |
| --- | --- |
| 以下内容为false | 设置“拒绝访问”后，如果用户不满足所选条件，则访问权限将受到限制。 |
| 以下是true | 设置“允许访问”后，如果用户符合所选条件，则允许访问。 |
| 匹配任意 | 用户的标签与应用到资源的任何标签相匹配。 |
| 全部匹配 | 用户具有所有与应用于资源的所有标签相匹配的标签。 |
| 核心标签 | 核心标签是Adobe定义的标签，可在所有Platform实例中使用。 |
| 自定义标签 | 自定义标签是您的组织创建的标签。 |

选择 **[!UICONTROL 以下内容为false]** 然后选择 **[!UICONTROL 未选择属性]**. 接下来，选择用户 **[!UICONTROL 核心标签]**，然后选择 **[!UICONTROL 全部匹配]**. 选择资源 **[!UICONTROL 核心标签]** 最后选择 **[!UICONTROL 添加资源]**.

![显示正在选择的条件和正在选择的添加资源的图像](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>资源是主题可以或不能访问的资产或对象。 资源可以是区段或架构。

要拒绝访问区段，请使用下拉箭头并选择 **[!UICONTROL 拒绝访问]** 然后选择 **[!UICONTROL 未选择任何资源]**. 接下来，选择 **[!UICONTROL 区段]** 然后选择 **[!UICONTROL 全部]**.

选择 **[!UICONTROL 以下内容为false]** 然后选择 **[!UICONTROL 未选择属性]**. 接下来，选择用户 **[!UICONTROL 核心标签]**，然后选择 **[!UICONTROL 全部匹配]**. 选择资源 **[!UICONTROL 核心标签]** 最后选择 **[!UICONTROL 保存]**.

![显示已选择并正在选择保存的条件的图像](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

选择 **[!UICONTROL 激活]** 激活策略时，将显示一个对话框，提示您确认激活。 选择 **[!UICONTROL 确认]** 然后选择 **[!UICONTROL 关闭]**.

![显示要激活的策略的图像 ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png)

## 后续步骤

您已完成将标签应用到角色、架构字段和区段。 分配给这些角色的外部代理在架构、数据集和配置文件视图中无法查看这些标签及其值。 在使用区段生成器时，这些字段也会受到限制，无法在区段定义中使用。

有关基于属性的访问控制的详细信息，请参阅 [基于属性的访问控制概述](./overview.md).

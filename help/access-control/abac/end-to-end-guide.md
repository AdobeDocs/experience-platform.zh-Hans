---
keywords: Experience Platform；主页；热门主题；访问控制；基于属性的访问控制；
title: 基于属性的访问控制端到端指南
description: 本文档提供了有关Adobe Experience Platform中基于属性的访问控制的端到端指南
exl-id: 7e363adc-628c-4a66-a3bd-b5b898292394
source-git-commit: 004f6183f597132629481e3792b5523317b7fb2f
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 19%

---

# 基于属性的访问控制端到端指南

基于属性的访问控制是Adobe Experience Platform的一项功能，它为注重隐私的多品牌客户提供了更大的灵活性来管理用户访问权限。 可以使用基于对象属性和角色的策略授予/拒绝对单个对象（如架构字段和区段）的访问权限。 此功能允许您为组织中的特定Platform用户授予或撤消对单个对象的访问权限。

利用此功能，可使用定义组织或数据使用范围的标签对架构字段、区段等进行分类。 您可以将这些相同的标签应用于Adobe Journey Optimizer中的历程、选件和其他对象。 同时，管理员可以围绕体验数据模型(XDM)架构字段定义访问策略，并更好地管理哪些用户或组（内部、外部或第三方用户）可以访问这些字段。

>[!NOTE]
>
>本文档重点介绍访问控制策略的用例。 如果您尝试设置策略来管理 **use** 的端到端指南，请参阅 [数据管理](../../data-governance/e2e.md) 中。

## 快速入门

本教程需要对以下平台组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md):中的分段引擎 [!DNL Platform] 用于根据客户行为和属性从客户配置文件创建受众区段。

### 用例概述

您将完成一个基于属性的访问控制工作流示例，在该工作流中，您将创建并分配角色、标签和策略，以配置用户是否可以访问组织中的特定资源。 本指南使用限制对敏感数据的访问的示例来演示工作流。 下面概述了此用例：

您是医疗保健提供商，希望配置对组织中资源的访问权限。

* 您的内部营销团队应能够 **[!UICONTROL PHI/受管健康数据]** 数据。
* 外部机构应该无法访问 **[!UICONTROL PHI/受管健康数据]** 数据。

为此，您必须配置角色、资源和策略。

您将：

* [为用户设置角色标签](#label-roles):使用其营销组与外部代理合作的医疗保健提供商(ACME Business Group)的示例。
* [为资源设置标签（架构字段和区段）](#label-resources):分配 **[!UICONTROL PHI/受管健康数据]** 为架构资源和区段设置标签。
* 
   * [激活将它们链接在一起的策略： ](#policy):启用默认策略，通过将资源上的标签连接到您角色中的标签来阻止对架构字段和区段的访问。 随后，具有匹配标签的用户将有权访问架构字段并在所有沙箱中进行分段。

## 权限

[!UICONTROL 权限] 是Experience Cloud区域，管理员可以在其中定义用户角色和策略，以管理产品应用程序中功能和对象的权限。

到达 [!UICONTROL 权限]，则可以创建和管理角色，并为这些角色分配所需的资源权限。 [!UICONTROL 权限还允许您管理与特定角色关联的标签、沙盒和用户。]

如果您没有管理员权限，请联系您的系统管理员以获取访问权限。

拥有管理员权限后，请转到 [Adobe Experience Cloud](https://experience.adobe.com/) 并使用您的Adobe凭据登录。 登录后， **[!UICONTROL 概述]** 会为您的组织显示页面。 此页面显示贵组织订阅的产品，以及向组织添加用户和管理员的其他控件。 选择 **[!UICONTROL 权限]** 以打开用于Platform集成的工作区。

![显示在Adobe Experience Cloud中选择的权限产品的图像](../images/flac-ui/flac-select-product.png)

此时会显示平台UI的“权限”工作区，该工作区在 **[!UICONTROL 角色]** 页面。

## 将标签应用于角色 {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="标签是什么？"
>abstract="通过标签，可根据适用于数据的使用策略将数据集和字段分类。Platform 提供若干由 Adobe 定义的“核心”数据使用标签，这些标签涵盖适用于数据治理的多种常见限制。例如，通过 RHD（受监管的健康数据）等敏感的“S”标签，可将涉及受保护的健康信息 (PHI) 的数据分类。还可自行定义适合组织需求的自定义标签。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=zh-Hans#understanding-data-usage-labels" text="数据使用标签概述"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="创建新标签"
>abstract="可自行创建自定义标签以适合组织需求。自定义标签可用于将数据治理和访问控制配置应用于您的数据。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=zh-Hans#manage-labels" text="管理自定义标签"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="角色是什么？"
>abstract="角色是将与您的 Platform 实例交互的用户的类型分类的方法，还是访问控制策略的构建块。一个角色具有一组给定的权限，可将您组织的成员分配给一个或多个角色，具体取决于他们需要的查看或写入访问权限的范围。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=zh-Hans" text="管理角色"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="创建新角色"
>abstract="可创建新角色以更好地将访问您的 Platform 实例的用户分类。例如，可为内部营销团队创建一个角色，并将 RHD 标签应用于该角色，使您的内部营销团队可访问受保护的健康信息 (PHI)。或者，还可为外部机构创建一个角色，并通过不将 RHD 标签应用于该角色而拒绝该角色访问 PHI 数据。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=zh-Hans#create-a-new-role" text="创建新角色"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="角色概述"
>abstract="角色概述对话框显示允许给定角色访问的资源和沙盒。"

角色是对与您的平台实例交互的用户类型进行分类的方法，是访问控制策略的构建基块。 角色具有一组给定的权限，并且可以根据组织成员需要的访问权限范围，将其分配给一个或多个角色。

要开始配置，请选择 **[!UICONTROL ACME Business Group]** 从 **[!UICONTROL 角色]** 页面。

![显示在“职责”中选择的ACME业务职责的图像](../images/abac-end-to-end-user-guide/abac-select-role.png)

接下来，选择 **[!UICONTROL 标签]** 然后选择 **[!UICONTROL 添加标签]**.

![显示在“标签”选项卡上选择“添加标签”的图像](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

此时会显示组织中所有标签的列表。 选择 **[!UICONTROL RHD]** 为添加标签 **[!UICONTROL PHI/受管制的健康数据]**. 允许在标签旁边显示一些蓝色复选标记，然后选择 **[!UICONTROL 保存]**.

![显示正在选择和保存的RHD标签的图像](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

>[!NOTE]
>
>将组织组添加到角色时，该组中的所有用户都将添加到该角色。 对组织组所做的任何更改（删除或添加的用户）将在角色中自动更新。

## 将标签应用于架构字段 {#label-resources}

现在，您已使用 [!UICONTROL RHD] 标签，下一步是将相同的标签添加到您要控制的该角色的资源中。

选择 **[!UICONTROL 模式]** 从左侧导航中，然后选择 **[!UICONTROL ACME Healthcare]** 从显示的架构列表中。

![显示从“架构”选项卡中选择的ACME医疗保健架构的图像](../images/abac-end-to-end-user-guide/abac-select-schema.png)

接下来，选择 **[!UICONTROL 标签]** 以查看显示与您的架构关联的字段的列表。 从此处，您可以一次为一个或多个字段分配标签。 选择 **[!UICONTROL 血糖]** 和 **[!UICONTROL 胰岛素水平]** 字段，然后选择 **[!UICONTROL 应用访问和数据管理标签]**.

![显示正在选择的血糖和胰岛素水平以及正在选择的访问和数据管理标签的图像](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

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

## 激活访问控制策略 {#policy}

默认的访问控制策略将利用标签来定义哪些用户角色有权访问特定的平台资源。 在此示例中，对于未在架构字段中具有相应标签的角色的用户，将拒绝在所有沙箱中访问架构字段和区段。

要激活访问控制策略，请选择 [!UICONTROL 权限] 从左侧导航中，然后选择 **[!UICONTROL 策略]**.

![显示的策略列表](../images/abac-end-to-end-user-guide/abac-policies-page.png)

接下来，选择省略号(`...`)，并且下拉列表会显示用于编辑、激活、删除或复制角色的控件。 选择 **[!UICONTROL 激活]** 从下拉菜单中。

![用于激活策略的下拉列表](../images/abac-end-to-end-user-guide/abac-policies-activate.png)

此时会出现激活策略对话框，提示您确认激活。 选择 **[!UICONTROL 确认]**.

![激活策略对话框](../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)

收到策略激活的确认函，您将返回到 [!UICONTROL 策略] 页面。

![激活策略确认](../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

<!-- ## Create an access control policy {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="What are policies?"
>abstract="Policies are statements that bring attributes together to establish permissible and impermissible actions. Every organization comes with a default policy that you must activate to define rules for resources like segments and schema fields. Default policies can neither be edited nor deleted. However, default policies can be activated or deactivated."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en" text="Manage policies"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Create a policy"
>abstract="Create a policy to define the actions that your users can and cannot take against your segments and schema fields."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#create-a-new-policy" text="Create a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Configure permissible and impermissible actions for a policy"
>abstract="A <b>deny access to</b> policy will deny users access when the criteria is met. Combined with <b>The following being false</b> - all users will be denied access unless they meet the matching criteria set. This type of policy allows you to protect a sensitive resource and only allow access to users with matching labels. <br>A <b>permit access to</b> policy will permit users access when the criteria are met. When combined with <b>The following being true</b> - users will be given access if they meet the matching criteria set. This does not explicitly deny access to users, but adds a permit access. This type of policy allows you to give additional access to resource and in addition to those users who might already have access through role permissions."</br>
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#edit-a-policy" text="Edit a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Configure permissions for a resource"
>abstract="A resource is the asset or object that a user can or cannot access. Resources can be segments or schemas fields. You can configure write, read, or delete permissions for segments and schema fields."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Edit conditions"
>abstract="Apply conditional statements to your policy to configure user access to certain resources. Select match all to require users to have roles with the same labels as a resource to be permitted access. Select match any to require users to have a role with just one label matching a label on a resource. Labels can either be defined as core or custom labels, with core labels representing labels created and provided by Adobe and custom labels representing labels that you created for your organization."

Access control policies leverage labels to define which user roles have access to specific Platform resources. Policies can either be local or global and can override other policies. In this example, access to schema fields and segments will be denied in all sandboxes for users who don't have the corresponding labels in the schema field.

>[!NOTE]
>
>A "deny policy" is created to grant access to sensitive resources because the role grants permission to the subjects. The written policy in this example **denies** you access if you are missing the required labels.

To create an access control policy, select **[!UICONTROL Permissions]** from the left navigation and then select **[!UICONTROL Policies]**. Next, select **[!UICONTROL Create policy]**.

![Image showing Create policy being selected in the Permissions](../images/abac-end-to-end-user-guide/abac-create-policy.png)

The **[!UICONTROL Create new policy]** dialog appears, prompting you to enter a name and an optional description. Select **[!UICONTROL Confirm]** when finished.

![Image showing the Create new policy dialog and selecting Confirm](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

To deny access to the schema fields, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Schema Field]** and then select **[!UICONTROL All]**.

![Image showing Deny access and resources selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

The table below shows the conditions available when creating a policy:

| Conditions | Description |
| --- | --- |
| The following being false| When 'Deny access to' is set, access will be restricted if the user does not meet the criteria selected. |
| The following being true| When 'Permit access to' is set, access will be permitted if the user meets the selected criteria. |
| Matches any| The user has a label that matches any label applied to a resource. |
| Matches all| The user has all labels that matches all labels applied to a resource. |
| Core label| A core label is an Adobe-defined label that is available in all Platform instances.|
| Custom label| A custom label is a label that has been created by your organization.|

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Add resource]**.

![Image showing the conditions being selected and Add resource being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>A resource is the asset or object that a subject can or cannot access. Resources can be segments or schemas.

To deny access to the segments, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Segment]** and then select **[!UICONTROL All]**.

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Save]**.

![Image showing conditions selected and Save being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Select **[!UICONTROL Activate]** to activate the policy, and a dialog appears which prompts you to confirm activation. Select **[!UICONTROL Confirm]** and then select **[!UICONTROL Close]**.

![Image showing the Policy being activated ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png) -->

## 后续步骤

您已完成将标签应用到角色、架构字段和区段。 分配给这些角色的外部代理在架构、数据集和配置文件视图中无法查看这些标签及其值。 在使用区段生成器时，这些字段也会受到限制，无法在区段定义中使用。

有关基于属性的访问控制的详细信息，请参阅 [基于属性的访问控制概述](./overview.md).

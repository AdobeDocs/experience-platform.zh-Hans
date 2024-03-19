---
title: 使用访问标签管理用户对目标数据流的访问
description: 了解如何使用访问标签来管理用户对目标数据流的访问，以便只有贵组织中的一部分用户有权访问特定的目标数据流。
badgePrivateBeta: label="私人测试版" type="Informative"
hide: true
hidefromtoc: true
role: Developer, Admin, User
source-git-commit: 5e5dc2f755be0f396dec1d3f19c166bae3bc9575
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 1%

---


# 使用访问标签管理用户对目标数据流的访问

作为 [!UICONTROL 基于属性的访问控制] Real-Time CDP功能，您现在可以将访问标签应用于目标数据流。 因此，您可以确保组织中只有一部分用户有权访问特定的目标数据流。

向特定目标添加访问标签时，只有对分配了该标签的角色具有访问权限的用户才能查看和编辑该目标数据流。 如果目标数据流未标记任何标签，则属于您组织的所有用户都可看到它。

请参阅此页面以了解示例用例、在使用此功能时将访问标签应用于目标数据流之前的先决条件以及其他重要标注。

## 先决条件 {#prerequisites}

在开始使用此功能之前，请注意要完成的以下先决条件。 熟悉 [!UICONTROL 基于属性的访问控制] 功能，Adobe还建议您阅读以下文章：

* [基于属性的访问控制概述](/help/access-control/abac/overview.md)
* [基于属性的访问控制端到端指南](/help/access-control/abac/end-to-end-guide.md)

### 访问权限UI {#access-permissions-ui}

[!UICONTROL 权限] 是Experience Cloud区域，管理员可以在其中定义用户角色和策略，以管理产品应用程序内功能和对象的权限。 阅读 [权限部分](/help/access-control/abac/end-to-end-guide.md#permissions) 以开始使用。

### 创建角色、标签和分配用户 {#create-roles-labels-assign-users}

在访问 [!UICONTROL 权限] UI中，您或团队成员必须设置角色，并将所需的标签添加到这些角色中。 最后，必须将应该访问带有特定标签的资源的用户添加到角色中。 请参阅以下文档部分：

* [创建新角色](/help/access-control/abac/ui/roles.md)
* [向角色添加标签](/help/access-control/abac/end-to-end-guide.md#label-roles)
* [将用户添加到角色](/help/access-control/ui/users.md)

### 创建目标数据流 {#create-dataflow}

您首先需要连接到所需的目标并创建数据流以导出数据，然后才能将访问标签应用于数据流。

阅读指南 [连接到目标](/help/destinations/ui/connect-destination.md) 和 [将数据激活到目标](/help/destinations/ui/activation-overview.md). 然后，从中选择所需的目标 [可用连接器的目录](/help/destinations/catalog/overview.md).

## 已可用：将访问标签应用于其他Experience Platform资源 {#apply-labels-other-resources}

虽然通过此版本可以授予用户对特定目标数据流的对象级访问权限，但授予对象级访问权限的功能通常对其他Experience Platform资源可用，例如 [受众](/help/access-control/abac/end-to-end-guide.md#apply-labels-to-segments).

## 用例示例 {#use-case-example}

通过对目标的对象级访问控制，可以限制特定营销人员团队只能访问其特定目标。 例如，如果您的组织在多个地理位置（如美国和英国）拥有客户数据，您可以将营销团队限制为仅查看和编辑美国位置的数据流，将另一营销团队限制为查看和编辑英国位置的数据流。

## 将访问标签应用于目标数据流 {#apply-labels-to-destination-dataflow}

要将访问标签应用于特定数据流，请执行以下操作：

1. 导航到 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]** 并找到要限制用户访问的目标数据流。
1. 选择省略号(`...`) [!UICONTROL 名称] 列并使用 ![编辑详细信息控件](/help/access-control/images/olac/key-icon.svg) **[!UICONTROL 应用访问标签]** 控制以添加新标签并管理数据流的现有标签。
   ![在目标工作区的浏览视图中选择应用访问标签。](/help/access-control/images/olac/apply-access-labels.png)
1. 选择要添加到目标数据流的标签并选择 **[!UICONTROL 保存]**.
   ![选择中应应用于目标数据流的访问标签。](/help/access-control/images/olac/view-access-labels.png)
1. 请注意数据流现在如何在UI中显示访问标签。
   ![查看具有选定数据流的多个目标数据流，了解如何显示访问标签。](/help/access-control/images/olac/dataflow-with-access-label.png)

如果目标数据流未标记任何标签，则会向所有用户显示。 如果数据流标有一个或多个访问标签，则它只为属于具有相同标签或标签组合的角色的用户显示。

您可以将标准和自定义标签添加到目标数据流。 将标签添加到目标数据流后：

* 分配了具有相同标签访问权限的角色的用户可以在UI中查看带有新标签的数据流。 他们可以在用户界面中或通过API查看和编辑目标数据流。

* 用户 *非* 分配给有权访问相同标签的角色无权访问目标数据流，无法在用户界面中或通过API查看或编辑它。

## 要了解的重要标注和项 {#important-callouts}

目前，访问标签只能应用于现有数据流。 这意味着在应用访问标签之前，需要创建到目标的数据流。

如果您无权访问某个访问标签，则无法将该访问标签应用于目标数据流。

向目标数据流添加多个标签时，必须将应该能够查看和编辑数据流的用户添加到至少具有相同标签组合的角色中。 例如，如果将标签C1、I2和另一个自定义标签应用于目标数据流，则只有添加到角色且具有这三个标签组合访问权限的用户才能查看和编辑此特定目标数据流。

![维恩图显示仅特定用户如何访问应用了多个标签的目标。](/help/access-control/images/olac/multiple-labels-venn.png)

## 后续步骤 {#next-steps}

通过执行本文档中的步骤，您现在知道如何将访问标签应用于目标数据流，以便只有组织中的用户子集才能访问特定的目标数据流。

接下来，您可以详细了解受支持的其他功能 [!UICONTROL 基于属性的访问控制] 将数据激活到目标时。 例如，您可以将用户的访问权限限制为 [仅查看和激活特定字段](/help/access-control/abac/overview.md#destinations).
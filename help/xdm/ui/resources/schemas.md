---
keywords: Experience Platform；主页；热门主题；API;API;XDM;XDM系统；体验数据模型；数据模型；UI；工作区；模式；模式；
solution: Experience Platform
title: 在UI中创建和编辑架构
description: 了解如何在Experience Platform用户界面中创建和编辑模式的基础知识。
topic-legacy: user guide
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 49a54b78d1e3745694352e779fb2226acd99d663
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 0%

---

# 在UI中创建和编辑架构

本指南概述了如何在Adobe Experience Platform UI中为贵组织创建、编辑和管理Experience Data Model(XDM)模式。

>[!IMPORTANT]
>
>XDM架构是完全可自定义的，因此创建架构时涉及的步骤可能会因您希望架构捕获的数据类型而异。 因此，本文档仅涵盖您在UI中与架构进行的基本交互，并排除了自定义类、架构字段组、数据类型和字段等相关步骤。
>
>有关模式创建过程的完整教程，请遵循 [模式创建教程](../../tutorials/create-schema-ui.md) 创建完整的示例模式，并熟悉 [!DNL Schema Editor].

## 先决条件

本指南需要对XDM系统有一定的了解。 请参阅 [XDM概述](../../home.md) 介绍XDM在Experience Platform生态系统中的作用，以及 [架构组合基础知识](../../schema/composition.md) 概述如何构建模式。

## 创建新架构 {#create}

在 [!UICONTROL 模式] 工作区，选择 **[!UICONTROL 创建架构]** 中。 在显示的下拉菜单中，您可以选择 **[!UICONTROL XDM个人配置文件]** 和 **[!UICONTROL XDM ExperienceEvent]** 作为架构的基类。 或者，您也可以选择 **[!UICONTROL 浏览]** 从可用类的完整列表中进行选择，或 [创建新的自定义类](./classes.md#create) 中。

![](../../images/ui/resources/schemas/create-schema.png)

选择类后， [!DNL Schema Editor] 将显示，并且架构的基本结构（由类提供）将显示在画布中。 从此处，您可以使用右边栏添加 **[!UICONTROL 显示名称]** 和 **[!UICONTROL 描述]** 的子目录。

![](../../images/ui/resources/schemas/schema-details.png)

您现在可以通过 [添加架构字段组](#add-field-groups).

## 编辑现有架构 {#edit}

>[!NOTE]
>
>保存架构并在数据摄取中使用后，只能对其进行附加更改。 请参阅 [模式演化规则](../../schema/composition.md#evolution) 以了解更多信息。

要编辑现有架构，请选择 **[!UICONTROL 浏览]** 选项卡，然后选择要编辑的架构的名称。

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>您可以使用工作区的搜索和筛选功能来帮助更轻松地查找架构。 请参阅 [浏览XDM资源](../explore.md) 以了解更多信息。

选择架构后， [!DNL Schema Editor] 显示，画布中显示了架构的结构。 您现在可以 [添加字段组](#add-field-groups) 到架构， [编辑字段显示名称](#display-names)或 [编辑现有自定义字段组](./field-groups.md#edit) 如果架构使用任何。

## 将字段组添加到架构 {#add-field-groups}

>[!NOTE]
>
>本节介绍如何将现有字段组添加到架构。 如果要创建新的自定义字段组，请参阅 [创建和编辑字段组](./field-groups.md#create) 中。

在中打开架构后 [!DNL Schema Editor]，则可以通过使用字段组将字段添加到架构。 要开始，请选择 **[!UICONTROL 添加]** 下一页 **[!UICONTROL 字段组]** 中。

![](../../images/ui/resources/schemas/add-field-group-button.png)

此时会出现一个对话框，其中显示了可为架构选择的字段组列表。 由于字段组只与一个类兼容，因此将只列出与架构的选定类关联的那些字段组。 默认情况下，列出的字段组会根据其在您组织内的使用受欢迎程度进行排序。

![](../../images/ui/resources/schemas/field-group-popularity.png)

如果您知道要添加的字段的常规活动或业务区域，请在左边栏中选择一个或多个垂直行业类别，以过滤显示的字段组列表。

![](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>有关XDM中特定于行业的数据建模最佳实践的更多信息，请参阅 [行业数据模型](../../schema/industries/overview.md).

您还可以使用搜索栏帮助查找所需的字段组。 名称与查询匹配的字段组显示在列表顶部。 在 **[!UICONTROL 标准字段]**，则会显示包含描述所需数据属性的字段的字段组。

![](../../images/ui/resources/schemas/field-group-search.png)

选中要添加到架构的字段组名称旁边的复选框。 您可以从列表中选择多个字段组，每个选定的字段组都显示在右边栏中。

![](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>对于列出的任何字段组，您可以将鼠标悬停或集中在信息图标(![](../../images/ui/resources/schemas/info-icon.png))以查看字段组捕获的数据类型的简要描述。 您还可以选择预览图标(![](../../images/ui/resources/schemas/preview-icon.png))以查看字段组提供的字段结构，然后再决定将其添加到架构。

选择字段组后，选择 **[!UICONTROL 添加字段组]** 以将其添加到架构。

![](../../images/ui/resources/schemas/add-field-group-finish.png)

的 [!DNL Schema Editor] 重新显示，画布中显示的字段组提供的字段。

![](../../images/ui/resources/schemas/field-groups-added.png)

## 为实时客户用户档案启用架构 {#profile}

[实时客户资料](../../../profile/home.md) 合并来自不同来源的数据，以构建每个客户的完整视图。 如果您希望架构捕获的数据参与此过程，则必须启用该架构以在中使用 [!DNL Profile].

>[!IMPORTANT]
>
>为了为 [!DNL Profile]，则必须定义主标识字段。 请参阅 [定义标识字段](../fields/identity.md) 以了解更多信息。

要启用架构，请首先在左边栏中选择架构的名称，然后选择 **[!UICONTROL 用户档案]** 在右边栏中切换。

![](../../images/ui/resources/schemas/profile-toggle.png)

此时会出现一个弹出窗口，警告您在启用并保存架构后，便无法禁用该架构。 选择 **[!UICONTROL 启用]** 继续。

![](../../images/ui/resources/schemas/profile-confirm.png)

画布将重新显示，其中 [!UICONTROL 用户档案] 启用切换。

>[!IMPORTANT]
>
>由于架构尚未保存，因此如果您改变主意让架构参与实时客户资料，则此点不会返回：保存已启用的架构后，便无法再将其禁用。 选择 **[!UICONTROL 用户档案]** 再次切换以禁用架构。

要完成该过程，请选择 **[!UICONTROL 保存]** 以保存架构。

![](../../images/ui/resources/schemas/profile-enabled.png)

此架构现已启用，可在实时客户资料中使用。 当Platform根据此架构将数据摄取到数据集时，该数据将并入合并的用户档案数据中。

## 编辑架构字段的显示名称 {#display-names}

在为架构分配了类并将字段组添加到架构后，您可以编辑该架构中任何字段的显示名称，而不管这些字段是由标准XDM资源还是自定义XDM资源提供。

>[!NOTE]
>
>请记住，属于标准类或字段组的字段的显示名称只能在特定架构的上下文中编辑。 换言之，更改一个架构中标准字段的显示名称不会影响使用相同关联类或字段组的其他架构。
>
>更改架构字段的显示名称后，这些更改会立即反映在基于该架构的任何现有数据集中。

要编辑架构字段的显示名称，请在画布中选择该字段。 在右边栏中，在 **[!UICONTROL 显示名称]**.

![](../../images/ui/resources/schemas/display-name.png)

选择 **[!UICONTROL 应用]** 在右边栏中，画布会更新以显示字段的新显示名称。 选择 **[!UICONTROL 保存]** 以将更改应用到架构。

![](../../images/ui/resources/schemas/display-name-changed.png)

## 更改架构的类 {#change-class}

在保存架构之前，您可以在初始合成过程中的任意时刻更改架构的类。

>[!WARNING]
>
>重新分配模式的类时应格外谨慎。 字段组仅与某些类兼容，因此更改类将重置画布和您添加的任何字段。

要重新分配类，请选择 **[!UICONTROL 分配]** 在画布的左侧。

![](../../images/ui/resources/schemas/assign-class-button.png)

此时会出现一个对话框，其中显示所有可用类的列表，包括您的组织定义的任何类(所有者为“[!UICONTROL 客户]“”)以及由Adobe定义的标准类。

从列表中选择一个类，以在对话框的右侧显示其说明。 您还可以选择 **[!UICONTROL 预览类结构]** 以查看与类关联的字段和元数据。 选择 **[!UICONTROL 分配类]** 继续。

![](../../images/ui/resources/schemas/assign-class.png)

此时将打开一个新对话框，要求您确认您希望分配一个新类。 选择 **[!UICONTROL 分配]** 确认。

![](../../images/ui/resources/schemas/assign-confirm.png)

确认类更改后，画布将重置，所有合成进度都将丢失。

## 后续步骤

本文档介绍了在Platform UI中创建和编辑架构的基础知识。 强烈建议您查看 [模式创建教程](../../tutorials/create-schema-ui.md) 有关在UI中构建完整架构的全面工作流，包括为独特用例创建自定义字段组和数据类型。

有关 [!UICONTROL 模式] 工作区，请参阅 [[!UICONTROL 模式] 工作区概述](../overview.md).

了解如何在 [!DNL Schema Registry] API，请参阅 [schema endpoint指南](../../api/schemas.md).

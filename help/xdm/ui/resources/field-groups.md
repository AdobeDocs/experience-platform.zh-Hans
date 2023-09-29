---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；数据模型；ui；工作区；字段组；字段组；
solution: Experience Platform
title: 在UI中创建和编辑架构字段组
description: 了解如何在Experience Platform用户界面中创建和编辑架构字段组。
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: 0375ddcb7d06208199bf1172b157aa6eb28811f6
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 8%

---

# 在 UI 中创建和编辑架构字段组 {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_filter"
>title="标准或自定义字段组筛选器"
>abstract="根据如何创建可用的字段预先过滤可用的字段的列表。选中单选按钮可在“标准”与“自定义”选项之间选择。“标准”选项显示由 Adobe 创建的实体，而“自定义”选项显示在您的组织内创建的实体。请参阅文档以详细了解创建和编辑字段组。"

在Experience Data Model (XDM)中，架构字段组是可重复使用的组件，这些组件定义一个或多个实施某些功能（如个人详细信息、酒店偏好设置或地址）的字段。 字段组旨在作为实现兼容类的架构的一部分包含。

字段组根据字段组表示的数据的行为（记录或时间序列）定义其兼容的类。 这意味着并非所有字段组都可以与所有类一起使用。

Adobe Experience Platform提供了许多标准字段组，涵盖广泛的营销用例。 但是，您还可以创建和编辑自己的自定义字段组，以定义与XDM架构中的业务相关的其他概念。 本指南概述了如何在Platform UI中为您的组织创建、编辑和管理自定义字段组。

## 先决条件

本指南要求您对XDM系统有一定的了解。 请参阅 [XDM概述](../../home.md) 介绍XDM在Experience Platform生态系统中的作用，以及 [模式组合基础](../../schema/composition.md) 了解字段组对XDM架构的贡献方式。

虽然本指南并非必需，但建议您也按照以下内容阅读本教程： [在UI中组合架构](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor].

## 创建新字段组 {#create}

要创建新字段组，您必须首先选择要将该字段组添加到的架构。 您可以选择 [创建新架构](./schemas.md#create) 或 [选择要编辑的现有架构](./schemas.md#edit).

一旦您在中打开架构， [!DNL Schema Editor]，选择 **[!UICONTROL 添加]** 旁边的 [!UICONTROL 字段组] 部分。

![](../../images/ui/resources/field-groups/add-field-group.png)

在显示的对话框中，选择 **[!UICONTROL 创建新字段组]**. 在这里，您可以提供 **[!UICONTROL 显示名称]** 和 **[!UICONTROL 描述]** 对于字段组。 完成后，选择 **[!UICONTROL 添加字段组]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

此 [!DNL Schema Editor] 此时会重新显示，左侧边栏中列出了新的字段组。 由于这是一个全新的字段组，它当前不向架构提供任何字段，因此画布保持不变。 您现在可以开始 [向字段组添加字段](#add-fields).

![](../../images/ui/resources/field-groups/field-group-added.png)

## 筛选字段组 {#filter}

根据如何创建可用的字段预先过滤可用的字段的列表。默认设置显示由Adobe定义的字段组。 但是，您还可以筛选列表以显示由您的组织创建的列表。 选择单选按钮以选择 [!UICONTROL 标准] 和 [!UICONTROL 自定义] 选项。 此 [!UICONTROL 标准] 选项显示由Adobe创建的实体以及 [!UICONTROL 自定义] 选项显示组织内创建的实体。

![此 [!UICONTROL 字段组] 选项卡 [!UICONTROL 架构] 工作区，使用 [!UICONTROL 标准] 和 [!UICONTROL 自定义] 突出显示。](../../images/ui/resources/field-groups/standard-and-custom-field-groups.png)

## 编辑现有字段组 {#edit}

>[!NOTE]
>
>只能完全编辑和自定义由您的组织定义的自定义字段组。 对于由Adobe定义的核心字段组，只能在单个架构的上下文中编辑其字段的显示名称。 请参阅以下部分 [编辑架构字段的显示名称](./schemas.md#display-names) 以了解详细信息。
>
>保存自定义字段组并在架构中使用它进行数据摄取后，以后只能对字段组进行附加更改。 请参阅 [模式演化规则](../../schema/composition.md#evolution) 以了解更多信息。

要编辑现有字段组，您必须首先打开一个架构，该架构采用 [!DNL Schema Editor]. 您可以 [选择要编辑的现有架构](./schemas.md#edit)，或者您可以 [创建新架构](./schemas.md#create) 并添加相关字段组。

在编辑器中打开架构后，您可以启动 [向字段组添加字段](#add-fields).

## 将字段添加到字段组 {#add-fields}

>[!NOTE]
>
>本节重点介绍如何向自定义字段组添加字段。 有关如何将自定义字段添加到标准字段组的信息，请参阅 [架构UI指南](./schemas.md#custom-fields-for-standard-groups).

要将字段添加到自定义字段组，请从选择 **加(+)** 图标（位于画布中的架构名称旁）。

![](../../images/ui/resources/field-groups/add-field.png)

An **[!UICONTROL 无标题的字段]** 占位符显示在画布中，右边栏更新以显示用于配置字段属性的控件。 请参阅指南，网址为 [在UI中定义字段](../fields/overview.md#define) 有关如何配置不同字段类型的具体步骤。

下 **[!UICONTROL 分配给]**，选择 **[!UICONTROL 字段组]** 选项，然后使用下拉菜单从列表中选择所需的字段组。 您可以开始键入字段组的名称来缩小结果范围。

![](../../images/ui/resources/field-groups/select-field-group.png)

下 **[!UICONTROL 分配给]**，选择 **[!UICONTROL 字段组]** 选项，然后使用下拉菜单从列表中选择所需的字段组。 您可以开始键入字段组的名称来缩小结果范围。

![](../../images/ui/resources/field-groups/select-field-group.png)

将字段添加到架构后，即会将其分配给所选的字段组。 继续向字段组添加所需数量的字段。 完成后，选择 **[!UICONTROL 保存]** 以保存架构和字段组。

![](../../images/ui/resources/field-groups/complete-field-group.png)

如果其他架构中已应用相同的字段组，则新添加的字段将自动出现在这些架构中。

## 后续步骤

本指南介绍了如何使用Platform UI创建和编辑字段组。 欲知关于 [!UICONTROL 架构] 工作区，请参见 [[!UICONTROL 架构] 工作区概述](../overview.md).

要了解如何使用管理字段组 [!DNL Schema Registry] API，请参见 [字段组端点指南](../../api/field-groups.md).

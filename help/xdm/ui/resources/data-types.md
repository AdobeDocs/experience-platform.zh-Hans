---
keywords: Experience Platform；主页；热门主题；UI;XDM;XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；架构注册；架构注册；架构；架构；架构；架构；创建；数据类型；数据类型；
solution: Experience Platform
title: 使用UI创建和编辑数据类型
topic-legacy: tutorial
type: Tutorial
description: 了解如何在Experience Platform用户界面中创建和编辑数据类型。
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 0%

---

# 使用UI创建和编辑数据类型

在体验数据模型(XDM)中，数据类型是包含多个子字段的可重用字段。 尽管与中的架构字段组类似，它们允许一致地使用多字段结构，但数据类型更加灵活，因为它们可以包含在架构结构中的任意位置，而字段组只能在根级别添加。

Adobe Experience Platform提供了许多标准数据类型，可用于涵盖各种常见的体验管理用例。 但是，您还可以定义自己的自定义数据类型，以满足您独特的业务需求。

本教程介绍了在Platform用户界面中创建和编辑自定义数据类型的步骤。

## 先决条件

本指南需要对XDM系统有一定的了解。 请参阅 [XDM概述](../../home.md) 介绍XDM在Experience Platform生态系统中的作用，以及 [架构组合基础知识](../../schema/composition.md) 了解数据类型对XDM模式的贡献情况。

虽然本指南不是必需的，但建议您也要遵循 [在UI中合成架构](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor].

## 打开 [!DNL Schema Editor] （数据类型）

在平台UI中，选择 **[!UICONTROL 模式]** 在左侧导航中打开 [!UICONTROL 模式] 工作区，然后选择 **[!UICONTROL 数据类型]** 选项卡。 此时会显示可用数据类型的列表，包括由Adobe定义的数据类型和由您的组织创建的数据类型。

![](../../images/ui/resources/data-types/data-types-tab.png)

从此处，您有两个选项：

- [创建新数据类型](#create)
- [选择要编辑的现有数据类型](#edit)

### 创建新数据类型 {#create}

从 **[!UICONTROL 数据类型]** 选项卡，选择 **[!UICONTROL 创建数据类型]**.

![](../../images/ui/resources/data-types/create.png)

的 [!DNL Schema Editor] 显示画布中新数据类型的当前结构。 在编辑器的右侧，您可以为数据类型提供显示名称和可选描述。 确保您为数据类型提供了唯一且简洁的名称，因为这是在将数据类型添加到架构时如何标识该数据类型的。

本教程将创建一个描述餐厅属性的数据类型，因此该数据类型的显示名称为“Restaurant”。

![](../../images/ui/resources/data-types/data-type-properties.png)

从此处，您可以跳到 [下一部分](#add-fields) 开始向新数据类型添加字段。

### 编辑现有数据类型

>[!NOTE]
>
>在已启用用于实时客户资料的架构中使用现有数据类型后，以后只能对该数据类型进行无损更改。 请参阅 [模式演化规则](../../schema/composition.md#evolution) 以了解更多信息。

只能编辑您的组织定义的自定义数据类型。 要缩小显示的列表范围，请选择过滤器图标(![过滤器图标](../../images/ui/resources/data-types/filter.png))以显示根据 [!UICONTROL 所有者]. 选择 **[!UICONTROL 客户]** 以仅显示您的组织拥有的自定义数据类型。

从列表中选择要编辑的数据类型以打开右边栏，其中显示数据类型的详细信息。 在右边栏中选择数据类型的名称，以在 [!DNL Schema Editor].

![](../../images/ui/resources/data-types/edit.png)

## 向数据类型添加字段 {#add-fields}

要开始向数据类型添加字段，请选择 **加号(+)** 图标。 下面将显示一个新字段，右边栏会更新以显示新字段的控件。

![](../../images/ui/resources/data-types/new-field.png)

使用右边栏中的控件配置新字段的详细信息。 请参阅 [在UI中定义字段](../fields/overview.md#define) 以了解有关如何配置字段并将其添加到数据类型的特定步骤。

餐厅数据类型需要一个字符串字段来表示餐厅的名称。 因此， [!UICONTROL 字段名称] 设置为“name”，则 [!UICONTROL 类型] 设置为&quot;[!UICONTROL 字符串]&quot; 选择 **[!UICONTROL 应用]** 以将更改应用到字段。

![](../../images/ui/resources/data-types/name-field.png)

根据需要继续向数据类型添加更多字段。 “餐厅”数据类型示例现在包含品牌、座位容量和楼面空间的附加字段。

![](../../images/ui/resources/data-types/more-fields.png)

除了基本字段之外，您还可以在自定义数据类型中嵌套其他数据类型。 例如，Restaurant数据类型需要一个表示属性物理地址的字段。 在此方案中，您可以添加一个新的“地址”字段，该字段已分配标准数据类型“[!UICONTROL 邮政地址]&quot;

![](../../images/ui/resources/data-types/address-field.png)

这显示了在描述数据方面数据类型的灵活性：数据类型可以采用也是数据类型的字段，这些字段本身可以包含其他数据类型，等等。 这样，您就可以在整个XDM架构中提取和重用通用数据模式，从而更轻松地表示复杂的数据结构。

完成向数据类型添加字段后，请选择 **[!UICONTROL 保存]** 保存更改并将数据类型添加到 [!DNL Schema Library].

## 将数据类型添加到类或字段组

创建数据类型后，即可在架构中开始使用该数据类型。 由于XDM架构由类和零个或多个字段组组成，因此不能直接将数据类型提供的字段添加到架构中。 而是必须包含在类或字段组中。

首先，执行 [向类添加字段](./classes.md#add-fields) 或 [向字段组添加字段](./field-groups.md#add-fields). 当您选择 **[!UICONTROL 类型]** 对于新字段，从下拉菜单中选择数据类型的名称。

## 将多字段对象转换为数据类型 {#convert}

在 [!DNL Schema Editor]，则可以将该字段转换为数据类型，以便在其他类或字段组中使用该相同字段结构。

要将对象类型字段转换为数据类型，请在画布中选择该字段。 在转换字段之前，请确保 **[!UICONTROL 显示名称]** 描述对象将包含的数据，因为这将成为数据类型的名称。 准备好转换字段后，选择 **[!UICONTROL 转换为新数据类型]** 中。

![](../../images/ui/resources/data-types/convert-object.png)

画布会从“[!UICONTROL 对象]”更改为新数据类型。 子字段旁边还有一些小的锁图标，表示它们不再是单个字段，而是多字段数据类型的一部分。 现在，通过从 **[!UICONTROL 类型]** 下拉列表。

![](../../images/ui/resources/data-types/converted.png)

## 后续步骤

本指南介绍了如何使用平台UI创建和编辑数据类型。 有关 [!UICONTROL 模式] 工作区，请参阅 [[!UICONTROL 模式] 工作区概述](../overview.md).

了解如何使用 [!DNL Schema Registry] API，请参阅 [data types endpoint指南](../../api/data-types.md).

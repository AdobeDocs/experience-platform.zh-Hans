---
keywords: Experience Platform；主页；热门主题；ui；XDM；XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；架构注册表；架构注册表；架构；架构；架构；架构；创建；数据类型；数据类型；
solution: Experience Platform
title: 使用UI创建和编辑数据类型
type: Tutorial
description: 了解如何在Experience Platform用户界面中创建和编辑数据类型。
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 6%

---

# 使用 UI 创建和编辑数据类型 {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_datatype_filter"
>title="标准或自定义数据类型过滤器"
>abstract="根据如何创建可用的数据类型预先过滤可用的数据类型的列表。选中单选按钮可在“标准”与“自定义”选项之间选择。“标准”选项显示由 Adobe 创建的实体，而“自定义”选项显示在您的组织内创建的实体。请参阅文档以详细了解创建和编辑数据类型。"

在Experience Data Model (XDM)中，数据类型是包含多个子字段的可重用字段。 虽然与架构字段组类似，因为它们允许一致地使用多字段结构，但数据类型更灵活，因为它们可以包含在架构结构中的任意位置，而字段组只能在根级别添加。

Adobe Experience Platform提供了许多标准数据类型，可用于涵盖各种常见的体验管理用例。 但是，您还可以定义自己的自定义数据类型，以满足独特的业务需求。

>[!NOTE]
>
>如果字段被定义为特定数据类型，则无法在另一个架构中创建具有不同数据类型的相同字段。 此限制适用于您组织的租户。

本教程介绍了在Experience Platform用户界面中创建和编辑自定义数据类型的步骤。

## 先决条件 {#prerequisites}

本指南要求您对XDM系统有一定的了解。 请参阅[XDM概述](../../home.md)，了解XDM在Experience Platform生态系统中的角色简介，以及架构组合的[基础知识](../../schema/composition.md)，了解数据类型对XDM架构的贡献。

虽然本指南并非必需，但建议您也学习有关[在UI](../../tutorials/create-schema-ui.md)中撰写架构的教程，以熟悉[!DNL Schema Editor]的各种功能。

## 为数据类型打开[!DNL Schema Editor] {#data-type}

在Experience Platform UI中，在左侧导航中选择&#x200B;**[!UICONTROL 架构]**&#x200B;以打开[!UICONTROL 架构]工作区，然后选择&#x200B;**[!UICONTROL 数据类型]**&#x200B;选项卡。 此时将显示可用数据类型的列表。 系统会根据数据类型的创建方式自动筛选数据类型列表。 默认设置显示由Adobe定义的数据类型。 您还可以筛选列表以显示您的组织创建的那些列表。

![左侧导航中带有[!UICONTROL 架构]且突出显示[!UICONTROL 数据类型]的[!UICONTROL 架构]工作区。](../../images/ui/resources/data-types/data-types-tab.png)

在此处，您可以选择以下选项：

- [创建新数据类型](#create)
- [筛选数据类型](#filter)
- [选择要编辑的现有数据类型](#edit)

### 创建新数据类型 {#create}

从&#x200B;**[!UICONTROL 数据类型]**&#x200B;选项卡中，选择&#x200B;**[!UICONTROL 创建数据类型]**。

![突出显示了[!UICONTROL 架构]工作区[!UICONTROL 数据类型]选项卡（带有[!UICONTROL 创建数据类型]）。](../../images/ui/resources/data-types/create.png)

此时将显示[!DNL Schema Editor]，显示画布中新数据类型的当前结构。 在编辑器的右侧，您可以为数据类型提供显示名称和可选描述。 请确保为数据类型提供唯一且简洁的名称，以将其添加到架构时采用的方式进行识别。

本教程将创建一个用于描述餐厅属性的数据类型，因此该数据类型的显示名称为“Restaurant”。

![](../../images/ui/resources/data-types/data-type-properties.png)

从此处，您可以跳到[下一部分](#add-fields)以开始向新数据类型添加字段。

### 筛选数据类型 {#filter}

根据如何创建可用的数据类型预先过滤可用的数据类型的列表。选择单选按钮以在[!UICONTROL 标准]和[!UICONTROL 自定义]选项之间进行选择。 [!UICONTROL Standard]选项显示Adobe创建的实体，[!UICONTROL Custom]选项显示组织内创建的实体。

![已突出显示[!UICONTROL 架构]工作区的[!UICONTROL 数据类型]选项卡，其中包含[!UICONTROL 标准]和[!UICONTROL 自定义]。](../../images/ui/resources/data-types/standard-and-custom-data-types.png)

### 编辑现有数据类型 {#edit}

>[!NOTE]
>
>在启用了实时客户档案的架构中使用现有数据类型后，此后只能对该数据类型进行非破坏性更改。 有关详细信息，请参阅架构演变[规则](../../schema/composition.md#evolution)。

只能编辑由您的组织定义的自定义数据类型。 选择&#x200B;**[!UICONTROL 自定义]**&#x200B;以仅显示您的组织拥有的自定义数据类型。

从列表中选择要编辑的数据类型以打开右边栏，显示数据类型的详细信息。 您还可以从详细信息面板下载样例文件、复制JSON结构或将数据类型添加到包中。

在右边栏中选择数据类型的名称，以在[!DNL Schema Editor]中打开其结构。

![已突出显示[!UICONTROL 架构]工作区的[!UICONTROL 数据类型]选项卡，该选项卡的数据类型为[!UICONTROL 自定义]和数据类型[!UICONTROL 名称]。](../../images/ui/resources/data-types/edit.png)

## 向数据类型添加字段 {#add-fields}

要开始向数据类型添加字段，请选择画布中根级别字段旁边的&#x200B;**加号(+)**&#x200B;图标。 下面将显示一个新字段，右边栏将更新以显示该新字段的控件。

![](../../images/ui/resources/data-types/new-field.png)

使用右边栏中的控件配置新字段的详细信息。 有关如何配置字段并将其添加到数据类型的具体步骤，请参阅[在UI](../fields/overview.md#define)中定义字段的指南。

Restaurant数据类型需要一个字符串字段来表示餐厅的名称。 因此，[!UICONTROL 字段名称]设置为“name”，[!UICONTROL 类型]设置为“[!UICONTROL String]”。 选择&#x200B;**[!UICONTROL 应用]**&#x200B;以将更改应用到字段。

![](../../images/ui/resources/data-types/name-field.png)

根据需要继续向数据类型添加更多字段。 示例Restaurant数据类型现在具有额外的品牌、座位容量和占地面积字段。

![](../../images/ui/resources/data-types/more-fields.png)

除了基本字段之外，您还可以将其他数据类型嵌套在自定义数据类型中。 例如，Restaurant数据类型需要一个表示资产的物理地址的字段。 在此方案中，您可以添加新的“地址”字段，该字段被分配了标准数据类型“[!UICONTROL 邮政地址]”。

![](../../images/ui/resources/data-types/address-field.png)

这说明了数据类型在描述数据方面可以有多灵活：数据类型可以应用字段，这些字段也是数据类型，本身可以包含更多数据类型，等等。 这允许您在XDM架构中抽象和重用常见数据模式，使其更易于表示复杂的数据结构。

完成向数据类型添加字段后，选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更改并将数据类型添加到[!DNL Schema Library]。

## 将数据类型添加到架构 {#add-data-type}

创建数据类型后，即可开始在架构中使用它。 由于XDM架构由一个类以及零个或多个字段组组成，因此数据类型提供的字段无法直接添加到架构中。 相反，它们必须包含在类或字段组中。

首先执行[将字段添加到类](./classes.md#add-fields)或[将字段添加到字段组](./field-groups.md#add-fields)所涉及的步骤。 或者，您可以开始[将字段直接添加到架构](./schemas.md#add-individual-fields)，然后从中选择父类或字段组。 为新字段选择&#x200B;**[!UICONTROL 类型]**&#x200B;时，请从下拉菜单中选择数据类型的名称。

## 将多字段对象转换为数据类型 {#convert}

当您在[!DNL Schema Editor]中创建具有多个子字段的对象类型字段时，可以将该字段转换为数据类型，以便在不同的类或字段组中使用相同的字段结构。

要将对象类型字段转换为数据类型，请在画布中选择该字段。 在转换字段之前，请确保&#x200B;**[!UICONTROL 显示名称]**&#x200B;描述对象将包含的数据，因为这将成为数据类型的名称。 准备转换字段时，在右边栏中选择&#x200B;**[!UICONTROL 转换为新数据类型]**。

![](../../images/ui/resources/data-types/convert-object.png)

画布将字段的数据类型从“[!UICONTROL 对象]”更新为新数据类型。 通过定义新字段时从&#x200B;**[!UICONTROL 类型]**&#x200B;下拉列表中选择此数据类型，此结构现在可以在其他类和字段组中重复使用。

![](../../images/ui/resources/data-types/converted.png)

## 后续步骤 {#next-steps}

本指南介绍了如何使用Experience Platform UI创建和编辑数据类型。 有关[!UICONTROL 架构]工作区的功能的更多信息，请参阅[[!UICONTROL 架构]工作区概述](../overview.md)。

要了解如何使用[!DNL Schema Registry] API管理数据类型，请参阅[数据类型端点指南](../../api/data-types.md)。

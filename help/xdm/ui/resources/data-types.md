---
keywords: Experience Platform；主题；热门主题；ui;XDM;XDM系统；体验数据模型；体验数据模型；数据模型；模式注册；模式注册；模式;模式;模式;模式；创建；数据类型；数据类型；
solution: Experience Platform
title: 使用UI创建和编辑数据类型
topic-legacy: tutorial
type: Tutorial
description: 了解如何在Experience Platform用户界面中创建和编辑数据类型。
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 0%

---

# 使用UI创建和编辑数据类型

在体验模式模型(XDM)中，数据类型与基本文本字段一样用作类或数据字段组中的引用类型字段，关键区别在于数据类型可以定义多个子字段。 虽然与字段组中允许一致使用多字段结构的字段组类似，但数据类型更灵活，因为它们可以包含在模式结构中的任意位置，而字段组只能添加在根级别。

Adobe Experience Platform提供许多标准数据类型，可用于涵盖各种常见体验管理用例。 但是，您也可以定义自己的自定义数据类型以满足您独特的业务需求。

本教程介绍在平台用户界面中创建和编辑自定义数据类型的步骤。

## 先决条件

本指南要求对XDM系统有充分的了解。 有关Experience Platform生态系统中XDM角色的介绍，请参阅[XDM概述](../../home.md)，以及[模式合成基础知识](../../schema/composition.md)，了解数据类型对XDM模式的贡献。

虽然本指南不是必需的，但建议您也要按照有关在UI](../../tutorials/create-schema-ui.md)中编写模式的教程来熟悉[!DNL Schema Editor]的各种功能。[

## 打开[!DNL Schema Editor]数据类型

在平台UI中，选择左侧导航中的&#x200B;**[!UICONTROL Schemas]**&#x200B;以打开[!UICONTROL Schemas]工作区，然后选择&#x200B;**[!UICONTROL Data types]**&#x200B;选项卡。 将显示可用列表类型，包括由Adobe定义的数据类型以及由您的组织创建的数据类型。

![](../../images/ui/resources/data-types/data-types-tab.png)

从此处，您有两个选择：

- [创建新数据类型](#create)
- [选择要编辑的现有数据类型](#edit)

### 创建新数据类型{#create}

从&#x200B;**[!UICONTROL Data types]**&#x200B;选项卡中，选择&#x200B;**[!UICONTROL Create data type]**。

![](../../images/ui/resources/data-types/create.png)

出现[!DNL Schema Editor]，显示画布中新数据类型的当前结构。 在编辑器的右侧，您可以为数据类型提供显示名称和可选说明。 确保为您的数据类型提供唯一、简洁的名称，在将数据类型添加到模式时，将如此标识它。

本教程创建一个描述餐馆属性的数据类型，因此数据类型的显示名称为“Restaurant”。

![](../../images/ui/resources/data-types/data-type-properties.png)

从此处，您可以跳到[下一节](#add-fields)以开始向新数据类型添加字段。

### 编辑现有数据类型

只能编辑您的单位定义的自定义数据类型。 要缩小显示的列表，请选择过滤器图标（![过滤器图标](../../images/ui/resources/data-types/filter.png)）以显示用于基于[!UICONTROL Owner]进行过滤的控件。 选择&#x200B;**[!UICONTROL Customer]**&#x200B;以仅显示您的组织拥有的自定义数据类型。

从列表中选择要编辑的数据类型以打开右边栏，其中显示了数据类型的详细信息。 在右边栏中选择数据类型的名称，以在[!DNL Schema Editor]中打开其结构。

![](../../images/ui/resources/data-types/edit.png)

## 向数据类型{#add-fields}添加字段

要开始向数据类型添加字段，请选择画布中根级字段旁边的加号(+)**图标。**&#x200B;下面将显示一个新字段，右边栏将更新以显示新字段的控件。

![](../../images/ui/resources/data-types/new-field.png)

使用右边栏中的控件配置新字段的详细信息。 有关如何配置字段并将其添加到数据类型的具体步骤，请参阅[在UI](../fields/overview.md#define)中定义字段的指南。

Restaurant数据类型需要一个字符串字段来表示餐馆的名称。 因此，[!UICONTROL Field name]设置为“name”，[!UICONTROL Type]设置为“[!UICONTROL String]”。 选择&#x200B;**[!UICONTROL Apply]**&#x200B;以将更改应用到字段。

![](../../images/ui/resources/data-types/name-field.png)

根据需要继续向数据类型添加更多字段。 Restaurant数据类型示例现在包含品牌、座位容量和楼面空间的其他字段。

![](../../images/ui/resources/data-types/more-fields.png)

除了基本字段之外，您还可以在自定义数据类型中嵌套其他数据类型。 例如，“餐厅”数据类型需要一个表示属性物理地址的字段。 在此方案中，您可以添加新的“地址”字段，该字段分配了标准数据类型“[!UICONTROL Postal address]”。

![](../../images/ui/resources/data-types/address-field.png)

这说明了在描述数据时数据类型的灵活性：数据类型可以采用也是数据类型的字段，这些字段本身可以包含更多数据类型，等等。 这使您能够抽象和重用整个XDM模式中的常见数据模式，从而更轻松地呈现复杂的数据结构。

将字段添加完数据类型后，选择&#x200B;**[!UICONTROL Save]**&#x200B;以保存更改并将数据类型添加到[!DNL Schema Library]。

## 将数据类型添加到类或字段组

创建数据类型后，即可在模式中使用它。 由于XDM模式由类和零个或多个字段组组成，因此不能将数据类型提供的字段直接添加到模式。 而必须将它们包含在类或字段组中。

开始，方法是按照将字段添加到类](./classes.md#add-fields)或[添加字段到字段组](./field-groups.md#add-fields)中涉及的步骤进行操作。 [为新字段选择&#x200B;**[!UICONTROL Type]**&#x200B;时，请从下拉菜单中选择数据类型的名称。

## 将多字段对象转换为数据类型{#convert}

在[!DNL Schema Editor]中创建具有多个子字段的对象类型字段时，可以将该字段转换为数据类型，以便在其他类或字段组中使用相同的字段结构。

要将对象类型字段转换为数据类型，请在画布中选择该字段。 在转换字段之前，请确保&#x200B;**[!UICONTROL Display name]**&#x200B;描述对象将包含的数据，因为这将成为数据类型的名称。 准备好转换字段时，请选择右边栏中的&#x200B;**[!UICONTROL Convert to new data type]**。

![](../../images/ui/resources/data-types/convert-object.png)

画布将字段的数据类型从“[!UICONTROL Object]”更新为新数据类型。 子字段旁边还有小的锁图标，表示它们不再是单个字段，而是多字段数据类型的一部分。 现在，在定义新字段时，可以从&#x200B;**[!UICONTROL Type]**&#x200B;下拉列表中选择此数据类型，即可在其他类和字段组中重复使用此结构。

![](../../images/ui/resources/data-types/converted.png)

## 后续步骤

本指南介绍了如何使用平台用户界面创建和编辑数据类型。 有关[!UICONTROL Schemas]工作区功能的详细信息，请参阅[[!UICONTROL Schemas]工作区概述](../overview.md)。

要了解如何使用[!DNL Schema Registry] API管理数据类型，请参阅[数据类型终结点指南](../../api/data-types.md)。

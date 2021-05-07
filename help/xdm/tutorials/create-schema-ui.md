---
keywords: Experience Platform；主页；热门主题；ui;UI;XDM;XDM系统；体验数据模型；体验数据模型；数据模型；模式编辑器；模式编辑器；模式;模式;模式;模式；创建
solution: Experience Platform
title: 使用模式编辑器创建模式
topic-legacy: tutorial
type: Tutorial
description: 本教程介绍了在 Experience Platform 中使用模式编辑器创建模式的步骤。
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '3588'
ht-degree: 0%

---

# 使用[!DNL Schema Editor]创建模式

Adobe Experience Platform用户界面允许您在称为[!DNL Schema Editor]的交互式可视画布中创建和管理[!DNL Experience Data Model](XDM)模式。 本教程介绍如何使用[!DNL Schema Editor]创建模式。

>[!NOTE]
>
>出于演示目的，本教程中的步骤包括创建一个描述客户忠诚度项目成员的示例模式。 虽然您可以使用这些步骤为自己创建不同的模式，但建议您首先创建示例模式，以了解[!DNL Schema Editor]的功能。

如果您希望使用[!DNL Schema Registry] API编写模式，请先阅读[[!DNL Schema Registry] 开发人员指南](../api/getting-started.md)，然后尝试使用[创建模式时的教程](create-schema-api.md)。

## 入门指南

本教程要求对Adobe Experience Platform在创建模式时涉及的各个方面有充分的了解。 在开始本教程之前，请查阅以下概念的文档：

* [[!DNL Experience Data Model (XDM)]](../home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。
   * [模式合成的基础](../schema/composition.md):XDM模式及其构建块的概述，包括类、模式字段组、数据类型和单个字段。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

## 打开[!UICONTROL Schemas]工作区{#browse}

[!DNL Platform] UI中的[!UICONTROL Schemas]工作区提供了[!DNL Schema Library]的可视化，允许您视图管理组织可用的模式。 工作区还包括[!DNL Schema Editor]，在本教程中，您可以在该画布上构建模式。

登录[!DNL Experience Platform]后，在左侧导航中选择&#x200B;**[!UICONTROL Schemas]**&#x200B;以打开&#x200B;**[!UICONTROL Schemas]**&#x200B;工作区。 **[!UICONTROL Browse]**&#x200B;选项卡显示一列表模式（[!DNL Schema Library]的表示形式），您可以对其进行视图和自定义。 列表包括模式所基于的名称、类型、类和行为（记录或时间序列），以及模式上次修改的日期和时间。

有关详细信息，请参阅[探索UI](../ui/explore.md)中现有XDM资源的指南。

## 创建模式并命名{#create}

要开始合成模式，请选择&#x200B;**[!UICONTROL Schemas]**&#x200B;工作区右上角的&#x200B;**[!UICONTROL Create schema]**。 此时将显示一个下拉菜单，提供在核心类[!UICONTROL XDM Individual Profile]和[!UICONTROL XDM ExperienceEvent]之间进行选择的选项。 如果这些类不适合您的用途，您还可以选择&#x200B;**[!UICONTROL Browse]**&#x200B;从其他可用类中进行选择，或者[创建新类](#create-new-class)。

为本教程的目的，请选择&#x200B;**[!UICONTROL XDM Individual Profile]**。

![](../images/tutorials/create-schema/create_schema_button.png)

由于您选择了标准XDM类作为模式的基础，因此将显示&#x200B;**[!UICONTROL Add field group]**&#x200B;对话框，允许您立即开始向模式添加字段。 现在，选择&#x200B;**[!UICONTROL Cancel]**&#x200B;退出对话框。

![](../images/tutorials/create-schema/cancel-field-group.png)

出现[!DNL Schema Editor]。 这是您将在其上合成模式的画布。 当您到达编辑器时，未命名的模式将自动在画布的&#x200B;**[!UICONTROL Structure]**&#x200B;部分中创建，并基于该类在所有模式中包含的标准字段。 **[!UICONTROL Composition]**&#x200B;部分的&#x200B;**[!UICONTROL Class]**&#x200B;下还列出了模式的已分配类。

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>在保存模式之前，您可以在初始合成过程中的任何时间点[更改模式](#change-class)的类，但应非常小心。 字段组仅与某些类兼容，因此更改类将重置画布和您添加的任何字段。

使用编辑器右侧的字段为模式提供显示名称和可选说明。 输入名称后，画布会随之更新，以反映模式的新名称。

![](../images/tutorials/create-schema/name_schema.png)

在为模式确定名称时，需要考虑以下几个重要事项：

* 模式名称应简短且描述性，以便以后可以轻松找到模式。
* 模式名称必须是唯一的，这意味着它还应足够具体，以便将来不再重用它。 例如，如果您的组织有针对不同品牌的不同忠诚度项目，则最好将您的模式命名为“Brand A Loyalty Members”，以便与您稍后可能定义的其他与忠诚度相关的模式轻松区分。
* 您还可以使用模式描述来提供有关模式的任何其他上下文信息。

本教程组成一个模式，用于收集与忠诚度项目成员相关的数据，因此该模式名为“忠诚度成员”。

## 添加字段组{#field-group}

您现在可以通过添加字段组开始向模式添加字段。 字段组是一个或多个字段的组，这些字段通常一起用于描述特定概念。 本教程使用字段组描述忠诚度项目的成员并捕获关键信息，如姓名、生日、电话号码、地址等。

要添加字段组，请在&#x200B;**[!UICONTROL Field groups]**&#x200B;子部分中选择&#x200B;**[!UICONTROL Add]**。

![](../images/tutorials/create-schema/add-field-group-button.png)

此时将显示新对话框，显示可用字段组的列表。 每个字段组仅用于特定类，因此对话框仅列表与所选类（本例中为[!DNL XDM Individual Profile]类）兼容的字段组。 如果您使用标准XDM类，则将根据使用人气智能地对字段组的列表进行排序。

![](../images/tutorials/create-schema/field-group-popularity.png)

从列表中选择字段组会使其显示在右侧边栏中。 您可以根据需要选择多个字段组，在确认之前将每个字段组添加到右侧边栏中的列表。 此外，当前选定字段组的右侧会显示一个图标，通过该图标可预览其提供的字段的结构。

![](../images/tutorials/create-schema/preview-field-group-button.png)

预览字段组时，右侧边栏中会提供字段组模式的详细说明。 您还可以在提供的画布中浏览字段组的字段。 当您选择不同的字段时，右侧边栏会更新，以显示有关该字段的详细信息。 预览完毕后，选择&#x200B;**[!UICONTROL Back]**&#x200B;以返回到字段组选择对话框。

![](../images/tutorials/create-schema/preview-field-group.png)

对于本教程，选择&#x200B;**[!UICONTROL Demographic Details]**&#x200B;字段组，然后选择&#x200B;**[!UICONTROL Add field group]**。

![](../images/tutorials/create-schema/demographic-details.png)

将重新显示模式画布。 **[!UICONTROL Field groups]**&#x200B;部分现在列表“[!UICONTROL Demographic Details]”，而&#x200B;**[!UICONTROL Structure]**&#x200B;部分包含字段组提供的字段。 您可以在&#x200B;**[!UICONTROL Field groups]**&#x200B;部分下选择字段组的名称，以突出显示它在画布中提供的特定字段。

![](../images/tutorials/create-schema/demographic-details-structure.png)

此字段组在顶级名称`person`下提供数据类型为“[!UICONTROL Person]”的多个字段。 这组字段描述有关个人的信息，包括姓名、出生日期和性别。

>[!NOTE]
>
>请记住，字段可能使用标量类型（如字符串、整数、数组或日期）以及[!DNL Schema Registry]中定义的任何数据类型（表示通用概念的一组字段）。

请注意，`name`字段的数据类型为“[!UICONTROL Person name]”，这意味着它也描述了通用概念，并包含与名称相关的子字段，如名、姓、名、字幕和后缀。

在画布中选择不同的字段，以显示它们贡献到模式结构的任何其他字段。

## 添加另一个字段组{#field-group-2}

您现在可以重复相同步骤以添加另一个字段组。 当您此次视图&#x200B;**[!UICONTROL Add field group]**&#x200B;对话框时，请注意，“[!UICONTROL Demographic Details]”字段组已灰显，并且其旁边的复选框无法选中。 这可防止您意外复制当前模式中已包含的字段组。

对于本教程，从对话框中选择“[!DNL Personal Contact Details]”字段组，然后选择&#x200B;**[!UICONTROL Add field group]**&#x200B;将其添加到模式。

![](../images/tutorials/create-schema/personal-contact-details.png)

添加后，画布将重新显示。 “[!UICONTROL Personal Contact Details]”现在列在&#x200B;**[!UICONTROL Composition]**&#x200B;部分的&#x200B;**[!UICONTROL Field groups]**&#x200B;下，**[!UICONTROL Structure]**&#x200B;下添加了有关家庭地址、移动电话等的字段。

与`name`字段类似，您刚添加的字段表示多字段概念。 例如，`homeAddress`的数据类型为“[!UICONTROL Postal address]”，而`mobilePhone`的数据类型为“[!UICONTROL Phone number]”。 您可以选择其中每个字段以展开它们，并查看数据类型中包含的其他字段。

![](../images/tutorials/create-schema/personal-contact-details-structure.png)

## 定义自定义字段组{#define-field-group}

“[!UICONTROL Loyalty Members]”模式用于捕获与忠诚度项目成员相关的数据，因此它需要一些特定的与忠诚度相关的字段。

您可以向模式添加一个标准[!UICONTROL Loyalty Details]字段组，以捕获与忠诚度项目相关的常用字段。 尽管强烈建议您使用标准字段组来表示模式捕获的概念，但标准忠诚度字段组的结构可能无法捕获特定忠诚度项目的所有相关数据。 在此方案中，您可以选择定义新的自定义字段组来捕获这些字段。

再次打开&#x200B;**[!UICONTROL Add Field group]**&#x200B;对话框，但此次选择顶部附近的&#x200B;**[!UICONTROL Create New Field group]**。 随后会要求您提供字段组的显示名称和说明。

![](../images/tutorials/create-schema/create-new-field-group.png)

与类名一样，字段组名称应简短，用于描述字段组将对模式的贡献。 这些名称也是唯一的，因此您将无法重用该名称，因此必须确保其足够具体。

在本教程中，将新字段组命名为“忠诚度详细信息”。

选择&#x200B;**[!UICONTROL Add field group]**&#x200B;以返回到[!DNL Schema Editor]。 “[!UICONTROL Loyalty Details]”现在应显示在画布左侧的&#x200B;**[!UICONTROL Field groups]**&#x200B;下，但还没有与其关联的字段，因此在&#x200B;**[!UICONTROL Structure]**&#x200B;下面没有新字段。

## 将字段添加到字段组{#field-group-fields}

现在您已创建“忠诚度详细信息”字段组，现在应该定义字段组将贡献给模式的字段。

要开始，请在&#x200B;**[!UICONTROL Field groups]**&#x200B;部分选择字段组名称。 执行此操作后，字段组的属性显示在编辑器的右侧，并且&#x200B;**[!UICONTROL Structure]**&#x200B;下模式名称旁边将显示一个&#x200B;**加号(+)**&#x200B;图标。

![](../images/tutorials/create-schema/loyalty_details_structure.png)

选择“[!DNL Loyalty Members]”旁边的&#x200B;**加号(+)**&#x200B;图标以在结构中创建新节点。 此节点（在此示例中称为`_tenantId`）表示您的IMS组织的租户ID，前面加下划线。 租户ID的存在表示您正在添加的字段包含在您组织的命名空间中。

换句话说，您添加的字段对您的组织而言是唯一的，将保存在[!DNL Schema Registry]中仅对您的组织可访问的特定区域。 您定义的字段必须始终添加到您的租户命名空间中，以防止与来自其他标准类、字段组、数据类型和字段的名称发生冲突。

在该命名空间节点中是“[!UICONTROL New Field]”。 这是“[!UICONTROL Loyalty Details]”字段组的开头。

![](../images/tutorials/create-schema/new_field_loyalty.png)

使用编辑器右侧的控件，通过创建类型为“[!UICONTROL Object]”的`loyalty`字段来开始，该字段将用于保存您的忠诚度相关字段。 完成后，选择&#x200B;**[!UICONTROL Apply]**。

![](../images/tutorials/create-schema/loyalty_object.png)

将应用更改，并显示新创建的`loyalty`对象。 选择对象旁边的&#x200B;**加号(+)**&#x200B;图标以添加其他与忠诚度相关的字段。 画布的右侧将显示“[!UICONTROL New Field]”和&#x200B;**[!UICONTROL Field properties]**&#x200B;部分。

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

每个字段都需要以下信息：

* **[!UICONTROL Field Name]:** 字段的名称，用驼峰大小写写。示例：loyaltyLevel
* **[!UICONTROL Display Name]:** 以标题大小写写入的字段名称。示例：忠诚度级别
* **[!UICONTROL Type]:** 字段的数据类型。这包括基本标量类型和在[!DNL Schema Registry]中定义的任何数据类型。 示例：[!UICONTROL String]、[!UICONTROL Integer]、[!UICONTROL Boolean]、[!UICONTROL Person]、[!UICONTROL Address]、[!UICONTROL Phone number]等。
* **[!UICONTROL Description]:** 字段的可选描述应包含在内，以句子为例编写，最多包含200个字符。

`Loyalty`对象的第一个字段将是名为`loyaltyId`的字符串。 将新字段的类型设置为“[!UICONTROL String]”时，**[!UICONTROL Field properties]**&#x200B;部分将填充几个用于应用约束的选项，包括默认值、格式和最大长度。

![](../images/tutorials/create-schema/string_constraints.png)

根据所选数据类型，可使用不同的约束选项。 由于`loyaltyId`将是电子邮件地址，请从&#x200B;**[!UICONTROL Format]**&#x200B;下拉菜单中选择“[!UICONTROL email]”。 选择&#x200B;**[!UICONTROL Apply]**&#x200B;以应用您所做的更改。

![](../images/tutorials/create-schema/loyaltyId_field.png)

## 向字段组{#field-group-fields-2}添加更多字段

现在，您已经添加了`loyaltyId`字段，可以添加其他字段来捕获与忠诚度相关的信息，例如：

* 点（整数）
* 会员自（日期）

要将每个字段添加到模式中，请选择`loyalty`对象旁的&#x200B;**加号(+)**&#x200B;图标并填写所需信息。

完成后，Loyalty对象将包含忠诚度ID、积分和成员 — 自的字段。

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## 向字段组{#enum}添加枚举字段

在[!DNL Schema Editor]中定义字段时，可以对基本字段类型应用一些其他选项，以便对字段可包含的数据提供进一步约束。 下表说明了这些约束的用例：

| 约束 | 描述 |
| --- | --- |
| [!UICONTROL Required] | 指示数据获取需要此字段。 在摄取时，任何基于此模式上载到不包含此字段的数据集的数据都将失败。 |
| [!UICONTROL Array] | 指示字段包含一组值，每个值都指定了数据类型。 例如，对数据类型为“[!UICONTROL String]”的字段使用此约束指定该字段将包含字符串数组。 |
| [!UICONTROL Enum] | 指示此字段必须包含可能值的枚举列表中的值之一。 |
| [!UICONTROL Identity] | 指示此字段是标识字段。 本教程](#identity-field)的后面提供了有关标识字段的详细信息。[ |
| [!UICONTROL Relationship] | 虽然可以通过使用模式模式和[!DNL Real-time Customer Profile]推断出合并关系，但这仅适用于共享同一类的模式。 [!UICONTROL Relationship]约束表示此字段引用基于不同类的模式的主标识，这表示两个模式之间的关系。 有关详细信息，请参阅[定义关系](./relationship-ui.md)的教程。 |

>[!NOTE]
>
>所有必填、标识或关系字段都显示在左边栏中，这样您便可以轻松定位这些字段，而不管模式的复杂性如何。
>
>![](../images/tutorials/create-schema/left-rail-special.png)

在本教程中，模式中的[!DNL "loyalty"]对象需要一个新枚举字段来描述客户的“忠诚度级别”，其中该值只能是四个可能选项之一。 要将此字段添加到模式，请选择`loyalty`对象旁边的&#x200B;**加号(+)**&#x200B;图标，并填写&#x200B;**[!UICONTROL Field name]**&#x200B;和&#x200B;**[!UICONTROL Display name]**&#x200B;的必填字段。 对于&#x200B;**[!UICONTROL Type]**，选择“[!UICONTROL String]”。

![](../images/tutorials/create-schema/loyalty-level-type.png)

选择字段类型后，将为其显示其他复选框，包括&#x200B;**[!UICONTROL Array]**、**[!UICONTROL Enum]**&#x200B;和&#x200B;**[!UICONTROL Identity]**&#x200B;的复选框。

选中&#x200B;**[!UICONTROL Enum]**&#x200B;复选框以打开下面的&#x200B;**[!UICONTROL Enum values]**&#x200B;部分。 在此，您可以为每个可接受的忠诚度级别输入&#x200B;**[!UICONTROL Value]**（在camelCase中）和&#x200B;**[!UICONTROL Label]**（在“标题大小写”中输入一个可选的、对读者友好的名称）。

完成所有字段属性后，选择&#x200B;**[!UICONTROL Apply]**&#x200B;以将“[!DNL loyaltyLevel]”字段添加到`loyalty`对象。

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## 将多字段对象转换为数据类型{#datatype}

`loyalty`对象现在包含多个特定于忠诚度的字段，并表示一个在其他模式中可能有用的通用数据结构。 [!DNL Schema Editor]允许您通过将这些对象的结构转换为数据类型来轻松应用可重用的多字段对象。

数据类型允许一致地使用多字段结构，并提供比字段组更灵活的性，因为它们可以在模式中的任意位置使用。 这是通过将字段的&#x200B;**[!UICONTROL Type]**&#x200B;值设置为[!DNL Schema Registry]中定义的任何数据类型来实现的。

要将`loyalty`对象转换为数据类型，请选择&#x200B;**[!UICONTROL Structure]**&#x200B;下的`loyalty`字段，然后选择编辑器右侧&#x200B;**[!UICONTROL Field properties]**&#x200B;下的&#x200B;**[!UICONTROL Convert to new data type]**。 出现绿色快显，确认对象已成功转换。

![](../images/tutorials/create-schema/convert-data-type.png)

现在，当您查看&#x200B;**[!UICONTROL Structure]**&#x200B;下时，您会发现`loyalty`字段的数据类型为“[!DNL Loyalty]”，并且这些字段旁边有小的锁图标，表示它们不再是单个字段，而是多字段数据类型的一部分。

![](../images/tutorials/create-schema/loyalty_data_type.png)

在将来的模式中，您现在可以将字段指定为“[!DNL Loyalty]”类型，并自动包含ID、忠诚度级别、成员自身和积分的字段。

>[!NOTE]
>
>您还可以创建和编辑自定义数据类型，而与编辑模式无关。 有关详细信息，请参阅[创建和编辑数据类型](../ui/resources/data-types.md)的指南。

## 搜索和筛选模式字段

除了基类提供的字段外，您的模式现在还包含多个字段组。 处理较大的模式时，您可以选中左边栏中字段组名称旁边的复选框，以将显示的字段筛选为仅由您感兴趣的字段组提供的字段。

![](../images/tutorials/create-schema/filter-by-field-group.png)

如果您要在模式中查找特定字段，则还可以使用搜索栏按名称筛选显示的字段，而不管这些字段是在哪个字段组下提供的。

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>搜索函数在显示匹配字段时会考虑任何选定的字段组过滤器。 如果搜索查询未显示您期望的结果，您可能需要多次检查您是否未过滤掉任何相关字段组。

## 将模式字段设置为标识字段{#identity-field}

模式提供的标准数据结构可用于在多个源中识别属于同一个人的数据，从而允许不同的下游用例，如分段、报告、数据科学分析等。 要根据个人身份拼接数据，键字段必须标记为适用模式中的[!UICONTROL Identity]字段。

[!DNL Experience Platform] 通过使用中的复选框，可轻松地指示 **[!UICONTROL Identity]** 身份字段 [!DNL Schema Editor]但是，您必须根据数据的性质确定哪个字段是用作标识的最佳候选。

例如，可能有数千个忠诚度项目成员属于相同的“忠诚度级别”，但忠诚度项目的每个成员都有唯一的`loyaltyId`（在本例中为单个成员的电子邮件地址）。 `loyaltyId`是每个成员的唯一标识符这一事实使其成为标识字段的良好候选者，而`loyaltyLevel`则不是。

>[!IMPORTANT]
>
>下面介绍的步骤包括如何向现有模式字段添加标识描述符。 作为在模式本身的结构中定义标识字段的替代方法，您还可以使用`identityMap`字段来包含标识信息。
>
>如果您计划使用`identityMap`，请记住，它将覆盖您直接添加到模式的任何主标识。 有关详细信息，请参阅模式合成指南[基础知识](../schema/composition.md#identityMap)中的`identityMap`部分。

在编辑器的&#x200B;**[!UICONTROL Structure]**&#x200B;部分，选择`loyaltyId`字段，并在&#x200B;**[!UICONTROL Field properties]**&#x200B;下方显示&#x200B;**[!UICONTROL Identity]**&#x200B;复选框。 选中该框和选项，在出现&#x200B;**[!UICONTROL Primary identity]**&#x200B;时设置此值。 也选择此框。

>[!NOTE]
>
>每个模式只能包含一个主标识字段。 将模式字段设置为主标识后，如果您稍后尝试将模式中的其他标识字段设置为主标识，您将收到一条错误消息。

接下来，您必须从下拉菜单中预定义命名空间的列表中提供&#x200B;**[!UICONTROL Identity namespace]**。 由于`loyaltyId`是客户的电子邮件地址，请从下拉菜单中选择“[!UICONTROL Email]”。 选择&#x200B;**[!UICONTROL Apply]**&#x200B;以确认对`loyaltyId`字段的更新。

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>有关标准命名空间及其定义的列表，请参阅[[!DNL Identity Service] 文档](../../identity-service/troubleshooting-guide.md#standard-namespaces)。

应用更改后，`loyaltyId`的图标会显示指纹符号，指示它现在是标识字段。

![](../images/tutorials/create-schema/identity-applied.png)

现在，收录到`loyaltyId`字段中的所有数据都将用于帮助识别该个人，并将该客户的单个视图拼接在一起。 要了解有关在[!DNL Experience Platform]中使用身份的更多信息，请查阅[[!DNL Identity Service]](../../identity-service/home.md)文档。

## 启用模式以在[!DNL Real-time Customer Profile] {#profile}中使用

[[!DNL Real-time Customer Profile]](../../profile/home.md) 利用身份数据 [!DNL Experience Platform] 为每位客户提供整体视图。该服务构建了360°用户档案的客户属性以及客户在与[!DNL Experience Platform]集成的任何系统中拥有的每个交互的时间戳帐户。

要使模式能够与[!DNL Real-time Customer Profile]一起使用，必须定义主标识。 如果您尝试在未先定义主标识的情况下启用模式，将收到错误消息。

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

要启用[!DNL Profile]中的“Loyalty Members”模式，请首先在编辑器的&#x200B;**[!UICONTROL Structure]**&#x200B;部分选择“[!DNL Loyalty Members]”。

在编辑器的右侧，将显示有关模式的信息，包括其显示名称、说明和类型。 除此信息外，还有一个&#x200B;**[!UICONTROL Profile]**&#x200B;切换按钮。

![](../images/tutorials/create-schema/profile-toggle.png)

选择&#x200B;**[!UICONTROL Profile]**&#x200B;并出现一个快显窗口，要求您确认是否要为[!DNL Profile]启用模式。

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>为[!DNL Real-time Customer Profile]启用模式并保存后，便无法禁用它。

选择&#x200B;**[!UICONTROL Enable]**&#x200B;以确认您的选择。 您可以根据需要再次选择&#x200B;**[!UICONTROL Profile]**&#x200B;切换键以禁用模式，但在[!DNL Profile]启用时保存模式后，便无法再禁用它。

## 后续步骤和其他资源

现在，您已完成模式的编写，您可以在画布中看到完整的模式。 选择&#x200B;**[!UICONTROL Save]**,模式将保存到[!DNL Schema Library]中，使[!DNL Schema Registry]可访问。

您的新模式现在可用于将数据收录到[!DNL Platform]中。 请记住，一旦使用模式收录数据，只能进行附加更改。 有关模式版本控制的详细信息，请参阅[模式合成基础知识](../schema/composition.md)。

您现在可以按照上的教程定义UI](./relationship-ui.md)中的模式关系，在“Loyalty Members”模式中添加新关系字段。[

还可以使用[!DNL Schema Registry] API查看和管理“Loyalty Members”模式。 要开始使用API，请阅读[[!DNL Schema Registry API] 开发人员指南](../api/getting-started.md)进行开始。

### 视频资源

>[!WARNING]
>
>以下视频中显示的[!DNL Platform] UI已过时。 有关最新的UI屏幕截图和功能，请参阅上述文档。

以下视频演示如何在[!DNL Platform] UI中创建简单模式。

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

以下视频旨在加深您对使用字段组和类的理解。

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## 附录

以下各节提供了有关使用[!DNL Schema Editor]的附加信息。

### 创建新类{#create-new-class}

[!DNL Experience Platform] 提供了根据组织特有的类定义模式的灵活性。要了解如何创建新类，请参阅有关在UI](../ui/resources/classes.md#create)中创建和编辑类的指南。[

### 更改模式{#change-class}的类

在保存模式之前，您可以在初始合成过程中的任意点更改模式的类。

>[!WARNING]
>
>重新分配模式的类应非常谨慎。 字段组仅与某些类兼容，因此更改类将重置画布和您添加的任何字段。

要了解如何更改模式的类，请参阅有关在UI](../ui/resources/schemas.md)中管理模式的指南。[

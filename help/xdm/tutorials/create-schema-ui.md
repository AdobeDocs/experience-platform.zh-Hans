---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: 使用模式编辑器创建模式 (schema)
topic: tutorial
type: Tutorial
description: 本教程介绍了在 Experience Platform 中使用模式编辑器创建模式的步骤。
translation-type: tm+mt
source-git-commit: e5c5fea783aa4088d225f771905fa8b2098613cf
workflow-type: tm+mt
source-wordcount: '3568'
ht-degree: 0%

---


# 使用[!DNL Schema Editor]创建模式

Adobe Experience Platform用户界面允许您在称为[!DNL Schema Editor]的交互式可视画布中创建和管理[!DNL Experience Data Model](XDM)模式。 本教程介绍如何使用[!DNL Schema Editor]创建模式。

>[!NOTE]
>
>为了进行演示，本教程中的步骤包括创建一个描述客户忠诚度模式成员的示例项目。 虽然您可以使用这些步骤为自己创建不同的模式，但建议您首先创建示例模式，以了解[!DNL Schema Editor]的功能。

如果您希望使用[!DNL Schema Registry] API编写模式，请先阅读[[!DNL Schema Registry] 开发人员指南](../api/getting-started.md)，然后再尝试使用[ API](create-schema-api.md)创建模式的教程。

## 入门指南

本教程需要对Adobe Experience Platform在模式创建中涉及的各个方面进行有效的理解。 在开始本教程之前，请查阅以下概念的文档：

* [[!DNL Experience Data Model (XDM)]](../home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。
   * [模式合成基础](../schema/composition.md):XDM模式及其构建块的概述，包括类、混合、数据类型和字段。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

## 打开[!UICONTROL 模式]工作区{#browse}

[!DNL Platform] UI中的[!UICONTROL 模式]工作区提供了[!DNL Schema Library]的可视化，允许您视图管理组织可用的模式。 工作区还包括[!DNL Schema Editor]，在本教程中，您可以在该画布上构建模式。

登录[!DNL Experience Platform]后，在左侧导航中选择&#x200B;**[!UICONTROL 模式]**&#x200B;以打开&#x200B;**[!UICONTROL 模式]**&#x200B;工作区。 **[!UICONTROL 浏览]**&#x200B;选项卡显示一列表模式（[!DNL Schema Library]的表示），您可以对其进行视图和自定义。 列表包括模式所基于的名称、类型、类和行为（记录或时间序列），以及模式上次修改的日期和时间。

有关详细信息，请参阅[在UI](../ui/explore.md)中探索现有XDM资源的指南。

## 创建并命名模式{#create}

要开始编写模式，请在&#x200B;**[!UICONTROL 模式]**&#x200B;工作区的右上角选择&#x200B;**[!UICONTROL 创建模式]**。 出现一个下拉菜单，允许您选择核心类[!UICONTROL XDM单个用户档案]和[!UICONTROL XDM ExperienceEvent]。 如果这些类不符合您的目的，您还可以选择&#x200B;**[!UICONTROL 浏览]**&#x200B;以从其他可用类中进行选择，或者[创建新类](#create-new-class)。

为本教程的目的，请选择&#x200B;**[!UICONTROL XDM单个用户档案]**。

![](../images/tutorials/create-schema/create_schema_button.png)

出现[!DNL Schema Editor]。 这是您将在其上创作模式的画布。 由于您选择了标准XDM类作为模式的基础，因此当您进入编辑器时，将在画布的&#x200B;**[!UICONTROL 结构]**&#x200B;部分自动创建无标题模式，并基于该类在所有模式中包含的标准字段。 该模式的已分配类也列在&#x200B;**[!UICONTROL Composition]**&#x200B;部分的&#x200B;**[!UICONTROL Class]**&#x200B;下。

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>在保存模式之前，您可以在初始合成过程中的任意点更改模式的类[，但应当非常小心。 ](#change-class)Mixin只与某些类兼容，因此更改类将重置画布和已添加的任何字段。

使用编辑器右侧的字段为模式提供显示名称和可选说明。 输入名称后，画布会随之更新，以反映模式的新名称。

![](../images/tutorials/create-schema/name_schema.png)

在为模式决定名称时，需要考虑以下几个重要事项：

* 模式名称应简短且具有说明性，以便以后可以轻松找到模式。
* 模式名称必须是唯一的，这意味着它也应足够具体，以便将来不再重用它。 例如，如果您的组织具有针对不同品牌的单独忠诚项目，则最好将您的模式命名为“Brand A Loyalty Members”，以便轻松与您稍后可能定义的其他与忠诚度相关的模式区分开来。
* 您还可以使用模式描述来提供与模式相关的任何其他上下文信息。

本教程构成一个模式，用于收集与忠诚项目成员相关的数据，因此该模式被命名为“忠诚会员”。

## 添加混合{#mixin}

您现在可以通过添加混音开始向模式添加字段。 混音是一个或多个字段的组，这些字段通常一起用于描述特定概念。 本教程使用mixins描述忠诚度项目的成员并捕获关键信息，如姓名、生日、电话号码、地址等。

要添加混音，请在&#x200B;**[!UICONTROL 混音]**&#x200B;子部分中选择&#x200B;**[!UICONTROL 添加]**。

![](../images/tutorials/create-schema/add_mixin_button.png)

将出现一个新对话框，显示可用混音的列表。 每个混音仅用于特定类，因此对话框仅用于与所选类（本例中为[!DNL XDM Individual Profile]类）兼容的列表混音。 如果您使用标准XDM类，将根据使用普及度智能地对混合列表进行排序。

![](../images/tutorials/create-schema/mixin-popularity.png)

从列表中选择混音会导致混音显示在右侧边栏中。 您可以根据需要选择多个混音，在确认之前将每个混音添加到右边栏的列表。 此外，当前所选混音的右侧会显示一个图标，通过该图标可以预览其提供的字段的结构。

![](../images/tutorials/create-schema/preview-mixin-button.png)

预览混音时，右边栏中会提供混音的模式的详细描述。 您还可以在提供的画布中浏览混音的字段。 当您选择不同的字段时，右边栏会更新，显示有关该字段的详细信息。 完成预览后，选择&#x200B;**[!UICONTROL 返回]**&#x200B;以返回到混音选择对话框。

![](../images/tutorials/create-schema/preview-mixin.png)

对于本教程，选择&#x200B;**[!UICONTROL 人口统计详细信息]**&#x200B;混音，然后选择&#x200B;**[!UICONTROL 添加混音]**。

![](../images/tutorials/create-schema/add_mixin_person_details.png)

模式画布将重新显示。 **[!UICONTROL Mixins]**&#x200B;部分现在列表“[!UICONTROL 人口统计详细信息]”，而&#x200B;**[!UICONTROL Structure]**&#x200B;部分包括混音贡献的字段。 您可以在&#x200B;**[!UICONTROL Mixins]**&#x200B;部分下选择混音的名称，以突出显示它在画布中提供的特定字段。

![](../images/tutorials/create-schema/person_details_structure.png)

此混音在顶级名称`person`下提供数据类型为“[!UICONTROL Person]”的多个字段。 这组字段描述有关个人的信息，包括姓名、出生日期和性别。

>[!NOTE]
>
>请记住，字段可能使用标量类型（如字符串、整数、数组或日期），以及[!DNL Schema Registry]中定义的任何数据类型（表示通用概念的字段组）。

请注意，`name`字段的数据类型为“[!UICONTROL 人员名称]”，这意味着它也描述了通用概念，并包含与名称相关的子字段，如名字、姓氏、字幕和后缀。

在画布中选择不同的字段，以显示它们贡献给模式结构的任何其他字段。

## 在{#mixin-2}中添加另一个混音

您现在可以重复相同的步骤来添加另一个混音。 当您此次视图&#x200B;**[!UICONTROL 添加mixin]**&#x200B;对话框时，请注意“[!UICONTROL 人口统计详细信息]”混音已灰显，且其旁边的复选框无法选中。 这可防止您意外复制已包含在当前模式中的混音。

对于本教程，从对话框中选择“[!DNL Personal Contact Details]” mixin，然后选择&#x200B;**[!UICONTROL 添加mixin]**&#x200B;将其添加到模式。

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

添加后，画布将重新显示。 “[!UICONTROL 个人联系人详细信息]”现在列在&#x200B;**[!UICONTROL 合成]**&#x200B;部分的&#x200B;**[!UICONTROL Mixins]**&#x200B;下，并且在&#x200B;**[!UICONTROL 结构]**&#x200B;下添加了家庭地址、移动电话等字段。

与`name`字段相似，您刚刚添加的字段表示多字段概念。 例如，`homeAddress`的数据类型为“[!UICONTROL 邮政地址]”，而`mobilePhone`的数据类型为“[!UICONTROL 电话号码]”。 您可以选择这些字段中的每个以展开它们，并查看数据类型中包含的其他字段。

![](../images/tutorials/create-schema/personal_details_structure.png)

## 定义新的混音{#define-mixin}

“[!UICONTROL 忠诚度成员]”模式用于捕获与忠诚度项目成员相关的数据，因此它需要一些特定的忠诚度相关字段。 没有包含必要字段的标准混音，因此您需要定义新混音。

此时，打开&#x200B;**[!UICONTROL 添加混音]**&#x200B;对话框时，选择&#x200B;**[!UICONTROL 创建新混音]**。 随后将要求您提供混音的显示名称和说明。

![](../images/tutorials/create-schema/mixin_create_new.png)

与类名称一样，混音名称应简短，用于描述混音对模式的贡献。 它们也是唯一的，因此您将无法重用该名称，因此必须确保其足够具体。

对于本教程，将新混音命名为“忠诚度详细信息”。

选择&#x200B;**[!UICONTROL 添加mixin]**&#x200B;以返回至[!DNL Schema Editor]。 “[!UICONTROL 忠诚度详细信息]”现在应显示在画布左侧的&#x200B;**[!UICONTROL Mixins]**&#x200B;下，但还没有与它关联的字段，因此在&#x200B;**[!UICONTROL 结构]**&#x200B;下没有新字段。

## 将字段添加到mixin {#mixin-fields}

现在您已创建“忠诚度详细信息”混音，是时候定义混音将对模式贡献的字段了。

首先，在&#x200B;**[!UICONTROL Mixins]**&#x200B;部分选择混音名称。 执行此操作后，混音的属性显示在编辑器的右侧，并且&#x200B;**[!UICONTROL 结构]**&#x200B;下模式名称旁将显示一个&#x200B;**加号(+)**&#x200B;图标。

![](../images/tutorials/create-schema/loyalty_details_structure.png)

选择“[!DNL Loyalty Members]”旁边的&#x200B;**加号(+)**&#x200B;图标以在结构中创建新节点。 此节点（在本示例中称为`_tenantId`）表示您的IMS组织的租户ID，前面加下划线。 租户ID的存在表示您正在添加的字段包含在您组织的命名空间中。

换言之，您添加的字段对您的组织而言是唯一的，并将保存在[!DNL Schema Registry]的特定区域中，该区域仅对您的组织可访问。 您定义的字段必须始终添加到租户命名空间，以防止与来自其他标准类、混音、数据类型和字段的名称发生冲突。

在该命名空间节点中是“[!UICONTROL 新字段]”。 这是“[!UICONTROL 忠诚度详细信息]”混音的开始。

![](../images/tutorials/create-schema/new_field_loyalty.png)

使用编辑器右侧的控件，通过创建类型为“[!UICONTROL Object]”的`loyalty`字段进行开始，该字段将用于保存您的忠诚度相关字段。 完成后，选择&#x200B;**[!UICONTROL 应用]**。

![](../images/tutorials/create-schema/loyalty_object.png)

将应用更改并显示新创建的`loyalty`对象。 选择对象旁的&#x200B;**加号(+)**&#x200B;图标以添加其他与忠诚度相关的字段。 出现“[!UICONTROL 新字段]”，画布右侧显示“**[!UICONTROL 字段属性]**”部分。

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

每个字段都需要以下信息：

* **[!UICONTROL 字段名]:** 字段的名称，以驼峰大小写写写。示例：loyaltyLevel
* **[!UICONTROL 显示名]:** 以标题大小写形式写入的字段名称。示例：忠诚度级别
* **[!UICONTROL 类型]:** 字段的数据类型。这包括基本标量类型和在[!DNL Schema Registry]中定义的任何数据类型。 示例：[!UICONTROL 字符串]、[!UICONTROL 整数]、[!UICONTROL 布尔]、[!UICONTROL 人员]、[!UICONTROL 地址]、[!UICONTROL 电话号码]等。
* **[!UICONTROL 描述]:** 字段的可选描述应包含在句子中，最多包含200个字符。

`Loyalty`对象的第一个字段将是一个名为`loyaltyId`的字符串。 将新字段的类型设置为“[!UICONTROL String]”时，**[!UICONTROL Field属性]**&#x200B;部分将填充几个用于应用约束的选项，包括默认值、格式和最大长度。

![](../images/tutorials/create-schema/string_constraints.png)

根据所选数据类型，可以使用不同的约束选项。 由于`loyaltyId`将是电子邮件地址，请从&#x200B;**[!UICONTROL 格式]**&#x200B;下拉菜单中选择“[!UICONTROL email]”。 选择&#x200B;**[!UICONTROL 应用]**&#x200B;以应用您所做的更改。

![](../images/tutorials/create-schema/loyaltyId_field.png)

## 将更多字段添加到mixin {#mixin-fields-2}

现在，您已添加`loyaltyId`字段，可以添加其他字段来捕获与忠诚度相关的信息，例如：

* 点（整数）
* 会员自（日期）

要向模式添加每个字段，请选择`loyalty`对象旁的&#x200B;**加号(+)**&#x200B;图标并填写所需信息。

完成后，Loyalty对象将包含忠诚度ID、积分和成员自定义字段。

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## 向混音{#enum}添加枚举字段

在[!DNL Schema Editor]中定义字段时，您可以将一些其他选项应用到基本字段类型，以便对字段可包含的数据提供进一步约束。 下表说明了这些限制的用例：

| 约束 | 描述 |
| --- | --- |
| [!UICONTROL 必需] | 指示数据获取需要此字段。 根据此模式上传到数据集且不包含此字段的任何数据在摄取时都将失败。 |
| [!UICONTROL 阵列] | 指示字段包含一组值，每个值都指定了数据类型。 例如，对数据类型为“[!UICONTROL String]”的字段使用此约束指定该字段将包含字符串数组。 |
| [!UICONTROL 枚举] | 指示此字段必须包含来自可能值的枚举列表的值之一。 |
| [!UICONTROL 身份] | 指示此字段是标识字段。 本教程[后面提供了有关标识字段的更多信息。](#identity-field) |
| [!UICONTROL 关系] | 虽然模式关系可以通过使用合并模式和[!DNL Real-time Customer Profile]来推断，但这仅适用于共享同一类的模式。 [!UICONTROL Relationship]约束表示此字段引用基于不同类的模式的主标识，这表示两个模式之间的关系。 有关详细信息，请参阅[定义关系](./relationship-ui.md)的教程。 |

>[!NOTE]
>
>所有必填字段、标识字段或关系字段都显示在左边栏中，使您能够轻松定位这些字段，而不管模式的复杂性如何。
>
>![](../images/tutorials/create-schema/left-rail-special.png)

对于本教程，模式中的[!DNL "loyalty"]对象需要一个新枚举字段来描述客户的“忠诚度级别”，其中值只能是四个可能的选项之一。 要将此字段添加到模式，请选择`loyalty`对象旁边的&#x200B;**加号(+)**&#x200B;图标，并填写&#x200B;**[!UICONTROL 字段名称]**&#x200B;和&#x200B;**[!UICONTROL 显示名称]**&#x200B;的必填字段。 对于&#x200B;**[!UICONTROL 类型]**，选择“[!UICONTROL 字符串]”。

![](../images/tutorials/create-schema/loyalty-level-type.png)

选择字段类型后，将显示该字段的其他复选框，包括&#x200B;**[!UICONTROL Array]**、**[!UICONTROL Enum]**&#x200B;和&#x200B;**[!UICONTROL Identity]**&#x200B;的复选框。

选中&#x200B;**[!UICONTROL 枚举]**&#x200B;复选框以打开下面的&#x200B;**[!UICONTROL 枚举值]**&#x200B;部分。 在此，您可以为每个可接受的忠诚度级别输入&#x200B;**[!UICONTROL 值]**（以camelCase为单位）和&#x200B;**[!UICONTROL 标签]**（标题大小写中的可选读者友好名称）。

完成所有字段属性后，选择&#x200B;**[!UICONTROL 应用]**&#x200B;将“[!DNL loyaltyLevel]”字段添加到`loyalty`对象。

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## 将多字段对象转换为数据类型{#datatype}

`loyalty`对象现在包含几个特定于忠诚度的字段，并表示一个通用的数据结构，该结构可能在其他模式中有用。 [!DNL Schema Editor]允许您通过将这些对象的结构转换为数据类型来轻松应用可重用的多字段对象。

数据类型允许多字段结构的一致使用，并提供比混音更灵活的性能，因为它们可以在模式的任何位置使用。 为此，请将字段的&#x200B;**[!UICONTROL Type]**&#x200B;值设置为[!DNL Schema Registry]中定义的任何数据类型的值。

要将`loyalty`对象转换为数据类型，请在&#x200B;**[!UICONTROL 结构]**&#x200B;下选择`loyalty`字段，然后在编辑器右侧的&#x200B;**[!UICONTROL 字段属性]**&#x200B;下选择&#x200B;**[!UICONTROL 转换为新数据类型]**。 出现绿色弹出窗口，确认对象已成功转换。

![](../images/tutorials/create-schema/convert-data-type.png)

现在，当您查看&#x200B;**[!UICONTROL Structure]**&#x200B;下时，您可以看到`loyalty`字段的数据类型为“[!DNL Loyalty]”，并且这些字段旁边有小的锁图标，表明它们不再是单个字段，而是多字段数据类型的一部分。

![](../images/tutorials/create-schema/loyalty_data_type.png)

在将来的模式中，您现在可以将字段指定为“[!DNL Loyalty]”类型，并且它将自动包含ID、忠诚度级别、成员自身和积分的字段。

>[!NOTE]
>
>您还可以创建和编辑自定义数据类型，而与编辑模式无关。 有关详细信息，请参见[创建和编辑数据类型](../ui/resources/data-types.md)的指南。

## 搜索和筛选模式字段

除了基类提供的字段外，您的模式现在还包含多个混音。 处理较大的模式时，您可以选择左边栏中混合名称旁的复选框，将显示的字段筛选为仅由您感兴趣的混合提供的字段。

![](../images/tutorials/create-schema/filter-by-mixin.png)

如果您在模式中查找特定字段，则还可以使用搜索栏按名称筛选显示的字段，而不管它们在哪个混音中提供。

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>在显示匹配字段时，搜索功能会考虑任何选定的混音过滤器。 如果搜索查询未显示您期望的结果，您可能需要多次检查您是否未过滤掉任何相关混音。

## 将模式字段设置为标识字段{#identity-field}

模式提供的标准数据结构可以跨多个源识别属于同一个人的数据，从而允许各种下游用例，如分段、报告、数据科学分析等。 要根据个人身份拼接数据，键字段必须标为适用模式中的[!UICONTROL Identity]字段。

[!DNL Experience Platform] 通过在中使用“标识”复选框，可轻松 **** 地指示标识字段 [!DNL Schema Editor]。但是，您必须根据数据的性质确定哪个字段是最适合用作标识的字段。

例如，可能有数千个忠诚项目成员属于同一“忠诚度级别”，但忠诚项目的每个成员都有唯一的`loyaltyId`（在本例中为单个成员的电子邮件地址）。 `loyaltyId`是每个成员的唯一标识符这一事实使它成为标识字段的最佳候选者，而`loyaltyLevel`则不是。

>[!IMPORTANT]
>
>下面介绍的步骤包括如何向现有模式字段添加标识描述符。 作为在模式本身的结构中定义标识字段的替代方法，您还可以使用`identityMap`字段来包含标识信息。
>
>如果您计划使用`identityMap`，请记住，它将覆盖您直接添加到模式的任何主标识。 有关详细信息，请参见[模式合成指南基础知识](../schema/composition.md#identityMap)中的`identityMap`一节。

在编辑器的&#x200B;**[!UICONTROL 结构]**&#x200B;部分，选择`loyaltyId`字段，并在&#x200B;**[!UICONTROL 字段属性]**&#x200B;下显示&#x200B;**[!UICONTROL 标识]**&#x200B;复选框。 选中该框和选项，将其设置为&#x200B;**[!UICONTROL 主标识]**。 也选中此框。

>[!NOTE]
>
>每个模式只能包含一个主标识字段。 将模式字段设置为主标识后，如果稍后尝试将模式中的其他标识字段设置为主标识，您将收到错误消息。

接下来，您必须从下拉菜单中预定义命名空间的列表中提供&#x200B;**[!UICONTROL 标识命名空间]**。 由于`loyaltyId`是客户的电子邮件地址，请从下拉菜单中选择“[!UICONTROL 电子邮件]”。 选择&#x200B;**[!UICONTROL 应用]**&#x200B;以确认对`loyaltyId`字段的更新。

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>有关标准命名空间及其定义的列表，请参阅[[!DNL Identity Service] 文档](../../identity-service/troubleshooting-guide.md#standard-namespaces)。

应用更改后，`loyaltyId`的图标会显示指纹符号，表明它现在是标识字段。

![](../images/tutorials/create-schema/identity-applied.png)

现在，所有收录到`loyaltyId`字段的数据都将用于帮助识别该个人，并将该客户的单个视图拼接在一起。 要进一步了解如何使用[!DNL Experience Platform]中的标识，请查阅[[!DNL Identity Service]](../../identity-service/home.md)文档。

## 启用模式以在[!DNL Real-time Customer Profile] {#profile}中使用

[[!DNL Real-time Customer Profile]](../../profile/home.md) 利用身份数 [!DNL Experience Platform] 据为每位客户提供整体视图。该服务在与[!DNL Experience Platform]集成的任何系统上建立了可靠、360°用户档案的客户属性以及客户拥有的每个交互的时间戳帐户。

要使模式能够与[!DNL Real-time Customer Profile]一起使用，它必须定义主标识。 如果您尝试启用模式而未先定义主标识，则会收到错误消息。

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

要启用“忠诚会员”模式以在[!DNL Profile]中使用，首先在编辑器的&#x200B;**[!UICONTROL 结构]**&#x200B;部分选择“[!DNL Loyalty Members]”。

在编辑器的右侧，显示有关模式的信息，包括其显示名称、说明和类型。 除此信息外，还有&#x200B;**[!UICONTROL 用户档案]**&#x200B;切换按钮。

![](../images/tutorials/create-schema/profile-toggle.png)

选择&#x200B;**[!UICONTROL 用户档案]**&#x200B;并显示一个弹出窗口，要求您确认是否要为[!DNL Profile]启用模式。

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>为[!DNL Real-time Customer Profile]启用模式并保存后，便无法禁用它。

选择&#x200B;**[!UICONTROL 启用]**&#x200B;以确认您的选择。 您可以根据需要再次选择&#x200B;**[!UICONTROL 用户档案]**&#x200B;切换，以禁用模式，但一旦保存了模式，而启用[!DNL Profile]，就不能再禁用它。

## 后续步骤和其他资源

现在您已完成模式的编写，您可以在画布中看到完整的模式。 选择&#x200B;**[!UICONTROL 保存]**,模式将保存到[!DNL Schema Library]中，使[!DNL Schema Registry]可以访问它。

您的新模式现在可用于将数据收录到[!DNL Platform]中。 请记住，一旦模式被用于摄取数据，只能进行附加更改。 有关模式版本控制的详细信息，请参阅[模式合成基础知识](../schema/composition.md)。

您现在可以按照上的教程在UI[中定义模式关系，向“Loyalty Members”模式添加新关系字段。](./relationship-ui.md)

还可以使用[!DNL Schema Registry] API查看和管理“Loyalty Members”模式。 要开始使用API，请阅读[[!DNL Schema Registry API] 开发人员指南](../api/getting-started.md)进行开始。

### 视频资源

>[!WARNING]
>
>以下视频中显示的[!DNL Platform] UI已过时。 有关最新的UI屏幕截图和功能，请参阅上面的文档。

以下视频演示如何在[!DNL Platform] UI中创建简单的模式。

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

以下视频旨在加深您对使用混音和类的理解。

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## 附录

以下各节提供了有关使用[!DNL Schema Editor]的附加信息。

### 创建新类{#create-new-class}

[!DNL Experience Platform] 提供了根据组织特有的类定义模式的灵活性。要了解如何创建新类，请参阅有关在UI[中创建和编辑类的指南。](../ui/resources/classes.md#create)

### 更改模式{#change-class}的类

在保存模式之前，您可以在初始合成过程中的任意点更改模式的类。

>[!WARNING]
>
>重新分配模式的课程时应非常谨慎。 Mixin只与某些类兼容，因此更改类将重置画布和已添加的任何字段。

要了解如何更改模式的类，请参阅UI](../ui/resources/schemas.md)中的[管理模式的指南。
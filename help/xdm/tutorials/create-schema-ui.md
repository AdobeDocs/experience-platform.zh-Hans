---
keywords: Experience Platform；主页；热门主题；UI;XDM;XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；架构编辑器；架构编辑器；架构；架构；架构；架构；架构；创建架构
solution: Experience Platform
title: 使用模式编辑器创建模式
topic-legacy: tutorial
type: Tutorial
description: 本教程介绍了在 Experience Platform 中使用模式编辑器创建模式的步骤。
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '3754'
ht-degree: 0%

---

# 使用[!DNL Schema Editor]创建架构

利用Adobe Experience Platform用户界面，可在名为[!DNL Schema Editor]的交互式可视画布中创建和管理[!DNL Experience Data Model](XDM)架构。 本教程介绍如何使用[!DNL Schema Editor]创建模式。

>[!NOTE]
>
>出于演示目的，本教程中的步骤涉及创建一个描述客户忠诚度计划成员的示例架构。 虽然您可以使用这些步骤创建其他模式以供您自己使用，但建议您先创建示例模式，以了解[!DNL Schema Editor]的功能。

如果您希望改用[!DNL Schema Registry] API编写架构，请首先阅读[[!DNL Schema Registry] 开发人员指南](../api/getting-started.md)，然后再尝试使用[ API](create-schema-api.md)创建架构的教程。

## 入门指南

本教程需要对创建架构时涉及的Adobe Experience Platform各个方面有一定的了解。 在开始本教程之前，请查看有关以下概念的文档：

* [[!DNL Experience Data Model (XDM)]](../home.md):用于组织客户体验数 [!DNL Platform] 据的标准化框架。
   * [架构组合的基础知识](../schema/composition.md):XDM架构及其构建块的概述，包括类、架构字段组、数据类型和单个字段。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

## 打开[!UICONTROL Schemas]工作区 {#browse}

 UI中的[!DNL Platform]架构工作区提供了[!DNL Schema Library]的可视化，允许您查看管理组织可用的架构。 该工作区还包含[!DNL Schema Editor]画布，在本教程中，您可以在该画布上撰写架构。

登录[!DNL Experience Platform]后，在左侧导航中选择&#x200B;**[!UICONTROL 架构]**&#x200B;以打开&#x200B;**[!UICONTROL 架构]**&#x200B;工作区。 **[!UICONTROL Browse]**&#x200B;选项卡显示一个架构列表（[!DNL Schema Library]的表示形式），您可以查看和自定义该列表。 该列表包括架构所基于的名称、类型、类和行为（记录或时间序列），以及上次修改架构的日期和时间。

有关更多信息，请参阅[在UI](../ui/explore.md)中浏览现有XDM资源的指南。

## 创建和命名架构 {#create}

要开始构建架构，请选择&#x200B;**[!UICONTROL 架构]**&#x200B;工作区右上角的&#x200B;**[!UICONTROL 创建架构]** 。 此时会出现一个下拉菜单，允许您选择在核心类[!UICONTROL XDM Indivial Profile]和[!UICONTROL XDM ExperienceEvent]之间进行选择。 如果这些类不适合您的目的，您还可以选择&#x200B;**[!UICONTROL Browse]**&#x200B;从其他可用类中进行选择，或选择[创建新类](#create-new-class)。

在本教程中，选择&#x200B;**[!UICONTROL XDM个人配置文件]**。

![](../images/tutorials/create-schema/create_schema_button.png)

由于您选择了标准XDM类来基于架构，因此会显示&#x200B;**[!UICONTROL 添加字段组]**&#x200B;对话框，允许您立即开始向架构添加字段。 现在，选择&#x200B;**[!UICONTROL 取消]**&#x200B;以退出对话框。

![](../images/tutorials/create-schema/cancel-field-group.png)

出现[!DNL Schema Editor]。 这是用于构建架构的画布。 当您进入编辑器时，将在画布的&#x200B;**[!UICONTROL 结构]**&#x200B;部分中自动创建无标题架构，以及基于该类的所有架构中包含的标准字段。 架构的分配类也列在&#x200B;**[!UICONTROL Composition]**&#x200B;部分的&#x200B;**[!UICONTROL Class]**&#x200B;下。

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>在保存架构之前，您可以在初始组合过程中的任意时刻[更改架构](#change-class)的类，但是这应该非常谨慎。 字段组仅与某些类兼容，因此更改类将重置画布和您添加的任何字段。

使用编辑器右侧的字段为架构提供显示名称和可选描述。 输入名称后，画布会随之更新，以反映架构的新名称。

![](../images/tutorials/create-schema/name_schema.png)

在决定架构的名称时，需要考虑以下几个重要事项：

* 架构名称应当简短且具有描述性，以便以后可以轻松找到架构。
* 架构名称必须是唯一的，这意味着它还应具有足够的特定性，以便将来不会重复使用。 例如，如果贵组织针对不同品牌分别实施了不同的忠诚度计划，则最好将架构命名为“品牌A忠诚度会员”，以便轻松与其他可能在以后定义的与忠诚度相关的架构区分开来。
* 您还可以使用架构描述提供有关该架构的任何其他上下文信息。

本教程将组成一个架构来摄取与忠诚度计划成员相关的数据，因此该架构名为“忠诚度会员”。

## 添加字段组{#field-group}

现在，您可以通过添加字段组，开始向架构添加字段。 字段组是由一个或多个字段组成的组，这些字段通常一起用于描述特定概念。 本教程使用字段组描述忠诚度计划的成员，并捕获关键信息，如姓名、生日、电话号码、地址等。

要添加字段组，请在&#x200B;**[!UICONTROL 字段组]**&#x200B;子部分中选择&#x200B;**[!UICONTROL Add]**。

![](../images/tutorials/create-schema/add-field-group-button.png)

此时会出现一个新对话框，其中显示了可用字段组的列表。 每个字段组仅用于特定类，因此对话框仅列出与您选择的类（在本例中为[!DNL XDM Individual Profile]类）兼容的字段组。 如果您使用标准XDM类，则将根据使用情况的受欢迎程度对字段组列表进行智能排序。

![](../images/tutorials/create-schema/field-group-popularity.png)

从列表中选择字段组会使其显示在右侧边栏中。 您可以根据需要选择多个字段组，在确认之前，将每个字段组添加到右边栏的列表。 此外，当前选定字段组的右侧会显示一个图标，用于预览其提供的字段结构。

![](../images/tutorials/create-schema/preview-field-group-button.png)

预览字段组时，右侧边栏中提供了字段组架构的详细描述。 您还可以在提供的画布中浏览字段组的字段。 当您选择不同的字段时，右边栏会更新，以显示有关该字段的详细信息。 完成预览后，选择&#x200B;**[!UICONTROL 返回]**&#x200B;以返回到字段组选择对话框。

![](../images/tutorials/create-schema/preview-field-group.png)

在本教程中，选择&#x200B;**[!UICONTROL 人口统计详细信息]**&#x200B;字段组，然后选择&#x200B;**[!UICONTROL 添加字段组]**。

![](../images/tutorials/create-schema/demographic-details.png)

将重新显示架构画布。 **[!UICONTROL 字段组]**&#x200B;部分现在列出“[!UICONTROL 人口统计详细信息]”，而&#x200B;**[!UICONTROL 结构]**&#x200B;部分包含字段组贡献的字段。 您可以在&#x200B;**[!UICONTROL 字段组]**&#x200B;部分下选择字段组的名称，以突出显示它在画布中提供的特定字段。

![](../images/tutorials/create-schema/demographic-details-structure.png)

此字段组在顶级名称`person`下提供数据类型为“[!UICONTROL Person]”的多个字段。 这组字段描述有关个人的信息，包括姓名、出生日期和性别。

>[!NOTE]
>
>请记住，字段可能使用标量类型（如字符串、整数、数组或日期），以及[!DNL Schema Registry]中定义的任何数据类型（一组表示通用概念的字段）。

请注意，`name`字段的数据类型为“[!UICONTROL 人员名称]”，这意味着该字段也描述了通用概念，并包含与名称相关的子字段，如名字、姓氏、礼貌标题和后缀。

选择画布中的不同字段，以显示它们对架构结构贡献的任何其他字段。

## 添加另一个字段组{#field-group-2}

您现在可以重复相同步骤以添加其他字段组。 此时，当您查看&#x200B;**[!UICONTROL 添加字段组]**&#x200B;对话框时，请注意“[!UICONTROL 人口统计详细信息]”字段组已灰显，其旁边的复选框无法选中。 这样可防止意外复制当前架构中已包含的字段组。

在本教程中，从对话框中选择“[!DNL Personal Contact Details]”字段组，然后选择&#x200B;**[!UICONTROL 添加字段组]**&#x200B;以将其添加到架构。

![](../images/tutorials/create-schema/personal-contact-details.png)

添加后，画布会重新显示。 “[!UICONTROL 个人联系人详细信息]”现在列在&#x200B;**[!UICONTROL 组合]**&#x200B;部分的&#x200B;**[!UICONTROL 字段组]**&#x200B;下，并且在&#x200B;**[!UICONTROL 结构]**&#x200B;下添加了有关家庭地址、移动电话等的字段。

与`name`字段类似，您刚才添加的字段表示多字段概念。 例如，`homeAddress`的数据类型为“[!UICONTROL 邮政地址]”，而`mobilePhone`的数据类型为“[!UICONTROL 电话号码]”。 您可以选择其中的每个字段以展开它们，并查看数据类型中包含的其他字段。

![](../images/tutorials/create-schema/personal-contact-details-structure.png)

## 定义自定义字段组{#define-field-group}

“[!UICONTROL 忠诚会员]”架构用于捕获与忠诚度计划会员相关的数据，因此它需要一些特定的忠诚度相关字段。

有一个标准的[!UICONTROL 忠诚度详细信息]字段组，您可以将其添加到架构中以捕获与忠诚度计划相关的常用字段。 虽然我们强烈建议您使用标准字段组来表示架构捕获的概念，但标准忠诚度字段组的结构可能无法捕获特定忠诚度计划的所有相关数据。 在此方案中，您可以选择定义新的自定义字段组来捕获这些字段。

再次打开&#x200B;**[!UICONTROL 添加字段组]**&#x200B;对话框，但此时在顶部附近选择&#x200B;**[!UICONTROL 创建新字段组]**。 然后，系统会要求您提供字段组的显示名称和描述。

![](../images/tutorials/create-schema/create-new-field-group.png)

与类名称一样，字段组名称应简短，用于描述字段组将对架构做出贡献。 这些名称也是唯一的，因此您将无法重复使用该名称，因此必须确保该名称足够具体。

在本教程中，将新字段组命名为“忠诚度详细信息”。

选择&#x200B;**[!UICONTROL 添加字段组]**&#x200B;以返回到[!DNL Schema Editor]。 “[!UICONTROL 忠诚度详细信息]”现在应显示在画布左侧的&#x200B;**[!UICONTROL 字段组]**&#x200B;下，但还没有与其关联的字段，因此在&#x200B;**[!UICONTROL 结构]**&#x200B;下不会显示任何新字段。

## 向字段组{#field-group-fields}添加字段

现在，您已创建“忠诚度详细信息”字段组，接下来该定义字段组将对架构贡献的字段。

要开始，请在&#x200B;**[!UICONTROL 字段组]**&#x200B;部分中选择字段组名称。 执行此操作后，字段组的属性将显示在编辑器的右侧，并且&#x200B;**+(+)**&#x200B;图标会显示在&#x200B;**[!UICONTROL Structure]**&#x200B;下架构名称的旁边。

![](../images/tutorials/create-schema/loyalty_details_structure.png)

选择“[!DNL Loyalty Members]”旁边的&#x200B;**加号(+)**&#x200B;图标，以在结构中创建新节点。 此节点（在本示例中称为`_tenantId`）表示您IMS组织的租户ID，前面有下划线。 租户ID的存在表示您添加的字段包含在您组织的命名空间中。

换言之，您添加的字段对贵组织是唯一的，并将保存在[!DNL Schema Registry]中仅供贵组织访问的特定区域。 必须始终将您定义的字段添加到租户命名空间中，以防止与其他标准类、字段组、数据类型和字段中的名称发生冲突。

在该命名空间节点内有一个“[!UICONTROL New Field]”。 这是“[!UICONTROL 忠诚度详细信息]”字段组的开头。

![](../images/tutorials/create-schema/new_field_loyalty.png)

使用编辑器右侧的控件，首先创建一个类型为“[!UICONTROL Object]”的`loyalty`字段，该字段将用于保存与忠诚度相关的字段。 完成后，选择&#x200B;**[!UICONTROL Apply]**。

![](../images/tutorials/create-schema/loyalty_object.png)

将应用更改，并出现新创建的`loyalty`对象。 选择对象旁边的&#x200B;**加号(+)**&#x200B;图标，以添加其他与忠诚度相关的字段。 将显示“[!UICONTROL New Field]”，画布右侧将显示&#x200B;**[!UICONTROL Field properties]**&#x200B;部分。

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

每个字段都需要以下信息：

* **[!UICONTROL 字段名称]:** 字段的名称，以驼峰式写成。示例：loyatyLevel
* **[!UICONTROL 显示名称]:** 以标题大小写写的字段名称。示例：忠诚度级别
* **[!UICONTROL 类型]:** 字段的数据类型。这包括基本标量类型和在[!DNL Schema Registry]中定义的任何数据类型。 示例：[!UICONTROL 字符串]、[!UICONTROL 整数]、[!UICONTROL 布尔]、[!UICONTROL 人员]、[!UICONTROL 地址]、[!UICONTROL 电话号码]等。
* **[!UICONTROL 描述]:** 应包含对字段的可选描述，以句子形式写成，最多200个字符。

`Loyalty`对象的第一个字段将是一个名为`loyaltyId`的字符串。 将新字段的类型设置为“[!UICONTROL String]”时，将填充&#x200B;**[!UICONTROL Field properties]**&#x200B;部分，其中包含多个应用约束的选项，包括默认值、格式和最大长度。

![](../images/tutorials/create-schema/string_constraints.png)

根据所选数据类型，可使用不同的约束选项。 由于`loyaltyId`将是电子邮件地址，请从&#x200B;**[!UICONTROL 格式]**&#x200B;下拉菜单中选择“[!UICONTROL email]”。 选择&#x200B;**[!UICONTROL Apply]**&#x200B;以应用更改。

![](../images/tutorials/create-schema/loyaltyId_field.png)

## 向字段组{#field-group-fields-2}添加更多字段

现在，您已添加`loyaltyId`字段，接下来可以添加其他字段以捕获与忠诚度相关的信息，例如：

* 点（整数）
* 会员（日期）

要向架构中添加每个字段，请选择`loyalty`对象旁边的&#x200B;**加号(+)**&#x200B;图标，然后填写所需信息。

完成后，忠诚度对象将包含忠诚度ID、积分和自成员以来的字段。

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## 向字段组添加枚举字段 {#enum}

在[!DNL Schema Editor]中定义字段时，可以对基本字段类型应用一些其他选项，以便对字段可包含的数据提供进一步的限制。 下表说明了这些约束的用例：

| 约束 | 描述 |
| --- | --- |
| [!UICONTROL 必需] | 表示数据摄取需要字段。 摄取时，任何上传到基于此架构且不包含此字段的数据集的数据都将失败。 |
| [!UICONTROL 数组] | 指示字段包含一个值数组，每个值都指定数据类型。 例如，对数据类型为“[!UICONTROL String]”的字段使用此约束指定该字段将包含字符串数组。 |
| [!UICONTROL 枚举] | 表示此字段必须包含可能值枚举列表中的值之一。 |
| [!UICONTROL 身份] | 表示此字段是标识字段。 有关身份字段的更多信息将在本教程的后面部分](#identity-field)提供。[ |
| [!UICONTROL 关系] | 虽然架构关系可以通过使用并集架构和[!DNL Real-time Customer Profile]来推断，但这仅适用于共享同一类的架构。 [!UICONTROL Relationship]约束表示此字段引用基于不同类的架构的主标识，这表示两个架构之间的关系。 有关更多信息，请参阅[定义关系](./relationship-ui.md)的教程。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>左边栏中显示了任何必需、身份或关系字段，无论架构的复杂性如何，都允许您轻松定位这些字段。
>
>![](../images/tutorials/create-schema/left-rail-special.png)

在本教程中，架构中的[!DNL "loyalty"]对象需要一个新的枚举字段来描述客户的“忠诚度级别”，其中的值只能是四个可能选项之一。 要将此字段添加到架构中，请选择`loyalty`对象旁边的&#x200B;**加号(+)**&#x200B;图标，并填写&#x200B;**[!UICONTROL 字段名称]**&#x200B;和&#x200B;**[!UICONTROL 显示名称]**&#x200B;的必填字段。 对于&#x200B;**[!UICONTROL Type]**，选择“[!UICONTROL 字符串]”。

![](../images/tutorials/create-schema/loyalty-level-type.png)

选择字段类型后，将显示其他复选框，包括&#x200B;**[!UICONTROL Array]**、**[!UICONTROL Enum]**&#x200B;和&#x200B;**[!UICONTROL Identity]**&#x200B;的复选框。

选中&#x200B;**[!UICONTROL Enum]**&#x200B;复选框以打开下面的&#x200B;**[!UICONTROL Enum values]**&#x200B;部分。 在此，您可以为每个可接受的忠诚度级别输入&#x200B;**[!UICONTROL Value]**（在camelCase中）和&#x200B;**[!UICONTROL Label]**（在标题大小写中是可选的、对读者友好的名称）。

完成所有字段属性后，选择&#x200B;**[!UICONTROL Apply]**&#x200B;以将“[!DNL loyaltyLevel]”字段添加到`loyalty`对象。

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## 将多字段对象转换为数据类型 {#datatype}

`loyalty`对象现在包含多个特定于忠诚度的字段，并表示在其他架构中可能有用的通用数据结构。 [!DNL Schema Editor]允许您通过将这些对象的结构转换为数据类型来轻松应用可重用的多字段对象。

数据类型允许一致地使用多字段结构，并比字段组提供更大的灵活性，因为它们可以在架构中的任意位置使用。 这是通过将字段的&#x200B;**[!UICONTROL Type]**&#x200B;值设置为[!DNL Schema Registry]中定义的任何数据类型的值来完成的。

要将`loyalty`对象转换为数据类型，请选择&#x200B;**[!UICONTROL 结构]**&#x200B;下的`loyalty`字段，然后选择编辑器右侧的&#x200B;**[!UICONTROL 字段属性]**&#x200B;下的&#x200B;**[!UICONTROL 转换为新数据类型]**。 出现绿色弹出窗口，确认对象已成功转换。

![](../images/tutorials/create-schema/convert-data-type.png)

现在，当您查看&#x200B;**[!UICONTROL 结构]**&#x200B;下时，您可以看到`loyalty`字段的数据类型为“[!DNL Loyalty]”，并且这些字段旁有小的锁图标，表示它们不再是单个字段，而是多字段数据类型的一部分。

![](../images/tutorials/create-schema/loyalty_data_type.png)

在将来的架构中，您现在可以将字段分配为“[!DNL Loyalty]”类型，并且该字段将自动包含ID、忠诚度级别、从成员到积分的字段。

>[!NOTE]
>
>您还可以创建和编辑自定义数据类型，而不依赖于编辑架构。 有关更多信息，请参阅[创建和编辑数据类型](../ui/resources/data-types.md)指南。

## 搜索和筛选架构字段

除了基类提供的字段之外，您的架构现在还包含多个字段组。 使用较大的架构时，您可以选中左边栏中字段组名称旁边的复选框，以仅将显示的字段筛选为您感兴趣的字段组提供的字段。

![](../images/tutorials/create-schema/filter-by-field-group.png)

如果您在架构中查找特定字段，则还可以使用搜索栏按名称筛选显示的字段，而不管这些字段在哪个字段组下提供。

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>显示匹配字段时，搜索函数会考虑任何选定的字段组过滤器。 如果搜索查询未显示您预期的结果，则可能需要再次检查您是否未过滤掉任何相关字段组。

## 将架构字段设置为标识字段{#identity-field}

架构提供的标准数据结构可用于在多个源中识别属于同一个人的数据，从而允许进行各种下游用例，如分段、报告、数据科学分析等。 要根据单个身份拼合数据，键字段必须在适用的架构中标记为[!UICONTROL Identity]字段。

[!DNL Experience Platform] 通过在中使用Identity复选框，可轻松表示 **** 标识字 [!DNL Schema Editor]段。但是，您必须根据数据的性质确定哪个字段是用作标识的最佳候选字段。

例如，忠诚度计划成员中可能有数千名属于同一“忠诚度级别”，但忠诚度计划的每个成员都有一个唯一的`loyaltyId`（在本例中为单个成员的电子邮件地址）。 `loyaltyId`是每个成员的唯一标识符这一事实使其成为标识字段的良好候选者，而`loyaltyLevel`则不是。

>[!IMPORTANT]
>
>下面概述的步骤包括如何向现有架构字段添加标识描述符。 作为在架构本身的结构中定义标识字段的替代方法，您还可以改用`identityMap`字段来包含标识信息。
>
>如果您计划使用`identityMap`，请记住，它将覆盖您直接添加到架构中的任何主标识。 有关更多信息，请参阅[架构组合指南](../schema/composition.md#identityMap)基础知识中`identityMap`部分。

在编辑器的&#x200B;**[!UICONTROL Structure]**&#x200B;部分中，选择`loyaltyId`字段，并在&#x200B;**[!UICONTROL Field properties]**&#x200B;下方显示&#x200B;**[!UICONTROL Identity]**&#x200B;复选框。 选中方框和选项，以在出现&#x200B;**[!UICONTROL 主标识]**&#x200B;时设置此标识。 也选中此框。

>[!NOTE]
>
>每个架构只能包含一个主标识字段。 将架构字段设置为主标识后，如果您稍后尝试将架构中的其他标识字段设置为主标识，则会收到一条错误消息。

接下来，您必须从下拉列表中预定义的命名空间列表中提供&#x200B;**[!UICONTROL Identity namespace]**。 由于`loyaltyId`是客户的电子邮件地址，请从下拉菜单中选择“[!UICONTROL Email]”。 选择&#x200B;**[!UICONTROL 应用]**&#x200B;以确认对`loyaltyId`字段的更新。

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>有关标准命名空间及其定义的列表，请参阅[[!DNL Identity Service] 文档](../../identity-service/troubleshooting-guide.md#standard-namespaces)。

应用更改后，`loyaltyId`的图标会显示指纹符号，表示该符号现在为标识字段。

![](../images/tutorials/create-schema/identity-applied.png)

现在，所有摄取到`loyaltyId`字段的数据都将用于帮助识别该个人，并拼合该客户的单个视图。 要了解有关在[!DNL Experience Platform]中使用身份的更多信息，请查阅[[!DNL Identity Service]](../../identity-service/home.md)文档。

## 启用架构以在[!DNL Real-time Customer Profile]中使用 {#profile}

[[!DNL Real-time Customer Profile]](../../profile/home.md) 在中利用身份数 [!DNL Experience Platform] 据，以提供每个客户的整体视图。该服务可构建360°的客户属性配置文件，以及客户在与[!DNL Experience Platform]集成的任何系统中的每个交互的带有时间戳的帐户。

要启用架构以与[!DNL Real-time Customer Profile]一起使用，必须定义主标识。 如果在未先定义主标识的情况下尝试启用架构，您将收到一条错误消息。

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

要启用“忠诚会员”架构以在[!DNL Profile]中使用，请首先在编辑器的&#x200B;**[!UICONTROL Structure]**&#x200B;部分中选择“[!DNL Loyalty Members]”。

在编辑器的右侧，显示了有关架构的信息，包括其显示名称、描述和类型。 除此信息外，还有一个&#x200B;**[!UICONTROL 配置文件]**&#x200B;切换按钮。

![](../images/tutorials/create-schema/profile-toggle.png)

选择&#x200B;**[!UICONTROL 配置文件]**，此时会出现一个弹出窗口，要求您确认是否要启用[!DNL Profile]架构。

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>为[!DNL Real-time Customer Profile]启用并保存架构后，便无法禁用该架构。

选择&#x200B;**[!UICONTROL 启用]**&#x200B;以确认您的选择。 如果需要，您可以再次选择&#x200B;**[!UICONTROL 配置文件]**&#x200B;切换开关以禁用架构，但在[!DNL Profile]启用架构后，该架构便无法再禁用。

## 后续步骤和其他资源

现在，您已完成架构的合成，接下来便可以在画布中看到完整的架构。 选择&#x200B;**[!UICONTROL Save]**，此架构将保存到[!DNL Schema Library]，以便[!DNL Schema Registry]访问。

您的新架构现在可用于将数据摄取到[!DNL Platform]中。 请记住，一旦使用架构摄取数据，则只能进行附加更改。 有关模式版本控制的更多信息，请参阅[架构组合基础知识](../schema/composition.md)。

现在，您可以按照[中的教程，在UI](./relationship-ui.md)中定义架构关系，以向“忠诚会员”架构添加新的关系字段。

“忠诚会员”架构也可使用[!DNL Schema Registry] API进行查看和管理。 要开始使用API，请首先阅读[[!DNL Schema Registry API] 开发人员指南](../api/getting-started.md)。

### 视频资源

>[!WARNING]
>
>以下视频中显示的[!DNL Platform] UI已过期。 有关最新的UI屏幕截图和功能，请参阅上述文档。

以下视频演示了如何在[!DNL Platform] UI中创建简单模式。

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

以下视频旨在增强您对使用字段组和类的了解。

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## 附录

以下各节提供了有关[!DNL Schema Editor]的使用的附加信息。

### 创建新类{#create-new-class}

[!DNL Experience Platform] 提供了根据组织特有的类定义架构的灵活性。要了解如何创建新类，请参阅[在UI](../ui/resources/classes.md#create)中创建和编辑类的指南。

### 更改架构{#change-class}的类

在保存架构之前，您可以在初始合成过程中的任意时刻更改架构的类。

>[!WARNING]
>
>重新分配模式的类时应格外谨慎。 字段组仅与某些类兼容，因此更改类将重置画布和您添加的任何字段。

要了解如何更改架构的类，请参阅[管理UI](../ui/resources/schemas.md)中的架构指南。

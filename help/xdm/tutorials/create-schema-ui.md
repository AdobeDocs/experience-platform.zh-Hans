---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: 使用架构编辑器创建架构
topic: tutorial
type: Tutorials
description: 本教程介绍了在模式中使用模式编辑器创建Experience Platform的步骤。
translation-type: tm+mt
source-git-commit: eb6505bdcad9eee6d7e9674504223ca919f19c34
workflow-type: tm+mt
source-wordcount: '3835'
ht-degree: 0%

---


# 使用 [!DNL Schema Editor]

Adobe Experience Platform用户界面允许您在称为“”的 [!DNL Experience Data Model] 交互式可视画布中创建和管理(XDM)模式 [!DNL Schema Editor]。 本教程介绍如何使用创建模式 [!DNL Schema Editor]。

>[!NOTE]
>
>为了进行演示，本教程中的步骤包括创建一个描述客户忠诚度模式成员的示例项目。 虽然您可以使用这些步骤为您自己创建不同的模式，但建议您首先创建示例模式，以了解其功能 [!DNL Schema Editor]。

如果您希望改用API编写模式, [!DNL Schema Registry] 请先阅读开发人员指 [[!DNL Schema Registry] 南](../api/getting-started.md) ，然后再尝试教程 [，关](create-schema-api.md)于使用API创建模式。

## 入门指南

本教程需要对Adobe Experience Platform在模式创建中涉及的各个方面进行有效的理解。 在开始本教程之前，请查阅以下概念的文档：

* [[!DNL体验数据模型(XDM)]](../home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。
   * [模式合成基础](../schema/composition.md):XDM模式及其构建块的概述，包括类、混合、数据类型和字段。
* [[!DNL实时客户用户档案]](../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

## 浏览模式工作区中的现 [!UICONTROL 有模式] {#browse}

UI [!UICONTROL 中的] 模式工作 [!DNL Platform] 区提供了可视化的内 [!DNL Schema Library]容，使您能够视图管理组织可用的模式。 工作区还包括画 [!DNL Schema Editor]布，在本教程中，您可以在画布上构建模式。

登录后， [!DNL Experience Platform]在左 **[!UICONTROL 侧导航]** 中选择模式以打 **[!UICONTROL 开模式工作区]** 。 “浏 **[!UICONTROL 览]** ”选项卡显示一列表模式(表示 [!DNL Schema Library])，您可以对其进行视图和自定义。 列表包括模式所基于的名称、类型、类和行为（记录或时间序列），以及模式上次修改的日期和时间。

选择搜索栏旁边的筛选器图标，以对注册表中的所有资源（包括类、混合和数据类型）使用筛选功能。 您还可以根据资源是否归Adobe或您的组织所有以及是否已启用在中使用，进行筛选 [!DNL Real-time Customer Profile]。

![](../images/tutorials/create-schema/schemas_filter.png)

## 创建和命名模式 {#create}

要开始编写模式，请 **[!UICONTROL 选择]** “模式”工作区右上角的“ **[!UICONTROL 创建模式]** ”。 此时会显示一个下拉菜单，允许您选择核心类XDM [!UICONTROL 单个用户档案][!UICONTROL 和XDM ExperienceEvent]。 如果这些类不符合您的目的，您还可以选择“浏 **[!UICONTROL 览]** ”，从其他可用类中进行选择 [或创建新类](#create-new-class)。

在本教程中，请选择“XDM单 **[!UICONTROL 个用户档案”]**。

![](../images/tutorials/create-schema/create_schema_button.png)

将出 [!DNL Schema Editor] 现。 这是您将在其上创作模式的画布。 由于您选择了标准XDM类作为模式的基础，因此当您到达编辑器时，将在画布的“结构 **** ”部分自动创建无标题模式，并基于该类的所有模式中包含标准字段。 模式的已分配类也列在“合成” **[!UICONTROL 部分]** 的“ **[!UICONTROL 类]** ”下。

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>在保 [存模式之前](#change-class) ，您可以在初始合成过程中的任意点更改模式的类，但应当非常小心。 Mixin只与某些类兼容，因此更改类将重置画布和已添加的任何字段。

使用编辑器右侧的字段为模式提供显示名称和可选说明。 输入名称后，画布会随之更新，以反映模式的新名称。

![](../images/tutorials/create-schema/name_schema.png)

在为模式决定名称时，需要考虑以下几个重要事项：

* 模式名称应简短且具有说明性，以便以后可以轻松找到模式。
* 模式名称必须是唯一的，这意味着它也应足够具体，以便将来不再重用它。 例如，如果您的组织具有针对不同品牌的单独忠诚项目，则最好将您的模式命名为“Brand A Loyalty Members”，以便轻松与您稍后可能定义的其他与忠诚度相关的模式区分开来。
* 您还可以使用模式描述来提供与模式相关的任何其他上下文信息。

本教程构成一个模式，用于收集与忠诚项目成员相关的数据，因此该模式被命名为“忠诚会员”。

## 添加混音 {#mixin}

您现在可以通过添加混音开始向模式添加字段。 混音是一个或多个字段的组，这些字段通常一起用于描述特定概念。 本教程使用mixins描述忠诚度项目的成员并捕获关键信息，如姓名、生日、电话号码、地址等。

要添加混音，请在 **[!UICONTROL Mixins]** 子部 **[!UICONTROL 分中选]** 择“添加”。

![](../images/tutorials/create-schema/add_mixin_button.png)

将出现一个新对话框，显示可用混音的列表。 每个混音仅用于特定类，因此对话框仅用于与所选类（本例中为类）兼容的列表混 [!DNL XDM Individual Profile] 音。 如果您使用标准XDM类，将根据使用普及度智能地对混合列表进行排序。

![](../images/tutorials/create-schema/mixin-popularity.png)

从列表中选择混音会导致混音显示在右侧边栏中。 您可以根据需要选择多个混音，在确认之前将每个混音添加到右边栏的列表。 此外，当前所选混音的右侧会显示一个图标，通过该图标可以预览其提供的字段的结构。

![](../images/tutorials/create-schema/preview-mixin-button.png)

预览混音时，右边栏中会提供混音的模式的详细描述。 您还可以在提供的画布中浏览混音的字段。 当您选择不同的字段时，右边栏会更新，显示有关该字段的详细信息。 预 **[!UICONTROL 览完]** 后，选择“返回”返回到混音选择对话框。

![](../images/tutorials/create-schema/preview-mixin.png)

在本教程中，选择混 **[!UICONTROL 音的用户档案]** ，然后选择 **[!UICONTROL 添加混音]**。

![](../images/tutorials/create-schema/add_mixin_person_details.png)

模式画布将重新显示。 Mixins **[!UICONTROL 部分现在]** 列表“[!UICONTROL 用户档案人详细信息]”，而 **[!UICONTROL Structure]** 部分包括混合所贡献的字段。 您可以在“混音”部分下选择混音 **[!UICONTROL 的名称]** ，以突出显示它在画布中提供的特定字段。

![](../images/tutorials/create-schema/person_details_structure.png)

此混音在顶级名称下提供数 `person` 据类型为“Person”的多个字段。 这组字段描述有关个人的信息，包括姓名、出生日期和性别。

>[!NOTE]
>
>请记住，字段可能使用在中定义的标量类型（如字符串、整数、数组或日期）以及任何数据类型（表示通用概念的字段组） [!DNL Schema Registry]。

请注意， `name` 该字段的数据类型为“[!UICONTROL 全名]”，这意味着它也描述一个通用概念，并包含与名称相关的子字段，如名字、姓氏、字幕和后缀。

在画布中选择不同的字段，以显示它们贡献给模式结构的任何其他字段。

## 添加另一个混音 {#mixin-2}

您现在可以重复相同的步骤来添加另一个混音。 当您此次视图 **[!UICONTROL “添加混音]** ”对话框时，请注意“[!UICONTROL 用户档案人详细信息]”混音已灰显，且其旁边的复选框无法选中。 这可防止您意外复制已包含在当前模式中的混音。

对于本教程，从对话[!DNL Profile personal details]框中选择“”混音，然 **[!UICONTROL 后选择]** “添加混音”将其添加到模式。

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

添加后，画布将重新显示。 “[!UICONTROL 用户档案]”现在列在“合成 **[!UICONTROL ”部分的]** Mixins下，并在结构中添加了家庭地址、手机等 ********&#x200B;字段。

与字段类 `name` 似，您刚刚添加的字段表示多字段概念。 例如， `homeAddress` 数据类型为“[!UICONTROL 邮政地址]”，数 `mobilePhone` 据类型为“电[!UICONTROL 话号码]”。 您可以选择这些字段中的每个以展开它们，并查看数据类型中包含的其他字段。

![](../images/tutorials/create-schema/personal_details_structure.png)

## 定义新混音 {#define-mixin}

“忠诚[!UICONTROL 会员]”模式用于捕获与忠诚项目成员相关的数据，因此它需要一些特定的忠诚度相关字段。 没有包含必要字段的标准混音，因此您需要定义新混音。

此时，打开“添加混 **[!UICONTROL 合”对话框]** ，选择 **[!UICONTROL “创建新混合”]**。 随后将要求您为混音提 **[!UICONTROL 供显示]****[!UICONTROL 名称和说]** 明。

![](../images/tutorials/create-schema/mixin_create_new.png)

与类名称一样，混音名称应简短，用于描述混音对模式的贡献。 它们也是唯一的，因此您将无法重用该名称，因此必须确保其足够具体。

在本教程中，将新的混音命名为“忠[!UICONTROL 诚度详细]信息”。

选 **[!UICONTROL 择“添加]** 混音”返回 [!DNL Schema Editor]。 “[!UICONTROL Loyalty Details]”现在应显示在画布左侧的 **[!UICONTROL Mixins下，但还没有与它关联的字段，因此“结构”下没有新的字]** 段 ****。

## 向混音添加字段 {#mixin-fields}

现在您已创建“忠[!UICONTROL 诚度]”混音，是时候定义混音将贡献给模式的字段了。

首先，在“混音”部分选择混 **[!UICONTROL 音名]** 。 执行此操作后，混音的属性显示在编辑器的右侧，并且“结构” **[!UICONTROL 下模式]** 的名称旁边会显示“添加字段” **[!UICONTROL 按钮]**。

![](../images/tutorials/create-schema/loyalty_details_structure.png)

选 **[!UICONTROL 择“]** ”旁的“[!DNL Loyalty Members]添加”字段，在结构中创建新节点。 此节点(在 `_tenantId` 本示例中调用)表示您的IMS组织的租户ID，前面有下划线。 租户ID的存在表示您正在添加的字段包含在您组织的命名空间中。

换言之，您添加的字段对您的组织而言是唯一的，并将保存在仅对您的组 [!DNL Schema Registry] 织可访问的特定区域中。 您定义的字段必须始终添加到租户命名空间，以防止与来自其他标准类、混音、数据类型和字段的名称发生冲突。

在该命名空间节点中有一个“[!UICONTROL 新字段]”。 这是“忠诚度细[!UICONTROL 节]”混合的开始。

![](../images/tutorials/create-schema/new_field_loyalty.png)

使用编辑器右侧的控件，通过创建类型为“Object `loyalty`”的字段进行开始，该字段将用于保存与您的忠诚度相关的字段。 完成后，选择“ **[!UICONTROL 应用]**”。

![](../images/tutorials/create-schema/loyalty_object.png)

将应用更改并显示新创建 `loyalty` 的对象。 选择 **[!UICONTROL 对象旁边]** 的“添加字段”以添加其他与忠诚度相关的字段。 将显[!UICONTROL 示“新]建字段”，画 **[!UICONTROL 布的右侧显]** 示“字段属性”部分。

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

每个字段都需要以下信息：

* **[!UICONTROL 字段名称]:** 字段的名称，用驼峰大小写写。 示例：loyaltyLevel
* **[!UICONTROL 显示名称]:** 字段的名称，以标题大小写写写。 示例：忠诚度级别
* **[!UICONTROL 类型]:** 字段的数据类型。 这包括基本标量类型和在中定义的任何数据类型 [!DNL Schema Registry]。 示例： [!UICONTROL 字符串]、整数 [!UICONTROL 、布尔]值 [!UICONTROL 、人员地]址 [!UICONTROL 、地址]、电话号、号等。
* **[!UICONTROL 描述]:** 该字段的可选描述应包含在句子中，最多200个字符。

对象的第一个字 `Loyalty` 段将是一个名为的字符串 `loyaltyId`。 当将新字段的类型设置为“[!UICONTROL String]”时，Field **[!UICONTROL 部分将填充几个用于应用约束的选项，包括]** 默认值 **[!UICONTROL 、]** Format、 ******** Jaximum长度和。

![](../images/tutorials/create-schema/string_constraints.png)

根据所选数据类型，可以使用不同的约束选项。 由于 `loyaltyId` 将是电子邮件地址，请从“格[!UICONTROL 式]”下拉菜 **[!UICONTROL 单中选择]** “email”。 选择 **[!UICONTROL 应用]** ，以应用更改。

![](../images/tutorials/create-schema/loyaltyId_field.png)

## 为混音添加更多字段 {#mixin-fields-2}

现在您已添加了字 `loyaltyId` 段，可以添加其他字段以捕获与忠诚度相关的信息，例如：

* 点（整数）
* 会员自（日期）

通过选择对象上 **[!UICONTROL 的“添加]** ”字段 `loyalty` 并填写所需信息来添加每个字段。

完成后，Loyalty对象将包含忠诚度ID、积分和成员自定义字段。

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## 向混音添加枚举字段 {#enum}

在中定义字段时， [!DNL Schema Editor]您可以应用一些其他选项来对基本字段类型进行限制，以便对字段可包含的数据提供进一步的约束。 下表说明了这些限制的用例：

| 约束 | 描述 |
| --- | --- |
| [!UICONTROL 必需] | 指示数据获取需要此字段。 根据此模式上传到数据集且不包含此字段的任何数据在摄取时都将失败。 |
| [!UICONTROL 阵列] | 指示字段包含一组值，每个值都指定了数据类型。 例如，对数据类型为“String”的字段使用此约[!UICONTROL 束]，指定该字段将包含字符串数组。 |
| [!UICONTROL 枚举] | 指示此字段必须包含来自可能值的枚举列表的值之一。 |
| [!UICONTROL 身份] | 指示此字段是标识字段。 有关标识字段的更多信 [息将在本教程后面提供](#identity-field)。 |
| [!UICONTROL 关系] | 虽然模式关系可以通过使用合并模式来推断， [!DNL Real-time Customer Profile]但这仅适用于共享同一类的模式。 “关 [!UICONTROL 系] ”约束表示此字段引用基于不同类的模式的主标识，这表示两个模式之间的关系。 有关详细信息，请 [参阅有关定义](./relationship-ui.md) 关系的教程。 |

对于本教程 [!DNL "loyalty"] ,模式中的对象需要一个新枚举字段来描述客户的“忠诚度级别”，其中值只能是四个可能的选项之一。 要将此字段添加到模式，请选 **[!UICONTROL 择对象旁]**`loyalty` 边的“添加字段 **[!UICONTROL ”，并填写字段名和显]** 示名的必 **[!UICONTROL 需]**&#x200B;字段。 对于 **[!UICONTROL 类型]**，选择“[!UICONTROL 字符串]”。

![](../images/tutorials/create-schema/loyalty-level-type.png)

选择字段类型后，将显示其他复选框，包括Array、 **[!UICONTROL Enum]**&#x200B;和 **[!UICONTROL Identity]**&#x200B;的复 **[!UICONTROL 选框]**。

选中“ **[!UICONTROL 枚举]** ”复选框以打开 **[!UICONTROL 下面的“枚]** 举值”部分。 在此，您可以为每 **[!UICONTROL 个可接受]** 的忠诚度级别输入Value **[!UICONTROL （在camelCase中）和]** Label（在Title Case中是可选的、对读者友好的名称）。

完成所有字段属性后，选 **[!UICONTROL 择]** “应用”[!DNL loyaltyLevel]将“”字段添加 `loyalty` 到对象。

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## 将多字段对象转换为数据类型 {#datatype}

该对 `loyalty` 象现在包含几个特定于忠诚度的字段，并表示一个可能在其他模式中有用的通用数据结构。 通过 [!DNL Schema Editor] 将这些对象的结构转换为数据类型，您可以轻松应用可重用的多字段对象。

数据类型允许多字段结构的一致使用，并提供比混音更灵活的性能，因为它们可以在模式的任何位置使用。 这是通过将字段的Type值设 **[!UICONTROL 置为]** 在中定义的任何数据类型来完成的 [!DNL Schema Registry]。

要将对 `loyalty` 象转换为数据类型，请在“结 `loyalty` 构”下选择字 **[!UICONTROL 段，然]**&#x200B;后在编辑器右侧的“字段属性”下选 **[!UICONTROL 择“转换为新数]******&#x200B;据类型”。 出现绿色弹出窗口，确认对象已成功转换。

![](../images/tutorials/create-schema/convert-data-type.png)

现在，当您查看“结 **[!UICONTROL 构]**`loyalty`[!DNL Loyalty]”下时，您可以看到字段的数据类型为“”，并且字段旁边有小的锁图标，表示它们不再是单个字段，而是多字段数据类型的一部分。

![](../images/tutorials/create-schema/loyalty_data_type.png)

在将来的模式中，您现在可以将一个 **[!UICONTROL 字段指定为]** “”的类型，并[!DNL Loyalty]且它将自动包括ID、忠诚度级别、成员自身和积分的字段。

## 搜索和筛选模式字段

除了基类提供的字段外，您的模式现在还包含多个混音。 处理较大的模式时，您可以选择左边栏中混合名称旁的复选框，将显示的字段筛选为仅由您感兴趣的混合提供的字段。

![](../images/tutorials/create-schema/filter-by-mixin.png)

如果您在模式中查找特定字段，则还可以使用搜索栏按名称筛选显示的字段，而不管它们在哪个混音中提供。

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>在显示匹配字段时，搜索功能会考虑任何选定的混音过滤器。 如果搜索查询未显示您期望的结果，您可能需要多次检查您是否未过滤掉任何相关混音。

## 将模式字段设置为标识字段 {#identity-field}

模式提供的标准数据结构可以跨多个源识别属于同一个人的数据，从而允许各种下游用例，如分段、报告、数据科学分析等。 要根据个人身份拼接数据，关键字段必须标为适用模式 [!UICONTROL 中的] “身份”字段。

[!DNL Experience Platform] 通过使用中的“标识”复选框，可以轻 **[!UICONTROL 松]** 地指示标识字 [!DNL Schema Editor]段。 但是，您必须根据数据的性质确定哪个字段是最适合用作标识的字段。

例如，可能有数千个忠诚项目成员属于同一“忠诚度级别”，但忠诚项目的每个成员都有一个唯一的(在本例中 `loyaltyId` 是单个成员的电子邮件地址)。 对于每个成 `loyaltyId` 员来说，标识符是唯一标识符，这使它成为标识字段的最佳候选者，而 `loyaltyLevel` 不是。

>[!IMPORTANT]
>
>下面介绍的步骤包括如何向现有模式字段添加标识描述符。 作为在模式本身的结构中定义标识字段的替代方法，您还可以使用字段 `identityMap` 来包含标识信息。
>
>如果您计划使 `identityMap`用，请记住，它将覆盖您直接添加到模式的任何主标识。 有关详细信息， `identityMap` 请参 [阅模式排版指南的基础](../schema/composition.md#identityMap) 中的一节。

在编辑器 **[!UICONTROL 的]** “结构”部分，选择字段 `loyaltyId` ，并在“字段属性”下 **[!UICONTROL 显示]** “标识” **[!UICONTROL 复选框]**。 选中该框和选项，将其设置为主 **[!UICONTROL 标识]** 。 也选中此框。

>[!NOTE]
>
>每个模式只能包含一个主标识字段。 将模式字段设置为主标识后，如果稍后尝试将模式中的其他标识字段设置为主标识，您将收到错误消息。

接下来，您必须从下 **[!UICONTROL 拉菜单中]** 预定义命名空间的列表中提供标识命名空间。 由 `loyaltyId` 于是客户的电子邮件地址，请从下拉[!UICONTROL 菜单中选择]“电子邮件”。 选择 **[!UICONTROL 应用]** ，以确认对字段的 `loyaltyId` 更新。

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>有关标准命名空间及其定义的列表，请参阅 [[!DNL Identity Service] 文档](../../identity-service/troubleshooting-guide.md#standard-namespaces)。

应用更改后，指 `loyaltyId` 纹符号的图标显示为标识字段。 此外，左边栏 [!DNL Loyalty Details] 中的混音列表它下方的身份字段，这样您便可以轻松确定模式中的哪个混音提供模式的身份字段。

![](../images/tutorials/create-schema/identity-applied.png)

现在，所有引入该 `loyaltyId` 字段的数据都将用于帮助识别该个人并整合该客户的单个视图。 要了解有关在中使用身份的更 [!DNL Experience Platform]多信息，请查 [看[!DNL Identity Service]文档](../../identity-service/home.md) 。

## 启用模式以在 [!DNL Real-time Customer Profile] {#profile}

[[!DNL实时客户用户档案]](../../profile/home.md) 利用身份 [!DNL Experience Platform] ，为每位客户提供整体视图。 该服务为客户在与集成的任何系统上的每次交互建立了可靠、360°用户档案的客户属性以及加盖时间戳的帐户 [!DNL Experience Platform]。

要使模式能够与之一起使用， [!DNL Real-time Customer Profile]必须定义主标识。 如果您尝试启用模式而未先定义主标识，则会收到错误消息。

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

要启用“忠诚会员”模式以 [!DNL Profile]在中使用，请[!DNL Loyalty Members]首先在编辑 **[!UICONTROL 器的“结]** 构”部分选择“”。

在编辑器的右侧，显示有关模式的信息，包括其显示名称、说明和类型。 除此信息外，还有一个 **[!UICONTROL 用户档案]** 切换按钮。

![](../images/tutorials/create-schema/profile-toggle.png)

选 **[!UICONTROL 择用户档案]** ，然后出现一个弹出窗口，要求您确认是否要启用模式 [!DNL Profile]。

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>在为模式启用并保 [!DNL Real-time Customer Profile] 存后，将无法禁用该。

选择 **[!UICONTROL 启用]** ，以确认您的选择。 您可以根据需要 **[!UICONTROL 再次选择]** “用户档案”切换以禁用模式，但一旦在启用时保存了模式，就 [!DNL Profile] 不能再将其禁用。

## 后续步骤和其他资源

现在您已完成模式的编写，您可以在画布中看到完整的模式。 选 **[!UICONTROL 择]** “保存”,模式将保存到 [!DNL Schema Library]中，以便由访问 [!DNL Schema Registry]。

您的新模式现在可用于将数据引入 [!DNL Platform]。 请记住，一旦模式被用于摄取数据，只能进行附加更改。 有关模式 [版本控制的更多信息](../schema/composition.md) ，请参阅模式合成的基础知识。

您现在可以按照教程 [在UI中定义模式关系](./relationship-ui.md) ，以向“Loyalty Members”模式添加新关系字段。

“忠诚会员”模式还可供使用API查看和管 [!DNL Schema Registry] 理。 要开始使用API，请阅读开发人员 [[!DNL Schema Registry API] 指南开始](../api/getting-started.md)。

### 视频资源

>[!WARNING]
>
>以 [!DNL Platform] 下视频中显示的UI已过期。 有关最新的UI屏幕截图和功能，请参阅上面的文档。

以下视频演示如何在UI中创建简单 [!DNL Platform] 模式。

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

以下视频旨在加深您对使用混音和类的理解。

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## 附录

以下各节提供了与使用相关的附加信息 [!DNL Schema Editor]。

### Create a new class {#create-new-class}

[!DNL Experience Platform] 提供了根据组织特有的类定义模式的灵活性。

在模式 **[!UICONTROL 工作]** 区中，选 **[!UICONTROL 择创建模式]**，然后从下 **[!UICONTROL 拉菜单中选择]** “浏览”。

![](../images/tutorials/create-schema/browse-classes.png)

将显示一个对话框，允许您从可用类的列表中进行选择。 在对话框顶部，选择“ **[!UICONTROL 创建新类”]**。 然后，您可以为新类提供 **[!UICONTROL 显示名称]** （类的简短、描述性、唯一且用户友好的名称）、 **[!UICONTROL Description]**&#x200B;和Behavior **[!UICONTROL (“]**RecordSeris”或“RecordSeries”)，以获取模式将定义的数据。

![](../images/tutorials/create-schema/create_new_class.png)

>[!IMPORTANT]
>
>构建实现组织定义的类的模式时，请记住，混合仅可用于兼容类。 由于您定义的类是新类，因此“添加混音”对话框中没有列 **[!UICONTROL 出兼容混音]** 。 相反，您需要选择“创 **[!UICONTROL 建新混音]** ”并定义一个混音以用于该类。 下次构建实现新类的模式时，将列出您定义的混音并可供使用。

### 更改模式的类 {#change-class}

在保存模式之前，您可以在初始合成过程中的任意点更改模式的类。

>[!WARNING]
>
>重新分配模式的课程时应非常谨慎。 Mixin只与某些类兼容，因此更改类将重置画布和已添加的任何字段。

要重新分配类，请 **[!UICONTROL 在画布]** 左侧选择“分配”。

![](../images/tutorials/create-schema/assign_class_button.png)

将显示一个对话框，其中显示所有可用类的列表，包括您的组织定义的任何类([!UICONTROL 所有者]为“客户”)以及Adobe定义的标准类。

从列表中选择一个类，在对话框的右侧显示其说明。 您还可以选择 **[!UICONTROL 预览类结构]** ，以查看与该类关联的字段和元数据。 选择 **[!UICONTROL 分配类]** ，继续。

![](../images/tutorials/create-schema/assign_class.png)

此时会打开一个新对话框，要求您确认要分配新类。 选择 **[!UICONTROL 分配]** ，以进行确认。

![](../images/tutorials/create-schema/assign-confirm.png)

确认类更改后，画布将重置，所有合成进度将丢失。
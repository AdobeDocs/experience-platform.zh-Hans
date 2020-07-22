---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用架构编辑器创建架构
topic: tutorials
translation-type: tm+mt
source-git-commit: 661789fa15ea11b0e42060b1b90d74785c04fa1f
workflow-type: tm+mt
source-wordcount: '3376'
ht-degree: 0%

---


# 使用 [!DNL Schema Editor]

提供 [!DNL Schema Registry] 了一个用户界面和RESTful API，您可以从中视图和管理Adobe Experience Platform中的所有资源 [!DNL Schema Library]。 它 [!DNL Schema Library] 包含Adobe、Experience Platform合作伙伴、您所使用应用程序的供应商为您提供的资源，以及您定义并保存到的资源 [!DNL Schema Registry]。

本教程介绍使用模式编辑器创建模式的步骤 [!DNL Experience Platform]。 如果您希望使用模式注册表API编写模式，请先阅读模式注册表开 [发人员指南](../api/getting-started.md) ，然后再 [尝试使用API创建模式](create-schema-api.md)。

本教程还包含定 [义新类的步骤](#create-new-class) ，您随后可以使用它构建模式。

## 入门指南

本教程需要对使用Adobe Experience Platform编辑器时涉及的模式的各个方面进行有效的了解。 在开始本教程之前，请查阅以下概念的文档：

* [!DNL Experience Data Model (XDM)](../home.md): 平台组织客户体验数据的标准化框架。
* [模式合成基础](../schema/composition.md): XDM模式及其构建块的概述，包括类、混合、数据类型和字段。
* [!DNL Real-time Customer Profile](../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

本教程要求您具有访问权限 [!DNL Experience Platform]。 如果您无权访问中的IMS组织，请在继 [!DNL Experience Platform]续操作之前与系统管理员联系。

## 浏览模式工作区中的现有模式 {#browse}

中的模式工 [!DNL Experience Platform] 作区可以 [!DNL Schema Library]可视化模式，使您能够视图和管理所有可用，并创作新。 工作区还包括模式编辑器，在本教程中，您将在画布上构建模式。

登录后 [!DNL Experience Platform]，在左 **[!UICONTROL 侧导航]** 中单击模式，您将转到模式工作区。 您将看到一列表模式(其表示形 [!DNL Schema Library]式)，您可以在其中视图、管理和自定义所有可用的模式。 列表包括模式所基于的名称、类型、类和行为（记录或时间序列），以及模式上次修改的日期和时间。

单击“搜索”栏旁边的筛选器图标，以对注册表中的所有资源（包括类、混合和数据类型）使用筛选功能。

![视图模式库](../images/tutorials/create-schema/schemas_filter.png)

## 创建和命名模式 {#create}

要开始编写模式，请单 **[!UICONTROL 击模式]** 工作区右上角的“创建模式”。

![创建模式按钮](../images/tutorials/create-schema/create_schema_button.png)

出现 *模式编* 辑器。 这是您将在其上创作模式的画布。 当您到达编辑器时，画布的“结构”部分会自 *动创建* “无标题模式”，以便您开始自定义。

![模式编辑器](../images/tutorials/create-schema/schema_editor.png)

在编辑器的右侧是模式属 *性* ，您可以在其中提供模式的名称(使用显 **[!UICONTROL 示名称]** 字段)。 输入名称后，画布会随之更新，以反映模式的新名称。

![模式画布](../images/tutorials/create-schema/name_schema.png)

在为模式决定名称时，需要考虑以下几个重要事项：

* 模式名称应简短且具有描述性，以便以后可以在库中轻松找到模式。
* 模式名称必须是唯一的，这意味着它也应足够具体，以便将来不再重用它。 例如，如果您的组织具有针对不同品牌的单独忠诚项目，则最好将您的模式命名为“Brand A Loyalty Members”，以便轻松与您稍后可能定义的其他与忠诚度相关的模式区分开来。
* 或者，您也可以使用“说明”字段提供有关模式的 **[!UICONTROL 其他]** 信息。

本教程构建一个模式，用于收集与忠诚项目成员相关的数据，因此该模式命名为“忠诚会员”。

## 分配类 {#class}

编辑器的左侧是“合成” *部分* 。 它当前包含两个子部分： *[!UICONTROL 模式]* 和 *[!UICONTROL 课程]*。

既然模式有名称，就该指定模式将实现的类了。 单击 **[!UICONTROL “类]** ”旁 *[!UICONTROL 的“分配]*”。

![](../images/tutorials/create-schema/assign_class_button.png)

将显 *[!UICONTROL 示“指定类]* ”对话框。 此窗口显示所有可用类的列表，包括您的组织定义的任何类（所有者是“客户”）以及Adobe定义的标准类。

单击类名称可显示类的说明。 您还可以选择 **[!UICONTROL 预览类结构]** ，以查看与类关联的字段和元数据。

本教程使用 [!DNL XDM Individual Profile] 类。 单击类旁的单选按钮进行选择，然后单击“指 **[!UICONTROL 定类”]**。

![“指定类”对话框](../images/tutorials/create-schema/assign_class.png)

画布将重新显示。 “ *[!UICONTROL 类]* ”部分现在包含您选择的类([!DNL XDM Individual Profile])，并且类贡献的字段现在 [!DNL XDM Individual Profile] 在“结构”部分 *[!UICONTROL 中可见]* 。

![已分配XDM单个用户档案类](../images/tutorials/create-schema/class_assigned_structure.png)

字段以“fieldName”格式显示 |数据类型”。 本教程稍后提供了在UI中定义模式字段的步骤。

>[!NOTE]
>
>在保 [存模式之前](#change-class) ，您可以在初始合成过程中的任意点更改模式的类，但应当非常小心。 Mixins仅与某些类兼容，因此更改类将重置画布和已添加的任何字段。

## 添加混音 {#mixin}

既然已分配了类，“合 *成* ”部分包含第三个子部分： *[!UICONTROL 混音]*。

您现在可以通过添加混音开始向模式添加字段。 混音是由一个或多个字段组成的组，用于描述特定概念。 本教程使用mixins描述忠诚度项目的成员并捕获关键信息，如姓名、生日、电话号码、地址等。

要添加混音，请单 **击** Mixins *子部* 分中的“添加”。

![](../images/tutorials/create-schema/add_mixin_button.png)

将出 *[!UICONTROL 现“添加混合]* ”对话框。 混合仅用于特定类，因此混合的列表只显示与您选择的类（本例中为类）兼容的 [!DNL XDM Individual Profile] 类。

选择混音旁的单选按钮将为您提供“预览混音结 **[!UICONTROL 构”选项]**。 选择“用户档案人详细信息”混音，然后单击“添 **[!UICONTROL 加混音”]**。

![](../images/tutorials/create-schema/add_mixin_person_details.png)

模式画布将重新显示。 Mixins *[!UICONTROL 部分]* 现在列表“[!UICONTROL 用户档案人详细信息]”混合，而 *[!UICONTROL Structure]* 部分包括混合所贡献的字段。

![](../images/tutorials/create-schema/person_details_structure.png)

此混音在顶级名称“person”下提供数据类型为“Person”的多个字段。 这组字段描述有关个人的信息，包括姓名、出生日期和性别。

>[!NOTE]
>
>请记住，字段可能使用标量类型（如字符串、整数、数组或日期）作为其数据类型，以及中的任何“数据类型”（表示通用概念的字段组） [!DNL Schema Registry]。

请注意，“[!UICONTROL 名]”字段的数据类型为“人[!UICONTROL 员姓名]”，这意味着它也描述了通用概念，并包含与名称相关的子字段，如名字、姓氏和全名。

单击画布中的不同字段，查看它们贡献给模式结构的任何其他字段。

## 添加另一个混音 {#mixin-2}

您现在可以重复相同的步骤来添加另一个混音。 当您此次视图 *[!UICONTROL “添加]* Mixin”对话框时[!UICONTROL ，请注意“]用户档案人详细信息”混音已灰显，且其旁边的单选按钮无法被选中。 这可防止您意外复制已包含在当前模式中的混音。

您现在可以从“添加[!DNL Profile Personal Details" mixin] 混音” *[!UICONTROL 对话框中添加]* “”。

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

添加后，画布将重新显示。 “用户档案[!UICONTROL 个人详细信]息”现在列在“合成 *[!UICONTROL ”部分的Mixins下，并且已在“结构”下添加了家庭地址、移]*****&#x200B;动电话等。

与“名称”字段相似，您刚刚添加的字段表示多字段概念。 例如，“[!UICONTROL homeAddress]”的数据类型为“[!UICONTROL Address]”,“[!UICONTROL mobilePhone]”的数据类型为“Phone Number”。 您可以单击其中的每个字段展开它们，并查看数据类型中包含的其他字段。

![](../images/tutorials/create-schema/personal_details_structure.png)

## 定义新混音 {#define-mixin}

“忠诚[!UICONTROL 会员]”模式用于捕获与忠诚项目成员相关的数据，因此它需要一些特定的忠诚度相关字段。 没有包含必要字段的标准混音，因此您需要定义新混音。

此时，打开“添加混 *[!UICONTROL 合”对话框]* ，选择 **[!UICONTROL “创建新混合”]**。 随后将要求您为混音提 **[!UICONTROL 供显示]****[!UICONTROL 名称和说]** 明。

![](../images/tutorials/create-schema/mixin_create_new.png)

与类名称一样，混音名称应简短，用于描述混音对模式的贡献。 它们也是唯一的，因此您将无法重用该名称，因此必须确保其足够具体。

在本教程中，将新的混音命名为“忠[!UICONTROL 诚度详细]信息”。

单击 **[!UICONTROL “添加混合]** ”以返回到模式编辑器。 “[!UICONTROL Loyalty Details]”现在应显示在画布左侧的 *[!UICONTROL Mixins下，但还没有与它关联的字段，因此“结构”下没有新的字]* 段 **。

## 向混音添加字段 {#mixin-fields}

现在您已创建“忠[!UICONTROL 诚度]”混音，是时候定义混音将贡献给模式的字段了。

要开始，请单击“混音”部分中的混 *[!UICONTROL 音名]* 。 完成此操作后， *[!UICONTROL 编辑器的右侧将显示]* “Mixin Properties”（混合属性），并且“Structure”（结构）下的模式名 **[!UICONTROL 称旁将显示“Add Field]** ”（添加字段） *[!UICONTROL 按钮]*。

![](../images/tutorials/create-schema/loyalty_details_structure.png)

单 **[!UICONTROL 击“Loyalty]** Members”旁[!UICONTROL 的“添加字段]”，在结构中创建新节点。 此节点（在本示例中称为“_tenantId”）表示您的IMS组织的租户ID，前面有下划线。 租户ID的存在表示您正在添加的字段包含在您组织的命名空间中。

换言之，您添加的字段对您的组织来说是独一无二的，并将保存在仅可 [!DNL Schema Registry] 供IMS组织访问的特定区域中。 您定义的字段必须始终添加到您的命名空间中，以防止与来自其他标准类、混音、数据类型和字段的名称发生冲突。

在该命名空间节点中有一个“[!UICONTROL 新字段]”。 这是“忠诚度细[!UICONTROL 节]”混合的开始。

![](../images/tutorials/create-schema/new_field_loyalty.png)

使 *[!UICONTROL 用编辑器]* 右侧的字段属性，通过创建类型为“Object[!UICONTROL ”的“loyalty]”字段来开始该字段，该字段将用于保存您的忠诚度相关字段。 完成后，单击“ **[!UICONTROL 应用]**”。

![](../images/tutorials/create-schema/loyalty_object.png)

将应用更改并显示新创建的“[!UICONTROL 忠诚度]”对象。 单 **[!UICONTROL 击对象旁]** “添加字段”以添加其他与忠诚度相关的字段。 将显示“新建字段” *[!UICONTROL ，画布]* 右侧将显示“字段属性”部分。

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

每个字段都需要以下信息：

* **[!UICONTROL 字段名称]:**字段的名称，用驼峰大小写写。 示例： loyaltyLevel
* **[!UICONTROL 显示名称]:**字段的名称，以标题大小写写写。 示例： 忠诚度级别
* **[!UICONTROL 类型]:**字段的数据类型。 这包括基本标量类型和在中定义的任何数据类型[!DNL Schema Registry]。 示例： 字符串、整数、布尔值、人员、地址、电话号码等。
* **[!UICONTROL 描述]:**该字段的可选描述应包含在句子中。 （最多200个字符。）

Loyalty对象的第一个字段将是一个名为“loyaltyId”[!UICONTROL 的字符串]。 当将新字段的类型设置为“[!UICONTROL String]”时，“字段属性 *[!UICONTROL ”窗口将填充多个用于应用约束的选项，]* 包括默认值 **[!UICONTROL 、]**&#x200B;格式、 ********、最大长度。

![](../images/tutorials/create-schema/string_constraints.png)

根据所选数据类型，可以使用不同的约束选项。 由于“[!UICONTROL loyaltyId]”将是电子邮件地址，因此从“格式”下拉菜单中选 **[!UICONTROL 择“email]** ”。 选择 **[!UICONTROL 应用]** ，以应用更改。

![](../images/tutorials/create-schema/loyaltyId_field.png)

## 添加更多字段以混音 {#mixin-fields-2}

现在您已添加“[!UICONTROL loyaltyId]”字段，您可以添加其他字段来捕获与忠诚度相关的信息，例如：

* 点（整数）
* 会员自（日期）

通过单击忠诚度对象 **[!UICONTROL 上的“添加字段]** ”并填写所需的信息，可添加每个字段。

完成后，Loyalty对象将包含以下字段： 忠诚度ID、积分和会员。

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## 添加“枚举”字段以混音 {#enum}

在模式编辑器中定义字段时，您可以应用一些其他选项来对基本字段类型进行限制，以便对字段可以包含的数据提供进一步的约束。

此示例为“忠诚度[!UICONTROL 级别]”字段，其中值只能是四个可能选项之一。 要将此字段添加到模式，请 **[!UICONTROL 单击]** “loyalty”对象旁[!UICONTROL 的“添加字]段”，并填写“字段属性”下的 *[!UICONTROL 必填字段]*。

对于 **[!UICONTROL 类型]**，选择“字符串”，您将看到Array、Enum和Identity **[!UICONTROL Adobe的其]**&#x200B;他复选 ********&#x200B;框出现。

选中枚 **[!UICONTROL 举]** 复选框以打开 *[!UICONTROL 下面的枚]* 举值。 在此，您可以为每 **[!UICONTROL 个可接受]** 的忠诚度级别输入Value **[!UICONTROL （在camelCase中）和]** Label（在Title Case中是可选的、对读者友好的名称）。

完成所有字段属性后，单 **[!UICONTROL 击]** “应用[!UICONTROL ”],“loyaltyLevel”字段将添加到“loyalty”对象。

![](../images/tutorials/create-schema/loyalty_level_enum.png)

有关可用附加约束的更多信息：

* **[!UICONTROL 必需]:**指示数据获取需要此字段。 根据此模式上传到数据集且不包含此字段的任何数据在摄取时都将失败。
* **[!UICONTROL 阵列]:**指示字段包含一组值，每个值都指定了数据类型。 例如，选择“字符串”的数据类型并选中“数组”复选框表示字段将包含字符串数组。
* **[!UICONTROL 枚举]:**指示此字段必须包含来自可能值的枚举列表的值之一。
* **[!UICONTROL 身份]:**指示此字段是标识字段。 有关标识字段的更多信[息将在本教程后面提供](#identity-field)。

## 将多字段对象转换为数据类型 {#datatype}

添加多个特定于忠诚度的字段后，“[!UICONTROL loyalty]”对象现在包含一个公共数据结构，该结构可能在其他模式中有用。

当您认为多字段结构可以重复使用，并且希望能够灵活地在其他位置使用相同的模式结构时，编辑器可以将该结构转换为数据类型。

数据类型允许多字段结构的一致使用，并提供比混音更灵活的性能，因为它们可以在模式的任何位置使用。 这是通过将混合中 **[!UICONTROL 字段的]** “类型”设置为注册表中定义的任何数据类型来完成的。

要将“[!UICONTROL loyalty]”对象转换为数据类型，请单击“结构”下的“loyalty”字段，然后 *[!UICONTROL 选择Field Properties Properties下编辑器右侧的“Convert to New Data Type]* ”（转换为新数据类型） ******。 出现一个小的绿色弹出窗口，确认“[!UICONTROL 对象已转换为数据类型]”。

现在，当您在“结 *[!UICONTROL 构]*”下查看时，您会看到“[!UICONTROL loyalty]”字段的数据类型为“Loyalty”，并且这些字段旁边有小的锁图标，表示它们不再是单个字段，而是多字段结构的一部分。

在将来的模式中，您现在可以为 **[!UICONTROL 字段分配]** “Loyalty”的类[!UICONTROL 型]，并自动包括Loyalty Level、Points、Member Since和Loyalty ID字段。

![](../images/tutorials/create-schema/loyalty_data_type.png)

## 将模式字段设置为标识字段 {#identity-field}

模式用于将数据引入 [!DNL Experience Platform]其中，而数据最终用于识别个体并整合来自多个来源的信息。 要帮助处理此过程，键字段可标记为“[!UICONTROL Identity]”字段。

[!DNL Experience Platform] 通过使用中的“标识”复选框，可以轻 **[!UICONTROL 松]** 地指示标识字 [!DNL Schema Editor]段。

例如，忠诚度项目中可能有数千个成员属于同一“级别”，但忠诚度项目的每个成员都有唯一的“loyaltyId”（在此实例中为单个成员的电子邮件地址）。 “loyaltyId”是每个成员的唯一标识符，这一事实使它成为标识字段的最佳候选者，而“level”则不是。

在编辑 *[!UICONTROL 器的]* “结构”部分，单击您创建的“[!UICONTROL loyaltId]”字段，您将看到“Identity **[!UICONTROL ”复选框显示在“字段属]****&#x200B;性”下。 选中该框，您将可以选择将其设置为主 **[!UICONTROL 标识]**。 同时选中该框。

接下来，您必须提供 **[!UICONTROL 标识名称空间]**。 有几个预定义的命名空间，但由于“[!UICONTROL loyaltyId]”是成员的电子邮件地址，因此请从下拉列表中选择“电子邮件”。 您现在可以单 **[!UICONTROL 击]** “应用”以确认对“loyaltyId”字段的更新。

现在，所有引入“[!UICONTROL loyaltyId]”字段的数据都将用于帮助识别该个人并整合该客户的单个视图。

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>将模式字段设置为主标识后，如果稍后尝试将模式中的其他字段设置为主标识，您将收到错误消息。 每个模式只能包含一个主标识字段。

要进一步了解如何使用身份，请查阅 [!DNL Identity Service](../../identity-service/home.md) 文档。

<!-- ## Relationship

Schemas define a static view of a concept, but do not provide specific details on how data based on these schemas (datasets, etc) may relate to one another. Adobe Experience Platform allows you to describe these relationships through the **Relationship** checkbox in the schema editor. 

In order to define a relationship, click on the field and check the **Relationship** checkbox on the right-side of the canvas. 

![](../images/tutorials/create-schema/relationship.png)

More information about relationships and other schema metadata can be found in the [Schema Registry API Developer Guide](../schema_registry_developer_guide.md). -->

## 启用模式以在 [!DNL Real-time Customer Profile] {#profile}

模式编辑器允许模式与一起使用 [!DNL Real-time Customer Profile](../../profile/home.md)。 [!DNL Profile] 通过构建可靠、360°的客户属性用户档案以及客户在与之集成的任何系统中进行的每次交互的时间戳帐户，为每位客户提供全面视图 [!DNL Experience Platform]。

要使模式能够与之一起使用， [!DNL Real-time Customer Profile]必须定义主标识。 如果您尝试启用模式而未先定义主标识，则会收到“缺少主标识”错误消息。

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

要启用“忠诚会员”模式以在 [!DNL Profile]中使用，请首先单击编辑器“结构” *部分* 中的“忠诚会员”。

在编辑器的右侧的“模式属性” *下*，将显示有关模式的信息，包括其显示名称、说明和类型。 除此信息外，还有一个名为用户档案的切换 **[!UICONTROL 按钮]**。

![](../images/tutorials/create-schema/unified_profile_toggle.png)

单 **[!UICONTROL 击用户档案]** ，然后出现一个弹出窗口，要求您确认是否要为启用模式 [!DNL Profile]。

![](../images/tutorials/create-schema/enable_unified_profile.png)

>[!NOTE]
>
>在为模式启用并保 [!DNL Real-time Customer Profile] 存后，将无法禁用该。

## 后续步骤和其他资源

现在您已完成编写“忠诚[!UICONTROL 会员]”模式，您可以在编辑器的“结构” *部分看到* 完整模式。 单 **[!UICONTROL 击]** “保存 [!DNL Schema Library]”,模式将保存到中， [!DNL Schema Registry]供用户访问。

您的新模式现在可用于将数据引入 [!DNL Platform]。 请记住，一旦模式被用于摄取数据，只能进行附加更改。 有关模式 [版本控制的更多信息](../schema/composition.md) ，请参阅模式合成的基础知识。

“忠[!UICONTROL 诚会员]”模式也可供使用API查看和管 [!DNL Schema Registry] 理。 要开始使用API，请阅读开始注册表API开 [发人员指南进行模式](../api/getting-started.md)。

>[!WARNING]
>
>以 [!DNL Platform] 下视频中显示的UI已过期。 有关最新的UI屏幕截图和功能，请参阅上面的文档。

以下视频演示如何在UI中创建简单 [!DNL Platform] 模式。

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

以下视频旨在加深您对使用混音和类的理解。

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## 附录

以下信息是模式编辑器教程的补充。

### Create a new class {#create-new-class}

[!DNL Experience Platform] 提供了根据组织特有的类定义模式的灵活性。

在模式编 *[!UICONTROL 辑器的]* “类”部分中单 **[!UICONTROL 击]** “分 *[!UICONTROL 配”，打开]* “分配类”对话框。 在对话框中，选择“ **[!UICONTROL 创建新类”]**。

然后，您可以为新类提供 **[!UICONTROL 显示名称]** （类的简短、描述性、唯一且用户友好的名称）、 **[!UICONTROL 说明]**&#x200B;和行为( **[!UICONTROL “”]**或“时间序列”)，以获取模式将定义的数据。

![新建类详细信息](../images/tutorials/create-schema/create_new_class.png)

>[!NOTE]
>
>构建实现组织定义的类的模式时，请记住，混合仅可用于兼容类。 由于您定义的类是新类，因此“添加混音”对话框中未列 *出兼容混音* 。 相反，您需要选择“创 **[!UICONTROL 建新混音]** ”并定义一个混音以用于该类。 下次构建实现新类的模式时，将列出您定义的混音并可供使用。

### 更改模式的类 {#change-class}

在初始模式合成过程中的任何时间，在保存模式之前，您都可以更改模式所基于的类。

>[!WARNING]
>
>在更改课程之前，请务必小心。 Mixins仅与某些类兼容，因此更改类会重置画布并删除已添加到该点的所有字段。

要更改类，请在编辑 **[!UICONTROL 器的]** “合 *[!UICONTROL 成]* ”部分中单 *[!UICONTROL 击“类]* ”旁边的“分配”。

当“分 *[!UICONTROL 配类]* ”对话框打开时，您可以从可用列表中选择新类。 单 **[!UICONTROL 击“分配]** 类”，此时将打开一个新对话框，要求您确认要分配新类。

![更改类](../images/tutorials/create-schema/assign_new_class_warning.png)

如果您确认类更改，画布将重置，并且所有合成进度都将丢失。
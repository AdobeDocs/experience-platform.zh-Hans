---
keywords: Experience Platform；主页；热门主题；ui；UI；UI；XDM；XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；架构编辑器；架构编辑器；架构；架构；架构；架构；创建
solution: Experience Platform
title: 使用架构编辑器创建架构
type: Tutorial
description: 本教程介绍了在 Experience Platform 中使用架构编辑器创建架构的步骤。
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '4915'
ht-degree: 1%

---

# 使用[!DNL Schema Editor]创建架构

Adobe Experience Platform用户界面允许您在称为[!DNL Schema Editor]的交互式可视画布中创建和管理[!DNL Experience Data Model] (XDM)架构。 本教程介绍如何使用[!DNL Schema Editor]创建架构。

出于演示目的，本教程中的步骤涉及创建一个描述客户忠诚度计划成员的示例架构。 虽然您可以使用这些步骤创建其他架构以满足您自己的目的，但建议您先创建示例架构并学习[!DNL Schema Editor]的功能。

>[!NOTE]
>
>如果您要将CSV数据摄取到Experience Platform，则可以[将该数据映射到由AI生成的推荐](../../ingestion/tutorials/map-csv/recommendations.md)（当前为测试版）创建的XDM架构，而无需自己手动创建架构。
>
>如果您希望使用[!DNL Schema Registry] API编写架构，请先阅读[[!DNL Schema Registry] 开发人员指南](../api/getting-started.md)，然后再尝试阅读有关[使用API创建架构](create-schema-api.md)的教程。

## 快速入门

本教程需要对架构创建所涉及的Adobe Experience Platform各个方面有一定的了解。 在开始本教程之前，请查看文档以了解以下概念：

* [[!DNL Experience Data Model (XDM)]](../home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../schema/composition.md)： XDM架构及其构建块的概述，包括类、架构字段组、数据类型和单个字段。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

## 打开[!UICONTROL 架构]工作区 {#browse}

[!DNL Experience Platform] UI中的[!UICONTROL 架构]工作区提供了[!DNL Schema Library]的可视化图表，允许您查看管理组织可用的架构。 该工作区还包括[!DNL Schema Editor]，在本教程中，您可以在该画布上撰写架构。

登录[!DNL Experience Platform]后，在左侧导航中选择&#x200B;**[!UICONTROL 架构]**&#x200B;以打开&#x200B;**[!UICONTROL 架构]**&#x200B;工作区。 **[!UICONTROL 浏览]**&#x200B;选项卡显示架构列表（[!DNL Schema Library]的表示形式），供您查看和自定义。 此列表包括架构所基于的名称、类型、类和行为（记录或时间序列），以及上次修改架构的日期和时间。

有关详细信息，请参阅[在UI](../ui/explore.md)中浏览现有XDM资源的指南。

## 创建架构并为其命名 {#create}

要开始撰写架构，请在&#x200B;**[!UICONTROL 架构]**&#x200B;工作区的右上角选择&#x200B;**[!UICONTROL 创建架构]**。

![突出显示了[!UICONTROL 架构]工作区[!UICONTROL 浏览]选项卡和[!UICONTROL 创建架构]。](../images/tutorials/create-schema/create-schema-button.png)

出现[!UICONTROL 创建架构]对话框。 在此对话框中，您可以选择通过添加字段和字段组手动创建架构，也可以上传CSV文件并使用ML算法生成架构。 从对话框中选择架构创建工作流。

![使用工作流选项创建架构对话框并选择高亮显示。](../images/tutorials/create-schema/create-a-schema-dialog.png)

### [!BADGE Beta]{type=Informative}手动或ML辅助的架构创建 {#manual-or-assisted}

要了解如何使用ML算法根据上传的文件推荐架构结构，请参阅[机器学习辅助架构创建指南](../ui/ml-assisted-schema-creation.md)。 本UI指南重点介绍手动创建工作流。

### 选择基类 {#choose-a-class}

出现[!UICONTROL 创建架构]工作流。 接下来，为架构选择一个基类。 您可以选择[!UICONTROL XDM Individual Profile]和[!UICONTROL XDM ExperienceEvent]的核心类，或者[!UICONTROL Other]（如果这些类不适合您的用途）。 [!UICONTROL Other]类选项允许您[创建新类](#create-new-class)或从其他预先存在的类中进行选择。

有关这些类的详细信息，请参阅[[!UICONTROL XDM个人配置文件]](../classes/individual-profile.md)和[[!UICONTROL XDM ExperienceEvent]](../classes/experienceevent.md)文档。 在本教程中，请选择&#x200B;**[!UICONTROL XDM Individual Profile]**，然后选择&#x200B;**[!UICONTROL 下一步]**。

![包含[!UICONTROL XDM单个配置文件]选项和[!UICONTROL 下一个]突出显示的[!UICONTROL 创建架构]工作流。](../images/tutorials/create-schema/individual-profile-base-class.png)

### 命名并查看 {#name-and-review}

选择类后，将显示[!UICONTROL 名称和审阅]部分。 在此部分中，您会提供用于标识架构的名称和描述。 在决定架构的名称时，需要考虑以下几个重要因素：

* 架构名称应简短且具有描述性，以便之后可以轻松找到架构。
* 架构名称必须是唯一的，这意味着它还应该足够具体，以便将来不会重复使用。 例如，如果贵组织为不同品牌制定了单独的忠诚度计划，则明智的做法是将您的架构命名为“品牌A忠诚度成员”，以便轻松区别于您稍后可能定义的其他忠诚度相关架构。
* 您还可以使用架构描述提供有关架构的任何其他上下文信息。

本教程包含一个架构以摄取与忠诚度计划成员相关的数据，因此该架构名为“[!DNL Loyalty Members]”。

架构&#x200B;的基本结构（由类提供）显示在画布中，供您查看和验证选定的类和架构结构。

在文本字段中输入人性化的[!UICONTROL 架构显示名称]。 接下来，输入适当的描述以帮助识别您的架构。 当您查看了架构结构并且满意您的设置时，请选择&#x200B;**[!UICONTROL 完成]**&#x200B;以创建您的架构。

![高亮显示[!UICONTROL 创建架构]工作流的[!UICONTROL 名称和审核]部分，该工作流具有[!UICONTROL 架构显示名称]、[!UICONTROL 描述]和[!UICONTROL 完成]。](../images/ui/resources/schemas/name-and-review.png)

### 编写架构 {#compose-your-schema}

出现[!DNL Schema Editor]。 这是您将在其中构建架构的画布。 当您到达编辑器时，会在画布的&#x200B;**[!UICONTROL 结构]**&#x200B;部分自动创建自标题架构，以及您选择的基类中包含的标准字段。 架构的分配类也在&#x200B;**[!UICONTROL 合成]**&#x200B;部分的&#x200B;**[!UICONTROL 类]**&#x200B;下列出。

>[!NOTE]
>
您可以从&#x200B;**[!UICONTROL 架构属性]**&#x200B;侧边栏中更新架构的显示名称和可选描述。 输入新名称后，画布会自动更新以反映架构的新名称。

![基类和架构图突出显示的架构编辑器。](../images/tutorials/create-schema/loyalty-members-schema-editor.png)

>[!NOTE]
>
在保存架构之前，您可以在初始组合过程中随时[更改架构](#change-class)的类，但应极其谨慎地执行此操作。 字段组仅与某些类兼容，因此更改该类将重置画布和您已添加的所有字段。

## 添加字段组 {#field-group}

您现在可以通过添加字段组开始向架构添加字段。 字段组是由一个或多个字段组成的组，这些字段通常一起用于描述特定概念。 本教程使用字段组描述忠诚度计划的成员并捕获关键信息，如姓名、生日、电话号码、地址等。

要添加字段组，请在&#x200B;**[!UICONTROL 字段组]**&#x200B;子部分中选择&#x200B;**[!UICONTROL 添加]**。

![突出显示了“添加字段组”按钮的架构编辑器。](../images/tutorials/create-schema/add-field-group-button.png)

此时将显示一个新对话框，其中显示了可用字段组的列表。 每个字段组仅用于特定类，因此该对话框仅列出与您选择的类（在本例中为[!DNL XDM Individual Profile]类）兼容的字段组。 如果您使用的是标准XDM类，则字段组的列表将根据使用流行程度智能排序。

![[!UICONTROL 添加字段组]对话框。](../images/tutorials/create-schema/field-group-popularity.png)

您可以在左边栏中选择一个过滤器，以将标准字段组列表缩小到特定[行业](../schema/industries/overview.md)，如零售、金融服务和医疗保健。

![与突出显示的行业字段组的[!UICONTROL 添加字段组]对话框。](../images/tutorials/create-schema/industry-field-groups.png)

从列表中选择字段组会导致该字段组显示在右边栏中。 如果需要，您可以选择多个字段组，并在确认之前将每个字段组添加到右边栏中的列表。 此外，当前选定的字段组的右侧会显示一个图标，允许您预览它提供的字段的结构。

![突出显示所选字段组预览图标的[!UICONTROL 添加字段组]对话框。](../images/tutorials/create-schema/preview-field-group-button.png)

预览字段组时，右边栏中提供该字段组架构的详细说明。 您还可以浏览提供的画布中的字段组字段。 当您选择不同的字段时，右边栏会更新，以显示有关所涉字段的详细信息。 完成预览后选择&#x200B;**[!UICONTROL 上一步]**&#x200B;以返回字段组选择对话框。

![预览了包含人口统计详细信息字段组的[!UICONTROL 预览字段组]对话框。](../images/tutorials/create-schema/preview-field-group.png)

在本教程中，选择&#x200B;**[!UICONTROL 人口统计详细信息]**&#x200B;字段组，然后选择&#x200B;**[!UICONTROL 添加字段组]**。

![已选中“人口统计详细信息”字段组的[!UICONTROL 添加字段组]对话框并突出显示[!UICONTROL 添加字段组]。](../images/tutorials/create-schema/demographic-details.png)

此时将重新显示架构画布。 **[!UICONTROL 字段组]**&#x200B;部分现在列出“[!UICONTROL 人口统计详细信息]”，而&#x200B;**[!UICONTROL 结构]**&#x200B;部分包含字段组贡献的字段。 您可以在&#x200B;**[!UICONTROL 字段组]**&#x200B;部分下选择字段组的名称，以突出显示它在画布中提供的特定字段。

![突出显示了“人口统计详细信息”字段组的架构编辑器。](../images/tutorials/create-schema/demographic-details-structure.png)

>[!NOTE]
>
在架构编辑器中，标准(Adobe生成的)类和字段组以挂锁图标（![A挂锁图标）表示。](/help/images/icons/lock-closed.png)的问题。挂锁显示在左边栏中的类或字段组名称旁边，以及架构图中作为系统生成资源一部分的任意字段旁边。
>
![带有挂锁图标的架构编辑器突出显示](../images/ui/explore/padlock-icon-highlight.png)

此字段组在顶级名称`person`下分配多个具有数据类型的字段 "[!UICONTROL 人员]”。 这一组字段描述有关个人的信息，包括姓名、出生日期和性别。

>[!NOTE]
>
请记住，字段可以使用标量类型 (such 作为字符串、整数、数组或日期)以及任何数据类型 (a 在[!DNL Schema Registry]中定义的表示通用概念的字段组)。

请注意，`name`字段具有数据类型 of “[!UICONTROL 全名]”，表示它也描述了常见概念并包含与名称相关的子字段，如名字、姓氏、礼貌标题和后缀。

选择画布中的不同字段以显示它们为架构结构贡献的任何其他字段。

## 添加更多字段组 {#field-group-2}

您现在可以重复相同的步骤来添加另一个字段组。 当您这次查看&#x200B;**[!UICONTROL 添加字段组]**&#x200B;对话框时，请注意，“[!UICONTROL 人口统计详细信息]”字段组已灰显，并且无法选中它旁边的复选框。 这样可防止意外重复您已在当前架构中包含的字段组。

在本教程中，从列表中选择标准字段组&#x200B;**[!UICONTROL 个人联系人详细信息]**&#x200B;和&#x200B;**[!UICONTROL 忠诚度详细信息]**，然后选择&#x200B;**[!UICONTROL 添加字段组]**&#x200B;以将其添加到架构中。

![已选定两个新字段组且[!UICONTROL 已突出显示添加字段组]的[!UICONTROL 添加字段组]对话框。](../images/tutorials/create-schema/more-field-groups.png)

画布将重新显示，其中在&#x200B;**[!UICONTROL 合成]**&#x200B;部分的&#x200B;**[!UICONTROL 字段组]**&#x200B;下列出的已添加字段组，并且其复合字段已添加到架构结构中。

![突出显示具有新复合架构结构的架构编辑器。](../images/tutorials/create-schema/updated-structure.png)

## 定义自定义字段组 {#define-field-group}

[!UICONTROL 忠诚度成员]架构用于捕获与忠诚度计划成员相关的数据，而您添加到该架构中的标准[!UICONTROL 忠诚度详细信息]字段组提供了其中的大多数数据，包括计划类型。 points, 加入日期等。

但是，在某些情况下，您可能希望包含标准字段组未涵盖的其他自定义字段，以便实现用例。 在添加自定义忠诚度字段的情况下，您有两个选项：

1. 创建新的自定义字段组以捕获这些字段。 本教程将介绍此方法。
1. 使用自定义字段扩展标准[!UICONTROL 忠诚度详细信息]字段组。 这会导致[!UICONTROL 忠诚度详细信息]转换为自定义字段组，原始标准字段组将不再可用。 有关[将自定义字段添加到标准字段组的结构](../ui/resources/schemas.md#custom-fields-for-standard-groups)的更多信息，请参阅[!UICONTROL 架构] UI指南。

要创建新字段组，请在&#x200B;**[!UICONTROL 字段组]**&#x200B;子部分中选择&#x200B;**[!UICONTROL 添加]**（与以前类似），但这次在出现的对话框顶部附近选择&#x200B;**[!UICONTROL 新建字段组]**。 然后，系统会要求您提供新字段组的显示名称和描述。 在本教程中，将新的字段组命名为“[!DNL Custom Loyalty Details]”，然后选择&#x200B;**[!UICONTROL 添加字段组]**。

![与[!UICONTROL 创建新字段组]、[!UICONTROL 显示名称]和[!UICONTROL 描述]一起突出显示的[!UICONTROL 添加字段组]对话框。](../images/tutorials/create-schema/create-new-field-group.png)

>[!NOTE]
>
与类名一样，字段组名称应简短而简单，描述字段组对架构的贡献。 这些名称也是唯一的，因此您将无法重用该名称，因此必须确保它足够具体。

&quot;[!DNL Custom Loyalty Details]&quot;现在应显示在画布左侧的&#x200B;**[!UICONTROL 字段组]**&#x200B;下，但尚未有与其关联的字段，因此&#x200B;**[!UICONTROL 结构]**&#x200B;下未显示任何新字段。

## 将字段添加到字段组 {#field-group-fields}

现在您已经创建了&quot;[!DNL Custom Loyalty Details]&quot;字段组，接下来该定义该字段组将参与到架构中的字段。

要开始，请选择画布中架构名称旁边的&#x200B;**加号(+)**&#x200B;图标。

![突出显示加号图标的架构编辑器。](../images/tutorials/create-schema/add-field.png)

画布中显示“[!UICONTROL 无标题字段]”占位符，右边栏更新以显示该字段的配置选项。

![已突出显示[!UICONTROL 无标题字段]和架构[!UICONTROL 字段属性]的架构编辑器。](../images/tutorials/create-schema/untitled-field.png)

在此方案中，架构需要具有对象类型 field 该报表详细描述了人员当前的忠诚度级别。 使用右边栏中的控件，开始创建具有类型的`loyaltyTier`字段 "用于保存相关字段的[!UICONTROL 对象]。

在&#x200B;**[!UICONTROL 分配给]**&#x200B;下，您必须选择要将该字段分配到的字段组。 请记住，所有架构字段都属于类或字段组，由于此架构使用标准类，因此您的唯一选项是选择字段组。 开始键入名称“[!DNL Custom Loyalty Details]”，然后从列表中选择字段组。

完成后，选择&#x200B;**[!UICONTROL 应用]**。

![已将忠诚度层对象添加到架构[!UICONTROL 字段属性]的架构编辑器突出显示。](../images/tutorials/create-schema/loyalty-tier-object.png)

应用更改并显示新创建的`loyaltyTier`对象。 由于这是一个自定义字段，因此它会自动嵌套在您组织的租户ID命名空间中的对象中，前面加有下划线（本示例中为`_tenantId`）。

![架构图表中突出显示了租户ID和忠诚度级别的架构编辑器。](../images/tutorials/create-schema/tenant-id.png)

>[!NOTE]
>
租户ID对象的存在表示您要添加的字段包含在您的组织的命名空间中。
>
换言之，您添加的字段对于您的组织是唯一的，并将保存在仅供您的组织访问的特定区域的[!DNL Schema Registry]中。 必须始终将您定义的字段添加到租户命名空间，以防止与其他标准类、字段组、数据类型、 and 字段。

选择`loyaltyTier`对象旁边的&#x200B;**加号(+)**&#x200B;图标以开始添加子字段。 此时会出现一个新的字段占位符，**[!UICONTROL 字段属性]**&#x200B;部分显示在画布的右侧。

![架构编辑器中具有租户ID和新的子字段已添加到架构图中的忠诚度级别。](../images/tutorials/create-schema/new-field-in-loyalty-tier-object.png)

每个字段都需要以下信息：

* **[!UICONTROL 字段名称]：**&#x200B;字段的名称，最好用驼峰式大小写写。 不允许使用空格字符。 这是用于在代码和其他下游应用程序中引用字段的名称。
   * 示例： loyaltyLevel
* **[!UICONTROL 显示名称]：**&#x200B;字段的名称，用标题大小写表示。 这是查看或编辑架构时将在画布中显示的名称。
   * 示例：忠诚度级别
* **[!UICONTROL 类型]：**&#x200B;数据类型 of 字段。 这包括基本标量类型 and 任何数据类型 defined 在[!DNL Schema Registry]中。 示例： [!UICONTROL String]、[!UICONTROL Integer]、[!UICONTROL Boolean]、[!UICONTROL Person]、[!UICONTROL Address]、[!UICONTROL 电话号码]等。
* **[!UICONTROL 描述]：**&#x200B;字段的可选描述应包含最多200个字符。

`loyaltyTier`对象的第一个字段将是一个名为`id`的字符串，表示忠诚度会员当前层的ID。 由于该公司根据不同的因素为每个客户设置了不同的忠诚度级别阈值，因此每个忠诚度会员的层ID都是唯一的。 设置新字段的类型 to “[!UICONTROL 字符串]”和&#x200B;**[!UICONTROL 字段属性]**&#x200B;部分会使用多个应用约束的选项进行填充，包括默认值、格式和最大长度。 请参阅有关数据验证字段[最佳实践的文档](../schema/best-practices.md#data-validation-fields)以了解更多信息。

![架构编辑器高亮显示新ID字段的字段属性值。](../images/tutorials/create-schema/string-constraints.png)

由于`id`将是一个随机生成的自由格式字符串，因此无需进一步约束。 选择&#x200B;**[!UICONTROL 应用]**&#x200B;以应用更改。

![已添加并突出显示ID字段的架构编辑器。](../images/tutorials/create-schema/id-field-added.png)

## 向字段组添加更多字段 {#field-group-fields-2}

现在您已经添加了`id`字段，接下来可以添加其他字段以获取忠诚度等级信息，例如：

* 当前点阈值（整数）：成员必须保持为保留在当前层中的最小忠诚度点数。
* 下一层点阈值（整数）：成员必须累计以毕业到下一层的忠诚度点数。
* 有效日期（日期时间）：忠诚度成员加入此层的日期。

要将每个字段添加到架构，请选择`loyalty`对象旁边的&#x200B;**加号(+)**&#x200B;图标并填写所需信息。

完成后，`loyaltyTier`对象将包含`id`、`currentThreshold`、`nextThreshold`和`effectiveDate`的字段。

![高亮显示忠诚度层对象的架构编辑器。](../images/tutorials/create-schema/loyalty-tier-object-fields.png)

## 向字段组添加一个枚举字段 {#enum}

在[!DNL Schema Editor]中定义字段时，有一些其他选项可应用到基本字段类型 in 以便为该字段可以包含的数据提供进一步限制。 下表说明了这些限制的用例：

| 约束 | 描述 |
| --- | --- |
| [!UICONTROL 必需] | 指示字段是进行数据摄取所必需的。 摄取后，任何上传到基于此架构、不包含此字段的数据集的数据都将失败。 |
| [!UICONTROL 数组] | 指示字段包含一个值数组，每个值都有数据类型 specified. 例如，对具有数据类型的字段使用此约束 of “[!UICONTROL 字符串]”指定该字段将包含字符串数组。 |
| [!UICONTROL 枚举和建议值] | 枚举表示此字段必须包含可能值的枚举列表中的值之一。 或者，您也可以使用此选项仅提供字符串字段的建议值列表，而不将该字段限制为这些值。 |
| [!UICONTROL 身份标识] | 指示此字段是标识字段。 有关标识字段的更多信息，请参阅[稍后本教程](#identity-field)。 |
| [!UICONTROL 关系] | 虽然可以使用合并架构和[!DNL Real-Time Customer Profile]推断架构关系，但这仅适用于共享相同类的架构。 [!UICONTROL Relationship]约束指示此字段基于不同的类引用架构的主要标识，这意味着两个架构之间的关系。 有关详细信息，请参阅有关[定义关系](./relationship-ui.md)的教程。 |

{style="表格布局：自动"}

>[!NOTE]
>
>任何必填、身份或关系字段都将在左边栏中各自的部分中列出，无论架构的复杂性如何，都允许您轻松找到这些字段。

在本教程中，架构中的`loyaltyTier`对象需要一个描述层类的新枚举字段，其中值只能是四个可能选项之一。 要将此字段添加到架构，请选择`loyaltyTier`对象旁边的&#x200B;**加号(+)**&#x200B;图标，并填写&#x200B;**[!UICONTROL 字段名称]**&#x200B;和&#x200B;**[!UICONTROL 显示名称]**&#x200B;的必填字段。 对于&#x200B;**[!UICONTROL Type]**，请选择“[!UICONTROL String]”。

![在[!UICONTROL 字段属性].](../images/tutorials/create-schema/tier-class-type.png)中添加并突出显示具有层类对象的架构编辑器

选择字段类型后，该字段会显示其他复选框，包括&#x200B;**[!UICONTROL 数组]**、**[!UICONTROL 枚举和建议值]**、**[!UICONTROL 标识]**&#x200B;和&#x200B;**[!UICONTROL 关系]**&#x200B;的复选框。

选中&#x200B;**[!UICONTROL 枚举和建议值]**&#x200B;复选框，然后选择&#x200B;**[!UICONTROL 枚举]**。 您可以在此为每个可接受的忠诚度级别类输入&#x200B;**[!UICONTROL 值]**（在驼峰式大小写中）和&#x200B;**[!UICONTROL 显示名称]**（标题大写中为便于阅读器的可选名称）。

完成所有字段属性后，选择&#x200B;**[!UICONTROL 应用]**&#x200B;以将`tierClass`字段添加到`loyaltyTier`对象。

![枚举和建议值字段属性已完成，突出显示[!UICONTROL 应用]。](../images/tutorials/create-schema/tier-class-enum.png)

## 将多字段对象转换为数据类型 {#datatype}

`loyaltyTier`对象现在包含多个字段，并代表可能在其他架构中使用的通用数据结构。 [!DNL Schema Editor]允许您通过将可重用多字段对象的结构转换为数据类型来轻松应用这些对象。

数据类型允许一致地使用多字段结构，并且比字段组提供更大的灵活性，因为它们可以在架构内的任何位置使用。 这是通过将字段的&#x200B;**[!UICONTROL Type]**&#x200B;值设置为[!DNL Schema Registry]中定义的任何数据类型的值来完成的。

若要将`loyaltyTier`对象转换为数据类型，请在画布中选择`loyaltyTier`字段，然后在&#x200B;**[!UICONTROL 字段属性]**&#x200B;下选择编辑器右侧的&#x200B;**[!UICONTROL 转换为新数据类型]**。

![带有loyaltyTier对象和[!UICONTROL 转换为新数据类型的架构编辑器突出显示]。](../images/tutorials/create-schema/convert-data-type.png)

此时将显示通知，确认已成功转换对象。 在画布中，您现在可以看到`loyaltyTier`字段现在有一个链接图标，右边栏表示它的数据类型为“[!DNL Loyalty Tier]”。

![架构编辑器，该架构编辑器突出显示loyaltyTier对象和新显示名称。](../images/tutorials/create-schema/loyalty-tier-data-type.png)

在未来的架构中，您现在可以将字段分配为“[!DNL Loyalty Tier]”类型，它将自动包含ID、层类、点阈值和有效日期的字段。

>[!NOTE]
>
您还可以独立于编辑模式创建和编辑自定义数据类型。 有关详细信息，请参阅[创建和编辑数据类型](../ui/resources/data-types.md)指南。

## 搜索和筛选架构字段

除了其基类提供的字段外，您的架构现在还包含多个字段组。 使用较大的架构时，您可以选中左边栏中的字段组名称旁边的复选框，将显示的字段过滤为仅由您感兴趣的字段组提供的字段。

![在架构编辑器的“字段组”部分选中了某些复选框以减小架构图的大小。](../images/tutorials/create-schema/filter-by-field-group.png)

如果您在架构中查找特定字段，则还可以使用搜索栏按名称筛选显示的字段，而不管这些字段是在哪个字段组下提供的。

![架构编辑器的搜索字段，其相关结果在画布上突出显示。](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
显示匹配字段时，搜索功能会考虑任何选定的字段组筛选器。 如果搜索查询未显示预期的结果，您可能需要仔细检查是否未过滤掉任何相关的字段组。

## 将架构字段设置为标识字段 {#identity-field}

可利用架构提供的标准数据结构来识别跨多个源属于同一个人的数据，从而允许各种下游用例，例如分段、报表、数据科学分析等。 为了根据单个身份拼合数据，键字段必须在适用的架构中标记为[!UICONTROL 身份]字段。

[!DNL Experience Platform]可通过在[!DNL Schema Editor]中使用&#x200B;**[!UICONTROL 标识]**&#x200B;复选框轻松表示标识字段。 但是，您必须根据数据的性质确定哪个字段是用作标识的最佳候选字段。

例如，可能有数千名忠诚度计划成员属于同一忠诚度级别，并且可能有几个成员共享同一实际地址。 但是，在这种情况下，在注册时，忠诚度计划的每个成员都会提供其个人电子邮件地址。 由于个人电子邮件地址通常由一人管理，因此字段`personalEmail.address`（由[!UICONTROL 个人联系人详细信息]字段组提供）是标识字段的好候选项。

>[!IMPORTANT]
>
以下步骤概述了如何向现有架构字段添加身份描述符。 作为在架构本身的结构中定义标识字段的替代方法，您还可以使用`identityMap`字段来包含标识信息。
>
如果您计划使用`identityMap`，请记住，它将覆盖您直接添加到架构的任何主标识。 有关详细信息，请参阅架构组合指南](../schema/composition.md#identityMap)的[基础知识中有关`identityMap`的部分。

在画布中选择`personalEmail.address`字段，并且&#x200B;**[!UICONTROL 字段属性]**&#x200B;下会显示&#x200B;**[!UICONTROL 标识]**&#x200B;复选框。 选中框和选项以将此项设置为&#x200B;**[!UICONTROL 主标识]**。 也选中此框。

>[!NOTE]
>
每个架构只能包含一个主标识字段。 一旦将某个架构字段设置为主标识，如果您稍后尝试将该架构中的另一个标识字段设置为主标识，您将收到一条错误消息。

接下来，必须从下拉列表中的预定义命名空间列表中提供&#x200B;**[!UICONTROL 身份命名空间]**。 由于此字段是客户的电子邮件地址，请从下拉列表中选择“[!UICONTROL 电子邮件]”。 选择&#x200B;**[!UICONTROL 应用]**&#x200B;以确认`personalEmail.address`字段的更新。

![电子邮件地址突出显示的架构编辑器并启用了“主要身份”复选框。](../images/tutorials/create-schema/primary-identity.png)

>[!NOTE]
>
有关标准命名空间及其定义的列表，请参阅[[!DNL Identity Service] 文档](../../identity-service/troubleshooting-guide.md#standard-namespaces)。

应用更改后，`personalEmail.address`的图标将显示一个指纹符号，表示它现在是一个标识字段。 该字段还列在左边栏中的&#x200B;**[!UICONTROL 标识]**&#x200B;下。

![架构编辑器在架构组合侧边栏中突出显示了电子邮件地址，并突出显示了身份字段。](../images/tutorials/create-schema/identity-applied.png)

现在，摄取到`personalEmail.address`字段中的所有数据将用于帮助识别该个人并将该客户的单个视图拼接在一起。 要了解有关使用[!DNL Experience Platform]中的标识的更多信息，请查阅[[!DNL Identity Service]](../../identity-service/home.md)文档。

## 启用架构以在[!DNL Real-Time Customer Profile]中使用 {#profile}

[[!DNL Real-Time Customer Profile]](../../profile/home.md)利用[!DNL Experience Platform]中的身份数据提供每个客户的整体视图。 该服务构建可靠的客户属性360°配置文件，以及客户在与[!DNL Experience Platform]集成的任何系统中进行的每次交互的时间戳记帐户。

为了使架构能够与[!DNL Real-Time Customer Profile]一起使用，它必须定义主标识。 如果您尝试在不首先定义主标识的情况下启用架构，则会收到一条错误消息。

![缺少主标识对话框。](../images/tutorials/create-schema/missing-primary-identity.png)

要启用“忠诚会员”架构以在[!DNL Profile]中使用，请先在画布中选择架构标题。

在编辑器的右侧，将显示有关架构的信息，包括其显示名称、描述和类型。 除此信息外，还有&#x200B;**[!UICONTROL 配置文件]**&#x200B;切换按钮。

![架构编辑器的架构根和为配置文件启用切换突出显示。](../images/tutorials/create-schema/profile-toggle.png)

选择&#x200B;**[!UICONTROL 配置文件]**，此时会出现弹出窗口，要求您确认要为[!DNL Profile]启用架构。

![为配置文件启用确认对话框。](../images/tutorials/create-schema/enable-profile.png)

>[!WARNING]
>
在为[!DNL Real-Time Customer Profile]启用架构并保存后，无法禁用该架构。

选择&#x200B;**[!UICONTROL 启用]**&#x200B;以确认您的选择。 您可以再次选择&#x200B;**[!UICONTROL 配置文件]**&#x200B;切换来禁用架构（如果需要），但一旦在启用[!DNL Profile]的同时保存了架构，则不能再禁用该架构。

## 更多操作 {#more}

在架构编辑器中，您还可以执行快速操作以复制架构的JSON结构或删除架构。 选择视图顶部的[!UICONTROL 更多]以显示包含快速操作的下拉列表。

![突出显示了“更多”按钮并显示下拉选项的架构编辑器。](../images/tutorials/create-schema/more-actions.png)

### 删除架构 {#delete-a-schema}

[!CONTEXTUALHELP]
id="platform_schemas_delete_profileenabledwithdatasets"
title="无法删除架构"
abstract="无法删除该架构，因为它已为轮廓启用，并且具有关联的数据集。"

[!CONTEXTUALHELP]
id="platform_schemas_delete_profileenablednodatasets"
title="无法删除架构"
abstract="无法删除该架构，因为它已为轮廓启用。"

[!CONTEXTUALHELP]
id="platform_schemas_delete_withdatasetsnotprofileenabled"
title="无法删除架构"
abstract="无法删除该架构，因为它具有关联的数据集。"

可以使用[!UICONTROL 更多]操作从UI中删除架构，也可以从[!UICONTROL 浏览]选项卡的架构详细信息中删除架构。 在某些情况下，无法删除架构。 如果符合以下条件，则无法删除架构：

* 已为配置文件启用架构。
* 架构已为配置文件启用，并具有关联的数据集。
* 架构具有关联的数据集，但未为配置文件启用。

### 复制 JSON 结构 {#copy-json-structure}

选择&#x200B;**[!UICONTROL 复制JSON结构]**&#x200B;为架构库中的任何架构生成导出有效负载。 此操作会将JSON结构复制到剪贴板。 然后，您可以使用导出的JSON将架构和任何相关资源导入其他沙盒或组织。 这使得不同环境之间的架构共享和重用变得简单而高效。

## 后续步骤和其他资源

现在，您已完成架构的合成，您可以在画布中查看完整的架构。 选择&#x200B;**[!UICONTROL 保存]**，架构将保存到[!DNL Schema Library]中，以供[!DNL Schema Registry]访问。

您的新架构现在可用于将数据摄取到[!DNL Experience Platform]。 请记住，一旦使用架构来摄取数据，可能只进行额外的更改。 有关架构版本控制的详细信息，请参阅架构组合的[基础知识](../schema/composition.md)。

您现在可以按照有关[在UI](./relationship-ui.md)中定义架构关系的教程，向“忠诚度成员”架构中添加新的关系字段。

还可以使用[!DNL Schema Registry] API查看和管理“忠诚度成员”架构。 要开始使用API，请先阅读[[!DNL Schema Registry API] 开发人员指南](../api/getting-started.md)。

### 视频资源

>[!WARNING]
>
以下视频中显示的[!DNL Experience Platform] UI已过期。 有关最新的UI屏幕截图和功能，请参阅上述文档。

以下视频说明如何在[!DNL Experience Platform] UI中创建简单架构。

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

以下视频旨在加深您对使用现场小组和课堂的理解。

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## 附录

以下部分提供有关使用[!DNL Schema Editor]的附加信息。

### 创建新类 {#create-new-class}

[!DNL Experience Platform]提供了灵活性，可以根据组织独有的类定义架构。 要了解如何创建新类，请参阅[在UI中创建和编辑类的指南](../ui/resources/classes.md#create)。

### 更改架构的类 {#change-class}

在保存架构之前，您可以在初始构成过程中随时更改架构的类。

>[!WARNING]
>
为架构重新分配类应极其谨慎。 字段组仅与某些类兼容，因此更改该类将重置画布和您已添加的所有字段。

要了解如何更改架构的类，请参阅UI中[管理架构的指南](../ui/resources/schemas.md#change-class)。

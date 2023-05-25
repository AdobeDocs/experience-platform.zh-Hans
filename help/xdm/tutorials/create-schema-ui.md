---
keywords: Experience Platform；主页；热门主题；UI；UI；XDM；XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；架构编辑器；架构编辑器；架构；架构；架构；创建
solution: Experience Platform
title: 使用架构编辑器创建架构
type: Tutorial
description: 本教程介绍了在 Experience Platform 中使用模式编辑器创建模式的步骤。
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '3959'
ht-degree: 0%

---

# 使用创建架构 [!DNL Schema Editor]

Adobe Experience Platform用户界面允许您创建和管理 [!DNL Experience Data Model] (XDM)模式在称为 [!DNL Schema Editor]. 本教程介绍如何使用 [!DNL Schema Editor].

出于演示目的，本教程中的步骤涉及创建一个描述客户忠诚度计划成员的示例架构。 虽然您可以使用这些步骤创建不同的架构以满足您自己的目的，但建议您先创建示例架构并了解 [!DNL Schema Editor].

>[!NOTE]
>
>如果您要将CSV数据摄取到Platform，则可以 [将该数据映射到由AI生成的推荐创建的XDM架构](../../ingestion/tutorials/map-csv/recommendations.md) （目前为测试版），无需自行手动创建架构。
>
>如果您希望使用 [!DNL Schema Registry] API，首先阅读 [[!DNL Schema Registry] 开发人员指南](../api/getting-started.md) 在尝试教程之前，请执行以下操作 [使用API创建架构](create-schema-api.md).

## 快速入门

本教程需要深入了解Adobe Experience Platform在模式创建过程中涉及的各个方面。 在开始本教程之前，请查看文档以了解以下概念：

* [[!DNL Experience Data Model (XDM)]](../home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。
   * [模式组合基础](../schema/composition.md)：XDM架构及其构建块的概述，包括类、架构字段组、数据类型和单个字段。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

## 打开 [!UICONTROL 架构] 工作区 {#browse}

此 [!UICONTROL 架构] 中的工作区 [!DNL Platform] UI提供了以下项目的可视化： [!DNL Schema Library]，允许您查看并管理对您的组织可用的架构。 该工作区还包括 [!DNL Schema Editor]，即可在其中撰写架构的画布。

登录后 [!DNL Experience Platform]，选择 **[!UICONTROL 架构]** 在左侧导航中打开 **[!UICONTROL 架构]** 工作区。 此 **[!UICONTROL 浏览]** 选项卡显示架构列表(表示以下内容： [!DNL Schema Library])，您可以查看和自定义这些字段。 此列表包括架构所基于的名称、类型、类和行为（记录或时间序列），以及上次修改架构的日期和时间。

请参阅指南，网址为 [在UI中探索现有XDM资源](../ui/explore.md) 了解更多信息。

## 创建架构并为其命名 {#create}

要开始构成架构，请选择 **[!UICONTROL 创建架构]** 右上角的 **[!UICONTROL 架构]** 工作区。 此时会显示一个下拉菜单，为您提供在核心类之间进行选择的选项 [!UICONTROL XDM个人资料] 和 [!UICONTROL XDM ExperienceEvent]. 如果这些类不适合您的用途，您还可以选择 **[!UICONTROL 浏览]** 从其它可用类中选择，或 [创建新类](#create-new-class).

在本教程中，选择 **[!UICONTROL XDM个人资料]**.

![](../images/tutorials/create-schema/create-schema-button.png)

此 [!DNL Schema Editor] 显示。 这是用于编写架构的画布。 系统会自动在中创建一个无标题架构 **[!UICONTROL 结构]** 部分，以及基于该类的所有架构中包含的标准字段。 为架构分配的类也列在下 **[!UICONTROL 类]** 在 **[!UICONTROL 合成]** 部分。

![](../images/tutorials/create-schema/schema-editor.png)

>[!NOTE]
>
>您可以 [更改架构的类](#change-class) 在保存模式之前的初始组合过程中的任何时候，但应极其谨慎地执行此操作。 字段组仅与某些类兼容，因此更改该类将重置画布和您已添加的任何字段。

下 **[!UICONTROL 架构属性]**，提供架构的显示名称和可选描述。 输入名称后，画布将更新以反映架构的新名称。

![](../images/tutorials/create-schema/name-schema.png)

在决定架构的名称时，需要考虑以下几个重要因素：

* 架构名称应简短且具有描述性，以便稍后可以轻松找到架构。
* 架构名称必须是唯一的，这意味着它还应该足够具体，以便将来不会重复使用。 例如，如果贵组织为不同品牌制定了单独的忠诚度计划，则最好将架构命名为“品牌A忠诚度会员”，以便轻松区别于您稍后可能定义的其他忠诚度相关架构。
* 您还可以使用架构描述提供有关架构的任何其他上下文信息。

本教程包含一个架构，用于摄取与忠诚度计划成员相关的数据，因此该架构被命名为“[!DNL Loyalty Members]“。

## 添加字段组 {#field-group}

您现在可以通过添加字段组开始向架构添加字段。 字段组是由一个或多个字段组成的组，这些字段通常一起用于描述特定概念。 本教程使用字段组描述忠诚度计划的成员并捕获关键信息，如姓名、生日、电话号码、地址等。

要添加字段组，请选择 **[!UICONTROL 添加]** 在 **[!UICONTROL 字段组]** 子区域。

![](../images/tutorials/create-schema/add-field-group-button.png)

此时将显示一个新对话框，其中显示了可用字段组的列表。 每个字段组仅用于特定类，因此该对话框仅列出与您选择的类兼容的字段组(在本例中， [!DNL XDM Individual Profile] 类)。 如果您使用的是标准XDM类，则字段组的列表将根据使用流行程度智能排序。

![](../images/tutorials/create-schema/field-group-popularity.png)

您可以在左边栏中选择一个过滤器，以将标准字段组列表缩小到特定 [行业](../schema/industries/overview.md) 比如零售、金融服务和医疗保健。

![](../images/tutorials/create-schema/industry-field-groups.png)

从列表中选择字段组会导致该字段组显示在右边栏中。 如果需要，您可以选择多个字段组，并在确认之前将每个字段组添加到右边栏中的列表。 此外，当前选定的字段组的右侧会出现一个图标，通过该图标可预览其提供的字段的结构。

![](../images/tutorials/create-schema/preview-field-group-button.png)

预览字段组时，右侧边栏中提供了字段组架构的详细说明。 您还可以浏览提供的画布中的字段组字段。 当您选择不同的字段时，右边栏会更新，以显示有关有问题的字段的详细信息。 选择 **[!UICONTROL 返回]** 完成预览以返回字段组选择对话框。

![](../images/tutorials/create-schema/preview-field-group.png)

在本教程中，选择 **[!UICONTROL 人口统计详细信息]** 字段组，然后选择 **[!UICONTROL 添加字段组]**.

![](../images/tutorials/create-schema/demographic-details.png)

此时将重新显示架构画布。 此 **[!UICONTROL 字段组]** 部分现在列出&quot;[!UICONTROL 人口统计详细信息]”和 **[!UICONTROL 结构]** 部分包括由字段组贡献的字段。 您可以在下面选择字段组的名称 **[!UICONTROL 字段组]** 部分，以突出显示它在画布中提供的特定字段。

![](../images/tutorials/create-schema/demographic-details-structure.png)

此字段组在顶级名称下提供多个字段 `person` 具有数据类型&quot;[!UICONTROL 人员]“。 这一组字段描述有关个人的信息，包括姓名、出生日期和性别。

>[!NOTE]
>
>请记住，字段可以使用标量类型（如字符串、整数、数组或日期），也可以使用中定义的任何数据类型（表示通用概念的一组字段） [!DNL Schema Registry].

请注意 `name` 字段的数据类型为&quot;[!UICONTROL 全名]“”，这意味着它也描述了一个通用概念并包含与名称相关的子字段，例如名字、姓氏、尊称和后缀。

选择画布中的不同字段以显示它们为架构结构贡献的任何其他字段。

## 添加更多字段组 {#field-group-2}

您现在可以重复相同的步骤来添加另一个字段组。 当您查看 **[!UICONTROL 添加字段组]** 这次是对话框，请注意“[!UICONTROL 人口统计详细信息]“字段组已灰显，并且无法选中它旁边的复选框。 这样可防止意外地复制已包含在当前架构中的字段组。

在本教程中，选择标准字段组 **[!UICONTROL 个人联系人详细信息]** 和 **[!UICONTROL 忠诚度详细信息]** 从列表中，然后选择 **[!UICONTROL 添加字段组]** 以将其添加到架构中。

![](../images/tutorials/create-schema/more-field-groups.png)

画布将重新显示，并在下面列出已添加的字段组 **[!UICONTROL 字段组]** 在 **[!UICONTROL 合成]** 以及添加到架构结构的复合字段。

![](../images/tutorials/create-schema/updated-structure.png)

## 定义自定义字段组 {#define-field-group}

此 [!UICONTROL 忠诚会员] 架构旨在捕获与忠诚度计划成员相关的数据，以及标准 [!UICONTROL 忠诚度详细信息] 您添加到架构的字段组可提供大多数此类内容，包括项目类型、点、加入日期等。

但是，在某些情况下，您可能希望包含标准字段组未涵盖的其他自定义字段，以便实现用例。 在添加自定义忠诚度字段的情况下，您有两个选项：

1. 创建新的自定义字段组以捕获这些字段。 本教程将介绍此方法。
1. 扩展标准 [!UICONTROL 忠诚度详细信息] 包含自定义字段的字段组。 这导致 [!UICONTROL 忠诚度详细信息] 字段组，而原始标准字段组将不再可用。 请参阅 [!UICONTROL 架构] UI指南，以了解有关 [将自定义字段添加到标准字段组的结构](../ui/resources/schemas.md#custom-fields-for-standard-groups).

要创建新字段组，请选择 **[!UICONTROL 添加]** 在 **[!UICONTROL 字段组]** 子部分与以前类似，但这次选择 **[!UICONTROL 创建新字段组]** 在出现的对话框顶部附近。 然后，系统会要求您提供新字段组的显示名称和描述。 在本教程中，将新字段组命名为&quot;[!DNL Custom Loyalty Details]&quot;，然后选择 **[!UICONTROL 添加字段组]**.

![](../images/tutorials/create-schema/create-new-field-group.png)

>[!NOTE]
>
>与类名一样，字段组名称应简短而简单，描述字段组对架构的贡献。 这些名称也是唯一的，因此您将无法重用该名称，因此必须确保它足够具体。

”[!DNL Custom Loyalty Details]”现在应显示在下 **[!UICONTROL 字段组]** ，但是还没有任何字段与其关联，因此下不会显示任何新字段 **[!UICONTROL 结构]**.

## 将字段添加到字段组 {#field-group-fields}

现在您已创建“[!DNL Custom Loyalty Details]”字段组，现在可以定义字段组将贡献给架构的字段。

要开始，请选择 **加(+)** 图标（位于画布中的架构名称旁）。

![](../images/tutorials/create-schema/add-field.png)

一个“[!UICONTROL 无标题字段]”占位符显示在画布中，右边栏更新以显示字段的配置选项。

![](../images/tutorials/create-schema/untitled-field.png)

在此方案中，架构需要有一个对象类型字段，用于详细描述人员当前的忠诚度等级。 使用右边栏中的控件，开始创建 `loyaltyTier` 类型为“”的字段[!UICONTROL 对象]”来保存您的相关字段。

下 **[!UICONTROL 分配给]**&#x200B;中，您必须选择要将该字段分配到的字段组。 请记住，所有架构字段都属于类或字段组，由于此架构使用标准类，因此您的唯一选项是选择字段组。 开始键入名称&#39;&#39;[!DNL Custom Loyalty Details]“”，然后从列表中选择字段组。

完成后，选择 **[!UICONTROL 应用]**.

![](../images/tutorials/create-schema/loyalty-tier-object.png)

应用更改和新创建的 `loyaltyTier` 对象出现。 由于这是自定义字段，因此会自动嵌套在您组织的租户ID命名空间中的对象，前面加下划线(`_tenantId` 在此示例中)。

![](../images/tutorials/create-schema/tenant-id.png)

>[!NOTE]
>
>租户ID对象的存在表示您添加的字段包含在贵组织的命名空间中。
>
>换言之，您添加的字段对于您的组织是唯一的，并将保存在 [!DNL Schema Registry] 仅供贵组织访问的特定区域中。 必须始终将您定义的字段添加到租户命名空间，以防止与其他标准类、字段组、数据类型和字段的名称冲突。

选择 **加(+)** 图标 `loyaltyTier` 对象以开始添加子字段。 此时将显示一个新的字段占位符，并且 **[!UICONTROL 字段属性]** 区域在画布右侧可见。

![](../images/tutorials/create-schema/new-field-in-loyalty-tier-object.png)

每个字段都需要以下信息：

* **[!UICONTROL 字段名称]：** 字段的名称，最好用camelCase编写。 不允许使用空格字符。 这是用于在代码和其他下游应用程序中引用字段的名称。
   * 示例： loyaltyLevel
* **[!UICONTROL 显示名称]：** 字段的名称，用大写字母表示。 这是查看或编辑架构时将在画布中显示的名称。
   * 示例：忠诚度级别
* **[!UICONTROL 类型]：** 字段的数据类型。 这包括基本标量类型和中定义的任何数据类型。 [!DNL Schema Registry]. 示例： [!UICONTROL 字符串]， [!UICONTROL 整数]， [!UICONTROL 布尔型]， [!UICONTROL 人员]， [!UICONTROL 地址]， [!UICONTROL 电话号码]等。
* **[!UICONTROL 描述]：** 字段的可选描述应最多包含200个字符。

的第一个字段 `loyaltyTier` 对象将是一个名为的字符串 `id`，表示忠诚度会员当前层的ID。 每个忠诚度会员的层ID都是唯一的，因为该公司会根据不同的因素为每个客户设置不同的忠诚度层点阈值。 将新字段的类型设置为&quot;[!UICONTROL 字符串]“，以及 **[!UICONTROL 字段属性]** 部分会填充多个用于应用约束的选项，包括默认值、格式和最大长度。

![](../images/tutorials/create-schema/string-constraints.png)

从 `id` 将是一个随机生成的自由格式字符串，无需进一步约束。 选择 **[!UICONTROL 应用]** 以应用更改。

![](../images/tutorials/create-schema/id-field-added.png)

## 向字段组添加更多字段 {#field-group-fields-2}

现在您已添加 `id` 字段，则可以添加其他字段以获取忠诚度等级信息，例如：

* 当前点阈值（整数）：成员必须保持为保留在当前层中的忠诚度点数下限。
* 下一层点阈值（整数）：成员必须累计的忠诚度点数，以升级到下一层。
* 生效日期（日期时间）：忠诚度成员加入此层的日期。

要将每个字段添加到架构，请选择 **加(+)** 图标 `loyalty` 对象并填写所需信息。

完成后， `loyaltyTier` 对象将包含 `id`， `currentThreshold`， `nextThreshold`、和 `effectiveDate`.

![](../images/tutorials/create-schema/loyalty-tier-object-fields.png)

## 向字段组添加枚举字段 {#enum}

在中定义字段时 [!DNL Schema Editor]，有一些其他选项可应用到基本字段类型，以对字段可包含的数据提供进一步限制。 下表说明了这些限制的用例：

| 约束 | 描述 |
| --- | --- |
| [!UICONTROL 必需] | 指示字段是数据摄取所必需的。 摄取后，任何上传到基于此架构、不包含此字段的数据集的数据都将失败。 |
| [!UICONTROL 数组] | 指示字段包含值的数组，每个值都指定了数据类型。 例如，在数据类型为&quot;的字段上使用此约束[!UICONTROL 字符串]”指定字段将包含字符串数组。 |
| [!UICONTROL 枚举和建议值] | 枚举表示此字段必须包含可能值的枚举列表中的值之一。 或者，您也可以使用此选项仅提供字符串字段的建议值列表，而不将该字段限制为这些值。 |
| [!UICONTROL 标识] | 指示此字段是标识字段。 提供了有关身份字段的更多信息 [在本教程的后面部分介绍](#identity-field). |
| [!UICONTROL 关系] | 虽然可以通过使用合并架构和来推断架构关系 [!DNL Real-Time Customer Profile]，这仅适用于共享相同类的架构。 此 [!UICONTROL 关系] constraint表示此字段基于不同的类引用架构的主要标识，这意味着两个架构之间的关系。 请参阅上的教程 [定义关系](./relationship-ui.md) 了解更多信息。 |

{style="table-layout:auto"}

>[!NOTE]
>
>任何必需、标识或关系字段均在左边栏中各自的部分中列出，这使您能够轻松找到这些字段，而不管架构的复杂性如何。

在本教程中， `loyaltyTier` 架构中的对象需要一个描述层类的新枚举字段，其中值只能是四个可能选项之一。 要将此字段添加到架构，请选择 **加(+)** 图标 `loyaltyTier` 对象并填写以下项的必填字段： **[!UICONTROL 字段名称]** 和 **[!UICONTROL 显示名称]**. 对象 **[!UICONTROL 类型]**，选择“[!UICONTROL 字符串]“。

![](../images/tutorials/create-schema/tier-class-type.png)

选择字段类型后，该字段会显示其他复选框，包括复选框 **[!UICONTROL 数组]**， **[!UICONTROL 枚举和建议值]**， **[!UICONTROL 身份]**、和 **[!UICONTROL 关系]**.

选择 **[!UICONTROL 枚举和建议值]** 复选框，然后选择 **[!UICONTROL 枚举]**. 在这里，您可以输入 **[!UICONTROL 值]** （在camelCase中）和 **[!UICONTROL 显示名称]** （标题大写中一个可选的读者友好名称），用于每个可接受的忠诚度级别分类。

完成所有字段属性后，选择 **[!UICONTROL 应用]** 以添加 `tierClass` 字段到 `loyaltyTier` 对象。

![](../images/tutorials/create-schema/tier-class-enum.png)

## 将多字段对象转换为数据类型 {#datatype}

此 `loyaltyTier` 对象现在包含多个字段，并代表可用于其他架构的通用数据结构。 此 [!DNL Schema Editor] 允许通过将可重用多字段对象的结构转换为数据类型来轻松应用这些对象。

数据类型允许一致地使用多字段结构，并且比字段组提供更大的灵活性，因为它们可以在架构内的任何位置使用。 这是通过设置字段的 **[!UICONTROL 类型]** 值为中定义的任何数据类型的值 [!DNL Schema Registry].

要转换 `loyaltyTier` 对象到数据类型，选择 `loyaltyTier` 字段，然后选择 **[!UICONTROL 转换为新数据类型]** 在编辑器的右侧，位于 **[!UICONTROL 字段属性]**.

![](../images/tutorials/create-schema/convert-data-type.png)

此时将显示通知，确认已成功转换对象。 在画布中，您现在可以看到 `loyaltyTier` 字段现在有一个链接图标，右边栏指示它的数据类型为&quot;[!DNL Loyalty Tier]“。

![](../images/tutorials/create-schema/loyalty-tier-data-type.png)

在将来的模式中，您现在可以将字段分配为&quot;[!DNL Loyalty Tier]“ type并且它会自动包含ID、层类别、点阈值和有效日期的字段。

>[!NOTE]
>
>您还可以独立于编辑架构创建和编辑自定义数据类型。 请参阅指南，网址为 [创建和编辑数据类型](../ui/resources/data-types.md) 了解更多信息。

## 搜索和筛选架构字段

除了其基类提供的字段外，您的架构现在还包含多个字段组。 使用较大的架构时，您可以选中左边栏中字段组名称旁边的复选框，以将显示的字段筛选为仅由感兴趣的字段组提供的字段。

![](../images/tutorials/create-schema/filter-by-field-group.png)

如果您在架构中查找特定字段，则还可以使用搜索栏按名称筛选显示的字段，而不管这些字段是在哪个字段组下提供的。

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>显示匹配字段时，搜索功能会考虑任何选定的字段组筛选器。 如果搜索查询未显示预期的结果，您可能需要仔细检查是否未过滤掉任何相关的字段组。

## 将架构字段设置为标识字段 {#identity-field}

架构提供的标准数据结构可用于跨多个源识别属于同一个人的数据，允许各种下游用例，例如分段、报表、数据科学分析等。 要根据个人身份拼接数据，关键字段必须标记为 [!UICONTROL 身份] 个字段。

[!DNL Experience Platform] 使通过使用表示标识字段变得容易 **[!UICONTROL 身份]** 中的复选框 [!DNL Schema Editor]. 但是，您必须根据数据的性质确定哪个字段是用作标识的最佳候选字段。

例如，可能有数千名忠诚度计划成员属于同一忠诚度级别，并且可能有几个成员共享同一实际地址。 但是，在这种情况下，在注册时，忠诚度计划的每个成员都会提供其个人电子邮件地址。 由于个人电子邮件地址通常由一人管理，因此字段 `personalEmail.address` (由 [!UICONTROL 个人联系人详细信息] 字段组)是标识字段的良好候选项。

>[!IMPORTANT]
>
>以下概述的步骤包括如何向现有架构字段添加身份描述符。 作为在架构本身结构中定义标识字段的替代方法，您还可以使用 `identityMap` 字段以包含身份信息。
>
>如果您计划使用 `identityMap`，请记住，这将覆盖您直接添加到架构的任何主标识。 请参阅以下部分： `identityMap` 在 [模式组合指南基础](../schema/composition.md#identityMap) 了解更多信息。

选择 `personalEmail.address` 字段，以及 **[!UICONTROL 身份]** 复选框显示在下 **[!UICONTROL 字段属性]**. 选中该框和选项可将此框设置为 **[!UICONTROL 主要身份]** 显示。 也选中此框。

>[!NOTE]
>
>每个架构只能包含一个主标识字段。 一旦某个架构字段被设置为主标识，如果您稍后尝试将该架构中的另一个标识字段设置为主标识，您将收到一条错误消息。

接下来，您必须提供 **[!UICONTROL 身份命名空间]** 从下拉菜单中的预定义命名空间列表中。 由于此字段是客户的电子邮件地址，请选择“[!UICONTROL 电子邮件]”从下拉菜单中。 选择 **[!UICONTROL 应用]** 以确认更新 `personalEmail.address` 字段。

![](../images/tutorials/create-schema/primary-identity.png)

>[!NOTE]
>
>有关标准命名空间及其定义的列表，请参阅 [[!DNL Identity Service] 文档](../../identity-service/troubleshooting-guide.md#standard-namespaces).

应用更改后，的图标 `personalEmail.address` 显示指纹符号，指示它现在为标识字段。 该字段也列在左边栏的下方 **[!UICONTROL 身份]**.

![](../images/tutorials/create-schema/identity-applied.png)

现在，所有数据都已引入 `personalEmail.address` 字段将帮助识别该个人，并将该客户的单个视图拼接在一起。 要了解有关在中使用标识的更多信息，请执行以下操作 [!DNL Experience Platform]，请查看 [[!DNL Identity Service]](../../identity-service/home.md) 文档。

## 启用架构以便用于 [!DNL Real-Time Customer Profile] {#profile}

[[!DNL Real-Time Customer Profile]](../../profile/home.md) 利用中的身份数据 [!DNL Experience Platform] 提供每个客户的整体视图。 该服务为客户在与集成的任何系统中进行的每次交互建立了强大的360°客户属性配置文件以及带有时间戳的帐户 [!DNL Experience Platform].

为了启用架构以用于 [!DNL Real-Time Customer Profile]，则必须定义主标识。 如果您尝试在不首先定义主标识的情况下启用架构，则会收到一条错误消息。

![](../images/tutorials/create-schema/missing-primary-identity.png)

启用“忠诚度成员”架构以用于 [!DNL Profile]，首先在画布中选择架构标题。

在编辑器的右侧，将显示有关架构的信息，包括其显示名称、描述和类型。 除此信息外，还有 **[!UICONTROL 个人资料]** 切换按钮。

![](../images/tutorials/create-schema/profile-toggle.png)

选择 **[!UICONTROL 个人资料]** 此时会出现一个弹出窗口，要求您确认要为以下项启用架构 [!DNL Profile].

![](../images/tutorials/create-schema/enable-profile.png)

>[!WARNING]
>
>为启用架构后 [!DNL Real-Time Customer Profile] 并保存，则无法禁用该设置。

选择 **[!UICONTROL 启用]** 以确认您的选择。 您可以选择 **[!UICONTROL 个人资料]** 再次切换可禁用架构（如果需要），但一旦架构已保存，则 [!DNL Profile] 已启用，无法再禁用它。

## 后续步骤和其他资源

现在，您已经完成架构的撰写，您可以在画布中看到完整的架构。 选择 **[!UICONTROL 保存]** 架构将保存到 [!DNL Schema Library]，使其可由 [!DNL Schema Registry].

您的新架构现在可用于将数据摄取到 [!DNL Platform]. 请记住，一旦使用架构来摄取数据，则只能进行额外的更改。 请参阅 [模式组合基础](../schema/composition.md) 有关模式版本控制的详细信息。

现在，您可以按照本教程中的以下内容进行操作： [在UI中定义架构关系](./relationship-ui.md) ，以向“忠诚会员”架构中添加新的关系字段。

“忠诚会员”模式也可以使用 [!DNL Schema Registry] API。 要开始使用API，请从阅读 [[!DNL Schema Registry API] 开发人员指南](../api/getting-started.md).

### 视频资源

>[!WARNING]
>
>此 [!DNL Platform] 以下视频中显示的UI已过期。 有关最新的UI屏幕截图和功能，请参阅上述文档。

以下视频说明如何在中创建简单架构 [!DNL Platform] UI。

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

以下视频旨在加强您对使用现场小组和课的理解。

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## 附录

以下部分提供有关使用的附加信息 [!DNL Schema Editor].

### 创建新类 {#create-new-class}

[!DNL Experience Platform] 提供了根据组织特有的类定义架构的灵活性。 要了解如何创建新课程，请参阅以下指南中的 [在UI中创建和编辑类](../ui/resources/classes.md#create).

### 更改架构的类 {#change-class}

在保存架构之前，您可以在初始构成过程中随时更改架构的类。

>[!WARNING]
>
>为架构重新分配类应极其谨慎。 字段组仅与某些类兼容，因此更改该类将重置画布和您已添加的任何字段。

要了解如何更改架构的类，请参阅 [在UI中管理架构](../ui/resources/schemas.md#change-class).

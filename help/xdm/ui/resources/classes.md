---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；数据模型；ui；工作区；类；类；
solution: Experience Platform
title: 在UI中创建和编辑类
description: 了解如何在Experience Platform用户界面中创建和编辑类。
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: c04e5a49f2a4e90345ca20ecd0547d02b5004fcf
workflow-type: tm+mt
source-wordcount: '1458'
ht-degree: 5%

---

# 在 UI 中创建和编辑类 {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="标准或自定义类过滤器"
>abstract="根据如何创建可用的类预先过滤可用的类的列表。选中单选按钮可在“标准”与“自定义”选项之间选择。“标准”选项显示由 Adobe 创建的实体，并包括 XDM 个人配置文件和 XDM 体验事件类。“自定义”选项显示在您的组织内创建的实体。请参阅文档以详细了解创建和编辑类。"

在Adobe Experience Platform中，模式的类定义模式将包含的数据（记录或时间序列）的行为方面。 除此之外，类还描述了基于该类的所有架构所需包含的最少数量的公共属性，并提供了一种合并多个兼容数据集的方法。

Adobe提供了多个标准（“核心”）Experience Data Model (XDM)类，包括XDM Individual Profile和XDM ExperienceEvent。 除了这些核心类之外，您还可以创建自己的自定义类，以描述组织更具体的用例。

本文档概述了如何在Experience PlatformUI中创建、编辑和管理自定义类。

## 先决条件 {#prerequisites}

本指南要求您对XDM系统有一定的了解。 请参阅[XDM概述](../../home.md)，了解XDM在Experience Platform生态系统中的作用以及[架构组合的基础知识](../../schema/composition.md)，了解类对XDM架构的贡献。

虽然本指南并非必需，但建议您也学习有关[在UI](../../tutorials/create-schema-ui.md)中撰写架构的教程，以熟悉架构编辑器的各种功能。

## 快速入门 {#getting-started}

在Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 架构]**&#x200B;以打开[!UICONTROL 架构]工作区，然后选择&#x200B;**[!UICONTROL 类]**&#x200B;选项卡。 此时将显示可用类的列表。

## 筛选类 {#filter}

系统会根据类的创建方式自动筛选类列表。 默认设置显示由Adobe定义的类。 您还可以筛选列表以显示您的组织创建的那些列表。 选择单选按钮以在[!UICONTROL 标准]和[!UICONTROL 自定义]选项之间进行选择。 [!UICONTROL Standard]选项显示由Adobe创建的实体，[!UICONTROL Custom]选项显示组织内创建的实体。

![已突出显示[!UICONTROL 架构]工作区的[!UICONTROL 类]选项卡，其中包含[!UICONTROL 标准]和[!UICONTROL 自定义]。](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>使用搜索功能根据类名筛选或查找类。 有关详细信息，请参阅[浏览XDM资源](../explore.md)指南。

## 创建新类 {#create}

在Platform UI中创建类的方法有两种。 从[!UICONTROL 架构]工作区中的任意选项卡中选择&#x200B;**[!UICONTROL 创建架构]**，或者从[!UICONTROL 类]选项卡中选择&#x200B;**[!UICONTROL 创建类]**。

![使用[!UICONTROL 创建架构]和[!UICONTROL 创建类]的[!UICONTROL 架构]工作区的[!UICONTROL 类]选项卡突出显示](../../images/ui/resources/classes/create-class-methods.png)

如果选择&#x200B;**[!UICONTROL 创建类]**，将显示[!UICONTROL 创建类]对话框。 为类输入[!UICONTROL 显示名称]和[!UICONTROL 描述]，并使用单选按钮选择类的预期行为。 类可以是类型、记录系列或时间系列。 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以确认您的选择并返回[!UICONTROL 类]选项卡。

![与[!UICONTROL 创建]的[!UICONTROL 创建类]对话框突出显示。](../../images/ui/resources/classes/create-class-dialog.png)

您创建的类可用，并列在[!UICONTROL 类]视图中。

![最近创建类突出显示的[!UICONTROL 架构]工作区的[!UICONTROL 类]选项卡。](../../images/ui/resources/classes/new-class-listing.png)

### 创建或编辑类 {#create-or-edit}

或者，如果您选择&#x200B;**[!UICONTROL 创建架构]**，则会显示[!UICONTROL 创建架构]工作流。 在[!UICONTROL 架构详细信息]部分中，选择&#x200B;**[!UICONTROL 其他]**。 此时将显示可用类的列表。 在此处，您可以浏览和筛选新类所基于的现有类。

>[!NOTE]
>
>只能完全编辑和自定义由您的组织定义的自定义类。 对于由Adobe定义的核心类，只能在单个架构的上下文中编辑其字段的显示名称。 有关详细信息，请参阅有关[编辑架构字段的显示名称](./schemas.md#display-names)的部分。
>
>保存自定义类并在数据摄取中使用后，只能对其执行附加更改。 有关详细信息，请参阅架构演变[规则](../../schema/composition.md#evolution)。

![在[!UICONTROL 架构详细信息]部分中突出显示[!UICONTROL 使用[!UICONTROL 其他]创建架构]工作流。](../../images/ui/resources/classes/other-schema-details.png)

选择一个单选按钮，以根据类是自定义类还是标准类来筛选这些类。 您还可以根据行业筛选可用的结果，或使用搜索字段搜索特定类。

![已突出显示[!UICONTROL 使用搜索栏[!UICONTROL 自定义]和[!UICONTROL 行业]创建架构]工作流。](../../images/ui/resources/classes/filter-and-search.png)

为了帮助您确定相应的类，提供了信息(![信息图标。](../../images/ui/resources/classes/info.png))和预览(![预览图标。每个类的](../../images/ui/resources/classes/preview.png)个图标。 信息图标会打开一个对话框，其中提供了类及其关联的行业的说明。 预览图标将打开包含架构图及其属性的类的预览对话框。

![选定类的预览，其中突出显示了架构图和类属性。](../../images/ui/resources/classes/class-preview.png)

选择任意行以选择一个类，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以确认您的选择。

![使用从可用类表中选择的类并突出显示[!UICONTROL 下一步]的[!UICONTROL 创建架构]工作流。](../../images/ui/resources/classes/select-class.png)

此时将显示工作流的[!UICONTROL 名称和审核]部分。 在此部分中，提供用于标识您的架构的名称和描述。&#x200B;AEM架构的基本结构（由类提供）显示在画布中，供您查看和验证选定的类和架构结构。

在[!UICONTROL 架构显示名称]文本字段中，为类输入一个简短的、描述性的、唯一的和用户友好的名称。 接下来，输入适当的描述以标识架构定义的数据的行为。 当您查看了架构结构并且满意您的设置时，请选择&#x200B;**[!UICONTROL 完成]**&#x200B;以创建您的架构。

![高亮显示[!UICONTROL 创建架构]工作流的[!UICONTROL 名称和审核]部分，该工作流具有[!UICONTROL 架构显示名称]、[!UICONTROL 描述]和[!UICONTROL 完成]。](../../images/ui/resources/classes/name-and-review-class.png)

此时将显示架构编辑器，其中架构的结构显示在画布中。 您现在可以开始[向类](#add-fields)添加字段。

![画布中显示架构结构的架构编辑器。](../../images/ui/resources/classes/edit.png)

## 向类添加字段 {#add-fields}

一旦您在[!UICONTROL 架构编辑器]中打开了一个使用自定义类的架构，就可以开始向该类添加字段。 要添加新字段，请选择架构名称旁边的&#x200B;**加号(+)**&#x200B;图标。

>[!IMPORTANT]
>
>在构建实现由您的组织定义的类的架构时，请记住，架构字段组只能与兼容类一起使用。 由于您定义的类是新的，因此&#x200B;**[!UICONTROL 添加字段组]**&#x200B;对话框中列出的字段组不兼容。 相反，您需要[创建新的字段组](./field-groups.md#create)以便与该类一起使用。 下次编写实现新类的架构时，将列出您定义的字段组以供使用。

![突出显示添加按钮的架构编辑器。](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>请记住，您添加到类的任何字段都将在使用该类的所有架构中使用。 因此，您应该仔细考虑哪些字段在所有架构用例中将很有用。 如果您考虑添加一个在此类下的某些架构中可能仅能使用的字段，您可能需要考虑通过[创建字段组](./field-groups.md#create)来将其添加到这些架构中。

画布中显示&#x200B;**[!UICONTROL 无标题字段]**&#x200B;占位符，右边栏更新以显示用于配置字段属性的控件。 在&#x200B;**[!UICONTROL 分配给]**&#x200B;下，选择&#x200B;**[!UICONTROL 类]**。

![架构编辑器画布中的无标题字段，选中并突出显示“分配给类”字段属性。](../../images/ui/resources/classes/assign-to-class.png)

有关如何配置字段并将其添加到类的特定步骤，请参阅[在UI](../fields/overview.md#define)中定义字段的指南。 继续向类添加所需数量的字段。 完成后，选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存架构和类。

![架构编辑器的画布上新创建的架构，突出显示[!UICONTROL 保存]。](../../images/ui/resources/classes/save.png)

如果您之前已创建采用此类的架构，则新添加的字段将自动出现在这些架构中。

## 更改架构的类 {#schema}

在保存架构之前，您可以在初始创建过程中随时更改架构的类。 但是，应谨慎执行此操作，因为字段组仅与某些类兼容。 更改类会重置画布和您已添加的任何字段。
有关详细信息，请参阅[创建和编辑架构](./schemas.md#change-class)指南。

## 后续步骤 {#next-steps}

本文档介绍了如何使用Platform UI创建和编辑类。 有关[!UICONTROL 架构]工作区的功能的更多信息，请参阅[[!UICONTROL 架构]工作区概述](../overview.md)。

要了解如何使用架构注册表API管理类，请参阅[类端点指南](../../api/classes.md)。

---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；数据模型；ui；工作区；类；类；
solution: Experience Platform
title: 在UI中创建和编辑类
description: 了解如何在Experience Platform用户界面中创建和编辑类。
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: a05ee385694b028b513e2fa632079e665ba815bb
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 5%

---

# 在 UI 中创建和编辑类 {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="标准或自定义类过滤器"
>abstract="根据如何创建可用的类预先过滤可用的类的列表。选中单选按钮可在“标准”与“自定义”选项之间选择。“标准”选项显示由 Adobe 创建的实体，并包括 XDM 个人轮廓和 XDM 体验事件类。“自定义”选项显示在您的组织内创建的实体。请参阅文档以详细了解创建和编辑类。"

在Adobe Experience Platform中，模式的类定义模式将包含的数据（记录或时间序列）的行为方面。 除此之外，类还描述了基于该类的所有架构所需包含的最少数量的公共属性，并提供了一种合并多个兼容数据集的方法。

Adobe提供了多个标准（“核心”）体验数据模型(XDM)类，包括[XDM Individual Profile](../../classes/individual-profile.md)和[XDM ExperienceEvent](../../classes/experienceevent.md)。 除了这些核心类之外，您还可以创建自己的自定义类，以描述组织更具体的用例。

本文档概述如何在Experience Platform UI中创建、编辑和管理自定义类。

## 先决条件 {#prerequisites}

本指南要求您对XDM系统有一定的了解。 请参阅[XDM概述](../../home.md)，了解XDM在Experience Platform生态系统中的角色以及[架构组合的基础知识](../../schema/composition.md)，了解类如何对XDM架构做出贡献。

虽然本指南并非必需，但建议您也学习有关[在UI](../../tutorials/create-schema-ui.md)中撰写架构的教程，以熟悉架构编辑器的各种功能。

## 快速入门 {#getting-started}

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL Schemas]**&#x200B;以打开[!UICONTROL Schemas]工作区，然后选择&#x200B;**[!UICONTROL Classes]**&#x200B;选项卡。 此时将显示可用类的列表。

![已突出显示[!UICONTROL Classes]工作区[!UICONTROL Schemas]和[!UICONTROL Classes]的[!UICONTROL Schemas]选项卡中的类数。](../../images/ui/resources/classes/available-classes.png)

## 筛选类 {#filter}

系统会根据类的创建方式自动筛选类列表。 默认设置显示由Adobe定义的类。 您还可以筛选列表以显示您的组织创建的那些列表。 选择单选按钮以在[!UICONTROL Standard]和[!UICONTROL Custom]选项之间进行选择。 [!UICONTROL Standard]选项显示由Adobe创建的实体，[!UICONTROL Custom]选项显示组织内创建的实体。

![突出显示带有[!UICONTROL Classes]和[!UICONTROL Schemas]的[!UICONTROL Standard]工作区的[!UICONTROL Custom]选项卡。](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>使用搜索功能根据类名筛选或查找类。 有关详细信息，请参阅[浏览XDM资源](../explore.md)指南。

## 创建新类 {#create}

在Experience Platform UI中通过&#x200B;**[!UICONTROL Create class]**&#x200B;或&#x200B;**[!UICONTROL Create schema]**&#x200B;创建类的方法有两种。

### 创建类

从&#x200B;**[!UICONTROL Create class]**&#x200B;工作区的[!UICONTROL Classes]选项卡中选择[!UICONTROL Schemas]。

![突出显示了[!UICONTROL Classes]的[!UICONTROL Schemas]工作区的[!UICONTROL Create class]选项卡](../../images/ui/resources/classes/create-class.png)

出现[!UICONTROL Create class]对话框。 为类输入[!UICONTROL Display name]和[!UICONTROL Description]，然后使用单选按钮选择类的预期行为。 类可以是[!UICONTROL Record]或[!UICONTROL Time-series]类型。 选择&#x200B;**[!UICONTROL Create]**&#x200B;以确认您的选择并返回到[!UICONTROL Classes]选项卡。

![与[!UICONTROL Create class]的[!UICONTROL Create]对话框突出显示。](../../images/ui/resources/classes/create-class-dialog.png)

您创建的类可用，并列在[!UICONTROL Classes]视图中。

![最近创建类突出显示的[!UICONTROL Classes]工作区的[!UICONTROL Schemas]选项卡。](../../images/ui/resources/classes/new-class-listing.png)

### 创建架构

或者，您也可以通过手动创建架构来创建类。 从&#x200B;**[!UICONTROL Create schema]**&#x200B;工作区的[!UICONTROL Classes]选项卡中选择[!UICONTROL Schemas]。

![突出显示了[!UICONTROL Classes]的[!UICONTROL Schemas]工作区的[!UICONTROL Create schema]选项卡](../../images/ui/resources/classes/create-schema.png)

在出现的&#x200B;**[!UICONTROL Manual]**&#x200B;对话框中选择[!UICONTROL Create a schema]。

>[!NOTE]
>
>如果使用ML辅助模式创建工作流，则可以上传文件并使用ML算法生成推荐的模式。 在该架构创建工作流中，您不需要为架构指定基类。 要了解ML如何推荐基于csv文件的架构结构，请参阅[机器学习辅助架构创建指南](../ml-assisted-schema-creation.md)。

![使用工作流选项创建架构对话框并选择高亮显示。](../../images/ui/resources/classes/manually-create-a-schema.png)

此时将显示架构创建工作流。 在[!UICONTROL Schema details]部分中，选择&#x200B;**[!UICONTROL Other]**。 此时将显示可用类的列表。 选择 **[!UICONTROL Create class]**。

![在[!UICONTROL Create schema]部分中高亮显示具有[!UICONTROL Other]的[!UICONTROL Schema details]工作流。](../../images/ui/resources/classes/other-schema-details.png)

出现[!UICONTROL Create class]对话框。 为类输入[!UICONTROL Display name]和[!UICONTROL Description]，然后使用单选按钮选择类的预期行为。 类可以是[!UICONTROL Record]或[!UICONTROL Time-series]类型。 选择&#x200B;**[!UICONTROL Create]**&#x200B;以确认您的选择并返回到[!UICONTROL Classes]选项卡。

![与[!UICONTROL Create class]的[!UICONTROL Create]对话框突出显示。](../../images/ui/resources/classes/create-class-from-schema.png)

类列表将在[!UICONTROL Schema details]部分中刷新，并且新创建的类将被自动选中。 选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续创建架构。

![选择了新类并突出显示[!UICONTROL Schema details]的[!UICONTROL Next]节。](../../images/ui/resources/classes/select-new-class.png)

选择类后，将显示[!UICONTROL Name and review]部分。 在此部分中，您会提供用于标识架构的名称和描述。&#x200B;AEM架构的基本结构（由类提供）显示在画布中，供您查看和验证选定的类和架构结构。

在文本字段中输入人性化的[!UICONTROL Schema display name]。 接下来，输入适当的描述以帮助识别您的架构。 当您查看了架构结构并对设置感到满意时，请选择&#x200B;**[!UICONTROL Finish]**&#x200B;以创建您的架构。

![突出显示了[!UICONTROL Name and review]、[!UICONTROL Create schema]和[!UICONTROL Schema display name]的[!UICONTROL Description]工作流的[!UICONTROL Finish]部分。](../../images/ui/resources/classes/schema-details.png)

## 向类添加字段 {#add-fields}

一旦您在架构编辑器中打开了一个采用自定义类的架构，您就可以开始向该类添加字段。 要添加新字段，请选择架构名称旁边的&#x200B;**加号(+)**&#x200B;图标。

>[!IMPORTANT]
>
>在构建实现由您的组织定义的类的架构时，请记住，架构字段组只能与兼容类一起使用。 由于您定义的类是新的，因此&#x200B;**[!UICONTROL Add field group]**&#x200B;对话框中未列出兼容的字段组。 相反，您需要[创建新的字段组](./field-groups.md#create)以便与该类一起使用。 下次编写实现新类的架构时，将列出您定义的字段组以供使用。

![突出显示添加按钮的架构编辑器。](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>请记住，您添加到类的任何字段都将在使用该类的所有架构中使用。 因此，您应该仔细考虑哪些字段在所有架构用例中将很有用。 如果您考虑添加一个在此类下的某些架构中可能仅能使用的字段，您可能需要考虑通过[创建字段组](./field-groups.md#create)来将其添加到这些架构中。

画布中显示&#x200B;**[!UICONTROL Untitled Field]**&#x200B;占位符，右边栏更新以显示用于配置字段属性的控件。 在&#x200B;**[!UICONTROL Assign to]**&#x200B;下，选择&#x200B;**[!UICONTROL Class]**。

![架构编辑器画布中的无标题字段，选定并突出显示“分配给[!UICONTROL Class]”字段属性。](../../images/ui/resources/classes/assign-to-class.png)

有关如何配置字段并将其添加到类的特定步骤，请参阅[在UI](../fields/overview.md#define)中定义字段的指南。 继续向类添加所需数量的字段。 完成后，选择&#x200B;**[!UICONTROL Save]**&#x200B;以保存架构和类。

![架构编辑器的画布上新创建的架构，突出显示[!UICONTROL Save]。](../../images/ui/resources/classes/save.png)

如果您之前已创建采用此类的架构，则新添加的字段将自动出现在这些架构中。

## 编辑类 {#edit-a-class}

>[!NOTE]
>
>只能完全编辑和自定义由您的组织定义的自定义类。 对于由Adobe定义的核心类，只能在单个架构的上下文中编辑其字段的显示名称。 有关详细信息，请参阅有关[编辑架构字段的显示名称](./schemas.md#display-names)的部分。
>
>保存自定义类并在数据摄取中使用后，只能对其执行附加更改。 有关详细信息，请参阅架构演变[规则](../../schema/composition.md#evolution)。

您可以通过架构工作流编辑类，方法是：编辑扩展类的现有架构，或者手动创建架构。 无法直接编辑类。 从[!UICONTROL Browse]工作区的[!UICONTROL Schemas]选项卡内，选择现有类或&#x200B;**[!UICONTROL Create a schema]**。

![架构编辑器已突出显示现有类和[!UICONTROL Create a schema]。](../../images/ui/resources/classes/edit-class-options.png)

如果选择创建新架构，请参阅[创建架构](#create-schema)一节以了解详细信息。 创建完架构（或选择现有架构后）后，将显示架构编辑器。 要更新现有类字段，请从架构结构中选择该字段。 字段的信息将显示在右边栏中。 确保[!UICONTROL Assign to]
已选择选项&#x200B;**[!UICONTROL Class]**，或者您的更新不会影响类。

![架构编辑器，其中选定字段并突出显示，右边栏显示，突出显示[!UICONTROL Assign to]。](../../images/ui/resources/classes/edit-existing-field.png)

对字段进行任何所需的更改，在右边栏中向下滚动以选择&#x200B;**[!UICONTROL Apply]**&#x200B;以保存更改。

>[!IMPORTANT]
>
> 您对字段所做的任何更新都将应用于使用该类的所有架构，遵循架构演变[规则](../../schema/composition.md#evolution)。

![架构编辑器，已选定字段并公开右边栏，突出显示[!UICONTROL Apply]。](../../images/ui/resources/classes/save-changes.png)

要添加新字段，请按照[将字段添加到类](#add-fields-to-a-class)指南。 完成后，选择&#x200B;**[!UICONTROL Save]**&#x200B;以保存架构和类。

![已突出显示[!UICONTROL Save]的架构编辑器。](../../images/ui/resources/classes/save-schema.png)

## 更改架构的类 {#schema}

在保存架构之前，您可以在初始创建过程中随时更改架构的类。 但是，应谨慎执行此操作，因为字段组仅与某些类兼容。 更改类会重置画布和您已添加的任何字段。
有关详细信息，请参阅[创建和编辑架构](./schemas.md#change-class)指南。

## 后续步骤 {#next-steps}

本文档介绍了如何使用Experience Platform UI创建和编辑类。 有关[!UICONTROL Schemas]工作区的功能的更多信息，请参阅[[!UICONTROL Schemas]工作区概述](../overview.md)。

要了解如何使用架构注册表API管理类，请参阅[类端点指南](../../api/classes.md)。

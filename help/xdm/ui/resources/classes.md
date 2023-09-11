---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；数据模型；ui；工作区；类；类；
solution: Experience Platform
title: 在UI中创建和编辑类
description: 了解如何在Experience Platform用户界面中创建和编辑类。
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: 51ef116ad125b0d699bf4808e3d26d3b00b743e2
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# 在UI中创建和编辑类 {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="标准或自定义类过滤器"
>abstract="系统会根据可用类的创建方式对此类列表进行预筛选。 选择单选按钮以在“标准”和“自定义”选项之间进行选择。 标准选项显示由Adobe创建的实体，并包括XDM个人配置文件和XDM体验事件类。 自定义选项可显示在您的组织内创建的实体。 请参阅文档以了解有关创建和编辑类的更多信息。"

在Adobe Experience Platform中，模式的类定义模式将包含的数据（记录或时间序列）的行为方面。 除此之外，类还描述了基于该类的所有架构所需包含的最少数量的公共属性，并提供了一种合并多个兼容数据集的方法。

Adobe提供了多个标准（“核心”）体验数据模型(XDM)类，包括 [!DNL XDM Individual Profile] 和 [!DNL XDM ExperienceEvent]. 除了这些核心类之外，您还可以创建自己的自定义类，以描述组织更具体的用例。

本文档概述了如何在Experience PlatformUI中创建、编辑和管理自定义类。

## 先决条件

本指南要求您对XDM系统有一定的了解。 请参阅 [XDM概述](../../home.md) 介绍XDM在Experience Platform生态系统中的作用，以及 [模式组合基础](../../schema/composition.md) 以了解类如何对XDM架构做出贡献。

虽然本指南并非必需，但建议您也按照以下内容阅读本教程： [在UI中组合架构](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor].

## 创建新类 {#create}

在 **[!UICONTROL 架构]** 工作区，选择 **[!UICONTROL 创建架构]**，然后选择 **[!UICONTROL 浏览]** 从下拉菜单中查找。

![](../../images/ui/resources/classes/browse-classes.png)

将显示一个对话框，允许您从可用类列表中进行选择。 在对话框顶部，选择 **[!UICONTROL 创建新类]**. 然后，您可以为新类提供显示名称（类的简短名称、描述性名称、唯一名称以及用户友好名称）、描述以及架构将定义的数据行为(**[!UICONTROL 记录]** 或 **[!UICONTROL 时间序列]**)。

完成后，选择 **[!UICONTROL 分配类]**.

![](../../images/ui/resources/classes/class-details.png)

此 [!DNL Schema Editor] 显示，在画布中显示基于您刚刚创建的自定义类的新架构。 由于尚未向类添加字段，因此架构仅包含 `_id` 字段，表示系统生成的唯一标识符，自动应用于 [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>在构建实现由您的组织定义的类的架构时，请记住，架构字段组只能与兼容类一起使用。 由于您定义的类是新类，因此， **[!UICONTROL 添加字段组]** 对话框。 相反，您将需要 [创建新字段组](./field-groups.md#create) 用于该类。 下次编写实现新类的架构时，将列出您定义的字段组以供使用。

您现在可以开始 [向类中添加字段](#add-fields)，将由使用该类的所有架构共享。

## 编辑现有类 {#edit}

>[!NOTE]
>
>只能完全编辑和自定义由您的组织定义的自定义类。 对于由Adobe定义的核心类，只能在单个架构的上下文中编辑其字段的显示名称。 请参阅以下部分 [编辑架构字段的显示名称](./schemas.md#display-names) 以了解详细信息。
>
>保存自定义类并在数据摄取中使用后，只能对其执行附加更改。 请参阅 [模式演化规则](../../schema/composition.md#evolution) 以了解更多信息。

要编辑现有类，请选择 **[!UICONTROL 浏览]** 选项卡，然后选择采用要编辑的类的方案的名称。

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>您可以使用工作区的搜索和筛选功能来帮助更轻松地查找架构。 请参阅指南，网址为 [探索XDM资源](../explore.md) 以了解更多信息。

此 [!DNL Schema Editor] 此时将显示，并在画布中显示架构的结构。 您现在可以开始 [向类中添加字段](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## 向类添加字段 {#add-fields}

一旦您有一个采用自定义类的架构，该架构会在 [!UICONTROL 架构编辑器]中，您可以开始向类添加字段。 要添加新字段，请选择 **加(+)** 图标（在架构名称旁）。

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>请记住，您添加到类的任何字段都将在使用该类的所有架构中使用。 因此，您应该仔细考虑哪些字段在所有架构用例中将很有用。 如果您考虑添加一个字段，而该字段可能只在此类下的某些架构中使用，您可能需要考虑通过以下方式将其添加到这些架构中 [创建字段组](./field-groups.md#create) 而是。

An **[!UICONTROL 无标题的字段]** 占位符显示在画布中，右边栏更新以显示用于配置字段属性的控件。 下 **[!UICONTROL 分配给]**，选择 **[!UICONTROL 类]**.

![](../../images/ui/resources/classes/assign-to-class.png)

![](../../images/ui/resources/classes/assign-to-class.png)

请参阅指南，网址为 [在UI中定义字段](../fields/overview.md#define) 有关如何配置字段并将其添加到类的特定步骤。 继续向类添加所需数量的字段。 完成后，选择 **[!UICONTROL 保存]** 以保存架构和类。

![](../../images/ui/resources/classes/save.png)

如果您之前已创建采用此类的架构，则新添加的字段将自动出现在这些架构中。

## 更改架构的类 {#schema}

在保存架构之前，您可以在初始创建过程中随时更改架构的类。 请参阅指南，网址为 [创建和编辑模式](./schemas.md#change-class) 以了解更多信息。

## 后续步骤

本文档介绍了如何使用Platform UI创建和编辑类。 欲知关于 [!UICONTROL 架构] 工作区，请参见 [[!UICONTROL 架构] 工作区概述](../overview.md).

要了解如何使用 [!DNL Schema Registry] API，请参见 [类端点指南](../../api/classes.md).

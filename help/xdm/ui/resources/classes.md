---
keywords: Experience Platform；主页；热门主题；API;XDM;XDM系统；体验数据模型；数据模型；UI；工作区；类；类；
solution: Experience Platform
title: 在UI中创建和编辑类
description: 了解如何在Experience Platform用户界面中创建和编辑类。
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# 在UI中创建和编辑类

在Adobe Experience Platform中，架构的类定义架构将包含的数据的行为方面（记录或时间系列）。 除此之外，类还描述了所有基于该类的架构需要包含的公共属性的最小数量，并为合并多个兼容数据集提供了一种方法。

Adobe提供了多个标准（“核心”）体验数据模型(XDM)类，包括 [!DNL XDM Individual Profile] 和 [!DNL XDM ExperienceEvent]. 除了这些核心类之外，您还可以创建自己的自定义类，以描述贵组织的更具体用例。

本文档概述了如何在Experience PlatformUI中创建、编辑和管理自定义类。

## 先决条件

本指南需要对XDM系统有一定的了解。 请参阅 [XDM概述](../../home.md) 介绍XDM在Experience Platform生态系统中的作用，以及 [架构组合基础知识](../../schema/composition.md) 以了解类对XDM模式的贡献。

虽然本指南不是必需的，但建议您也要遵循 [在UI中合成架构](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor].

## 创建新类 {#create}

在 **[!UICONTROL 模式]** 工作区，选择 **[!UICONTROL 创建架构]**，然后选择 **[!UICONTROL 浏览]** 从下拉菜单中。

![](../../images/ui/resources/classes/browse-classes.png)

此时会出现一个对话框，允许您从可用类的列表中进行选择。 在对话框顶部，选择 **[!UICONTROL 创建新类]**. 然后，您可以为新类提供一个显示名称（类的简短、描述性、唯一性和用户友好名称）、描述以及架构将定义的数据的行为(**[!UICONTROL 记录]** 或 **[!UICONTROL 时间系列]**)。

完成后，选择 **[!UICONTROL 分配类]**.

![](../../images/ui/resources/classes/class-details.png)

的 [!DNL Schema Editor] 显示，画布中显示了一个基于您刚刚创建的自定义类的新架构。 由于尚未向类添加字段，因此架构仅包含 `_id` 字段，表示系统生成的唯一标识符，该标识符将自动应用于 [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>在构建实现由组织定义的类的架构时，请记住，架构字段组仅可与兼容类一起使用。 由于您定义的类是新类，因此 **[!UICONTROL 添加字段组]** 对话框。 相反，您需要 [创建新字段组](./field-groups.md#create) 用于该类。 下次构建实现新类的架构时，将列出您定义的字段组以供使用。

您现在可以开始 [向类添加字段](#add-fields)，所有使用类的架构都将共享该内容。

## 编辑现有类 {#edit}

>[!NOTE]
>
>只能完全编辑和自定义由您的组织定义的自定义类。 对于由Adobe定义的核心类，在单个架构的上下文中只能编辑其字段的显示名称。 请参阅 [编辑架构字段的显示名称](./schemas.md#display-names) 以了解详细信息。
>
>保存自定义类并在数据摄取中使用后，以后只能对其进行附加更改。 请参阅 [模式演化规则](../../schema/composition.md#evolution) 以了解更多信息。

要编辑现有类，请选择 **[!UICONTROL 浏览]** 选项卡，然后选择使用要编辑的类的架构的名称。

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>您可以使用工作区的搜索和筛选功能来帮助更轻松地查找架构。 请参阅 [浏览XDM资源](../explore.md) 以了解更多信息。

的 [!DNL Schema Editor] 显示，画布中显示了架构的结构。 您现在可以开始 [向类添加字段](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## 向类添加字段 {#add-fields}

在中打开使用自定义类的架构后， [!UICONTROL 架构编辑器]，则可以开始向类添加字段。 要添加新字段，请选择 **加号(+)** 图标。

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>请记住，您添加到类的任何字段都将用于使用该类的所有架构中。 因此，您应仔细考虑哪些字段在所有架构用例中都将很有用。 如果您想要添加一个字段，该字段可能只能看到此类下某些架构中的使用，则可能需要考虑通过 [创建字段组](./field-groups.md#create) 中。

A **[!UICONTROL 新建字段]** 将显示在画布中，并且右边栏会更新以显示用于配置字段属性的控件。 在 **[!UICONTROL 分配给]**，选择 **[!UICONTROL 类]**.

![](../../images/ui/resources/classes/assign-to-class.png)

请参阅 [在UI中定义字段](../fields/overview.md#define) 以了解有关如何配置字段并将其添加到类的具体步骤。 继续向类中添加所需数量的字段。 完成后，选择 **[!UICONTROL 保存]** 以保存架构和类。

![](../../images/ui/resources/classes/save.png)

如果您之前创建了使用此类的架构，则新添加的字段将自动显示在这些架构中。

## 更改架构的类 {#schema}

在保存架构之前，您可以在初始创建过程中的任意时刻更改该架构的类。 请参阅 [创建和编辑模式](./schemas.md#change-class) 以了解更多信息。

## 后续步骤

本文档介绍了如何使用Platform UI创建和编辑类。 有关 [!UICONTROL 模式] 工作区，请参阅 [[!UICONTROL 模式] 工作区概述](../overview.md).

了解如何使用 [!DNL Schema Registry] API，请参阅 [classes endpoint guide](../../api/classes.md).

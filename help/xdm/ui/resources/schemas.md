---
keywords: Experience Platform；主页；热门主题；api;API;XDM;XDM系统；体验数据模型；数据模型；ui；工作区；模式;模式;
solution: Experience Platform
title: 在UI中创建和编辑模式
description: 学习如何在Experience Platform用户界面中创建和编辑模式的基础知识。
topic-legacy: user guide
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 0%

---

# 在UI中创建和编辑模式

本指南概述了如何在Adobe Experience Platform UI中为您的组织创建、编辑和管理体验数据模型(XDM)模式。

>[!IMPORTANT]
>
>XDM模式是极其可自定义的，因此创建模式所涉及的步骤可能因模式要捕获的数据类型而异。 因此，此文档仅涵盖您可以在UI中与模式进行的基本交互，并不包括自定义类、混合、数据类型和字段等相关步骤。
>
>有关模式创建过程的完整演示，请按照[模式创建教程](../../tutorials/create-schema-ui.md)创建一个完整的示例模式，并熟悉[!DNL Schema Editor]的许多功能。

## 先决条件

本指南要求对XDM系统有充分的了解。 有关Experience Platform生态系统中XDM角色的介绍，请参阅[XDM概述](../../home.md)；有关如何构建模式的概述，请参阅[模式合成基础知识](../../schema/composition.md)。

## 新建模式{#create}

在[!UICONTROL Schemas]工作区中，选择右上角的&#x200B;**[!UICONTROL Create schema]**。 在显示的下拉列表中，您可以选择&#x200B;**[!UICONTROL XDM Individual Profile]**&#x200B;和&#x200B;**[!UICONTROL XDM ExperienceEvent]**&#x200B;作为模式的基类。 或者，您也可以选择&#x200B;**[!UICONTROL Browse]**&#x200B;以从可用类的完整列表中进行选择，或者改为创建新的自定义类](./classes.md#create)。[

![](../../images/ui/resources/schemas/create-schema.png)

选择类后，将显示[!DNL Schema Editor]，画布中将显示模式的基结构（由类提供）。 在此处，您可以使用右边栏为模式添加&#x200B;**[!UICONTROL Display name]**&#x200B;和&#x200B;**[!UICONTROL Description]**。

![](../../images/ui/resources/schemas/schema-details.png)

您现在可以通过添加mixins](#add-mixins)来开始构建模式的结构。[

## 编辑现有模式{#edit}

>[!NOTE]
>
>在保存模式并将其用于数据获取后，只能对其进行附加更改。 有关详细信息，请参阅[模式演化规则](../../schema/composition.md#evolution)。

要编辑现有模式，请选择&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡，然后选择要编辑的模式的名称。

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>您可以使用工作区的搜索和筛选功能来帮助更轻松地查找模式。 有关详细信息，请参阅[探索XDM资源](../explore.md)指南。

选择模式后，[!DNL Schema Editor]将显示，画布中显示了模式的结构。 现在，您可以[向模式添加mixins](#add-mixins)、[编辑字段显示名称](#display-names)或[编辑现有的自定义mixins](./mixins.md#edit)(如果模式使用任何)。

## 向模式{#add-mixins}添加混音

>[!NOTE]
>
>本节介绍如何将现有混音添加到模式。 如果要创建新的自定义混音，请参阅[创建和编辑混音](./mixins.md#create)的指南。

在[!DNL Schema Editor]中打开模式后，可以通过使用mixins将字段添加到模式。 要开始，请选择左边栏中&#x200B;**[!UICONTROL Mixins]**&#x200B;旁边的&#x200B;**[!UICONTROL Add]**。

![](../../images/ui/resources/schemas/add-mixin-button.png)

将显示一个对话框，其中显示可为模式选择的混音列表。 由于混合仅与一个类兼容，因此将只列出与模式的选定类关联的混合。 默认情况下，列出的混合会根据其在您组织中的使用受欢迎程度进行排序。

![](../../images/ui/resources/schemas/mixin-popularity.png)

如果您知道要添加的混合字段的常规活动或业务区，请在左边栏中选择一个或多个行业垂直类别以过滤显示的混合列表。

![](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>有关XDM中特定于行业的数据建模的最佳实践的详细信息，请参阅[行业数据模型](../../schema/industries/overview.md)的相关文档。

您还可以使用搜索栏帮助查找所需的混音。 其名称与查询匹配的混合显示在列表的顶部。 在&#x200B;**[!UICONTROL Standard Fields]**&#x200B;下，将显示包含描述所需数据属性的字段的混合。

![](../../images/ui/resources/schemas/mixin-search.png)

选中要添加到模式的混音名称旁边的复选框。 您可以从列表中选择多个混音，每个选定的混音将显示在右侧边栏中。

![](../../images/ui/resources/schemas/add-mixin.png)

>[!TIP]
>
>对于列出的任何混音，您可以将鼠标悬停在信息图标(![](../../images/ui/resources/schemas/info-icon.png))上或将焦点放在该图标上，以视图混音捕获的数据类型的简短描述。 在您决定将其添加到模式之前，您还可以选择预览图标(![](../../images/ui/resources/schemas/preview-icon.png))来视图混音所提供字段的结构。

选择混音后，选择&#x200B;**[!UICONTROL Add mixin]**&#x200B;将其添加到模式。

![](../../images/ui/resources/schemas/add-mixin-finish.png)

[!DNL Schema Editor]将重新显示，画布中显示混音提供的字段。

![](../../images/ui/resources/schemas/mixins-added.png)

## 为实时客户用户档案{#profile}启用模式

[实时客户概](../../../profile/home.md) 要分析从不同来源收集到的数据，以构建每个客户的完整视图。如果希望模式捕获的模式参与此过程，则必须启用该数据才能在[!DNL Profile]中使用。

>[!IMPORTANT]
>
>要为[!DNL Profile]启用模式，它必须定义主标识字段。 有关详细信息，请参阅[定义标识字段](../fields/identity.md)的指南。

要启用模式，请在左边栏中选择模式的名称，然后选择右边栏中的&#x200B;**[!UICONTROL Profile]**&#x200B;切换。

![](../../images/ui/resources/schemas/profile-toggle.png)

将显示一个快显窗口，警告您启用并保存模式后，将无法禁用它。 选择&#x200B;**[!UICONTROL Enable]**&#x200B;继续。

![](../../images/ui/resources/schemas/profile-confirm.png)

画布将重新显示，并启用[!UICONTROL Profile]切换。

>[!IMPORTANT]
>
>由于模式尚未保存，因此如果您改变主意让模式参与实时客户用户档案，这是没有回报的点：保存已启用的模式后，便无法再禁用它。 再次选择&#x200B;**[!UICONTROL Profile]**&#x200B;切换键以禁用模式。

要完成该过程，请选择&#x200B;**[!UICONTROL Save]**&#x200B;以保存模式。

![](../../images/ui/resources/schemas/profile-enabled.png)

现在，模式可用于实时客户用户档案。 当平台将数据引入基于此模式的数据集时，该数据将并入您合并的用户档案数据中。

## 编辑模式字段{#display-names}的显示名称

在为模式分配了类并添加了混音后，您可以编辑任何模式字段的显示名称，而不管这些字段是由标准还是自定义XDM资源提供的。

>[!NOTE]
>
>请记住，属于标准类或混合的字段的显示名称只能在特定模式的上下文中编辑。 换句话说，在一个模式中更改标准字段的显示名称不会影响使用相同关联类或混合的其他模式。

要编辑模式字段的显示名称，请在画布中选择该字段。 在右边栏中，在&#x200B;**[!UICONTROL Display name]**&#x200B;下提供新名称。

![](../../images/ui/resources/schemas/display-name.png)

在右边栏中选择&#x200B;**[!UICONTROL Apply]**，画布将更新以显示字段的新显示名称。 选择&#x200B;**[!UICONTROL Save]**&#x200B;以将更改应用到模式。

![](../../images/ui/resources/schemas/display-name-changed.png)

## 更改模式的类{#change-class}

在保存模式之前，您可以在初始合成过程中的任意点更改模式的类。

>[!WARNING]
>
>重新分配模式的类应非常谨慎。 Mixins仅与某些类兼容，因此更改类将重置画布和您添加的任何字段。

要重新分配类，请在画布左侧选择&#x200B;**[!UICONTROL Assign]**。

![](../../images/ui/resources/schemas/assign-class-button.png)

将显示一个对话框，其中显示所有可用类的列表，包括由您的组织定义的任何类（所有者为“[!UICONTROL Customer]”）以及由Adobe定义的标准类。

从列表中选择一个类，在对话框的右侧显示其说明。 您还可以选择&#x200B;**[!UICONTROL Preview class structure]**&#x200B;以查看与类关联的字段和元数据。 选择&#x200B;**[!UICONTROL Assign class]**&#x200B;继续。

![](../../images/ui/resources/schemas/assign-class.png)

此时将打开一个新对话框，要求您确认是否要指定新类。 选择&#x200B;**[!UICONTROL Assign]**&#x200B;进行确认。

![](../../images/ui/resources/schemas/assign-confirm.png)

确认类更改后，画布将重置，所有合成进度将丢失。

## 后续步骤

本文档介绍了在平台UI中创建和编辑模式的基础知识。 强烈建议您阅读[模式创建教程](../../tutorials/create-schema-ui.md)，了解在UI中构建完整模式（包括为独特用例创建自定义混合和数据类型）的全面工作流。

有关[!UICONTROL Schemas]工作区功能的详细信息，请参阅[[!UICONTROL Schemas]工作区概述](../overview.md)。

要了解如何在[!DNL Schema Registry] API中管理模式，请参阅[模式端点指南](../../api/schemas.md)。

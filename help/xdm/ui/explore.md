---
keywords: Experience Platform；主页；热门主题；ui;UI;XDM;XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；浏览；类；混合；数据类型；模式;
solution: Experience Platform
title: 在UI中浏览XDM资源
description: 了解如何在Experience Platform用户界面中探索现有模式、类、混音和数据类型。
topic-legacy: tutorial
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# 在UI中浏览XDM资源

在Adobe Experience Platform中，所有体验数据模型(XDM)资源都存储在[!DNL Schema Library]中，包括由Adobe提供的标准资源和您的组织定义的自定义资源。 在Experience Platform UI中，您可以视图[!DNL Schema Library]中任何现有模式、类、混音或数据类型的结构和字段。 在规划和准备数据摄取时，此功能特别有用，因为UI提供了有关这些XDM资源提供的每个字段的预期数据类型和使用案例的信息。

本教程介绍了在Experience Platform UI中探索现有模式、类、混合和数据类型的步骤。

## 查找XDM资源{#lookup}

在平台UI中，选择左侧导航中的&#x200B;**[!UICONTROL Schemas]**。 [!UICONTROL Schemas]工作区提供了&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡，用于浏览您组织中的所有现有XDM资源，以及用于专门浏览&#x200B;**[!UICONTROL Classes]**、**[!UICONTROL Mixins]**&#x200B;和&#x200B;**[!UICONTROL Data types]**&#x200B;的其他专用选项卡。

![](../images/ui/explore/tabs.png)

在[!UICONTROL Browse]选项卡上，可以使用过滤器图标（![过滤器图标图像](../images/ui/explore/icon.png)）显示左边栏中的控件，以缩小列出的结果范围。

例如，要筛选列表以仅显示Adobe提供的标准数据类型，请分别在&#x200B;**[!UICONTROL Type]**&#x200B;和&#x200B;**[!UICONTROL Owner]**&#x200B;节下选择&#x200B;**[!UICONTROL Datatype]**&#x200B;和&#x200B;**[!UICONTROL Adobe]**。

通过&#x200B;**[!UICONTROL Included in Profile]**&#x200B;切换，可以过滤结果，仅显示在已启用用于[实时客户用户档案](../../profile/home.md)的模式中使用的资源。

![](../images/ui/explore/filter.png)

您还可以使用搜索栏进一步缩小结果范围。 搜索词时，顶级项目表示其名称与搜索查询匹配的资源。 这些项目下方的&#x200B;**[!UICONTROL Standard Fields]**&#x200B;下将列出所有包含与查询匹配的字段的资源。 这样，您无需事先知道资源名称，即可根据所包含数据的类型搜索XDM资源。

![](../images/ui/explore/search.png)

找到要浏览的资源后，从列表中选择其名称以在画布中视图其结构。

## 在画布{#explore}中浏览XDM资源

选择资源后，其结构即会在画布中打开。

![](../images/ui/explore/canvas.png)

默认情况下，包含子属性的所有对象类型字段在首次出现在画布中时都会折叠。 要显示任何字段的子属性，请选择其名称旁的图标。

![](../images/ui/explore/field-expand.png)

### 系统生成的字段{#system-fields}

某些字段名称以下划线作为前缀，如`_repo`和`_id`。 这些表示在摄取数据时系统将自动生成并分配的字段的占位符。

因此，在引入平台时，这些字段中的大多数应排除在数据结构中。 此规则的主要例外是[`_{TENANT_ID}`字段](../api/getting-started.md#know-your-tenant_id)，您组织下创建的所有XDM字段都必须以字段命名。

### 数据类型 {#data-types}

对于画布中显示的每个字段，其相应的数据类型显示在其名称旁边，一目了然地指示字段需要摄取的数据类型。

![](../images/ui/explore/data-types.png)

附加了方括号(`[]`)的任何数据类型都表示该特定数据类型的数组。 例如，**[!UICONTROL String]\[]**&#x200B;的数据类型指示字段需要字符串值的数组。 **[!UICONTROL Payment Item]\[]**&#x200B;的数据类型表示符合[!UICONTROL Payment Item]数据类型的对象数组。

如果数组字段基于对象类型，您可以在画布中选择其图标以显示每个数组项目的预期属性。

![](../images/ui/explore/array-type.png)

### [!UICONTROL Field properties] {#field-properties}

选择画布中任意字段的名称时，右边栏会更新，显示&#x200B;**[!UICONTROL Field properties]**&#x200B;下有关该字段的详细信息。 这可以包括对字段预期用例、默认值、模式、格式的说明，无论字段是否为必填字段，等等。

![](../images/ui/explore/field-properties.png)

如果您正在检查的字段是枚举字段，则右边栏还将显示该字段希望接收的可接受值。

![](../images/ui/explore/enum-field.png)

### 标识字段{#identity}

在检查包含标识字段的模式时，这些字段将列在向模式提供标识字段的类或混音的左边栏中。 在左边栏中选择标识字段名称以在画布中显示该字段，而不管其嵌套的深度如何。

在画布中，标识字段会用指纹图标（![指纹图标图像](../images/ui/explore/identity-symbol.png)）高亮显示。 如果选择标识字段的名称，则可以视图其他信息，如[标识命名空间](../../identity-service/namespaces.md)，以及字段是否是模式的主标识。

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>有关标识字段及其与下游平台服务的关系的详细信息，请参阅[定义标识字段](./fields/identity.md)上的指南。

### 关系字段{#relationship}

如果您正在检查包含关系字段的模式，该字段将列在左边栏的&#x200B;**[!UICONTROL Relationships]**&#x200B;下。 在左边栏中选择关系字段名称以在画布中显示该字段，而不管它嵌套的深度如何。

在画布中，关系字段也以唯一方式高亮显示，显示字段引用的目标模式的名称。 如果选择关系字段的名称，则可以在右边栏中视图目标模式主要标识的标识命名空间。

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>有关在XDM模式中使用关系的详细信息，请参阅有关在UI](../tutorials/create-schema-ui.md)中创建关系的教程。[

## 后续步骤

本文档介绍了如何在Experience Platform UI中探索现有XDM资源。 有关[!UICONTROL Schemas]工作区和[!DNL Schema Editor]的不同功能的详细信息，请参阅[[!UICONTROL Schemas]工作区概述](./overview.md)。

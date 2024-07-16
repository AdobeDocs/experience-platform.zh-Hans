---
keywords: Experience Platform；主页；热门主题；ui；UI；UI；XDM；XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；浏览；类；字段组；数据类型；架构；
solution: Experience Platform
title: 浏览UI中的架构资源
description: 了解如何在Experience Platform用户界面中探索现有架构、类、架构字段组和数据类型。
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: 0e1fb15cfa56fb4c2a4a645578327f0a4bd22e68
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 0%

---

# 浏览UI中的架构资源

在Adobe Experience Platform中，所有Experience Data Model (XDM)架构资源都存储在[!DNL Schema Library]中，包括由Adobe提供的标准资源和由您的组织定义的自定义资源。 在Experience PlatformUI中，您可以查看[!DNL Schema Library]中任何现有架构、类、字段组或数据类型的结构和字段。 在规划和准备数据引入时，此功能特别有用，因为UI提供了有关这些XDM资源提供的每个字段的预期数据类型和用例的信息。

本教程介绍了在Experience PlatformUI中浏览现有架构、类、字段组和数据类型的步骤。

## 查找架构资源 {#lookup}

在Platform UI的左侧导航中选择&#x200B;**[!UICONTROL 架构]**。 [!UICONTROL 架构]工作区提供了&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡以浏览组织中的所有架构，以及额外的专用选项卡，分别用于浏览&#x200B;**[!UICONTROL 类]**、**[!UICONTROL 字段组]**&#x200B;和&#x200B;**[!UICONTROL 数据类型]**。

![](../images/ui/explore/tabs.png)

筛选器图标（![筛选器图标图像](../images/ui/explore/icon.png)）在左边栏中显示控件，以缩小列出的结果的范围。 根据所列的资源类型，显示的控件会有所不同。

例如，要筛选列表以仅显示Adobe提供的标准数据类型，请分别在&#x200B;**[!UICONTROL 类型]**&#x200B;和&#x200B;**[!UICONTROL 所有者]**&#x200B;部分下选择&#x200B;**[!UICONTROL 数据类型]**&#x200B;和&#x200B;**[!UICONTROL Adobe]**。

配置文件&#x200B;]**中包含的**[!UICONTROL &#x200B;切换允许您筛选结果，以仅显示架构中使用的资源，这些架构已启用在[实时客户配置文件](../../profile/home.md)中使用。 **[!UICONTROL 显示临时架构]**&#x200B;切换筛选使用字段创建的架构列表，这些字段仅供单个数据集使用。

![突出显示筛选器面板的[!UICONTROL 架构]工作区[!UICONTROL 浏览]选项卡。](../images/ui/explore/filter.png)

在&#x200B;**[!UICONTROL 类]**、**[!UICONTROL 字段组]**&#x200B;或&#x200B;**[!UICONTROL 数据类型]**&#x200B;选项卡上列出资源时，您可以选择&#x200B;**[!UICONTROL Adobe]**&#x200B;以仅显示标准资源，或选择&#x200B;**[!UICONTROL 客户]**&#x200B;以仅显示由您的组织创建的资源。

![](../images/ui/explore/filter-data-type.png)

您还可以使用搜索栏进一步缩小结果的范围。

![](../images/ui/explore/search.png)

搜索结果中显示的资源首先按标题匹配项排序，然后按说明匹配项排序。 反过来，这两个类别中的匹配词越多，列表中显示的资源就越多。

找到要浏览的资源后，从列表中选择其名称，以在画布中查看其结构。

## 在画布中浏览XDM资源 {#explore}

选择资源后，其结构将在画布中打开。

![](../images/ui/explore/canvas.png)

默认情况下，包含子属性的所有对象类型字段在首次出现在画布中时会折叠。 要显示任何字段的子属性，请选择其名称旁边的图标。

![](../images/ui/explore/field-expand.png)

### 标准类和字段组指示器 {#standard-class-and-field-group-indicator}

在架构编辑器中，标准(Adobe生成的)类和字段组以挂锁图标（![A挂锁图标）表示。](../images/ui/explore/padlock-icon.png)的问题。挂锁显示在左边栏中的类或字段组名称旁边，以及架构图中作为系统生成资源一部分的任意字段旁边。

![带有挂锁图标的架构编辑器突出显示](../images/ui/explore/schema-editor-padlock-icon.png)

有关指导，请参阅[将自定义字段添加到标准字段组](./resources/schemas.md)文档。 不能编辑标准类。

### 系统生成的字段 {#system-fields}

某些字段名称的前面带有下划线，如`_repo`和`_id`。 这些表示系统将在摄取数据时自动生成和分配的字段的占位符。

因此，在摄取到Platform中时，应该从数据的结构中排除这些字段中的大多数。 此规则的主要例外是[`_{TENANT_ID}`字段](../api/getting-started.md#know-your-tenant_id)，在您的组织下创建的所有XDM字段都必须在此字段下命名空间。

### 数据类型 {#data-types}

对于画布中显示的每个字段，其对应的数据类型会显示在名称旁边，这概览field希望摄取的数据类型。

![](../images/ui/explore/data-types.png)

任何附加了方括号(`[]`)的数据类型均表示该特定数据类型的数组。 例如，**[!UICONTROL String]\[]**&#x200B;的数据类型指示该字段需要字符串值的数组。 **[!UICONTROL 付款项]\[]**&#x200B;的数据类型表示符合[!UICONTROL 付款项]数据类型的对象数组。

如果数组字段基于对象类型，则可以在画布中选择其图标，以显示每个数组项的预期属性。

![](../images/ui/explore/array-type.png)

### [!UICONTROL 字段属性] {#field-properties}

当您选择画布中任何字段的名称时，右边栏会更新，以在&#x200B;**[!UICONTROL 字段属性]**&#x200B;下显示有关该字段的详细信息。 这可以包括字段的预期用例、默认值、模式、格式、字段是否为必填等的描述。

![](../images/ui/explore/field-properties.png)

如果您要检查的字段是枚举字段，则右边栏还会显示该字段预期接收的可接受值。

![](../images/ui/explore/enum-field.png)

### 标识字段 {#identity}

检查包含身份字段的架构时，这些字段在左边栏中列在提供给架构的类或字段组下。 选择左边栏中的身份字段名称以显示画布中的字段，无论其嵌套深度如何。

在画布中用指纹图标（![指纹图标图像](../images/ui/explore/identity-symbol.png)）突出显示身份字段。 如果选择身份字段的名称，则可以查看其他信息，如[身份命名空间](../../identity-service/features/namespaces.md)，以及该字段是否为架构的主要身份。

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>有关标识字段及其与下游平台服务的关系的详细信息，请参阅[定义标识字段](./fields/identity.md)指南。

### 关系字段 {#relationship}

如果要检查包含关系字段的架构，则该字段将列在左边栏中的&#x200B;**[!UICONTROL 关系]**&#x200B;下。 选择左边栏中的关系字段名称以显示画布中的字段，无论其嵌套深度如何。

关系字段在画布中也以唯一方式高亮显示，显示字段链接到的引用架构的名称。 如果选择关系字段的名称，则可以在右边栏中查看引用架构主要身份的身份命名空间。

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>有关在XDM架构中使用关系的详细信息，请参阅有关[在UI](../tutorials/relationship-ui.md)中创建关系的教程。

## 后续步骤

本文档介绍了如何在Experience PlatformUI中探索现有XDM资源。 有关[!UICONTROL 架构]工作区和[!DNL Schema Editor]的不同功能的详细信息，请参阅[[!UICONTROL 架构]工作区概述](./overview.md)。

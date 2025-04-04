---
keywords: Experience Platform；主页；热门主题；ui；UI；UI；XDM；XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；数据模型；浏览；类；字段组；数据类型；架构；
solution: Experience Platform
title: 浏览UI中的架构资源
description: 了解如何在Experience Platform用户界面中探索现有架构、类、架构字段组和数据类型。
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# 浏览UI中的架构资源

在Adobe Experience Platform中，所有Experience Data Model (XDM)架构资源都存储在[!DNL Schema Library]中，包括由Adobe提供的标准资源和由您的组织定义的自定义资源。 在Experience Platform UI中，您可以查看[!DNL Schema Library]中任何现有架构、类、字段组或数据类型的结构和字段。 在规划和准备数据引入时，此功能特别有用，因为UI提供了有关这些XDM资源提供的每个字段的预期数据类型和用例的信息。

本教程介绍了在Experience Platform UI中浏览现有架构、类、字段组和数据类型的步骤。

## 查找架构资源 {#lookup}

在Experience Platform UI的左侧导航中选择&#x200B;**[!UICONTROL 架构]**。 [!UICONTROL 架构]工作区提供了&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡以浏览组织中的所有架构，还提供了额外的专用选项卡，分别用于浏览&#x200B;**[!UICONTROL 类]**、**[!UICONTROL 字段组]**、**[!UICONTROL 数据类型]**&#x200B;和&#x200B;**[!UICONTROL 关系]**。

![突出显示带有多个选项卡的架构工作区。](../images/ui/explore/tabs.png)

筛选器图标（![筛选器图标图像](/help/images/icons/filter.png)）在左边栏中显示控件，以缩小列出的结果的范围。 资源筛选器分别可用于&#x200B;**[!UICONTROL 浏览]**&#x200B;和&#x200B;**[!UICONTROL 关系]**&#x200B;选项卡上的架构和关系。

在[!UICONTROL 架构]工作区的[!UICONTROL 浏览]选项卡上，您可以筛选架构清单。 使用&#x200B;**[!UICONTROL 包含在配置文件]**&#x200B;切换可仅显示已启用以便在[实时客户配置文件](../../profile/home.md)中使用的架构。 使用&#x200B;**[!UICONTROL 显示临时架构]**&#x200B;切换开关筛选使用仅供单个数据集使用的命名空间字段创建的架构列表。

![突出显示筛选器面板的[!UICONTROL 架构]工作区[!UICONTROL 浏览]选项卡。](../images/ui/explore/filters.png)

在[!UICONTROL 架构]工作区的[!UICONTROL 关系]选项卡上，您可以根据四个条件筛选关系列表。 这些筛选器包括[!UICONTROL Source架构]、[!UICONTROL 目标架构]、[!UICONTROL Source类]和[!UICONTROL 目标类]。 下表提供了这些过滤器的说明。

| 筛选条件 | 描述 |
|-----------------------------------|------------|
| [!UICONTROL Source架构] | 要查看所选架构是起点或“源”的所有关系，请从[!UICONTROL Source架构]下拉菜单中选择架构。 |
| [!UICONTROL 目标架构] | 要查看所选架构为目标或“目标”的所有关系，请从[!UICONTROL 目标架构]下拉菜单中选择架构。 |
| [!UICONTROL Source类] | 要根据初始架构的类筛选关系，请从[!UICONTROL Source class]下拉菜单中选择类。 |
| [!UICONTROL 目标类] | 要显示以特定类的架构结尾的关系，请从[!UICONTROL 目标类]下拉菜单中选择类。 |

{style="table-layout:auto"}

![突出显示筛选条件部分的“关系”选项卡。](../images/ui/explore/relationships-filter.png)

您还可以使用搜索栏进一步缩小结果的范围。

![突出显示搜索字段的架构工作区的“浏览”选项卡。](../images/ui/explore/search.png)

搜索结果中显示的资源首先按标题匹配项排序，然后按说明匹配项排序。 反过来，这两个类别中的匹配词越多，列表中显示的资源就越多。

找到要浏览的资源后，从列表中选择其名称，以在画布中查看其结构。

## 在画布中浏览XDM资源 {#explore}

选择资源后，其结构将在画布中打开。

![显示Commerce数据类型的数据类型工作区画布。](../images/ui/explore/canvas.png)

默认情况下，包含子属性的所有对象类型字段在首次出现在画布中时会折叠。 要显示任何字段的子属性，请选择其名称旁边的图标。

![已展开字段和子属性突出显示的数据类型工作区画布。](../images/ui/explore/field-expand.png)

### 标准类和字段组指示器 {#standard-class-and-field-group-indicator}

在架构编辑器中，标准(Adobe生成的)类和字段组以挂锁图标（![A挂锁图标）表示。](/help/images/icons/lock-closed.png)的问题。挂锁显示在左边栏中的类或字段组名称旁边，以及架构图中作为系统生成资源一部分的任意字段旁边。

![带有挂锁图标的架构编辑器突出显示](../images/ui/explore/schema-editor-padlock-icon.png)

有关指导，请参阅[将自定义字段添加到标准字段组](./resources/schemas.md)文档。 不能编辑标准类。

### 系统生成的字段 {#system-fields}

某些字段名称的前面带有下划线，如`_repo`和`_id`。 这些表示系统将在摄取数据时自动生成和分配的字段的占位符。

因此，在摄取到Experience Platform时，应该从数据结构中排除这些字段中的大多数。 此规则的主要例外是[`_{TENANT_ID}`字段](../api/getting-started.md#know-your-tenant_id)，在您的组织下创建的所有XDM字段都必须在此字段下命名空间。

### 数据类型 {#data-types}

对于画布中显示的每个字段，其对应的数据类型会显示在名称旁边，这概览field希望摄取的数据类型。

![画布上显示的“邮政地址”数据类型及其关联的数据类型突出显示。](../images/ui/explore/data-types.png)

任何附加了方括号(`[]`)的数据类型均表示该特定数据类型的数组。 例如，**[!UICONTROL String]\[]**&#x200B;的数据类型指示该字段需要字符串值的数组。 **[!UICONTROL 付款项]\[]**&#x200B;的数据类型表示符合[!UICONTROL 付款项]数据类型的对象数组。

如果数组字段基于对象类型，则可以在画布中选择其图标，以显示每个数组项的预期属性。

![画布中的对象，其数组字段突出显示，并显示每个数组项的预期属性。](../images/ui/explore/array-type.png)

### [!UICONTROL 字段属性] {#field-properties}

当您选择画布中任何字段的名称时，右边栏会更新，以在&#x200B;**[!UICONTROL 字段属性]**&#x200B;下显示有关该字段的详细信息。 这可以包括字段的预期用例、默认值、模式、格式、字段是否为必填等的描述。

![从Commerce数据类型中选择的字段具有突出显示的字段属性。](../images/ui/explore/field-properties.png)

如果您要检查的字段是枚举字段，则右边栏还会显示该字段预期接收的可接受值。

![架构编辑器，在字段属性边栏中选择了字段，并且枚举值和显示名称高亮显示。](../images/ui/explore/enum-field.png)

### 身份标识字段 {#identity}

检查包含身份字段的架构时，这些字段在左边栏中列在提供给架构的类或字段组下。 选择左边栏中的身份字段名称以显示画布中的字段，无论其嵌套深度如何。

在画布中用指纹图标（![指纹图标图像](/help/images/icons/identity-service.png)）突出显示身份字段。 如果选择身份字段的名称，则可以查看其他信息，如[身份命名空间](../../identity-service/features/namespaces.md)，以及该字段是否为架构的主要身份。

![架构编辑器在左边栏中突出显示了架构的标识，在架构图表中突出显示了字段，在字段属性中突出显示了标识命名空间。](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>有关标识字段及其与下游Experience Platform服务的关系的详细信息，请参阅[定义标识字段](./fields/identity.md)指南。

### 关系字段 {#relationship}

如果要检查包含关系字段的架构，则该字段将列在左边栏中的&#x200B;**[!UICONTROL 关系]**&#x200B;下。 选择左边栏中的关系字段名称以显示画布中的字段，无论其嵌套深度如何。 关系字段在画布中也以唯一方式高亮显示，显示字段链接到的引用架构的名称。 对于具有B2B功能的组织，可以编写自定义关系名称，并在这些情况下显示在画布上。

![架构编辑器突出显示了关系字段和编辑关系。](../images/ui/explore/relationship-field.png)

要查看引用架构的主要标识的标识命名空间，请选择关系字段，然后在[!UICONTROL 字段属性]侧边栏中&#x200B;**[!UICONTROL 编辑关系]**。 关系的参数显示在显示的[!UICONTROL 编辑关系]对话框中。

![显示具有关系参数的“编辑关系”对话框。](../images/ui/explore/edit-relationship-dialog.png)

有关在XDM架构中使用关系的详细信息，请参阅有关[在UI](../tutorials/relationship-ui.md)中创建关系的教程。

## 后续步骤

本文档介绍了如何在Experience Platform UI中探索现有XDM资源。 有关[!UICONTROL 架构]工作区和[!DNL Schema Editor]的不同功能的详细信息，请参阅[[!UICONTROL 架构]工作区概述](./overview.md)。

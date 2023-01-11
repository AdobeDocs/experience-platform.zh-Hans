---
keywords: Experience Platform；主页；热门主题；UI;XDM;XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；浏览；类；字段组；数据类型；架构；
solution: Experience Platform
title: 在UI中浏览架构资源
description: 了解如何在Experience Platform用户界面中探索现有模式、类、模式字段组和数据类型。
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 0%

---

# 在UI中浏览架构资源

在Adobe Experience Platform中，所有体验数据模型(XDM)架构资源都存储在 [!DNL Schema Library]，包括由Adobe提供的标准资源和由您的组织定义的自定义资源。 在Experience PlatformUI中，您可以在 [!DNL Schema Library]. 在规划和准备数据摄取时，这特别有用，因为UI提供了有关这些XDM资源提供的每个字段的预期数据类型和用例的信息。

本教程介绍了在Experience PlatformUI中探索现有架构、类、字段组和数据类型的步骤。

## 查找架构资源 {#lookup}

在平台UI中，选择 **[!UICONTROL 模式]** 中。 的 [!UICONTROL 模式] 工作区提供 **[!UICONTROL 浏览]** 选项卡，以浏览组织中的所有模式，以及用于浏览的其他专用选项卡 **[!UICONTROL 类]**, **[!UICONTROL 字段组]**&#x200B;和 **[!UICONTROL 数据类型]** 分别进行。

![](../images/ui/explore/tabs.png)

过滤器图标(![过滤器图标图像](../images/ui/explore/icon.png))会显示左边栏中的控件，以缩小列出的结果范围。 显示的控件因所列资源类型而异。

例如，要过滤列表以仅显示由Adobe提供的标准数据类型，请选择 **[!UICONTROL 数据类型]** 和 **[!UICONTROL Adobe]** 下 **[!UICONTROL 类型]** 和 **[!UICONTROL 所有者]** 部分。

的 **[!UICONTROL 包含在用户档案中]** 切换允许您筛选结果以仅显示在已启用以供使用的架构中使用的资源 [实时客户资料](../../profile/home.md).

![](../images/ui/explore/filter.png)

在 **[!UICONTROL 类]**, **[!UICONTROL 字段组]**&#x200B;或 **[!UICONTROL 数据类型]** 选项卡，您可以选择 **[!UICONTROL Adobe]** 仅显示标准资源或 **[!UICONTROL 客户]** 以仅显示您的组织创建的资源。

![](../images/ui/explore/filter-data-type.png)

您还可以使用搜索栏进一步缩小结果范围。

![](../images/ui/explore/search.png)

搜索结果中显示的资源首先按标题匹配、描述匹配进行排序。 反过来，其中任一类别中匹配的词越多，资源在列表中显示得越高。

找到要浏览的资源后，从列表中选择其名称以在画布中查看其结构。

## 在画布中浏览XDM资源 {#explore}

选择资源后，其结构将在画布中打开。

![](../images/ui/explore/canvas.png)

默认情况下，当包含子属性的所有对象类型字段首次显示在画布中时，这些字段都会折叠。 要显示任何字段的子属性，请选择其名称旁边的图标。

![](../images/ui/explore/field-expand.png)

### 系统生成的字段 {#system-fields}

某些字段名称前面加有下划线，例如 `_repo` 和 `_id`. 这些表示在摄取数据时系统将自动生成和分配的字段的占位符。

因此，在摄取到Platform时，这些字段中的大部分都应从数据结构中排除。 此规则的主要例外是 [`_{TENANT_ID}` 字段](../api/getting-started.md#know-your-tenant_id)，在您的组织下创建的所有XDM字段都必须与下面的字段同名。

### 数据类型 {#data-types}

对于画布中显示的每个字段，其名称旁边会显示其相应的数据类型，一目了然地显示该字段预期摄取的数据类型。

![](../images/ui/explore/data-types.png)

附加有方括号(`[]`)表示该特定数据类型的数组。 例如，数据类型为 **[!UICONTROL 字符串]\[]** 指示字段应为字符串值数组。 数据类型 **[!UICONTROL 付款项]\[]** 指示符合 [!UICONTROL 付款项] 数据类型。

如果数组字段基于对象类型，则可以在画布中选择其图标，以显示每个数组项目的预期属性。

![](../images/ui/explore/array-type.png)

### [!UICONTROL 字段属性] {#field-properties}

在画布中选择任意字段的名称时，右边栏会更新以显示下方有关该字段的详细信息 **[!UICONTROL 字段属性]**. 这可以包括对字段预期用例、默认值、模式、格式、字段是否为必填字段的描述等。

![](../images/ui/explore/field-properties.png)

如果您检查的字段是枚举字段，则右边栏还将显示该字段预期接收的可接受值。

![](../images/ui/explore/enum-field.png)

### 标识字段 {#identity}

检查包含标识字段的架构时，这些字段会列在提供给架构的类或字段组的左边栏中。 选择左边栏中的标识字段名称以在画布中显示该字段，无论其嵌套的深度如何。

标识字段在画布中以指纹图标(![指纹图标图像](../images/ui/explore/identity-symbol.png))。 如果选择标识字段的名称，则可以查看其他信息，例如 [标识命名空间](../../identity-service/namespaces.md) 以及字段是否是架构的主标识。

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>请参阅 [定义标识字段](./fields/identity.md) 有关身份字段及其与下游Platform服务的关系的更多信息。

### 关系字段 {#relationship}

如果您正在检查包含关系字段的架构，则该字段将列在 **[!UICONTROL 关系]**. 选择左边栏中的关系字段名称以在画布中显示该字段，无论其嵌套的深度如何。

关系字段也在画布中以唯一方式突出显示，显示字段引用的目标架构的名称。 如果选择关系字段的名称，则可以在右边栏中查看目标架构主标识的标识命名空间。

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>请参阅 [在UI中创建关系](../tutorials/relationship-ui.md) 有关在XDM模式中使用关系的更多信息。

## 后续步骤

本文档介绍了如何在Experience PlatformUI中浏览现有XDM资源。 有关 [!UICONTROL 模式] 工作区和 [!DNL Schema Editor]，请参阅 [[!UICONTROL 模式] 工作区概述](./overview.md).

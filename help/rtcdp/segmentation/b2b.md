---
title: Real-time CDP B2B Edition的分段用例概述。
description: 概述各种可用的实时CDP B2B Edition用例。
source-git-commit: e85d4b108e2d4a6a88772c071d9281603b695ada
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 实时客户数据平台B2B版（测试版）分段用例概述

<!-- This document relates to this [ticket](https://jira.corp.adobe.com/browse/PLAT-100468) -->

>[!IMPORTANT]
>
>Real-time CDP B2B Edition目前处于测试阶段。 文档和功能可能会发生变化。

本文档提供了有关Real-time CDP B2B Edition可用的分段示例，以及如何针对常见的B2B用例组合不同类型的属性。

>[!NOTE]
>
>这些分段用例所需的属性仅适用于实时客户数据平台B2B版客户。 要进一步了解Real-time CDP ，包括每种许可证类型可用的特性和功能，请首先阅读[Real-time CDP overview](../overview.md)。

## 先决条件

您必须先完成以下步骤，然后才能对B2B类使用分段属性：

1. 创建使用B2B类的架构。 B2B版本类包括Account 、 Campaign 、 Opportunity 、 Marketing List等。 有关[如何设置用于B2B类的架构的信息](../schemas/b2b.md) ，请参阅架构文档。
1. 在您的体验数据模型(XDM)B2B架构之间创建关系。 基于B2B版属性的区段需要类之间的关系才能充分利用扩展的B2B分段功能。 有关更多信息，请参阅[如何定义两个B2B架构之间的关系文档](../../xdm/tutorials/relationship-b2b.md)。
1. 使用基于B2B模式的数据集摄取数据。 有关如何摄取数据的信息，请参阅源文档[。](../../sources/connectors/adobe-applications/marketo/marketo.md)
1. 请阅读[区段生成器用户指南](../../segmentation/ui/segment-builder.md) ，了解有关如何构建区段的更详细指南。

满足这些要求后，您便可以将这些属性组合到常用的B2B用例中。

## 快速入门

在B2B类的并集架构建立关系并用于摄取数据后，区段生成器的左边栏中便会提供其属性。

B2B类及其属性会在分段工作区中附加一个`B2B`标签，以区分它们与实时客户数据平台中作为标准提供的类别。

为了有效地为B2B用例创建区段，必须深入了解模式并了解数据模型的外观。 此外，了解数据从一个数据对象获取到另一个数据对象的路径也非常有用。

下图说明了Real-time CDP B2B Edition中可用的B2B类之间的关系。

![B2B类ERD](../assets/segmentation/b2b-classes.png)

由于数据模型可能非常复杂，因此您可以使用Platform UI查看数据模型的更详细可视化表示形式，以帮助查找用例的相关属性。 要开始，请转到Platform UI并在左侧导航中选择架构。

从可用列表中选择相应的架构，然后从[!UICONTROL 组合]侧边栏中选择相应的关系。 在以下示例中，选择“人员”关系会显示当前架构中引用相关“人员”架构的属性（如果它是关系中的源架构），或者“人员”架构引用（如果它是关系中的目标架构）。

![在架构工作区中使用人员关系的源键示例](../assets/segmentation/source-key-schema-relationship-example.png)

此关系通过使用`Key`文件夹反映在区段生成器中，如下图所示。

![使用分段工作区中的区段生成器的源键示例](../assets/segmentation/source-key-segmentation-example.png)

有关可用B2B类的更多信息，请参阅实时客户数据平台B2B版本中的[架构文档](../schemas/b2b.md)。

下面的用例提供了有关哪些类用于在不同模式之间建立关系以实现这些结果的信息。 这些示例可帮助您创建自己的区段。

## 不同用例的示例

以下用例可用于使用B2B Edition进行分段。 每个示例都提供了区段功能的描述以及用于创建区段的类的描述。 提供的图像突出显示了[!UICONTROL Attributes]边栏中反映架构结构的文件路径。 显示右侧的[!UICONTROL 区段属性]部分包含区段属性的书面划分。

### 示例 1

找到所有机会的“决策者”。 此区段要求在[!UICONTROL XDM Individual Profile]类和[!UICONTROL XDM Business Opportunity Person Relation]类之间建立链接。

![显示示例1设置的UI](../assets/segmentation/example-1.png)

### 示例 2

查找直接分配到任何机会的人员，其中机会金额大于给定金额（100万美元）。 此区段要求在[!UICONTROL XDM Individual Profile]类、[!UICONTROL XDM Business Opportunity Person Relation]类和[!UICONTROL XDM Business Opportunity]类之间建立链接。

![显示示例2设置的UI](../assets/segmentation/example-2.png)

### 示例3

查找直接分配到帐户位于给定位置的任何业务机会的所有人员（加拿大）。 此区段要求在[!UICONTROL XDM Individual Profile]类、[!UICONTROL XDM Business Opportunity Person Relation]类、[!UICONTROL XDM Business Opportunity]类和[!UICONTROL XDM Business Account]类之间建立链接。

![显示示例3设置的UI](../assets/segmentation/example-3.png)

### 示例4

查找帐户位于“金融”行业的任意机会的“决策者”，并在最近三天访问定价页面的所有人员。 此区段要求在[!UICONTROL XDM Individual Profile]类、[!UICONTROL XDM Business Opportunity Person Relation]类、 [!UICONTROL XDM Business Opportunity]类和[!UICONTROL XDM Business Account]类和[!UICONTROL XDM ExperienceEvent]类之间建立链接。

![显示示例4设置的UI](../assets/segmentation/example-4.png)

### 示例5

查找在人力资源部（人力资源部）工作并且与任何具有至少一个机会（价值100万美元）或更高金额的帐户相关的所有人员。 此区段要求在[!UICONTROL XDM Indivial Profile]类、[!UICONTROL XDM Business Account]类和[!UICONTROL XDM Business Opportunity]类之间建立链接。

![显示示例5设置的UI](../assets/segmentation/example-5.png)

### 示例6

查找所有职位为副总裁且与任何年收入达到指定金额（1亿美元）或更高的帐户相关的人员，并在上个月至少访问了定价页面3次。 此区段需要在[!UICONTROL XDM个人配置文件]类、[!UICONTROL XDM业务帐户]类和[!UICONTROL XDM ExperienceEvent]类之间建立链接。

![显示示例6设置的UI](../assets/segmentation/example-6.png)

### 示例7

查找所有属于任何已关闭的销售机会的“决策者”，并在上周访问定价页面。 此区段要求在[!UICONTROL XDM Individual Profile]类、[!UICONTROL XDM Business Opportunity Person Relation]类、[!UICONTROL XDM Business Opportunity]类和[!UICONTROL XDM ExperienceEvent]类之间建立链接。

![显示示例7设置的UI](../assets/segmentation/example-7.png)

## 后续步骤

在阅读此概述后，您现在可以了解使用Real-time CDP B2B Edition提供的分段可能性。 有关Segmentation Service的更多信息，请阅读[Segmentation文档](../../segmentation/home.md)。

---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: XDM模式和描述符
topic: tutorial
type: Tutorial
description: 标准化和互操作性是Adobe Experience Platform背后的关键概念。 体验Adobe模型(XDM)由客户驱动，旨在实现客户体验数据标准化并为客户体验管理定义模式。 模式是描述Experience Platform中数据的标准方法，它允许符合模式的所有数据在整个组织内重复使用，而不会发生冲突，甚至可以在多个组织之间共享。
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# 使用( [!DNL Experience Data Model] XDM)模式和关系描述符

标准化和互操作性是Adobe Experience Platform背后的关键概念。 [!DNL Experience Data Model] (XDM)由Adobe驱动，旨在实现客户体验数据标准化并定义客户体验管理模式。 模式是描述中数据的标准方法，它允 [!DNL Experience Platform]许所有符合模式的数据可重复使用，而不会在组织内发生冲突，甚至可以在多个组织之间共享。 要进一步了解XDM模式，请阅读XDM系统 [概述开始](../xdm/home.md)。

## 使用模式注册表创建模式

模式注册表提供用户界面和RESTful API，您可以从中视图和管理Adobe Experience Platform模式库中的所有资源。 模式库包含由Adobe、合作伙伴和您使用其应用程 [!DNL Experience Platform] 序的供应商提供给您的资源，以及您定义并保存到模式注册表的资源。 要了解如何为组织创建模式，请按照教程使用 [模式注册表API创建模式](../xdm/tutorials/create-schema-api.md) , [或使用模式编辑器用户界面创建模式](../xdm/tutorials/create-schema-ui.md)。

## 定义两个模式之间的关系

了解不同渠道客户之间的关系及其与您品牌的互动是Adobe Experience Platform的重要部分。 在(XDM)模式结构中定 [!DNL Experience Data Model] 义这些关系，使您能够对客户数据获得复杂的洞察。 这些关系描述符可以使用模式注册表API和模式编辑器UI进行定义。 有关详细信息，请参阅使用API或UI定义两 [个模式之](../xdm/tutorials/relationship-api.md) 间 [关系的教程](../xdm/tutorials/relationship-ui.md)。

## 创建点对点模式

在特定情况下，可能需要创建一个( [!DNL Experience Data Model] XDM)模式，其中的字段以名称命名，仅供单个数据集使用。 这称为“临时”模式。 临时模式用于各种数据 [获取工作流](../ingestion/home.md) , [!DNL Experience Platform]包括获取CSV文件和创建某些类型 [的源连接](../sources/home.md)。 创建点对点模式是使用模式注册表API完成的，并准备与需要创建点对点模式作为其工作流的一部分的其 [!DNL Experience Platform] 他教程一起使用。 要开始创建点对点模式，请参阅 [使用API创建点对点模式的教程](../xdm/tutorials/ad-hoc.md)。

## 后续步骤

为组织定义模式后，您可以开始创建可摄取数据的数据集。 要开始，请参阅以下文档：

* [数据集概述](../catalog/datasets/overview.md)
* [数据摄取概述](../ingestion/home.md)
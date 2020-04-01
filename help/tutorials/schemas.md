---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: XDM模式和描述符
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# 使用体验数据模型(XDM)模式和关系描述符

标准化和互操作性是Adobe Experience Platform的主要概念。 Adobe推动的体验数据模型(XDM)旨在标准化客户体验数据并定义客户体验管理模式。 模式是描述Experience Platform中数据的标准方式，它允许符合模式的所有数据可重用，而不会在组织之间发生冲突，甚至可以在多个组织之间共享。 要进一步了解XDM模式，请阅读 [XDM系统概述进行开始](../xdm/home.md)。

## 使用模式注册表创建模式

模式注册表提供用户界面和RESTful API，您可以从中视图和管理Adobe Experience Platform模式库中的所有资源。 模式库包含Adobe、Experience Platform合作伙伴、您使用应用程序的供应商为您提供的资源以及您定义并保存到模式注册表的资源。 要了解如何为组织创建模式，请按照以下教程操作：使用 [模式注册表API创建模式](../xdm/tutorials/create-schema-api.md) ，或 [使用模式编辑器用户界面创建模式](../xdm/tutorials/create-schema-ui.md)。

## 定义两个模式之间的关系

了解客户之间的关系以及他们与不同渠道品牌之间的交互是Adobe Experience Platform的重要组成部分。 在体验数据模型(XDM)模式的结构中定义这些关系使您能够获得对客户数据的复杂洞察。 这些关系描述符可以使用模式注册表API和模式编辑器UI进行定义。 有关详细信息，请参阅使用API或UI定义两个模式 [之间关系](../xdm/tutorials/relationship-api.md)[的教程](../xdm/tutorials/relationship-ui.md)。

## 创建临时模式

在特定情况下，可能需要创建一个体验数据模型(XDM)模式，其中的字段以仅由单个数据集使用的名称命名。 这称为&quot;临时&quot;模式。 Ad-hoc模式用于Experience Platform的各种数 [据获取](../ingestion/home.md) 工作流，包括获取CSV文件和创建某些类型的源 [连接](../source-connectors/home.md)。 创建临时模式是使用模式注册表API完成的，并准备与其他体验平台教程一起使用，这些教程需要创建临时模式作为其工作流程的一部分。 要开始创建点对点模式，请参阅使用API [创建点对点模式的教程](../xdm/tutorials/ad-hoc.md)。

## 后续步骤

为组织定义模式后，您可以开始创建可收录数据的数据集。 要开始，请参阅以下文档：

* [数据集概述](../catalog/datasets/overview.md)
* [数据摄取概述](../ingestion/home.md)
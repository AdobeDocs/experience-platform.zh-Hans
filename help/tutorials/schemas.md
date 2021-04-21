---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: XDM模式和描述符
topic-legacy: tutorial
type: Tutorial
description: 标准化和互操作性是Adobe Experience Platform的主要概念。 由Adobe驱动的体验数据模型(XDM)旨在实现客户体验数据标准化并定义客户体验管理模式。 模式是描述Experience Platform中数据的标准方式，它允许符合模式的所有数据可重复使用，而不会在组织内发生冲突，甚至可以在多个组织之间共享。
exl-id: 1cdc45d7-57ca-4a2d-99a4-9a8cd885a511
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# 使用[!DNL Experience Data Model](XDM)模式和关系描述符

标准化和互操作性是Adobe Experience Platform的主要概念。 [!DNL Experience Data Model] (XDM)由Adobe驱动，旨在实现客户体验数据标准化并定义客户体验管理模式。模式是描述[!DNL Experience Platform]中数据的标准方式，它允许符合模式的所有数据可重复使用，而不会在组织之间发生冲突，甚至可以在多个组织之间共享。 要进一步了解XDM模式，请阅读[XDM系统概述](../xdm/home.md)进行开始。

## 使用模式注册表创建模式

模式 Registry提供了一个用户界面和RESTful API，您可以从中视图和管理Adobe Experience Platform模式库中的所有资源。 模式库包含由Adobe、[!DNL Experience Platform]合作伙伴、您使用应用程序的供应商提供给您的资源，以及您定义并保存到模式注册表的资源。 要了解如何为您的组织创建模式，请按照以下教程操作：[使用模式 Registry API](../xdm/tutorials/create-schema-api.md)或[使用模式 Editor用户界面](../xdm/tutorials/create-schema-ui.md)创建模式。

## 定义两个模式之间的关系

了解不同渠道客户之间的关系及其与品牌互动是Adobe Experience Platform的重要部分。 在[!DNL Experience Data Model](XDM)模式的结构中定义这些关系使您能够获得对客户数据的复杂洞察。 这些关系描述符可以使用模式 Registry API和模式 Editor UI进行定义。 有关详细信息，请参阅使用UI](../xdm/tutorials/relationship-ui.md)使用API](../xdm/tutorials/relationship-api.md)或[定义两个模式[之间关系的教程。

## 创建点对点模式

在特定情况下，可能需要创建一个[!DNL Experience Data Model](XDM)模式，其中的字段以仅由单个数据集使用命名。 这称为“临时”模式。 在[!DNL Experience Platform]的各种[模式摄取](../ingestion/home.md)工作流中使用Ad-hoc，包括摄取CSV文件和创建某些类型的[源连接](../sources/home.md)。 创建点对点模式是使用模式 Registry API完成的，它旨在与其他需要创建点对点模式作为其工作流的一部分的[!DNL Experience Platform]教程一起使用。 要开始创建点对点模式，请参阅使用API](../xdm/tutorials/ad-hoc.md)创建点对点模式的教程。[

## 后续步骤

为组织定义模式后，您可以开始创建可摄取数据的数据集。 要开始，请参阅以下文档：

* [数据集概述](../catalog/datasets/overview.md)
* [数据摄取概述](../ingestion/home.md)

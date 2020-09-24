---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据治理和隐私教程
topic: tutorial
type: Tutorial
description: 本文档概述了与Adobe Experience Platform数据治理和Adobe Experience Platform Privacy Service相关的各种可用教程。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---


# [!DNL Data Governance] 和 [!DNL Privacy] Tutorials

Adobe Experience Platform数据管理使您能够将数据使用标签应用于数据集和字段，根据相关数据使用策略对每个数据进行分类，并在对这些数据集和／或字段执行某些操作时评估策略违规情况。 在开始使用本文档中列出的教程之前，请参 [[!DNL Data Governance] 阅概述](../data-governance/home.md) ，以获得框架的更强大的介绍。

Adobe Experience Platform [!DNL Privacy Service] 提供了RESTful API和用户界面，使您能跨各种解决方案协调隐私和合规要求。 要了解更多信息，请首先阅读 [Privacy Service概述](../privacy-service/home.md)。

## 添加数据使用标签

数据使用标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 可随时应用标签，在数据管理方式上提供灵活性。 最佳实践是，在数据被引入或 [!DNL Experience Platform]数据可供使用时，立即添加标签 [!DNL Platform]。 在数据集级别应用的数据使用标签将传播到数据集中的所有字段。 标签还可以直接应用于数据集中的各个字段（列标题），而不会传播。 要了解如何将数据使用标签应用于您的数据，请访 [问数据使用标签概述](../data-governance/labels/overview.md)。

## 创建数据使用策略

API [!DNL Policy Service] 允许您创建和管理数据使用策略，以确定可以对包含某些使用标签的数据采取哪些营销操作。 要开始，请阅读数据使 [用策略概述](../data-governance/policies/overview.md)。

## 实施数据使用策略

为数据添加了使用标签，并针对这些标签创建了营销操作策略后，您便可以使用评估在对数据集或任意使用标签组执行营销 [!DNL Policy Service API] 操作时，是否构成策略违规。 然后，您可以设置自己的内部协议，根据API响应处理策略违规。 要开始，请访问策 [略实施概述](../data-governance/enforcement/overview.md)。

## 为受众区段强制实施数据使用合规性

允许在中使用的区段 [!DNL Real-time Customer Profile] 在其区段定义中包含合并策略ID。 此合并策略包含有关区段中要包含哪些数据集的信息，这些数据集又包含任何适用的数据使用标签。 有关强制受众区段遵守数据使用规范的具体步骤，请遵循区 [段的数据使用规范实施教程](../segmentation/tutorials/governance.md)。

## Get started with [!DNL Privacy Service]

[!DNL Privacy Service] 提供RESTful API和用户界面，允许您跨Adobe Experience Cloud应用程序管理数据主体（客户）的个人数据。 [!DNL Privacy Service] 还提供了一个中央审计和日志记录机制，允许您访问涉及应用程序的作业的状态和 [!DNL Experience Cloud] 结果。 有关如何创建和监视作业的 [!DNL Privacy Service] 说明，请按照Privacy Service开发人员指 [南或Privacy Service用户指](../privacy-service/api/getting-started.md) 南中提供的步骤操作 [](../privacy-service/ui/overview.md)。
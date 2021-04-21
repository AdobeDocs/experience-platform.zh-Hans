---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 数据治理和隐私教程
topic-legacy: tutorial
type: Tutorial
description: 本文档概述了与Adobe Experience Platform数据治理和Adobe Experience Platform Privacy Service相关的不同教程。
exl-id: c3cef447-b343-445b-a3ed-54f873f6dfb9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# [!DNL Data Governance] 和 [!DNL Privacy] Tutorials

Adobe Experience Platform Data Governance使您能够将数据使用标签应用于数据集和字段，根据相关数据使用策略对每个数据进行分类，并在对这些数据集和/或字段执行某些操作时评估策略违规情况。 在开始使用本文档中列出的教程之前，请参阅[[!DNL Data Governance] 概述](../data-governance/home.md)以了解框架的更加强大的介绍。

Adobe Experience Platform [!DNL Privacy Service]提供一个RESTful API和用户界面，允许您协调各种解决方案中的隐私和合规性请求。 要了解更多信息，请首先阅读[Privacy Service概述](../privacy-service/home.md)。

## 添加数据使用标签

数据使用标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 可随时应用标签，在您选择如何管理数据方面提供灵活性。 最佳做法鼓励在将数据引入[!DNL Experience Platform]或数据可用于[!DNL Platform]时立即标记数据。 在数据集级别应用的数据使用标签将传播到数据集中的所有字段。 标签还可以直接应用于数据集中的各个字段（列标题），而不会进行传播。 要了解如何将数据使用标签应用到您的数据，请访问[数据使用标签概述](../data-governance/labels/overview.md)。

## 创建数据使用策略

[!DNL Policy Service] API允许您创建和管理数据使用策略，以确定可以对包含某些使用标签的数据采取哪些营销操作。 要开始，请阅读[数据使用策略概述](../data-governance/policies/overview.md)。

## 实施数据使用策略

在为数据添加了使用标签并针对这些标签创建了市场营销操作的策略后，您可以使用[!DNL Policy Service API]评估在数据集或任意使用标签组上执行市场营销操作时是否构成策略违规。 然后，您可以设置自己的内部协议，以根据API响应处理策略违规。 要开始，请访问[策略实施概述](../data-governance/enforcement/overview.md)。

## 对受众区段强制实施数据使用合规性

允许在[!DNL Real-time Customer Profile]中使用的区段在其区段定义中包含合并策略ID。 此合并策略包含有关区段中要包含哪些数据集的信息，这些数据集又包含任何适用的数据使用标签。 有关强制受众区段符合数据使用规范的具体步骤，请遵循区段](../segmentation/tutorials/governance.md)[数据使用符合性实施教程。

## [!DNL Privacy Service] 快速入门

[!DNL Privacy Service] 提供RESTful API和用户界面，允许您跨Adobe Experience Cloud应用程序管理数据主体（客户）的个人数据。[!DNL Privacy Service] 还提供一个中央审核和日志记录机制，允许您访问涉及应用程序的作业的状态和 [!DNL Experience Cloud] 结果。有关如何创建和监视[!DNL Privacy Service]作业的说明，请按照[Privacy Service开发人员指南](../privacy-service/api/getting-started.md)或[Privacy Service用户指南](../privacy-service/ui/overview.md)中提供的步骤进行操作。

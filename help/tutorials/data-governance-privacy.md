---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据管理和隐私教程
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# 数据管理和隐私教程

数据使用标签和强制执行(DULE)是Adobe Experience Platform数据管理的核心机制。 DULE功能允许您将数据使用标签应用到数据集和字段，并根据相关的数据使用策略对每个标签进行分类。 在开始使用标签之前，请参阅 [数据管理概述](../data-governance/home.md) ，以了解有关平台中DULE框架的更强大介绍。

Adobe Experience Platform Privacy Service提供RESTful API和用户界面，使您能跨各种解决方案协调隐私和合规性请求。 要了解更多信息，请首先阅读隐私 [服务概述](../privacy-service/home.md)。

## 添加数据使用标签

数据使用标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 可随时应用标签，从而提供灵活的数据管理方式。 最佳实践是，在将数据引入Experience Platform时或在数据可用于Platform时立即标记数据。 在数据集级别应用的数据使用标签将传播到数据集中的所有字段。 标签还可以直接应用于数据集中的各个字段（列标题），而不会传播。 要了解如何将数据使用标签应用到您的数据，请访问数 [据使用标签概述](../data-governance/labels/overview.md)。

## 创建数据使用策略

DULE Policy Service API允许您创建和管理DULE策略，以确定可以对包含某些DULE标签的数据采取哪些营销操作。 要开始，请阅读数据使 [用策略概述](../data-governance/policies/overview.md)。

## 实施数据使用策略

为数据创建数据使用标签和强制(DULE)标签并针对这些标签创建了营销操作的DULE策略后，您便可以使用DULE Policy Service API评估对数据集或任意DULE标签组执行的营销操作是否构成策略违规。 然后，您可以设置自己的内部协议，以根据API响应处理策略违规。 要开始，请访问策略 [实施概述](../data-governance/enforcement/overview.md)。

## 为受众细分强制实施数据使用合规性

在实时客户用户档案中启用的区段在其区段定义中包含合并策略ID。 此合并策略包含有关区段中要包含哪些数据集的信息，这些数据集又包含任何适用的数据使用标签。 有关强制受众区段遵守数据使用规范的具体步骤，请遵循区 [段的数据使用规范实施教程](../segmentation/tutorials/governance.md)。

## 隐私服务入门

隐私服务提供RESTful API和用户界面，允许您跨Adobe Experience Cloud应用程序管理数据主体（客户）的个人数据。 隐私服务还提供了一个中央审核和记录机制，允许您访问涉及Experience Cloud应用程序的作业的状态和结果。 有关如何创建和监视隐私服务作业的说明，请按照隐私服务开发人员指南或隐私服务用户指南中提 [供的](../privacy-service/api/getting-started.md)[步骤操作](../privacy-service/ui/overview.md)。
---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据使用标签概述
topic: labels
translation-type: tm+mt
source-git-commit: 4b6b9ca5ae7861f8e8b974550be14fbce6efdcf1
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# 数据使用标签概述

数据使用标签和强制执行(DULE)是Adobe Experience Platform数据治理的核心机制。 DULE功能允许您将数据使用标签应用到数据集和字段，并根据相关的数据使用策略对每个标签进行分类。

此文档概述了Experience Platform中的数据使用标签（也称为DULE标签）。 在阅读本指南之前，请参 [阅数据管理概述](../home.md) ，以获得DULE框架的更强健的介绍。

## 了解数据使用标签

数据使用标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 可随时应用标签，在数据管理方式上提供灵活性。 最佳实践是鼓励在数据被引入Experience Platform后或数据可用于Platform时立即标记数据。

在数据集级别应用的数据使用标签将传播到数据集中的所有字段。 标签还可以直接应用于数据集中的各个字段（列标题），而不会传播。

有关Experience Platform中可用的数据使用标签及其代表的使用策略的详细信息，请参阅有关支持的数 [据使用标签的指南](reference.md)。

## 受众段的标签继承

Adobe Experience Platform Segmentation Service创建 [的所有受众细分](../../segmentation/home.md) ，都会继承其相应数据集的使用标签。 这允许在Experience Platform（如实时客户数据平台）之上构建的应用程序在将区段激活到目标时提供自动数据使用策略实施。

除了继承数据集级别标签外，默认情况下，区段还会继承其关联数据集中的所有字段级别标签。 根据基于平台的应用程序使用段的方式，您可以潜在地指定使用哪些字段，从而阻止段从被排除的字段继承标签。

有关自动执行在实时CDP中的工作方式的更多信息，请参 [阅实时CDP数据管理概述](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)。

## 后续步骤

现在，您已经引入了数据使用标签，您可以继续阅读 [用户指南](user-guide.md) ，以了解如何在Experience Platform UI中管理标签。 有关如何使用API管理标签的步骤，请参阅目录服务开发人 [员指南中的相应部分](../../catalog/api/labels.md)。
---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据使用标签概述
topic: labels
translation-type: tm+mt
source-git-commit: 4411018aa1d531b53bbe2431df71829fa07fee75

---


# 数据使用标签概述

数据使用标签和强制执行(DULE)是Adobe Experience Platform数据管理的核心机制。 DULE功能允许您将数据使用标签应用到数据集和字段，并根据相关的数据使用策略对每个标签进行分类。

本文档概述了Experience Platform中的数据使用标签（也称为DULE标签）。 在阅读本指南之前，请参阅 [数据管理概述](../home.md) ，了解DULE框架的更强大的介绍。

## 了解数据使用标签

数据使用标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 可随时应用标签，从而提供灵活的数据管理方式。 最佳实践是，在将数据引入Experience Platform时或在数据可用于Platform时立即标记数据。

在数据集级别应用的数据使用标签将传播到数据集中的所有字段。 标签还可以直接应用于数据集中的各个字段（列标题），而不会传播。

有关Experience Platform中可用数据使用标签及其代表的使用策略的详细信息，请参阅有关支持的数 [据使用标签的指南](reference.md)。

## 后续步骤

现在，您已经引入了数据使用标签，您可以继续阅读用户指南 [](user-guide.md) ，以了解如何在Experience Platform UI中管理标签。 有关如何使用API管理标签的步骤，请参阅目录服务开发人员指 [南中的相应部分](../../catalog/api/labels.md)。
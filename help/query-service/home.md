---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform查询服务
topic: overview
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# 查询服务概述

Adobe Experience Platform可从各种来源获取数据。 营销人员面临的一个主要挑战是理解这些数据，以获得有关其客户的洞察。 Adobe Experience Platform查询服务允许您使用标准SQL在平台中查询数据，从而简化了这一过程。 使用查询服务，您可以加入数据湖中的任何数据集，并将查询结果捕获为新数据集，以用于报告、机器学习或引入实时客户用户档案。 本文档概述了查询服务在Experience Platform中的角色。

## 使用查询服务

查询服务提供用户界面和RESTful API，您可以从中创建SQL查询以更好地分析数据。 通过用户界面，您可以编写和执行查询,视图先前执行的查询，以及访问IMS组织内用户保存的查询。 用户界面用作沙箱，在较宽的数据集上执行查询之前先测试这些沙箱。 有关在平台内使用交互式服务的更多信息，请参阅 [查询服务用户界面指南](ui/overview.md)。 RESTful API提供了类似的体验，允许您以编程方式编写和执行查询、计划查询以供将来使用和重复，以及为您希望编写的查询创建模板。 有关使用查询服务API的更多信息，请参阅查询服务开 [发人员指南](api/getting-started.md)。

## 查询服务和体验平台服务

查询服务可以与多个Experience Platform服务交互，并可以与之一起使用。 为了充分利用查询服务的功能，建议您熟悉这些服务以及它们与查询服务的交互方式。

### 数据科学工作区

Adobe Experience Platform Data Science Workspace使用机器学习和人工智能从Experience Platform中存储的数据中获得洞察。 数据科学工作区允许数据科学家根据有关客户及其活动的记录和时间序列数据构建方法，从而促进购买倾向和个人可能喜欢和使用的推荐优惠等预测。 通过将查询服务集成到JupyterLab中，您可以在数据科学工作区中使用SQL，从而使您能够探索、转换和分析Adobe Analytics数据。 请阅读数据科学工作区概述，了解有关数据科学工作区的更多信息，以及查询服务集成指南，以了解有关数据科学工作区如何与查询服务交互的更多信息。

### 分段服务

Adobe Experience Platform Segmentation Service允许用户将客户分为具有相似特征的较小组。 随后可以评估这些细分，以便更好地分析实时客户用户档案数据。 查询服务可用于通过在数据湖中运行此段数据的查询来提供此分析。 请阅读分段服务概述，了解有关分段的更多信息，并阅读用户档案查询语言(PQL)指南，了解有关如何分析区段的更多信息。

## 后续步骤

阅读本文档，您便了解了查询服务以及它在更大范围的Experience Platform中的运行方式。 有关与查询服务API中各个端点进行交互的详细信息，请阅读查询服务开发 [人员指南](api/getting-started.md)。 有关在平台内使用交互式服务的更多信息，请阅读 [查询服务用户界面指南](ui/overview.md)。 有关将外部客户端与查询服务连接的全面列表，请阅读 [查询服务客户端概述](clients/overview.md)。

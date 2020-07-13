---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform查询服务
topic: overview
translation-type: tm+mt
source-git-commit: cfd767a05ad4c1dd43ac2bdde1966f9c89f5d219
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---


# 查询服务概述

Adobe Experience Platform从各种来源获取数据。 营销人员面临的一个主要挑战是理解这些数据，以获得客户洞察。 Adobe Experience Platform查询服务允许您使用标准SQL在平台中查询数据，从而方便了这一点。 使用查询服务，您可以加入查询湖中的任何数据集，并将结果捕获为新数据集，以用于报告、机器学习或实时客户用户档案。 本文档概述了查询服务在Experience Platform中的作用。

查询服务使品牌能够连接线上到线下客户旅程并了解全渠道归因。 以下视频展示了体验式企业如何利用查询服务解决关键使用案例，以及查询服务如何工作。

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 使用查询服务

查询服务提供用户界面和REST风格的API，您可以从中创建SQL查询以更好地分析数据。 通过用户界面，您可以编写和执行查询,视图先前执行的查询，以及访问由IMS组织内的用户保存的查询。 该用户界面用作沙箱，在较宽的数据集上执行查询之前测试这些数据。 有关在平台内使用交互式服务的更多信息，请参 [阅查询服务用户界面指南](ui/overview.md)。 RESTful API提供类似的体验，允许您以编程方式编写和执行查询、计划查询以供将来使用和重复，以及为您希望编写的查询创建模板。 有关使用查询服务API的更多信息，请参阅查询服 [务开发人员指南](api/getting-started.md)。

## 查询服务和Experience Platform服务

查询服务交互，可与多个Experience Platform服务结合使用。 为了充分利用查询服务的功能，建议您熟悉这些服务以及它们如何与查询服务交互。

### 数据科学工作区

Adobe Experience Platform数据科学工作区使用机器学习和人工智能从Experience Platform内存储的数据中获得洞察。 数据科学工作区使数据科学家能够根据有关客户及其活动的记录和时间序列数据构建食谱，从而促进购买倾向和推荐优惠等预测，这些预测是个人可能欣赏和使用的。 通过将查询服务集成到JupyterLab中，您可以在数据科学工作区中使用SQL，从而使您能够探索、转换和分析AdobeAnalytics数据。 请阅读数据科学工作区概述，了解有关数据科学工作区的更多信息，以及查询服务集成指南，以了解有关数据科学工作区如何与查询服务交互的更多信息。

### 分段服务

Adobe Experience Platform细分服务允许用户将其客户分成具有相似特征的较小组。 随后可以评估这些细分，以便更好地分析实时客户用户档案数据。 查询服务可用于通过在分析湖中运行此段数据的查询来提供此数据。 请阅读分段服务概述以了解有关分段的更多信息，以及用户档案查询语言(PQL)指南，了解有关如何分析区段的更多信息。

### Looker BI用例

利用Adobe Experience Platform，您可以采集、存储、构建和拉取所有存储的数据集——包括行为、CRM和销售点数据。 利用 [!DNL Experience Platform's Query Service]这些数据集，您可以查询并回答有关业务的特定问题，然后开始产生有影响力的洞察。 以下视频演示了在商业智能(BI)工具中使用构建仪表板的价值 [!DNL Query Service]。

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## 后续步骤和其他资源

阅读本文档，您已被介绍到查询服务，以及它在更大Experience Platform范围内的功能。 有关与查询服务API中各个端点进行交互的详细信息，请阅读查询服务开 [发人员指南](api/getting-started.md)。 有关在平台中使用交互式服务的更多信息，请阅读 [查询服务用户界面指南](ui/overview.md)。 有关将外部客户端与查询服务连接的全面列表，请阅读 [查询服务客户端概述](clients/overview.md)。

为了更好地准备运行查询，请观看以下视频。 此视频分享了在查询编辑器界面、PSQL客户端、商业智能(BI)解决方案和HTTP API中运行查询的技巧和最佳实践。

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)

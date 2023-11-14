---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查询
solution: Experience Platform
title: 查询服务概述
description: 本文档概述了查询服务在Experience Platform中的角色。
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: e59def7a05862ad880d0b6ada13b1c69c655ff90
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# [!DNL Query Service] 概述

Adobe Experience Platform从各种来源摄取数据。 营销人员面临的一个主要挑战是了解此数据以深入了解其客户。 Adobe Experience Platform [!DNL Query Service] 通过允许您使用标准SQL在中查询数据，从而简化了 [!DNL Platform]. 使用 [!DNL Query Service]，您可以加入中的任意数据集 [!DNL Data Lake] 并将查询结果捕获为新的数据集，以用于报表、机器学习或摄取到 [!DNL Real-Time Customer Profile]. 本文档概述了以下角色 [!DNL Query Service] 范围 [!DNL Experience Platform].

[!DNL Query Service] 使品牌商能够连接线上到线下的客户历程并了解全渠道归因。 以下视频演示了体验业务可以如何利用 [!DNL Query Service] 解决主要用例以及如何实施 [!DNL Query Service] 有效。

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 使用 [!DNL Query Service]

[!DNL Query Service] 提供了用户界面和RESTful API，从中可创建SQL查询以更好地分析数据。 通过用户界面，您可以编写和执行查询，查看先前执行的查询，以及访问由您组织内的用户保存的查询。 用户界面旨在用作沙盒，以先测试您的查询，然后再在更广泛的数据集上执行它们。 有关在中使用交互式服务的更多信息 [!DNL Platform] 可在以下位置找到： [查询服务用户界面指南](ui/overview.md). RESTful API提供了类似的体验，允许您以编程方式编写和执行查询，安排查询以供将来使用和重复，以及为要编写的查询创建模板。 有关使用 [!DNL Query Service] API可在以下位置找到： [Query Service开发人员指南](api/getting-started.md).

## [!DNL Query Service] 和 [!DNL Experience Platform] 服务

[!DNL Query Service] 交互，并可与多个 [!DNL Experience Platform] 服务。 为了充分利用 [!DNL Query Service's] 建议您熟悉这些服务以及它们如何与交互 [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] 使用机器学习和人工智能从中存储的数据获得见解 [!DNL Experience Platform]. [!DNL Data Science Workspace] 允许数据科学家根据有关客户及其活动的记录和时间序列数据构建配方，从而促进购买倾向等预测，并提供个人可能会喜欢和使用的推荐选件。 可以在以下位置使用SQL： [!DNL Data Science Workspace] 通过集成 [!DNL Query Service] 到 [!DNL JupyterLab]，可让您探索、转换和分析Adobe Analytics数据。 请阅读 [!DNL Data Science Workspace] 概述以了解有关 [!DNL Data Science Workspace]，和 [!DNL Query Service] 集成指南，以了解关于如何 [!DNL Data Science Workspace] 与交互 [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] 允许用户将其客户划分为具有相似特征的较小组。 随后可以评估这些受众，以更好地分析您的 [!DNL Real-Time Customer Profile] 数据。 [!DNL Query Service] 可用于通过在中对此受众数据运行查询来提供此分析 [!DNL Data Lake]. 请阅读 [!DNL Segmentation Service] 概述，以了解有关分段以及 [!DNL Profile Query Language] (PQL)指南，以了解有关如何分析受众的更多信息。

## 用例

[!DNL Query Service] 提供了灵活的数据处理方法，具有多种用途。 其中包括，它可减轻营销人员的分段负担，并有助于生成切实可行的受众和有意义的业务见解。 以下用例更深入地展示了的强大功能 [!DNL Query Service].

### 放弃Adobe Analytics Browse

此 [浏览放弃示例以使用Adobe为中心 [!DNL Analytics]](./use-cases/abandoned-browse.md) 创建特定可操作受众的数据。 [!DNL Query Service] 为分段提供复杂的逻辑，用于计算各种个性化属性以用于下游，或极大地简化构建受众的方式。

### Looker BI仪表板

借助Adobe Experience Platform，您可以摄取、存储、构造和提取所有存储的数据集，包括行为、CRM和销售点数据。 使用 [!DNL Experience Platform's Query Service]之后，您可以查询这些数据集并回答有关业务的具体问题，然后开始生成有影响力的见解。 以下视频演示了使用在业务智能(BI)工具中构建功能板的价值 [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## 后续步骤和其他资源

通过阅读本文档，我们向您介绍 [!DNL Query Service] 以及如何在更广的范围内运行 [!DNL Experience Platform]. 有关与 [!DNL Query Service] API，请阅读 [Query Service开发人员指南](api/getting-started.md). 有关在中使用交互式服务的更多信息 [!DNL Platform]，请阅读 [查询服务用户界面指南](ui/overview.md). 有关连接外部客户端的完整列表 [!DNL Query Service]，请阅读 [查询服务客户端概述](clients/overview.md).

为了更好地准备运行查询，请观看以下视频。 此视频分享有关在查询编辑器界面、PSQL客户端、商业智能(BI)解决方案和HTTP API中运行查询的提示和最佳实践。

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)

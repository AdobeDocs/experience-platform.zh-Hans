---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查询
solution: Experience Platform
title: 查询服务概述
description: 了解查询服务在Experience Platform中的角色。
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: ad1827284b7070f73421d10c49e1e86e282839eb
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 0%

---

# 查询服务概述

Adobe Experience Platform从各种来源摄取数据。 营销人员面临的一个主要挑战是了解此数据以深入了解其客户。 要在Platform中查询数据，可以使用标准的SQL和Adobe Experience Platform查询服务。 您可以使用查询服务加入数据湖中的任何数据集，并将查询结果捕获为新数据集，以用于报表、机器学习或将其摄取到 [!DNL Real-Time Customer Profile]. 本文档概述了查询服务在Experience Platform中的角色。

您可以使用查询服务连接在线到离线客户历程并了解品牌的全渠道归因。 以下视频演示了体验企业如何使用查询服务解决关键用例以及查询服务的工作方式。

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 使用查询服务 {#usage}

要分析数据，可以使用查询服务用户界面和RESTful API，从中可以创建SQL查询。 通过用户界面，您可以编写和执行查询，查看先前执行的查询，以及访问由您组织内的用户保存的查询。 您可以像沙盒一样使用查询编辑器来测试查询，然后在更广泛的数据集上执行它们。 请参阅 [查询服务用户界面指南](ui/overview.md) 有关使用UI的更多信息。 RESTful API提供了类似体验。 您可以使用查询服务API以编程方式编写和执行查询，安排查询以供将来使用和重复，以及为要编写的查询创建模板。 有关使用查询服务API的更多信息，请参阅 [Query Service开发人员指南](api/getting-started.md).

## 查询服务和Experience Platform服务 {#experience-platform-services}

查询服务可交互，并可与多个Experience Platform服务一起使用。 为了充分利用Query Service的功能，您应该熟悉这些服务以及它们如何与Query Service交互。 此 [Experience Platform文档登陆页面](https://experienceleague.adobe.com/docs/experience-platform.html) 提供平台功能的摘要和链接。

### [!DNL Data Science Workspace] {#data-science-workspace}

Adobe Experience Platform [!DNL Data Science Workspace] 利用机器学习和人工智能，从Experience Platform中存储的数据获取见解。 数据科学家可以使用 [!DNL Data Science Workspace] 根据有关客户及其活动的记录和时间序列数据构建配方。 这些配方有助于进行预测，例如购买倾向和个人可能会喜欢和使用的推荐选件。 可以在以下位置使用SQL： [!DNL Data Science Workspace] 通过将查询服务集成到 [!DNL JupyterLab] 探索、转换和分析Adobe Analytics数据。 阅读 [[!DNL Data Science Workspace] 概述](../data-science-workspace/home.md) 和 [Jupyter Notebook连接指南](./clients/jupyter-notebook.md) 有关以下内容的更多信息： [!DNL Data Science Workspace] 与查询服务交互。

### [!DNL Segmentation Service] {#segmentation}

使用Adobe Experience Platform分段服务将客户划分为具有相似特征的较小群组。 然后，可以评估这些受众，以更好地分析实时客户档案数据。 您可以使用查询服务在数据湖中对此受众数据运行查询并提供分析。 阅读 [分段服务概述](../segmentation/home.md) 和 [[!DNL Profile Query Language] (PQL)指南](../segmentation/pql/overview.md) 有关如何分析受众的更多信息。

## 用例 {#use-cases}

查询服务提供了一种灵活的数据处理方法，具有多种用途。 此外，它还可以减轻营销人员划分客户时的负担，并有助于生成切实可行的受众和有意义的业务见解。 以下用例提供了更深入的查询服务功能示例。

### 放弃Adobe Analytics Browse {#abandon-browse}

此 [浏览放弃示例以使用Adobe为中心 [!DNL Analytics]](./use-cases/abandoned-browse.md) 创建特定可操作受众的数据。 查询服务可适应复杂的分段逻辑，以计算各种个性化属性以供下游使用，或极大地简化构建受众的方式。

## 使用自定义仪表板生成见解 {#custom-dashboards}

借助Adobe Experience Platform，您可以摄取、存储、构造和提取所有存储的数据集，包括行为、CRM和销售点数据。 使用 [!DNL Experience Platform's Query Service]之后，您可以查询这些数据集并回答有关业务的具体问题，然后开始生成有影响力的见解。 了解如何构建和管理自定义仪表板，以便在其中创建、添加和编辑定制构件以可视化关键量度 [用户定义的仪表板](../dashboards/user-defined-dashboards.md). 您甚至可以 [自定义您自己的Real-Time CDP报表](../dashboards/cdp-insights-data-model.md) SQL查询与Real-time Customer Data Platform分析数据模型结合使用来确定您的营销和KPI用例。

## 后续步骤和其他资源

通过阅读本文档，您已经了解了查询服务以及它如何在更大的Experience Platform范围内运行。 要继续了解查询服务功能，建议您阅读以下文档：

- 此 [Query Service开发人员指南](api/getting-started.md)：有关与查询服务API中的各种端点交互的更多信息。
- 此 [查询服务用户界面指南](ui/overview.md)：有关使用查询编辑器和UI的更多信息。
- 此 [查询服务客户端概述](clients/overview.md)：有关要与查询服务连接的外部客户端的完整列表。

为了更好地准备运行查询，请观看以下视频。 此视频分享有关在查询编辑器界面、PSQL客户端、商业智能(BI)解决方案和HTTP API中运行查询的提示和最佳实践。

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)

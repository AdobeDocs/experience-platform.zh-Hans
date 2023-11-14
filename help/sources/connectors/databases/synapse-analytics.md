---
title: azure synapseAnalytics源连接器概述
description: 了解如何使用API或用户界面将Azure synapse Analytics连接到Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# [!DNL Azure Synapse Analytics] 源

>[!IMPORTANT]
>
>此 [!DNL Azure Synapse Analytics] 源目录中的源可供已购买Real-time Customer Data Platform Ultimate的用户使用。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

[!DNL Experience Platform] 支持从第三方数据库引入数据。 [!DNL Platform] 可以连接到不同类型的数据库，如关系数据库、NoSQL数据库或数据仓库数据库。 对数据库提供程序的支持包括 [!DNL Azure Synapse Analytics].

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面以了解更多信息。

以下文档提供了有关如何连接的信息 [!DNL Azure Synapse Analytics] 到 [!DNL Platform] 使用API或用户界面：

## 连接 [!DNL Azure Synapse Analytics] 到 [!DNL Platform] 使用API

- [使用流服务API创建Azure synapseAnalytics基本连接](../../tutorials/api/create/databases/synapse-analytics.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为数据库源创建数据流](../../tutorials/api/collect/database-nosql.md)

## 连接 [!DNL Azure Synapse Analytics] 到 [!DNL Platform] 使用UI

- [在UI中创建Azure synapseAnalytics源连接](../../tutorials/ui/create/databases/synapse-analytics.md)
- [在用户界面中为数据库源连接创建数据流](../../tutorials/ui/dataflow/databases.md)

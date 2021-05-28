---
keywords: Experience Platform；主页；热门主题；Azure synapse分析；azure synapse分析；Synapse;Synapse
solution: Experience Platform
title: azure synapse分析源连接器概述
topic-legacy: overview
description: 了解如何使用API或用户界面将Azure synapse分析连接到Adobe Experience Platform。
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# [!DNL Azure Synapse Analytics] 连接器

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用[!DNL Platform]服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

[!DNL Experience Platform] 支持从第三方数据库摄取数据。[!DNL Platform] 可以连接到不同类型的数据库，如关系数据库、 NoSQL数据库或data warehouse。对数据库提供程序的支持包括[!DNL Azure Synapse Analytics]。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表。 无法将特定于区域的IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 有关更多信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页面。

>[!IMPORTANT]
>
>[!DNL Azure Synapse Analytics]源连接器当前不支持与平台的同一区域连接。 这意味着如果您的Azure实例使用与Platform相同的网络区域，则无法建立与Platform源的连接。 目前，仅支持跨区域连接。 有关更多信息，请联系您的Adobe客户经理。

以下文档提供了有关如何使用API或用户界面将[!DNL Azure Synapse Analytics]连接到[!DNL Platform]的信息：

## 使用API将[!DNL Azure Synapse Analytics]连接到[!DNL Platform]

- [使用流量服务API创建Azure synapse分析源连接](../../tutorials/api/create/databases/synapse-analytics.md)
- [使用流服务API浏览数据库系统](../../tutorials/api/explore/database-nosql.md)
- [使用流服务API从数据库收集数据](../../tutorials/api/collect/database-nosql.md)

## 使用UI将[!DNL Azure Synapse Analytics]连接到[!DNL Platform]

- [在UI中创建Azure synapse分析源连接](../../tutorials/ui/create/databases/synapse-analytics.md)
- [在UI中为数据库连接配置数据流](../../tutorials/ui/dataflow/databases.md)

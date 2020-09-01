---
keywords: Experience Platform;home;popular topics;Apache Spark;apache spark;Azure HDInsights;azure hdinsights
solution: Experience Platform
title: Azure HDInsights连接器上的Apache Spark
topic: overview
description: 以下文档提供了如何使用API或用户界面将Azure HDInsights上的Apache Spark连接到平台的信息。
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# （测试版） [!DNL Apache Spark] 连接 [!DNL Azure HDInsights] 器

>[!NOTE]
>
>开 [!DNL Apache Spark] 关接 [!DNL Azure HDInsights] 头为测试版。 有关使用 [测试版标记](../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform允许从外部来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)收集数据。

[!DNL Experience Platform] 支持从第三方数据库中摄取数据。 [!DNL Platform] 可以连接到不同类型的数据库，如关系型、NoSQL或data warehouse。 对数据库提供者的支持 [!DNL Apache Spark] 包括 [!DNL Azure HDInsights]在。

## IP地址允许列表

在使用源连接器之前，必须将以下IP地址添加到允许列表。 如果无法向允许列表添加特定于区域的IP地址，则在使用源时可能会导致错误或性能不佳。

### 美国东部地区

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### 西欧地区

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### 澳大利亚东部

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

以下文档提供了如何使用API [!DNL Apache Spark] 或 [!DNL Azure HDInsights] 用户 [!DNL Platform] 界面进行连接的信息：

## 使用 [!DNL Apache Spark] API [!DNL Azure HDInsights] 连接 [!DNL Platform] 到

- [在Azure HDInsights连接器上使用Flow Service API创建Apache Spark](../../tutorials/api/create/databases/spark.md)
- [使用Flow Service API浏览数据库系统](../../tutorials/api/explore/database-nosql.md)
- [使用Flow Service API从数据库收集数据](../../tutorials/api/collect/database-nosql.md)

## 使 [!DNL Apache Spark] 用 [!DNL Azure HDInsights] UI [!DNL Platform] 连接

- [在UI中在Azure HDInsights源连接器上创建Apache Spark](../../tutorials/ui/create/databases/spark.md)
- [在UI中为数据库连接器配置数据流](../../tutorials/ui/dataflow/databases.md)
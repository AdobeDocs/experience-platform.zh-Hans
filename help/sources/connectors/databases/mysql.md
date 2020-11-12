---
keywords: Experience Platform;home;popular topics;MySQL;mysql;My sql;My SQL
solution: Experience Platform
title: MySQL连接器
topic: overview
description: 以下文档提供了如何使用API或用户界面将MySQL连接到平台的信息。
translation-type: tm+mt
source-git-commit: e0a0b7fc28b8cc85c5140d3840e06e5c7078c307
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---


# （测试版）MySQL连接器

>[!NOTE]
>
>MySQL连接器处于测试状态。 有关使用 [测试版标记](../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform允许从外部来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)收集数据。

[!DNL Experience Platform] 支持从第三方数据库中摄取数据。 [!DNL Platform] 可以连接到不同类型的数据库，如关系型、NoSQL或data warehouse。 对数据库提供程序的支持包括MySQL。

## IP地址允许列表

在使用源连接器之前，必须向允许列表添加IP地址列表。 如果无法向允许列表添加特定于区域的IP地址，则在使用源时可能会导致错误或性能不佳。 有关详细 [信息，请参阅](../../ip-address-allow-list.md) “IP地址允许列表”页。

以下文档提供了如何将MySQL连接 [!DNL Platform] 到使用API或用户界面的信息：

## 将MySQL连接 [!DNL Platform] 到使用API

- [使用Flow Service API创建MySQL连接器](../../tutorials/api/create/databases/mysql.md)
- [使用Flow Service API浏览数据库系统](../../tutorials/api/explore/database-nosql.md)
- [使用Flow Service API从数据库收集数据](../../tutorials/api/collect/database-nosql.md)

## 将MySQL连 [!DNL Platform] 接到使用UI

- [在UI中创建MySQL源连接器](../../tutorials/ui/create/databases/mysql.md)
- [在UI中为数据库连接器配置数据流](../../tutorials/ui/dataflow/databases.md)
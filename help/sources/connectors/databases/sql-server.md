---
keywords: Experience Platform；主页；热门主题；Microsoft SQL;Microsoft SQL;SQL;SQL
solution: Experience Platform
title: SQL Server源连接器概述
topic-legacy: overview
description: 了解如何使用API或用户界面将Microsoft SQL Server连接到Adobe Experience Platform。
exl-id: 8a77f108-7e82-4e14-a470-a4ea97def89d
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# [!DNL Microsoft] SQL Server连接器

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用[!DNL Platform]服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

[!DNL Experience Platform] 支持从第三方数据库摄取数据。[!DNL Platform] 可以连接到不同类型的数据库，如关系数据库、 NoSQL数据库或data warehouse。对数据库提供程序的支持包括[!DNL Microsoft] SQL Server。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表。 无法将特定于区域的IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 有关更多信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页面。

>[!IMPORTANT]
>
>[!DNL Microsoft] SQL Server源连接器当前不支持与平台的同区域连接。 这意味着如果您的Azure实例使用与Platform相同的网络区域，则无法建立与Platform源的连接。 目前，仅支持跨区域连接。 有关更多信息，请联系您的Adobe客户经理。

以下文档提供了有关如何使用API或用户界面将[!DNL Microsoft] SQL Server连接到[!DNL Platform]的信息：

## 使用API将[!DNL Microsoft] SQL Server连接到[!DNL Platform]

- [使用流服务API创建Microsoft SQL Server基连接](../../tutorials/api/create/databases/sql-server.md)
- [使用流服务API探索数据库源的数据结构和内容](../../tutorials/api/explore/database-nosql.md)
- [使用流服务API为数据库源创建数据流](../../tutorials/api/collect/database-nosql.md)

## 使用UI将[!DNL Microsoft] SQL Server连接到[!DNL Platform]

- [在UI中创建Microsoft SQL Server源连接](../../tutorials/ui/create/databases/sql-server.md)
- [在UI中为数据库源连接创建数据流](../../tutorials/ui/dataflow/databases.md)

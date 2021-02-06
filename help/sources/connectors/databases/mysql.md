---
keywords: Experience Platform；主页；热门主题；MySQL;mysql;MySQL
solution: Experience Platform
title: MySQL源连接器概述
topic: overview
description: 了解如何使用API或用户界面将MySQL连接到Adobe Experience Platform。
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# （测试版）MySQL连接器

>[!NOTE]
>
>MySQL连接器处于测试状态。 有关使用测试版标签的连接器的详细信息，请参见[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform允许从外部源摄取数据，同时使您能够使用[!DNL Platform]服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)收集数据。

[!DNL Experience Platform] 支持从第三方数据库中摄取数据。[!DNL Platform] 可以连接到不同类型的数据库，如关系型、NoSQL或data warehouse。对数据库提供程序的支持包括MySQL。

## IP地址允许列表

在使用源连接器之前，必须向允许列表添加IP地址列表。 如果无法向允许列表添加特定于区域的IP地址，则在使用源时可能会导致错误或性能不佳。 有关详细信息，请参阅[ IP地址允许列表](../../ip-address-allow-list.md)页。

以下文档提供了如何使用API或用户界面将MySQL连接到[!DNL Platform]的信息：

## 使用API将MySQL连接到[!DNL Platform]

- [使用Flow Service API创建MySQL源连接](../../tutorials/api/create/databases/mysql.md)
- [使用Flow Service API浏览数据库系统](../../tutorials/api/explore/database-nosql.md)
- [使用Flow Service API从数据库收集数据](../../tutorials/api/collect/database-nosql.md)

## 使用UI将MySQL连接到[!DNL Platform]

- [在UI中创建MySQL源连接](../../tutorials/ui/create/databases/mysql.md)
- [在UI中为数据库连接配置数据流](../../tutorials/ui/dataflow/databases.md)
---
keywords: Experience Platform;home;popular topics;couchbase;Couchbase
solution: Experience Platform
title: Couchbase连接器
topic: overview
description: 以下文档提供了如何使用API或用户界面将Couchbase连接到平台的信息。
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# （测试版）连 [!DNL Couchbase] 接器

>[!NOTE]
>
>连接 [!DNL Couchbase] 器为测试版。 有关使用 [测试版标记](../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform为数据库提供 [!DNL Microsoft]商(如MySQL和 [!DNL Azure])提供本机连接，使您能够从这些系统中获取数据。 支持不同类型的第三方数据库，包括关系型、NoSQL或data warehouse。 对数据库提供者的支持包 [!DNL Couchbase]括。

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

以下文档提供了如何使用API [!DNL Couchbase] 或 [!DNL Platform] 用户界面连接的信息：

## 连接 [!DNL Couchbase] 到 [!DNL Platform] 使用API

- [使用Flow Service API创建Couchbase连接器](../../tutorials/api/create/databases/couchbase.md)
- [使用Flow Service API浏览数据库系统](../../tutorials/api/explore/database-nosql.md)
- [使用Flow Service API从数据库收集数据](../../tutorials/api/collect/database-nosql.md)

## 连接 [!DNL Couchbase] 到 [!DNL Platform] 使用UI

- [在UI中创建Couchbase源连接器](../../tutorials/ui/create/databases/couchbase.md)
- [在UI中为数据库连接器配置数据流](../../tutorials/ui/dataflow/databases.md)
---
keywords: Experience Platform；主页；热门主题；BigQuery;bigquery;Google BigQuery;Google bigQuery
solution: Experience Platform
title: Google BigQuery源连接器概述
topic-legacy: overview
description: 了解如何使用API或用户界面将Google BigQuery连接到Adobe Experience Platform。
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 9d68e54baa894ebeff4603c7df01a1fe42aa217f
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# （测试版）[!DNL Google BigQuery]连接器

>[!NOTE]
>
>[!DNL Google BigQuery]为测试版。 有关使用测试版标记的连接器的更多信息，请参阅[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

[!DNL Experience Platform] 支持从第三方数据库摄取数据。平台可以连接到不同类型的数据库，如关系数据库、 NoSQL数据库或data warehouse。 对数据库提供程序的支持包括[!DNL Google BigQuery]。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表。 无法将特定于区域的IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 有关更多信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页面。

## 先决条件

以下部分提供了在创建[!DNL Google BigQuery]源连接之前需要先设置的先决条件的详细信息。

### 生成[!DNL Google BigQuery]凭据

要将[!DNL Google BigQuery]连接到平台，您需要为以下凭据生成值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `project` | 项目是[!DNL Google Cloud]资源的基层组织实体，包括[!DNL Google BigQuery]。 |
| `clientID` | 客户端ID是[!DNL Google BigQuery] OAuth 2.0凭据的一半。 |
| `clientSecret` | 客户端密钥是[!DNL Google BigQuery] OAuth 2.0凭据的另一半。 |
| `refreshToken` | 刷新令牌允许您为API获取新的访问令牌。 访问令牌的生命周期有限，且可能会在您的项目过程中过期。 您可以根据需要使用刷新令牌来验证并请求项目的后续访问令牌。 |

有关如何为[!DNL Google] API生成OAuth 2.0凭据的详细说明，请参阅以下[[!DNL Google] OAuth 2.0身份验证指南](https://developers.google.com/identity/protocols/oauth2)。

## 将[!DNL Google BigQuery]连接到平台

以下文档提供了有关如何使用API或用户界面将[!DNL Google BigQuery]连接到平台的信息：

### 使用API

- [使用流服务API创建Google BigQuery源连接](../../tutorials/api/create/databases/bigquery.md)
- [使用流服务API浏览数据库系统](../../tutorials/api/explore/database-nosql.md)
- [使用流服务API从数据库收集数据](../../tutorials/api/collect/database-nosql.md)

### 使用UI

- [在UI中创建Google BigQuery源连接](../../tutorials/ui/create/databases/bigquery.md)
- [在UI中为数据库连接配置数据流](../../tutorials/ui/dataflow/databases.md)

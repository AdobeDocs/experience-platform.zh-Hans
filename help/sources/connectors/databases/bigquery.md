---
keywords: Experience Platform；主页；热门主题；BigQuery；bigquery；Google BigQuery；google bigquery
solution: Experience Platform
title: Google BigQuery源连接器概述
description: 了解如何使用API或用户界面将Google BigQuery连接到Adobe Experience Platform。
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# [!DNL Google BigQuery]

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

[!DNL Experience Platform] 支持从第三方数据库引入数据。 Platform可以连接到不同类型的数据库，例如关系数据库、NoSQL数据库或data warehouse数据库。 对数据库提供商的支持包括 [!DNL Google BigQuery].

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于地区的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面，以了解更多信息。

## 先决条件

以下部分提供了在创建之前所需的先决条件设置的详细信息 [!DNL Google BigQuery] 源连接。

### 生成您的 [!DNL Google BigQuery] 凭据

连接 [!DNL Google BigQuery] 对于Platform，您需要生成以下凭据的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `project` | 项目是的基础级别组织实体。 [!DNL Google Cloud] 资源，包括 [!DNL Google BigQuery]. |
| `clientID` | 客户端ID是 [!DNL Google BigQuery] OAuth 2.0凭据。 |
| `clientSecret` | 客户端密钥是你的另一半 [!DNL Google BigQuery] OAuth 2.0凭据。 |
| `refreshToken` | 刷新令牌允许您获取API的新访问令牌。 访问令牌的生命周期有限，并且在您的项目过程中可能会过期。 如果需要，您可以使用刷新令牌对项目进行身份验证并请求后续访问令牌。 |
| `largeResultsDataSetId` | 预创建的  [!DNL Google BigQuery] 启用对大型结果集的支持所需的数据集ID。 |

有关如何为生成OAuth 2.0凭据的详细说明 [!DNL Google] API，请参阅以下内容 [[!DNL Google] OAuth 2.0身份验证指南](https://developers.google.com/identity/protocols/oauth2).

## Connect [!DNL Google BigQuery] 目标平台

以下文档提供了有关如何连接的信息 [!DNL Google BigQuery] 至使用API或用户界面的Platform：

### 使用API

- [使用流服务API创建Google BigQuery基本连接](../../tutorials/api/create/databases/bigquery.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为数据库源创建数据流](../../tutorials/api/collect/database-nosql.md)

### 使用UI

- [在UI中创建Google BigQuery源连接](../../tutorials/ui/create/databases/bigquery.md)
- [在UI中为数据库源连接创建数据流](../../tutorials/ui/dataflow/databases.md)

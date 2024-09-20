---
title: Google BigQuery Source连接器概述
description: 了解如何使用API或用户界面将Google BigQuery连接到Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 1fa79b31b5a257ebb3cbd60246b757d8a4a63d7c
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# [!DNL Google BigQuery]源

>[!IMPORTANT]
>
>[!DNL Google BigQuery]源在源目录中可供已购买Real-time Customer Data Platform Ultimate的用户使用。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

阅读本文档以了解成功将[!DNL Google BigQuery]帐户连接到Experience Platform所需的先决步骤。

## 先决条件 {#prerequisites}

以下部分提供了在创建[!DNL Google BigQuery]源连接之前所需的先决条件设置的详细信息。

### IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

### 生成您的[!DNL Google BigQuery]凭据 {#credentials}

要将[!DNL Google BigQuery]连接到Experience Platform，您需要生成以下凭据的值：

>[!BEGINTABS]

>[!TAB 基本身份验证]

要使用OAuth 2.0和基本身份验证的组合进行身份验证，请为以下凭据提供适当的值。

| 凭据 | 描述 |
| --- | --- |
| `project` | 项目是[!DNL Google Cloud]资源（包括[!DNL Google BigQuery]）的基级别组织实体。 |
| `clientID` | 客户端ID是[!DNL Google BigQuery] OAuth 2.0凭据的一半。 |
| `clientSecret` | 客户端密钥是[!DNL Google BigQuery] OAuth 2.0凭据的另一半。 |
| `refreshToken` | 刷新令牌允许您获取API的新访问令牌。 访问令牌的生命周期有限，在您的项目过程中可能会过期。 如果需要，您可以使用刷新令牌对项目进行身份验证并请求后续访问令牌。 |
| `largeResultsDataSetId` | （可选）启用大型结果集支持所需的预创建[!DNL Google BigQuery]数据集ID。 |

有关如何为[!DNL Google] API生成OAuth 2.0凭据的详细说明，请参阅以下[[!DNL Google] OAuth 2.0身份验证指南](https://developers.google.com/identity/protocols/oauth2)。

>[!TAB 服务身份验证]

要使用服务身份验证进行身份验证，请为以下凭据提供适当的值。

**注意**：您的服务帐户必须具有足够的权限，例如： **[!DNL BigQuery Job User]**、**[!DNL BigQuery Data Viewer]**、**[!DNL BigQuery Read Session User]**&#x200B;和&#x200B;**[!DNL BigQuery Data Owner]**，才能通过服务身份验证成功进行身份验证。

| 凭据 | 描述 |
| --- | --- |
| `projectId` | 要查询的[!DNL Google BigQuery]的ID。 |
| `keyFileContent` | 用于验证服务帐户的密钥文件。 您可以从[[!DNL Google Cloud service accounts] 仪表板](https://console.cloud.google.com)检索此值。 密钥文件内容采用JSON格式。 对Experience Platform进行身份验证时，必须在[!DNL Base64]中对此进行编码。 |
| `largeResultsDataSetId` | （可选）启用大型结果集支持所需的预创建[!DNL Google BigQuery]数据集ID。 |

有关在[!DNL Google BigQuery]中使用服务帐户的详细信息，请阅读[在 [!DNL Google BigQuery]](https://cloud.google.com/bigquery/docs/use-service-accounts)中使用服务帐户的指南。

>[!ENDTABS]

## 将[!DNL Google BigQuery]连接到平台

以下文档提供了有关如何使用API或用户界面将[!DNL Google BigQuery]连接到Platform的信息：

### 使用API

- [使用流服务API创建Google BigQuery基本连接](../../tutorials/api/create/databases/bigquery.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为数据库源创建数据流](../../tutorials/api/collect/database-nosql.md)

### 使用UI

- [在UI中创建Google BigQuery源连接](../../tutorials/ui/create/databases/bigquery.md)
- [在用户界面中为数据库源连接创建数据流](../../tutorials/ui/dataflow/databases.md)

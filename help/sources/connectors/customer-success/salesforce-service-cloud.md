---
title: Salesforce Service Cloud Source连接器概述
description: 了解如何使用API或用户界面将Salesforce Service Cloud连接到Adobe Experience Platform。
exl-id: 9bebbc00-55b3-4aec-9357-4127c05844e2
source-git-commit: b9a9b00114b3c1159a14b7e39484d250fa7563ba
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---

# [!DNL Salesforce Service Cloud]

[!DNL Salesforce Service Cloud]是一个客户成功平台，旨在自动化服务工作流并简化公司与其客户之间的通信。 它将来自各种渠道（如电子邮件、电话、社交媒体和实时聊天）的请求整合到一个统一的代理控制台中。 这允许支持团队以全面了解客户历史的方式管理“案例”，从而确保无论客户如何提供服务，响应都是个性化和高效的。

您可以使用Adobe Experience Platform源中的[!DNL Salesforce Service Cloud]源连接器来连接您的[!DNL Salesforce Service Cloud]帐户并将您的数据引入到Experience Platform服务中。

阅读本文档了解如何设置[!DNL Salesforce Service Cloud]帐户并将其连接到Experience Platform。

## 先决条件 {#prerequisites}

请参阅此部分，了解在成功连接到Experience Platform之前必须完成的先决条件设置。

### IP地址允许列表 {#allowlist}

在将源连接到Experience Platform之前，必须将特定于区域的IP地址添加到允许列表。 有关详细信息，请阅读有关[将IP地址列入允许列表到Experience Platform](../../ip-address-allow-list.md)的指南。

### 收集所需的凭据 {#credentials}

您必须为以下凭据提供值，才能使用OAuth2客户端凭据连接您的[!DNL Salesforce Service Cloud]帐户。

| 凭据 | 描述 |
| --- | --- |
| 环境 URL | [!DNL Salesforce Service Cloud]源实例的URL。 |
| 客户端 ID | 在OAuth2身份验证中，客户端ID与客户端密钥结合使用。 客户端ID和客户端密钥共同使您的应用程序能够代表您的帐户运行，方法是向[!DNL Salesforce Service Cloud]标识您的应用程序。 |
| 客户端密码 | 客户端密钥与客户端ID结合使用，作为OAuth2身份验证的一部分。 客户端ID和客户端密钥共同使您的应用程序能够代表您的帐户运行，方法是向[!DNL Salesforce Service Cloud]标识您的应用程序。 |
| API 版本 | 您正在使用的[!DNL Salesforce Service Cloud]实例的REST API版本。 API版本的值必须使用小数格式设置。 例如，如果您使用的是API版本`52`，则必须以`52.0`的形式输入值。 如果此字段留空，Experience Platform将自动使用最新可用版本。 |

有关为[!DNL Salesforce Service Cloud]使用OAuth的更多信息，请阅读有关OAuth授权流程](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5)的[[!DNL Salesforce Service Cloud] 指南。

## 使用API将[!DNL Salesforce Service Cloud]连接到Experience Platform

- [使用流服务API创建Salesforce服务云基本连接](../../tutorials/api/create/customer-success/salesforce-service-cloud.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为客户成功来源创建数据流](../../tutorials/api/collect/customer-success.md)

## 使用UI将[!DNL Salesforce Service Cloud]连接到Experience Platform

- [在UI中创建Salesforce Service Cloud源连接](../../tutorials/ui/create/customer-success/salesforce-service-cloud.md)
- [在UI中为客户成功源连接创建数据流](../../tutorials/ui/dataflow/customer-success.md)

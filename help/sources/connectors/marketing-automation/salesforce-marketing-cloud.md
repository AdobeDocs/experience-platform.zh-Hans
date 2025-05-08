---
solution: Experience Platform
title: Salesforce Marketing Cloud Source概述
description: 了解如何使用API或用户界面将Salesforce Marketing Cloud连接到Adobe Experience Platform。
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-04-29T00:00:00Z
source-git-commit: ce96dbc64845fddb40ebee709828c56d51a6c6ba
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud]源将于2026年1月被弃用。 作为替代方案，将在今年晚些时候发布新的信息源。 发布新源后，您必须计划在2026年1月底之前通过创建新帐户连接和数据流迁移到新源。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform支持从第三方营销自动化系统中提取数据。 对营销自动化提供商的支持包括[!DNL Salesforce Marketing Cloud]。

## 先决条件

在将[!DNL Salesforce Marketing Cloud]源连接到Experience Platform之前，必须确保将以下&#x200B;**权限范围**&#x200B;配置为您的[!DNL Salesforce Marketing Cloud]客户端ID和客户端密钥组合：

* `campaign_read`
* `list_and_subscribers_read`

您可以通过调用[!DNL Salesforce Marketing Cloud] API的`v2/userinfo`资源来请求作用域。 有关如何请求和比较范围的指导，请参阅[[!DNL Salesforce Marketing Cloud] API集成权限范围文档](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>)。

有关作用域的更多信息，包括其相关权限和行为的列表，请参阅此[[!DNL Salesforce Marketing Cloud] REST API文档](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>)。

>[!IMPORTANT]
>
>[!DNL Salesforce Marketing Cloud]源集成当前不支持自定义对象摄取。

## IP地址允许列表

在将源连接到Experience Platform之前，必须将特定于区域的IP地址添加到允许列表。 有关详细信息，请阅读有关[将IP地址列入允许列表到Experience Platform](../../ip-address-allow-list.md)的指南。

>[!WARNING]
>
>如果您没有向帐户添加必要的IP地址，则[!DNL Salesforce Marketing Cloud]允许列表将不会连接到Experience Platform。

## 使用API将[!DNL Salesforce Marketing Cloud]连接到Experience Platform

以下文档提供了有关如何使用API将[!DNL Salesforce Marketing Cloud]连接到Experience Platform的信息：

* [使用流服务API创建Salesforce Marketing Cloud基本连接](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
* [使用流服务API为营销自动化源创建数据流](../../tutorials/api/collect/marketing-automation.md)

## 使用UI将[!DNL Salesforce Marketing Cloud]连接到Experience Platform

以下文档提供了有关如何使用用户界面将[!DNL Salesforce Marketing Cloud]连接到Experience Platform的信息：

* [在UI中创建Salesforce Marketing Cloud源连接](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [在UI中为Marketing Automation源连接创建数据流](../../tutorials/ui/dataflow/marketing-automation.md)

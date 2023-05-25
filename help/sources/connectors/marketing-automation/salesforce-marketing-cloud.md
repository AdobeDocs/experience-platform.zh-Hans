---
solution: Experience Platform
title: SalesforceMarketing Cloud源概述
description: 了解如何使用API或用户界面将SalesforceMarketing Cloud连接到Adobe Experience Platform。
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2023-03-25T00:00:00Z
source-git-commit: cfe5f34316e9db072f0a320143354f2771b4a3a9
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从第三方营销自动化系统中提取数据。 对营销自动化提供商的支持包括 [!DNL Salesforce Marketing Cloud].

## 先决条件

在连接之前 [!DNL Salesforce Marketing Cloud] 源到平台，您必须确保 **权限范围** 已配置到您的 [!DNL Salesforce Marketing Cloud] 客户端ID和客户端密钥组合：

* `campaign_read`
* `list_and_subscribers_read`

您可以通过调用 `v2/userinfo` 的资源 [!DNL Salesforce Marketing Cloud] API。 请参阅 [[!DNL Salesforce Marketing Cloud] API集成权限范围文档](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) 以获取有关如何请求和比较范围的指导。

有关范围的更多信息，包括其相关权限和行为的列表，请参阅此 [[!DNL Salesforce Marketing Cloud] REST API文档](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>自定义对象摄取当前不受支持 [!DNL Salesforce Marketing Cloud] 源集成。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于地区的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面，以了解更多信息。

## Connect [!DNL Salesforce Marketing Cloud] 到使用API的平台

以下文档提供了有关如何连接的信息 [!DNL Salesforce Marketing Cloud] 到使用API的平台：

* [使用流服务API创建SalesforceMarketing Cloud基本连接](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
* [使用流服务API为营销自动化源创建数据流](../../tutorials/api/collect/marketing-automation.md)

## Connect [!DNL Salesforce Marketing Cloud] 使用UI到Platform

以下文档提供了有关如何连接的信息 [!DNL Salesforce Marketing Cloud] 使用用户界面连接到Platform：

* [在UI中创建SalesforceMarketing Cloud源连接](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [在UI中为营销自动化源连接创建数据流](../../tutorials/ui/dataflow/marketing-automation.md)

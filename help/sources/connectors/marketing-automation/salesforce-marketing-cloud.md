---
solution: Experience Platform
title: SalesforceMarketing CloudSource概述
description: 了解如何使用API或用户界面将SalesforceMarketing Cloud连接到Adobe Experience Platform。
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: 0e3fee4d78646b1d1d6730495358b3ced4127f4e
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

>[!IMPORTANT]
>
>[!DNL Salesforce Marketing Cloud]源将于2025年5月底弃用。 作为替代方法，您可以使用[[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md)源。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从第三方营销自动化系统中提取数据。 对营销自动化提供商的支持包括[!DNL Salesforce Marketing Cloud]。

## 先决条件

在将[!DNL Salesforce Marketing Cloud]源连接到Platform之前，必须确保将以下&#x200B;**权限范围**&#x200B;配置为您的[!DNL Salesforce Marketing Cloud]客户端ID和客户端密钥组合：

* `campaign_read`
* `list_and_subscribers_read`

您可以通过调用[!DNL Salesforce Marketing Cloud] API的`v2/userinfo`资源来请求作用域。 有关如何请求和比较范围的指导，请参阅[[!DNL Salesforce Marketing Cloud] API集成权限范围文档](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>)。

有关作用域的更多信息，包括其相关权限和行为的列表，请参阅此[[!DNL Salesforce Marketing Cloud] REST API文档](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>)。

>[!IMPORTANT]
>
>[!DNL Salesforce Marketing Cloud]源集成当前不支持自定义对象摄取。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

## 使用API将[!DNL Salesforce Marketing Cloud]连接到平台

以下文档提供了有关如何使用API将[!DNL Salesforce Marketing Cloud]连接到Platform的信息：

* [使用流服务API创建SalesforceMarketing Cloud基本连接](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
* [使用流服务API为营销自动化源创建数据流](../../tutorials/api/collect/marketing-automation.md)

## 使用UI将[!DNL Salesforce Marketing Cloud]连接到平台

以下文档提供了有关如何使用用户界面将[!DNL Salesforce Marketing Cloud]连接到Platform的信息：

* [在UI中创建SalesforceMarketing Cloud源连接](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [在UI中为Marketing Automation源连接创建数据流](../../tutorials/ui/dataflow/marketing-automation.md)

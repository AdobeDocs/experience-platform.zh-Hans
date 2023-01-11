---
keywords: Experience Platform；主页；热门主题；Salesforce Marketing Cloud;SalesforceMarketing Cloud；营销自动化
solution: Experience Platform
title: SalesforceMarketing Cloud源概述
description: 了解如何使用API或用户界面将SalesforceMarketing Cloud连接到Adobe Experience Platform。
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# （测试版） [!DNL Salesforce Marketing Cloud]

>[!NOTE]
>
>的 [!DNL Salesforce Marketing Cloud] 来源为测试版。 请参阅 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

[!DNL Experience Platform] 支持从第三方营销自动化系统中摄取数据。 对营销自动化提供商的支持包括 [!DNL Salesforce Marketing Cloud].

## 先决条件

在连接 [!DNL Salesforce Marketing Cloud] 源到平台时，您必须确保 **权限范围** 已配置为 [!DNL Salesforce Marketing Cloud] 客户端ID和客户端密钥组合：

* `campaign_read`
* `list_and_subscribers_read`

您可以通过调用 `v2/userinfo` 资源 [!DNL Salesforce Marketing Cloud] API。 请参阅 [[!DNL Salesforce Marketing Cloud] API集成权限范围文档](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html) 以了解如何请求和比较范围。

有关范围（包括其相关权限和行为列表）的更多信息，请参阅此 [[!DNL Salesforce Marketing Cloud] REST API文档](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html).

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表。 无法将特定于区域的IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面以了解更多信息。

## 连接 [!DNL Salesforce Marketing Cloud] 到使用API的平台

以下文档提供了有关如何连接的信息 [!DNL Salesforce Marketing Cloud] 要使用API的平台，请执行以下操作：

* [使用流服务API创建SalesforceMarketing Cloud库连接](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [使用流量服务API浏览数据表](../../tutorials/api/explore/tabular.md)
* [使用流服务API为营销自动化源创建数据流](../../tutorials/api/collect/marketing-automation.md)

## 连接 [!DNL Salesforce Marketing Cloud] 到使用UI的平台

以下文档提供了有关如何连接的信息 [!DNL Salesforce Marketing Cloud] 到使用用户界面的平台：

* [在UI中创建SalesforceMarketing Cloud源连接](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [在UI中为营销自动化源连接创建数据流](../../tutorials/ui/dataflow/marketing-automation.md)

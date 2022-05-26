---
keywords: Experience Platform；主页；热门主题；Zendesk;Zendesk
solution: Experience Platform
title: Zendesk Source Connector概述
description: 了解如何使用API或用户界面将Zendesk连接到Adobe Experience Platform。
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# （测试版） [!DNL Zendesk]

>[!NOTE]
>
>的 [!DNL Zendesk] 来源为测试版。 请参阅 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

Experience Platform支持从第三方客户成功应用程序摄取数据。 对客户成功提供商的支持包括 [!DNL Zendesk].

这个Adobe Experience Platform [来源](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en) 利用 [Zendesk搜索API >导出搜索结果](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) 可将用户信息从Zendesk返回到Experience Platform中以进行进一步处理。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表。 无法将特定于区域的IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面以了解更多信息。

## 验证 [!DNL Zendesk] 帐户

[!DNL Zendesk] 使用承载令牌作为与通信的验证机制 [!DNL Zendesk] API。

本节概述了为验证您的 [!DNL Zendesk] 帐户。

* 验证 [!DNL Zendesk] 帐户是为了确保您 [!DNL Zendesk] 支持帐户。 如果您还没有看到 [[!DNL Zendesk]注册页面](https://www.zendesk.com/register/) 注册并创建您的Zendesk帐户。
* 成功注册后，导航到 [[!DNL Zendesk] 网站](https://www.zendesk.com/login/) 提供 **子域**.
* 接下来，选择 **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* 最后，从 **[!DNL API token]** 中。

![Zendesk API令牌](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

请参阅 [[!DNL Zendesk documentation on subdomains]](https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain-) 以了解有关如何检索子域的信息。 有关生成API令牌的信息，请参阅 [[!DNL Zendesk] 有关生成新API令牌的指南](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token).

以下文档提供了有关如何连接的信息 [!DNL Zendesk] 要使用API或用户界面实现平台，请执行以下操作：

## 连接 [!DNL Zendesk] 到使用API的平台

* [创建源连接和数据流 [!DNL Zendesk] 使用流量服务API](../../tutorials/api/create/customer-success/zendesk.md)

## 连接 [!DNL Zendesk] 到使用UI的平台

* [创建 [!DNL Zendesk ]UI中的源连接](../../tutorials/ui/create/customer-success/zendesk.md)
* [在UI中为客户成功源连接创建数据流](../../tutorials/ui/dataflow/customer-success.md)

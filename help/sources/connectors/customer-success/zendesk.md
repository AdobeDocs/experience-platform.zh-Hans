---
title: Zendesk源连接器概述
description: 了解如何使用API或用户界面将Zendesk连接到Adobe Experience Platform。
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: 6f8abca8f0db8a559fe62e6c143f2d0506d3b886
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 2%

---

# [!DNL Zendesk]

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从第三方客户成功应用程序中摄取数据。 对客户成功提供商的支持包括 [!DNL Zendesk].

此Adobe Experience Platform [源](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=zh-Hans) 利用 [Zendesk搜索API >导出搜索结果](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) 可将用户信息从Zendesk返回到Experience Platform中以供进一步处理。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于地区的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面，以了解更多信息。

## 验证您的 [!DNL Zendesk] 帐户

[!DNL Zendesk] 使用持有者令牌作为身份验证机制与 [!DNL Zendesk] API。

本节概述验证您的身份需要完成的先决条件步骤 [!DNL Zendesk] 帐户。

* 身份验证的第一步 [!DNL Zendesk] 帐户是为了确保您拥有 [!DNL Zendesk] 支持帐户。 如果您还没有这样的客户，请查看 [[!DNL Zendesk] 注册页面](https://www.zendesk.com/register/) 注册并创建您的Zendesk帐户。
* 成功注册后，导航至 [[!DNL Zendesk] 网站](https://www.zendesk.com/login/) 并提供 **子域**.
* 接下来，选择 **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* 最后，从检索API令牌 **[!DNL API token]** 部分。

![Zendesk API令牌](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

请参阅 [[!DNL Zendesk documentation on subdomains]](<https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain->) 以获取有关如何检索子域的信息。 有关生成API令牌的信息，请参阅 [[!DNL Zendesk] 有关生成新API令牌的指南](<https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token>).

以下文档提供了有关如何连接的信息 [!DNL Zendesk] 至使用API或用户界面的Platform：

## Connect [!DNL Zendesk] 到使用API的平台

* [创建源连接和数据流 [!DNL Zendesk] 使用流服务API](../../tutorials/api/create/customer-success/zendesk.md)

## Connect [!DNL Zendesk] 使用UI到Platform

* [创建 [!DNL Zendesk ]UI中的源连接](../../tutorials/ui/create/customer-success/zendesk.md)
* [在UI中为客户成功源连接创建数据流](../../tutorials/ui/dataflow/customer-success.md)

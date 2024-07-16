---
title: Zendesk Source Connector概述
description: 了解如何使用API或用户界面将Zendesk连接到Adobe Experience Platform。
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# [!DNL Zendesk]

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从第三方客户成功应用程序中摄取数据。 对客户成功提供商的支持包括[!DNL Zendesk]。

此Adobe Experience Platform [源](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=zh-Hans)利用[Zendesk Search API > Export Search Results](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results)，将用户信息从Zendesk返回到Experience Platform中以供进一步处理。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

## 验证您的[!DNL Zendesk]帐户

[!DNL Zendesk]使用持有者令牌作为与[!DNL Zendesk] API通信的身份验证机制。

本节概述了验证[!DNL Zendesk]帐户时需要完成的先决步骤。

* 验证您的[!DNL Zendesk]帐户的第一步是确保您拥有[!DNL Zendesk]支持帐户。 如果您还没有帐户，请查看[[!DNL Zendesk] 注册页面](https://www.zendesk.com/register/)以注册并创建您的Zendesk帐户。
* 成功注册后，导航到[[!DNL Zendesk] 网站](https://www.zendesk.com/login/)并提供您的&#x200B;**子域**。
* 接下来，选择&#x200B;**[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**。
* 最后，从&#x200B;**[!DNL API token]**&#x200B;部分检索API令牌。

![Zendesk API令牌](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

有关如何检索子域的信息，请参阅[[!DNL Zendesk documentation on subdomains]](<https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain->)。 有关生成API令牌的信息，请参阅有关生成新的API令牌的[[!DNL Zendesk] 指南](<https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token>)。

以下文档提供了有关如何使用API或用户界面将[!DNL Zendesk]连接到Platform的信息：

## 使用API将[!DNL Zendesk]连接到平台

* [使用流服务API为 [!DNL Zendesk] 创建源连接和数据流](../../tutorials/api/create/customer-success/zendesk.md)

## 使用UI将[!DNL Zendesk]连接到平台

* [在UI中创建 [!DNL Zendesk ]源连接](../../tutorials/ui/create/customer-success/zendesk.md)
* [在UI中为客户成功源连接创建数据流](../../tutorials/ui/dataflow/customer-success.md)

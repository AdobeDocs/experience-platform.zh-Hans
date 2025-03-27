---
title: Google Ads Source概述
description: 了解如何使用API或用户界面将Google Ads连接到Adobe Experience Platform。
exl-id: 1f6257e0-213c-4723-a240-511c11c5833c
source-git-commit: ac90eea69f493bf944a8f9920426a48d62faaa6c
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# [!DNL Google Ads]源

>[!NOTE]
>
>[!DNL Google Ads]源为测试版。 有关使用带有Beta标记的连接器的更多信息，请参阅[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform支持从第三方广告系统中提取数据。 对广告提供商的支持包括[!DNL Google Ads]。

## 先决条件 {#prerequisites}

### IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

### 在Experience Platform上配置权限

若要将您的[!DNL Google Ads]帐户连接到Experience Platform，您必须同时为您的帐户启用&#x200B;**[!UICONTROL 查看源]**&#x200B;和&#x200B;**[!UICONTROL 管理源]**&#x200B;权限。 请联系您的产品管理员以获取必要的权限。 有关详细信息，请阅读[访问控制UI指南](../../../access-control/ui/overview.md)。

### 收集所需的凭据

您必须为以下凭据提供相应的值，才能成功地将您的[!DNL Google Ads]帐户连接到Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| `clientCustomerId` | 客户端客户ID是与您要使用[!DNL Google Ads] API管理的[!DNL Google Ads]客户端帐户对应的帐号。 此ID遵循`123-456-7890`模板。 |
| `loginCustomerId` | 登录客户ID是与您的[!DNL Google Ads]经理帐户对应的帐号，用于从特定的操作客户获取报表数据。 有关登录客户ID的详细信息，请阅读[[!DNL Google Ads] API文档](https://developers.google.com/search-ads/reporting/concepts/login-customer-id)。 |
| `developerToken` | 开发人员令牌允许您访问[!DNL Google Ads] API。 您可以使用相同的开发人员令牌针对所有[!DNL Google Ads]帐户发出请求。 通过[登录到您的经理帐户](https://ads.google.com/home/tools/manager-accounts/)并导航到[!DNL API Center]页面来检索您的开发人员令牌。 |
| `refreshToken` | 刷新令牌是[!DNL OAuth2]身份验证的一部分。 此令牌允许您在访问令牌过期后重新生成访问令牌。 |
| `clientId` | 客户端ID与客户端密钥结合使用，作为[!DNL OAuth2]身份验证的一部分。 客户端ID和客户端密钥共同允许您的应用程序通过向[!DNL Google]标识您的应用程序来代表您的帐户运行。 |
| `clientSecret` | 客户端密钥与客户端ID结合使用，作为[!DNL OAuth2]身份验证的一部分。 客户端ID和客户端密钥共同允许您的应用程序通过向[!DNL Google]标识您的应用程序来代表您的帐户运行。 |
| `googleAdsApiVersion` | [!DNL Google Ads]支持的当前API版本。 尽管最新版本是`v18`，但Experience Platform上支持的最新版本是`v17`。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Google Ads]的连接规范ID为： `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 如果您使用[!DNL Flow Service] API连接[!DNL Google Ads]帐户，则需要此值。 |

## 将[!DNL Google Ads]连接到Experience Platform

以下文档提供了有关如何使用API或用户界面将[!DNL Google Ads]连接到Experience Platform的信息：

### 使用API

* [使用流服务API创建Google Ads基本连接](../../tutorials/api/create/advertising/ads.md)
* [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
* [使用流服务API为广告源创建数据流](../../tutorials/api/collect/advertising.md)

### 使用UI

* [在UI中创建Google Ads源连接](../../tutorials/ui/create/advertising/ads.md)
* [在UI中为广告源连接创建数据流](../../tutorials/ui/dataflow/advertising.md)

---
keywords: Experience Platform；主页；热门主题；Zoho CRM；zoho crm；Zoho；Zoho
solution: Experience Platform
title: Zoho CRM Source连接器概述
description: 了解如何使用API或用户界面将Zoho CRM连接到Adobe Experience Platform。
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# [!DNL Zoho CRM]

>[!WARNING]
>
>[!DNL Zoho CRM]源将于2025年6月底弃用。

Adobe Experience Platform允许从外部源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform支持从第三方CRM系统中摄取数据。 CRM提供商的支持包括[!DNL Zoho CRM]。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

## 检索[!DNL Zoho CRM]的身份验证凭据

在将数据从[!DNL Zoho CRM]帐户引入Experience Platform之前，必须首先检索凭据以验证您的[!DNL Zoho CRM]源。 按照以下步骤检索您的客户端ID、客户端密钥、访问令牌和刷新令牌。

### 注册您的应用程序

检索身份验证凭据的第一步是使用[[!DNL Zoho CRM] 开发人员控制台](https://accounts.zoho.com/)注册应用程序。 要注册应用程序，您必须从以下位置选择客户端类型：Java脚本、基于Web的移动应用程序、非浏览器的移动应用程序或自客户端。 接下来，为应用程序名称、网页URL和授权重定向URI提供值，然后[!DNL Zoho CRM]可以使用授权令牌重定向您。

成功注册将返回您的客户端ID和客户端密钥。

### 创建授权请求

接下来，必须使用基于Web的应用程序或自客户端创建[授权请求](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html)。 授权请求将返回您的授权令牌，从而允许您检索访问令牌。

创建授权请求时，必须填写&#x200B;**作用域**&#x200B;和&#x200B;**访问类型**&#x200B;的值。 有关作用域的更多信息，请参阅此[[!DNL Zoho CRM] 文档](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html)，而您的&#x200B;**访问类型**&#x200B;应始终设置为`offline`。

### 生成访问和刷新令牌

检索到授权令牌后，您可以生成[访问和刷新令牌](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html)，方法是在提供客户端ID、客户端密钥、授权令牌和重定向URI的同时向`{ACCOUNTS_URL}/oauth/v2/token`发出POST请求。 在此步骤中，还必须包含`grant_type`作为参数，并将值设置为`"authorization_code"`。

成功的请求会返回您的访问和刷新令牌，然后您可以使用这些令牌进行身份验证。

有关获取凭据的详细步骤，请参阅[[!DNL Zoho CRM] 身份验证指南](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html)。

## 使用API将[!DNL Zoho CRM]连接到[!DNL Experience Platform]

以下文档提供了有关如何使用API或用户界面将[!DNL Zoho CRM]连接到Experience Platform的信息：

- [使用流服务API创建 [!DNL Zoho CRM] 基本连接](../../tutorials/api/create/crm/zoho.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为CRM源创建数据流](../../tutorials/api/collect/crm.md)

## 使用UI将[!DNL Zoho CRM]连接到[!DNL Experience Platform]

- [在UI中创建 [!DNL Zoho CRM] 源连接](../../tutorials/ui/create/crm/zoho.md)
- [在用户界面中为CRM源连接创建数据流](../../tutorials/ui/dataflow/crm.md)

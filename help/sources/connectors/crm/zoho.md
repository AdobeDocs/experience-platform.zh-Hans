---
keywords: Experience Platform；主页；热门主题；Zoho CRM；zoho crm；Zoho；Zoho
solution: Experience Platform
title: Zoho CRM Source Connector概述
description: 了解如何使用API或用户界面将Zoho CRM连接到Adobe Experience Platform。
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# [!DNL Zoho CRM]

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从第三方CRM系统中摄取数据。 CRM提供商的支持包括 [!DNL Zoho CRM].

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于地区的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面，以了解更多信息。

## 检索您的身份验证凭据 [!DNL Zoho CRM]

在将数据从您的 [!DNL Zoho CRM] 帐户到Platform时，您必须首先检索凭据来验证您的 [!DNL Zoho CRM] 源。 按照以下步骤检索您的客户端ID、客户端密钥、访问令牌和刷新令牌。

### 注册您的应用程序

检索身份验证凭据的第一步是使用 [[!DNL Zoho CRM] 开发人员控制台](https://accounts.zoho.com/). 要注册应用程序，您必须从以下内容中选择客户端类型：Java脚本、基于Web的移动应用程序、非浏览器移动应用程序或自客户端。 接下来，为应用程序名称、网页URL和授权重定向URI提供值， [!DNL Zoho CRM] 然后，可以使用通过授权令牌重定向您。

成功注册将返回您的客户端ID和客户端密钥。

### 创建授权请求

接下来，您必须创建 [授权请求](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) 使用基于Web的应用程序或自客户端。 授权请求将返回您的授权令牌，从而允许您检索访问令牌。

创建授权请求时，必须填写两者的值 **范围** 和 **访问类型**. 请参阅此 [[!DNL Zoho CRM] 文档](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) 以了解有关范围的更多信息，同时 **访问类型** 应始终设置为 `offline`.

### 生成访问权杖并刷新令牌

检索授权令牌后，即可生成 [访问和刷新令牌](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) 向发出POST请求 `{ACCOUNTS_URL}/oauth/v2/token` 提供客户端ID、客户端密钥、授权令牌和重定向URI时。 在此步骤中，您还必须包含 `grant_type` 作为参数，并将值设置为 `"authorization_code"`.

成功的请求会返回您的访问和刷新令牌，然后您可以使用这些令牌进行身份验证。

有关获取凭据的详细步骤，请参阅 [[!DNL Zoho CRM] 身份验证指南](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Connect [!DNL Zoho CRM] 到 [!DNL Platform] 使用API

以下文档提供了有关如何连接的信息 [!DNL Zoho CRM] 至使用API或用户界面的Platform：

- [创建 [!DNL Zoho CRM] 使用流服务API进行基本连接](../../tutorials/api/create/crm/zoho.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为CRM源创建数据流](../../tutorials/api/collect/crm.md)

## Connect [!DNL Zoho CRM] 到 [!DNL Platform] 使用UI

- [创建 [!DNL Zoho CRM] UI中的源连接](../../tutorials/ui/create/crm/zoho.md)
- [在UI中为CRM源连接创建数据流](../../tutorials/ui/dataflow/crm.md)

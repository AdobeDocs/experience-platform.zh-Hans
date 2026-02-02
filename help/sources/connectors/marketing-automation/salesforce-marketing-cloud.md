---
title: Salesforce Marketing Cloud Source概述
description: 了解如何使用API或用户界面将Salesforce Marketing Cloud连接到Adobe Experience Platform。
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-05-17T00:00:00Z
source-git-commit: 4d47eae91711596677335b03568add9f6fbade74
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 2%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>[!DNL Oracle Salesforce Marketing Cloud]源现已弃用，不再可用。 使用新的[[!DNL Salesforce Marketing Cloud] (V2)源](sfmc.md)作为您的[!DNL Salesforce Marketing Cloud]数据的新连接器。

[!DNL Salesforce Marketing Cloud]使您能够从单一平台跨电子邮件、移动设备、社交媒体和广告管理和自动化客户参与。 借助Email Studio、历程生成器和Audience Builder等工具，您可以创建针对受众定制的个性化促销活动和客户历程。

您可以使用[!DNL Salesforce Marketing Cloud]源连接帐户并将数据导入Adobe Experience Platform。

## 先决条件

在将[!DNL Salesforce Marketing Cloud]源连接到Experience Platform之前，必须确保将以下&#x200B;**权限范围**&#x200B;配置为您的[!DNL Salesforce Marketing Cloud]客户端ID和客户端密钥组合：

* `campaign_read`
* `list_and_subscribers_read`

您可以通过调用`v2/userinfo` API的[!DNL Salesforce Marketing Cloud]资源来请求作用域。 有关如何请求和比较范围的指导，请参阅[[!DNL Salesforce Marketing Cloud] API集成权限范围文档](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>)。

有关作用域的更多信息，包括其相关权限和行为的列表，请参阅此[[!DNL Salesforce Marketing Cloud] REST API文档](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>)。

>[!IMPORTANT]
>
>[!DNL Salesforce Marketing Cloud]源集成当前不支持自定义对象摄取。

### IP地址允许列表

在将源连接到Experience Platform之前，必须将特定于区域的IP地址添加到允许列表。 有关详细信息，请阅读有关[将IP地址列入允许列表到Experience Platform](../../ip-address-allow-list.md)的指南。

>[!WARNING]
>
>如果您没有向帐户添加必要的IP地址，则[!DNL Salesforce Marketing Cloud]允许列表将不会连接到Experience Platform。

### 在Azure上对Experience Platform进行身份验证 {#azure}

必须提供以下凭据的值才能将[!DNL Salesforce Marketing Cloud]连接到[!DNL Azure]上的Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| Host | 应用程序的主机服务器。 这通常是您的子域。 **注意：**&#x200B;在输入`host`值时，需要指定`{subdomain}.rest.marketingcloudapis.com`。 例如，如果您的主机URL是`https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`，则必须输入`acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/`作为主机值。 |
| 客户端 ID | 与您的[!DNL Salesforce Marketing Cloud]应用程序关联的客户端ID。 |
| 客户端密码 | 与您的[!DNL Salesforce Marketing Cloud]应用程序关联的客户端密钥。 |
| 连接规范ID | **连接规范**&#x200B;提供数据源的连接器属性。 这包含身份验证规范和创建&#x200B;**Base**&#x200B;和&#x200B;**Source**&#x200B;连接的要求等详细信息。 对于[!DNL Salesforce Marketing Cloud]，连接规范ID为： `ea1c2a08-b722-11eb-8529-0242ac130003`。 **注意：**&#x200B;只有在通过API连接时才需要此凭据。 |

### 在Amazon Web Services (AWS)上对Experience Platform进行身份验证 {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../landing/multi-cloud.md)。

必须提供以下凭据的值，才能将[!DNL Salesforce Marketing Cloud]连接到AWS上的Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| 子域 | [!DNL Salesforce Marketing Cloud]实例URL的唯一部分，用于构建API端点。 |
| 客户端 ID | 在[!DNL Salesforce Marketing Cloud]中创建已安装的包时生成的应用程序的公共标识符 |
| 客户端密码 | 与您的客户端ID关联的机密密钥，也在已安装的软件包中生成。 |
| 连接规范ID | **连接规范**&#x200B;提供数据源的连接器属性。 这包含身份验证规范和创建&#x200B;**Base**&#x200B;和&#x200B;**Source**&#x200B;连接的要求等详细信息。 对于[!DNL Salesforce Marketing Cloud]，连接规范ID为： `ea1c2a08-b722-11eb-8529-0242ac130003`。 **注意：**&#x200B;只有在通过API连接时才需要此凭据。 |

有关详细信息，请阅读有关服务器到服务器集成的访问令牌的[[!DNL Salesforce] 文档](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html)。

## 使用API将[!DNL Salesforce Marketing Cloud]连接到Experience Platform

以下文档提供了有关如何使用API将[!DNL Salesforce Marketing Cloud]连接到Experience Platform的信息：

* [使用流服务API连接 [!DNL Salesforce Marketing Cloud] 到Experience Platform](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
* [使用流服务API为营销自动化源创建数据流](../../tutorials/api/collect/marketing-automation.md)

## 使用UI将[!DNL Salesforce Marketing Cloud]连接到Experience Platform

以下文档提供了有关如何使用用户界面将[!DNL Salesforce Marketing Cloud]连接到Experience Platform的信息：

* [在UI中将 [!DNL Salesforce Marketing Cloud] 连接到Experience Platform](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [在UI中为Marketing Automation源连接创建数据流](../../tutorials/ui/dataflow/marketing-automation.md)

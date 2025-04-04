---
title: Oracle NetSuite Source概述
description: 了解如何使用API或用户界面将Oracle NetSuite连接到Adobe Experience Platform。
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta 版
exl-id: 1dd30660-c990-4d3f-a64f-2a17e426f56d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 2%

---

# [!DNL Oracle NetSuite]

>[!NOTE]
>
>[!DNL Oracle NetSuite]源为测试版。 有关使用测试版标记源的更多信息，请阅读[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform为引入数据第三方营销自动化系统提供支持。 对营销自动化提供商的支持包括[!DNL Oracle NetSuite]。

[[!DNL Oracle NetSuite]](https://www.netsuite.com/)是基于云的业务管理套件，包括ERP/财务、CRM和电子商务解决方案。

您可以使用两个不同的源将数据从[!DNL Oracle NetSuite]摄取到Experience Platform：

* 使用[!DNL Oracle NetSuite Activities]源摄取事件数据。
* 使用[!DNL Oracle NetSuite Entities]源摄取客户和联系人数据。

有关两个[!DNL Oracle NetSuite]源的更多信息，请查看下表。

| 来源 | 类型 | 描述 |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | 活动 | 检索添加到日历中的计划活动。 |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | 客户 | 检索特定的客户数据，包括客户名称、地址和关键标识符等详细信息。 |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | 联系 | 检索联系人姓名、电子邮件、电话号码以及与客户关联的任何自定义联系人相关字段。 |

## IP地址允许列表 {#ip-allow-list}

在使用源连接器之前，可能需要将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

## 先决条件 {#prerequisites}

在将[!DNL Oracle NetSuite]数据带入Experience Platform之前，您必须首先确保您具备以下条件：

* **帐户[!DNL Oracle NetSuite]**。
   * 如果您还没有有效的帐户，请联系[[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml)。
* 任何[!DNL Oracle NetSuite]产品的&#x200B;**活动订阅**。
* **帐户ID**。
   * [!DNL Oracle NetSuite]源使用OAuth 2.0与[!DNL Oracle NetSuite] API进行通信。 如果您没有帐户ID，请访问[上的[!DNL Oracle]文档，了解如何检索帐户ID](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID)。
* **客户端ID**&#x200B;和&#x200B;**客户端密码**&#x200B;组合。
   * 访问[!DNL Oracle NetSuite] API需要客户端ID和客户端密钥。 在此步骤中，您还必须确保管理员能够：
      * 启用了OAuth 2.0功能并设置了适当的OAuth 2.0角色。
      * 已将用户分配给OAuth 2.0角色并创建了必要的集成记录。
* **访问令牌**&#x200B;和&#x200B;**刷新令牌**。
   * 有关如何生成访问和刷新令牌的信息，请参阅[OAuth 2.0授权代码授予流程](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow)上的[!DNL Oracle]指南。

### 收集所需的凭据 {#gather-credentials}

为了将[!DNL Oracle NetSuite]连接到Experience Platform，您必须提供以下连接属性的值：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| 客户端 ID | 在[!DNL Oracle NetSuite]中创建集成记录时生成的客户端ID值。 有关详细信息，请阅读有关如何[创建集成记录](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981)的[!DNL Oracle]指南。 | `7fce.....b42f`<br>该值是64个字符的字符串。 |
| 客户端密码 | 创建集成记录时生成的客户端密钥值。 有关详细信息，请阅读有关如何[创建集成记录](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981)的[!DNL Oracle]指南。 | `5c98.....1b46`<br>该值是64个字符的字符串。 |
| 授权测试URL | （可选）您的[!DNL NetSuite]授权测试URL。 | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| 访问令牌 | 访问令牌为JSON Web令牌(JWT)格式，仅有效60分钟。 有关如何检索访问令牌的更多信息，请阅读有关[OAuth 2.0 Authorization for NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint)的[!DNL Oracle]指南。 | `eyJr......f4V0`<br>该值是一个由1024个字符组成的字符串，格式为JSON Web令牌(JWT)。 |
| 刷新令牌 | 在访问令牌过期后，使用刷新可生成新的访问令牌。 刷新令牌的有效期为七天。 有关如何检索访问令牌的更多信息，请阅读有关[OAuth 2.0 Authorization for NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint)的[!DNL Oracle]指南。 | `eyJr......dmxM`<br>该值是一个由1024个字符组成的字符串，格式为JSON Web令牌(JWT)。 |
| 访问令牌URL | 应用程序将POST请求发送到的令牌端点。 | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>刷新令牌过期后，您必须在Experience Platform中使用更新的令牌创建一个新帐户。

## 将[!DNL Oracle NetSuite Activities]连接到Experience Platform {#oracle-netsuite-activities}

以下文档提供了有关如何使用API或用户界面将[!DNL Oracle NetSuite Activities]连接到Experience Platform的信息：

* [创建源连接和数据流以使用API将 [!DNL Oracle NetSuite Activities] 数据引入Experience Platform](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md)。
* 使用UI [将您的 [!DNL Oracle NetSuite Activities] 帐户连接到Experience Platform](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md)。
* [使用UI](../../tutorials/ui/dataflow/marketing-automation.md)为源连接创建数据流。

## 将[!DNL Oracle NetSuite Entities]连接到Experience Platform {#oracle-netsuite-entities}

以下文档提供了有关如何使用API或用户界面将[!DNL Oracle NetSuite Entities]连接到Experience Platform的信息：

* [创建源连接和数据流以使用API将 [!DNL Oracle NetSuite Entities] 数据引入Experience Platform](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md)。
* 使用UI [将您的 [!DNL Oracle NetSuite Entities] 帐户连接到Experience Platform](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md)。
* [使用UI](../../tutorials/ui/dataflow/marketing-automation.md)为源连接创建数据流。

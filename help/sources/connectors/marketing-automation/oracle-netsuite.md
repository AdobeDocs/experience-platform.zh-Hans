---
title: oracleNetSuite源概述
description: 了解如何使用API或用户界面将OracleNetSuite连接到Adobe Experience Platform。
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta 版
source-git-commit: 632cff3ee4ca82d391e9a1df0cb38d903e8a5428
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 1%

---

# [!DNL Oracle NetSuite]

>[!NOTE]
>
>此 [!DNL Oracle NetSuite] 源为测试版。 请阅读 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记源代码的更多信息。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform为第三方营销自动化系统提供数据提取支持。 对营销自动化提供商的支持包括 [!DNL Oracle NetSuite].

[[!DNL Oracle NetSuite]](https://www.netsuite.com/) 是一个基于云的业务管理套件，它包括ERP/财务、CRM和电子商务解决方案。

您可以使用两个不同的源来从中摄取数据 [!DNL Oracle NetSuite] 要Experience Platform：

* 使用 [!DNL Oracle NetSuite Activities] 用于摄取事件数据的源。
* 使用 [!DNL Oracle NetSuite Entities] 用于摄取客户和联系数据的源。

查看下表，以了解关于两者的更多信息 [!DNL Oracle NetSuite] 源。

| 来源 | 类型 | 描述 |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | 活动 | 检索添加到日历中的计划活动。 |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | 客户 | 检索特定的客户数据，包括客户名称、地址和关键标识符等详细信息。 |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | 联系人 | 检索联系人姓名、电子邮件、电话号码以及与客户关联的任何自定义联系人相关字段。 |

## IP地址允许列表 {#ip-allow-list}

在使用源连接器之前，可能需要将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面以了解更多信息。

## 先决条件 {#prerequisites}

在带上 [!DNL Oracle NetSuite] 要Experience Platform的数据，您必须首先确保具有以下项：

* **An [!DNL Oracle NetSuite] 帐户**.
   * 联系人 [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml) 如果您还没有有效的帐户。
* An **活动订阅** 到任意 [!DNL Oracle NetSuite] 产品。
* An **帐户ID**.
   * 此 [!DNL Oracle NetSuite] 源使用OAuth 2.0与 [!DNL Oracle NetSuite] API。 如果您没有帐户ID，请访问 [!DNL Oracle] 文档 [如何检索您的帐户ID](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID).
* A **客户端ID** 和 **客户端密码** 组合。
   * 需要客户端ID和客户端密钥才能访问 [!DNL Oracle NetSuite] API。 在此步骤中，您还必须确保管理员能够：
      * 启用了OAuth 2.0功能并设置了适当的OAuth 2.0角色。
      * 已将用户分配给OAuth 2.0角色并创建了必要的集成记录。
* An **访问令牌** 和 **刷新令牌**.
   * 请参阅 [!DNL Oracle] 指南 [OAuth 2.0授权代码授予流程](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow) 有关如何生成访问和刷新令牌的信息。

### 收集所需的凭据 {#gather-credentials}

为了连接 [!DNL Oracle NetSuite] 到Platform时，必须提供以下连接属性的值：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| 客户端ID | 在中创建集成记录时生成的客户端ID值 [!DNL Oracle NetSuite]. 阅读 [!DNL Oracle] 操作方法指南 [创建集成记录](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) 以了解更多信息。 | `7fce.....b42f`<br>该值是由64个字符组成的字符串。 |
| 客户端密码 | 创建集成记录时生成的客户端密钥值。 阅读 [!DNL Oracle] 操作方法指南 [创建集成记录](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) 以了解更多信息。 | `5c98.....1b46`<br>该值是由64个字符组成的字符串。 |
| 授权测试URL | （可选）您的 [!DNL NetSuite] 授权测试URL。 | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| 访问令牌 | 访问令牌为JSON Web令牌(JWT)格式，仅有效60分钟。 有关如何检索访问令牌的更多信息，请参阅 [!DNL Oracle] 指南 [适用于NetSuite的OAuth 2.0授权](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br> 该值是一个由1024个字符组成的字符串，格式为JSON Web令牌(JWT)。 |
| 刷新令牌 | 在访问令牌过期后，使用刷新可生成新的访问令牌。 刷新令牌的有效期为七天。 有关如何检索访问令牌的更多信息，请参阅 [!DNL Oracle] 指南 [适用于NetSuite的OAuth 2.0授权](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br> 该值是一个由1024个字符组成的字符串，格式为JSON Web令牌(JWT)。 |
| 访问令牌URL | 应用程序将POST请求发送到的令牌端点。 | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>刷新令牌过期后，您必须使用更新后的令牌在Experience Platform中创建新帐户。

## 连接 [!DNL Oracle NetSuite Activities] 目标平台 {#oracle-netsuite-activities}

以下文档提供了有关如何连接的信息 [!DNL Oracle NetSuite Activities] 使用API或用户界面连接到Platform：

* [创建源连接和数据流以引入 [!DNL Oracle NetSuite Activities] 使用API将数据发送到平台](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [连接您的 [!DNL Oracle NetSuite Activities] 要使用UIExperience Platform的帐户](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [使用用户界面为源连接创建数据流](../../tutorials/ui/dataflow/marketing-automation.md).

## 连接 [!DNL Oracle NetSuite Entities] 目标平台 {#oracle-netsuite-entities}

以下文档提供了有关如何连接的信息 [!DNL Oracle NetSuite Entities] 使用API或用户界面连接到Platform：

* [创建源连接和数据流以引入 [!DNL Oracle NetSuite Entities] 使用API将数据发送到平台](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [连接您的 [!DNL Oracle NetSuite Entities] 要使用UIExperience Platform的帐户](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [使用用户界面为源连接创建数据流](../../tutorials/ui/dataflow/marketing-automation.md).

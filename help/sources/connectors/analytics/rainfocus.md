---
title: RainFocus源概述
description: 了解如何将RainFocus帐户中的事件管理和分析数据引入Experience Platform
last-substantial-update: 2023-06-21T00:00:00Z
badge: Beta 版
exl-id: 88e333e3-2b93-4d66-8412-efadea58ac46
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 4%

---

# [!DNL RainFocus]

>[!NOTE]
>
>[!DNL RainFocus]源为测试版。 有关使用测试版标记源的更多信息，请阅读[源概述](../../home.md#terms-and-conditions)。

[!DNL RainFocus]是一个平台，可用于推广您的活动和构建您的受众。 您可以使用[!DNL RainFocus]创建精美的促销页面、跟踪促销活动表现以及优化注册转化。

在Adobe Experience Platform和Real-time Customer Data Platform中使用[!DNL RainFocus]源实时通过与会者体验事件自动扩充您的客户数据配置文件。 在启用后，体验事件会自动流式传输到Real-Time CDP中，以便利用下游目标和应用程序(如Customer Journey Analytics和Adobe Journey Optimizer)进行强大的受众分段、数据分析和激活与会者历程。

>[!IMPORTANT]
>
>此源连接器和文档页面由[!DNL RainFocus]团队创建和维护。 如有任何查询或更新请求，请直接通过clientcare<span>@rainfocus.com联系他们，或访问[[!DNL RainFocus] 帮助中心](https://help.rainfocus.com/hc/en-us)

## 先决条件

您必须先完成以下先决条件，然后才能在Experience Platform上激活[!DNL RainFocus]集成：

[在Adobe Developer门户中创建Adobe服务帐户(JWT)](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>Adobe最近宣布弃用JWT令牌以支持OAuth。 为了适应此更改，[!DNL RainFocus]源将在不久的将来迁移到OAuth。

### 收集所需的凭据

为了将[!DNL RainFocus]连接到Experience Platform，您必须在[!DNL RainFocus]中提供以下连接属性的值：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| 客户端 ID | 可从Adobe Developer门户的Adobe服务帐户中获取客户端ID。 | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| 客户端密码 | 客户端密钥可以从Adobe Developer门户中的Adobe服务帐户获取。 | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| 技术帐户ID | 技术帐户ID可以从Adobe Developer门户的Adobe服务帐户中获取。 | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| 组织 ID | 组织ID可以从Adobe Developer门户的Adobe服务帐户中获取 | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### 创建XDM架构并定义标识字段 {#create-an-xdm-schema-and-define-the-identity-field}

为了在Experience Platform中存储来自[!DNL RainFocus]的体验事件，您必须创建体验数据模型(XDM)架构以描述可以存储可能从[!DNL RainFocus]发送的字段和数据类型的数据集。

[!DNL RainFocus]建议使用以下字段，其中包含默认发送的所有可能数据。

还建议使用以下字段组（用前缀表示）：

* 与会者
* 参展商
* 潜在客户
* 会话
* 会话时间

**架构应包含以下字段：**

| 字段 | 类型 | 示例 | 描述 |
| --- | --- | --- | --- |
| `attendee.registered` | 字符串 | 是 | 确定与会者是否被视为已注册的标志。 |
| `attendee.attendeeId` | 字符串 | 1619119968857001fvLB | [!DNL RainFocus]中的与会者ID。 |
| `attendee.externalId` | 字符串 | 1666809456617001wyPj | 组织指定的外部ID。 |
| `attendee.clientId` | 字符串 | 8EFC1F57631CAFE70A495ECB@8f3f1f5c631caf3e495fd8.e | 与会者SSO客户端ID。 |
| `attendee.email` | 字符串 | user<span>@company.com | 与会者的电子邮件地址。 |
| `transmissionId` | 字符串 | 1680309557133001YHhz | 用于数据推送的唯一标识符。 |
| `eventType` | 字符串 | 已计划会话 | 与会者体验活动的名称。 |
| `timestamp` | 日期时间 | 2023-04-01T00:41:57.000Z | 数据推送的时间戳。 |
| `event.name` | 字符串 | Adobe Summit2023 | 发生传输的事件的名称。 |
| `exhibitor.exhibitorId` | 字符串 | 1680309557133001YHhz | 参展商的[!DNL RainFocus]标识符。 |
| `exhibitor.externalId` | 字符串 | 1666809514105001lSJN | 客户端系统中参展商的标识符。 |
| `exhibitor.name` | 字符串 | IBM | 参展商的名称。 |
| `lead.leadId` | 字符串 | 1666809456617001wyPj | 商机的[!DNL RainFocus]标识符。 |
| `lead.note` | 字符串 | | |
| `session.sessionId` | 字符串 | 1666809373585001t4aV | 会话的[!DNL RainFocus]标识符。 |
| `session.externalId` | 字符串 | 1666809456617001wyPj | 客户端系统中会话的标识符。 |
| `session.code` | 字符串 | GS3 | 会话的代码。 |
| `session.title` | 字符串 | Inspiration主题演讲 | 会话的标题。 |
| `session.length` | 整数 | 90 | 会话的长度。 |
| `sessiontime.sessiontimeId` | 字符串 | 1673033149739001OJLZ | 会话时间的[!DNL RainFocus]标识符。 |
| `sessiontime.startTime` | 字符串 | 2023-03-22 10:00:00 | 会话的开始时间。 |
| `sessiontime.endTime` | 字符串 | 2023-03-22 10:00:00 | 会话的结束时间。 |
| `sessiontime.room` | 字符串 | B32 | 用于会话的房间。 |

{style="table-layout:auto"}

要为[!DNL RainFocus]数据创建架构，请阅读以下文档，了解有关如何使用API或UI创建架构的步骤。

* [使用用户界面创建架构](../../../xdm/tutorials/create-schema-ui.md)
* [使用API创建架构](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* 架构必须扩展&#x200B;**XDM ExperienceEvent类。**
>* 您必须确保架构包含&#x200B;**主标识**，并且已为配置文件&#x200B;**启用**。 有关详细信息，请参阅[在UI中定义标识字段的指南](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html?lang=zh-Hans)
>* 您可以将示例身份(Email)替换为另一个合适的标识符，例如sha256电子邮件或ECID。

### 在RainFocus中创建集成配置文件 {#create-an-integration-profile-in-rainfocus}

服务帐户和XDM架构准备就绪后，您现在可以通过[!DNL RainFocus]平台激活[!DNL Integration Profile]。 [!DNL Integration Profile]负责将数据流式传输到Experience Platform。

登录到[[!DNL RainFocus] 平台](https://app.rainfocus.com)。 在主导航中，选择&#x200B;**[!DNL Libraries]**，然后选择&#x200B;**[!DNL Integration Profiles]**

![选择了库和集成配置文件的RainFocus UI。](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

要创建新配置文件，请选择&#x200B;**(`+`)**&#x200B;图标。 接下来，选择&#x200B;**Adobe Real-time Customer Data Platform**，然后选择&#x200B;**确定**。

![RainFocus UI中的创建集成配置文件窗口。](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

接下来，提供您在Adobe Developer门户项目中检索到的凭据：

* **客户端ID**
* **客户端密码**
* **技术帐户ID**
* **组织 ID**

提供凭据后，选择&#x200B;**[!DNL Save]**。您现在应会在[!DNL RainFocus]仪表板中看到新的[!DNL Integration Profile]列出。

选择您刚刚创建的[!DNL Integration Profile]以查看已配置的预定义&#x200B;**推送类型**&#x200B;的列表。 这些[体验事件](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html?lang=zh-Hans)在发生时将发送到Experience Platform。

![RainFocus仪表板中预定义的推送类型列表。](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

要检索示例JSON有效负载的副本，请选择&#x200B;**[!DNL Sample JSON Payload]**。 接下来，突出显示并复制示例JSON有效负载，并&#x200B;**将其保存在扩展名为.json**&#x200B;的新文件中。 稍后将在[映射配置](../../tutorials/ui/create/analytics/rainfocus.md#mapping)的Experience Platform中使用它。

![RainFocus仪表板中的JSON有效负载示例。](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**设置尚未完成**：创建数据流后，您需要通过提供您的&#x200B;**流式处理终结点URL**&#x200B;和&#x200B;**数据流ID**&#x200B;返回到[!DNL RainFocus]仪表板以完成[!DNL Integration Profile]。

## 后续步骤

通过阅读本文档，您已完成将[!DNL RainFocus]帐户中的数据流式传输到Experience Platform所需的先决条件设置。 现在，您可以继续阅读[使用用户界面](../../tutorials/ui/create/analytics/rainfocus.md)连接 [!DNL RainFocus] 以Experience Platform的指南。

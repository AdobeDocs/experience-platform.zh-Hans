---
keywords: Experience Platform；主页；热门主题；GDPR；gdpr；ccpa：CCPA；PDPA；PDPA_that；PDPA_THA；lgpd；LGPD；lgpd_bra；LGPD_BRA；
solution: Experience Platform
title: Privacy Service概述
description: Privacy Service使您能够在Experience Cloud数据操作中促进自动遵守法律隐私法规。
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 3296209a15a5f88ab14e16de25d554b9df712445
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 5%

---

# [!DNL Privacy Service] 概述

>[!IMPORTANT]
>
>Adobe Experience Platform Privacy Service的权限已得到改进，以提高其粒度级别。 这些更改使组织管理员能够通过所需的角色和权限级别授予更多用户访问权限。 技术帐户用户必须更新其Privacy Service权限，因为此即将进行的更新对他们来说是一项重大更改。 此权限更改的实施将发生在 **2023年4月13日**. 请参阅相关文档 [迁移旧版API凭据](./permissions.md#migrate-tech-accounts) 以获取有关解决此问题的指导。
>
>企业客户可以使用技术帐户，这些帐户是通过Adobe开发人员控制台创建的。 技术帐户持有人的Adobe ID结束于 `@techacct.adobe.com`. 如果您不确定您是否是技术帐户所有者，请联系您的组织管理员。

为了提供更好的客户体验，您需要收集和存储客户的个人数据。 在使用此类数据时，请务必了解和尊重客户的隐私。 新的法律和组织规定正在用户提供相应的权利，允许他们请求访问或删除您的数据存储中的用户个人数据。

Adobe Experience Platform [!DNL Privacy Service] 旨在应对要求企业管理其客户个人数据的方式发生的根本性变化。 的中心目的 [!DNL Privacy Service] 是自动遵守数据隐私法规，一旦违反这些法规，可能会导致严重罚款并中断业务的数据运营。

[!DNL Privacy Service] 提供RESTful API和用户界面，帮助您管理客户数据请求。 替换为 [!DNL Privacy Service]，您可以提交从Adobe Experience Cloud应用程序访问和删除个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

>[!IMPORTANT]
>
>Privacy Service仅适用于数据主体和消费者权利请求。 不支持或允许将Privacy Service用于数据清理或维护的任何其他用途。 Adobe有及时履行这些义务的法律义务。 因此，不允许对Privacy Service进行负载测试，因为它是仅用于生产的环境，并会创建有效隐私请求的不必要积压。
>
>现已设定每日硬性上传限制，以帮助防止滥用服务。 发现滥用系统的用户将禁用其对该服务的访问权限。 随后将与他们举行一次会议，讨论他们的行动并讨论可以接受的Privacy Service用途。

## 快速入门 [!DNL Privacy Service] {#getting-started}

为了利用 [!DNL Privacy Service]，需要根据贵组织的隐私要求、您从客户那里收集的身份数据类型以及将CRM系统与该服务连接的最佳方式做出几个关键决策。

可通过以下问题对这些决策进行总结：

1. **我从客户那里收集了哪些信息？**
   * 充分利用 [!DNL Privacy Service]中，您必须详细了解从客户那里收集的数据类型，以及哪些类型的数据受隐私法规的约束。 请参阅以下部分： [确定隐私要求](#requirements) 了解更多信息。
1. **我是否正确标记了数据？**
   * 必须正确标记数据，服务才能确定在隐私作业期间要访问或删除哪些字段。 请参阅以下部分： [标签数据](#label) 了解更多信息。
1. **我知不知道要将哪些ID发送到 [!DNL Privacy Service]？**
   * 在发送隐私请求时，必须提供特定Adobe应用程序特有的单个客户ID。 请参阅以下章节： [提供身份数据](#identity)  和 [提出隐私请求](#requests) 了解更多信息。
1. **如何跟踪我的隐私作业？**
   * 提出隐私请求后，有几个选项可用于跟踪其状态和结果。 请参阅以下部分： [监控隐私作业](#monitor) 了解更多信息。

以下部分提供了有关这些重要先决条件步骤的一般指导，同时还提供了指向更多步骤的链接 [!DNL Privacy Service] 文档，以了解更多详细信息。

### 确定贵组织的隐私要求 {#requirements}

根据您的业务性质及运营所在的司法管辖区，您的数据运营可能会受到隐私法规的约束。这些法规通常赋予您的客户请求访问您从他们那里收集的数据的权利，并且这些客户有权请求删除所存储的数据。在整个文档中，这些客户对其个人数据的请求称为“隐私请求”。

有关不同法律隐私法规的详细信息，这些法规 [!DNL Privacy Service] 管理对的请求，包括关键术语和常见问题的解答，请参阅 [隐私法规文档](./regulations/overview.md).

如果您的数据操作属于任何受支持法规的管辖范围，请查看其文档以了解重要信息，例如他们授予客户的特定隐私权，以及用于履行隐私请求的合规窗口。 在决定如何集成时，应考虑此信息 [!DNL Privacy Service] ，以及客户应如何与您的网站交互以便提出隐私请求。

除了法律法规之外，在做出这些决策时还应考虑适用于您组织的任何组织或行业标准。

### 为隐私请求设置数据标签 {#label}

根据 [!DNL Experience Cloud] 对于您正在使用的应用程序，您必须为响应隐私请求而应该访问或删除的特定数据字段设置标签。 标记数据的过程因应用程序而异。 要了解如何为每个受支持的Adobe应用程序标记数据，请参阅以下文档： [Experience Cloud应用程序](./experience-cloud-apps.md).

### 确定要发送到的身份数据的类型 [!DNL Privacy Service] {#identity}

为了 [!DNL Privacy Service] 要处理来自客户的隐私请求，必须在请求本身中为该客户至少提供一个唯一标识值。 唯一标识值是指可用于识别个人及其存储在您网站上的个人数据的任何信息， [!DNL Experience Cloud] 数据存储。 [!DNL Privacy Service] 根据请求的性质（访问、删除或选择退出），使用此身份信息查找和处理客户的个人数据。

根据 [!DNL Experience Cloud] 您的CRM系统所使用的应用程序，您必须为每个客户提供的标识值的类型和数量会有所不同。 某些应用程序使用自己的内部客户ID值(例如Adobe Target ID)，而其他解决方案依赖来自Adobe的全局标识符 [!DNL Experience Cloud Identity Service] (ECID)，用于跟踪所有报表包中的客户活动 [!DNL Experience Cloud] 应用程序。 此外，电子邮件地址或电话号码等通用个人信息也可以作为有效的身份数据。

上的文档 [隐私请求的身份数据](./identity-data.md) 提供有关接受的身份信息类型的更多详细信息 [!DNL Privacy Service]. 本文档还提供了有关如何利用Adobe技术在客户与您的网站交互时有效地从客户那里检索适当的身份信息并将该数据发送到的指导 [!DNL Privacy Service] 在API请求中。

### 开始提出隐私请求 {#requests}

确定企业的隐私需求并决定要将哪些身份值发送到后 [!DNL Privacy Service]，您可以开始提出隐私请求。 [!DNL Privacy Service] 允许您通过API或UI发送隐私请求。

>[!IMPORTANT]
>
>以下部分提供了指向文档的链接，这些文档介绍了如何在API或UI中提出通用隐私请求。 但是，取决于 [!DNL Experience Cloud] 如果您使用的应用程序，则您在请求有效负载中必须发送的字段可能与这些指南中显示的示例不同。
>
>当您遵循API或UI指南时，请参阅上的文档 [Privacy Service和Experience Cloud应用程序](./experience-cloud-apps.md) 有关如何为特定隐私请求设置格式的更多文档 [!DNL Experience Cloud] 应用程序。
>
>还需要注意的是，隐私请求会在Experience Cloud应用程序之间异步处理。 Privacy Service收到请求后，每个应用程序可能需要几分钟到几周的时间才能完成请求。 完成每个请求所需的时间取决于您所使用的应用程序，以及需要处理的数据量。

#### 使用 API

此 [[!DNL Privacy Service API]](https://www.adobe.io/experience-platform-apis/references/privacy-service/) 提供了多个端点，用于使用RESTful API调用创建和管理隐私作业，允许您以编程方式实现隐私法规的合规性。 [!DNL Experience Cloud] 应用程序。 有关如何使用API的详细步骤，请参阅 [Privacy ServiceAPI指南](api/overview.md).

#### 使用UI

>[!NOTE]
>
>此 [!DNL Privacy Service] UI当前仅支持访问和删除请求。 所有选择退出请求必须改通过API发出。

此 [!DNL Privacy Service] UI允许您使用图形界面创建和监控隐私作业。 UI包括 **[!UICONTROL 状态报告]** 此构件可提供所有活动请求状态的可视表示形式，并允许您使用内置的创建新请求 **[!UICONTROL 请求生成器]** 或上传JSON文件。 有关使用UI的更多信息，请参阅 [Privacy Service用户指南](ui/overview.md).

### 监控隐私作业 {#monitor}

制定隐私作业后，您有多个选项可用于监控其状态和结果：

| 监控方法 | 描述 |
| --- | --- |
| [!DNL Privacy Service] UI | 此 [!DNL Privacy Service] UI提供了一个监视仪表板，允许您查看所有活动请求状态的可视表示形式。 请参阅 [Privacy Service用户指南](ui/overview.md) 了解更多信息。 |
| [!DNL Privacy Service] API | 您可以使用提供的查找端点以编程方式监控隐私作业的状态。 [!DNL Privacy Service] API。 请参阅 [Privacy ServiceAPI指南](./api/overview.md) 有关如何使用API的详细步骤。 |
| [!DNL Privacy Events] | [!DNL Privacy Events] 利用发送到配置的webhook的Adobe I/O事件，以促进高效的作业请求自动化。 他们减少了或消除了投票 [!DNL Privacy Service] API，以检查作业是否已完成或是否已达到工作流中的某个里程碑。 请参阅上的教程 [订阅隐私事件](./privacy-events.md) 了解更多信息。 |

## 后续步骤

本文档提供了以下内容的高级概述 [!DNL Privacy Service] 以及开始使用该服务的功能所需的主要步骤。 有关使用的各个方面的更深入信息，请参阅整个概述中链接的文档 [!DNL Privacy Service].

---
keywords: Experience Platform；主页；热门主题；GDPR；gdpr；ccpa：CCPA；PDPA；PDPA_that；PDPA_THA；lgpd；LGPD；lgpd_bra；LGPD_BRA；
solution: Experience Platform
title: Privacy Service概述
description: 了解Privacy Service如何促进在您的Experience Cloud数据操作中自动遵守隐私法规。
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 61a5b4fd7af68e7379b456ddd37218d183e76256
workflow-type: tm+mt
source-wordcount: '1660'
ht-degree: 5%

---

# Privacy Service 概述

要提供更好的客户体验，您必须收集和存储客户的个人数据。 在使用此数据时，理解并尊重客户的隐私至关重要。 新的法律和组织规定正在用户提供相应的权利，允许他们请求访问或删除您的数据存储中的用户个人数据。

Adobe Experience Platform Privacy Service的开发旨在应对企业管理客户个人数据的方式发生根本性转变的情况。 Privacy Service的中心目的是自动遵守数据隐私法规，一旦违反这些法规，可能会导致严重罚款并中断业务的数据操作。

Privacy Service提供了RESTful API和用户界面，帮助您管理客户数据请求。 您可以使用Privacy Service提交从Adobe Experience Cloud应用程序访问和删除个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

>[!IMPORTANT]
>
>Privacy Service仅适用于数据主体和消费者权利请求。 不支持或允许将Privacy Service用于数据清理或维护。 Adobe有及时履行这些义务的法律义务。 因此，不允许对Privacy Service进行负载测试，因为它是仅用于生产的环境，并会创建有效隐私请求的不必要积压。
>
>现已设定每日硬性上传限制，以防止滥用服务。 发现滥用系统的用户将禁用其对该服务的访问权限。 随后将与他们举行一次会议，讨论他们的行动并讨论可接受的Privacy Service用途。

## Privacy Service快速入门 {#getting-started}

要优化使用Privacy Service，必须根据贵组织的隐私要求、您从客户那里收集的身份数据类型以及将CRM系统与该服务连接的最佳方式做出几项关键决策。

可通过以下问题对这些决策进行总结：

1. **我正在从客户那里收集哪些信息？**
   * 要充分利用Privacy Service，您必须详细了解从客户那里收集的数据类型，以及哪些类型受隐私法规的约束。 有关详细信息，请参阅[确定隐私要求](#requirements)一节。
1. **我是否正确标记了数据？**
   * 必须为服务正确标记数据，以确定在隐私作业期间要访问或删除哪些字段。 有关详细信息，请参阅有关[为数据设置标签](#label)的部分。
1. **我知不知道要向Privacy Service发送哪些ID？**
   * 在发送隐私请求时，必须提供特定Adobe应用程序特有的单个客户ID。 有关详细信息，请参阅[提供身份数据](#identity)和[提出隐私请求](#requests)中的部分。
1. **我如何跟踪我的隐私作业？**
   * 发出隐私请求后，可通过多个选项跟踪其状态和结果。 有关详细信息，请参阅有关[监视隐私作业](#monitor)的部分。

以下各部分提供了有关这些重要先决条件步骤的一般指导，同时还提供了指向更多Privacy Service文档的链接，以便了解更多详细信息。

### 确定贵组织的隐私要求 {#requirements}

根据您的业务性质及运营所在的司法管辖区，您的数据运营可能会受到隐私法规的约束。这些法规通常赋予您的客户请求访问您从他们那里收集的数据的权利，并且这些客户有权请求删除所存储的数据。在整个文档中，这些客户对其个人数据的请求都称为“隐私请求”。

有关Privacy Service管理请求的各种法律隐私法规的详细信息（包括关键术语和常见问题解答），请参阅[隐私法规文档](./regulations/overview.md)。

如果您的数据操作属于任何受支持法规的管辖范围，请查看相关文档以了解重要信息，例如它们为客户提供的特定隐私权，以及用于履行隐私请求的合规窗口。 在决定如何将Privacy Service集成到您的CRM系统中，以及客户应如何与您的网站交互以便提出隐私请求时，应考虑这些信息。

除了法规之外，在做出这些决策时还应考虑适用于您组织的任何组织或行业标准。

### 为隐私请求标记数据 {#label}

根据您使用的[!DNL Experience Cloud]应用程序，必须标记在响应隐私请求时应该访问或删除的特定数据字段。 标记数据的过程因应用程序而异。 要了解如何为每个支持的Adobe应用程序标记数据，请参阅[Experience Cloud应用程序](./experience-cloud-apps.md)上的文档。

### 确定要发送到Privacy Service的标识数据的类型 {#identity}

为了使Privacy Service处理来自客户的隐私请求，必须在请求本身中为该客户提供至少一个唯一标识值。 唯一标识值是可用于在[!DNL Experience Cloud]数据存储中识别个人及其存储的个人数据的任何信息。 Privacy Service使用此身份信息，根据请求的性质（访问、删除或选择退出）查找和处理客户的个人数据。

根据您的CRM系统使用的[!DNL Experience Cloud]应用程序，您必须为每个客户提供的标识值的类型和数量会有所不同。 某些应用程序使用自己的内部客户ID值(如Adobe Target ID)，而其他解决方案依赖来自Adobe[!DNL Experience Cloud Identity Service] (ECID)的全局标识符来跟踪所有[!DNL Experience Cloud]应用程序中的客户活动。 此外，电子邮件地址或电话号码等通用个人信息也可以用作有效的身份数据。

阅读有关[隐私请求的身份数据](./identity-data.md)的文档，以了解有关接受Privacy Service的身份信息类型的详细信息。 本文档还提供了有关如何应用Adobe技术在客户与您的网站交互时有效地从客户检索适当的身份信息，并在API请求中将数据发送到Privacy Service的指南。

### 开始发出隐私请求 {#requests}

一旦您确定了企业的隐私需求，并确定了要将哪些身份值发送到Privacy Service，就可以开始发出隐私请求。 使用Privacy Service通过API或UI发送隐私请求。

#### 访问请求文件详细信息 {#access-requests}

在响应成功的访问请求时，有一个&#x200B;**下载URL**&#x200B;包含多个文件。 为请求数据的每个Adobe应用程序提供一个文件。 请注意，每个应用程序的文件格式可能因应用程序的数据结构而异。

#### 删除请求 — 无下载URL {#delete-requests}

**删除请求**&#x200B;的响应中&#x200B;**没有下载URL**，因为未检索到任何客户数据。

>[!IMPORTANT]
>
>以下部分提供了文档链接，这些文档涵盖如何在API或UI中发出通用隐私请求。 但是，根据您使用的[!DNL Experience Cloud]应用程序，您在请求有效负载中必须发送的字段可能与这些指南中显示的示例不同。
>
>与API或UI指南一起使用时，请参阅[Privacy Service和Experience Cloud应用程序](./experience-cloud-apps.md)上的文档，以获取有关如何为特定[!DNL Experience Cloud]应用程序设置隐私请求格式的更多文档。
>
>还需要注意的是，隐私请求是跨Experience Cloud应用程序异步处理的。 Privacy Service收到请求后，每个应用程序可能需要几分钟到几周的时间才能完成请求。 完成每个请求所需的时间取决于您所使用的应用程序，以及需要处理的数据量。

#### 使用 API {#api}

若要以编程方式实现[!DNL Experience Cloud]应用程序的隐私法规合规性，您可以使用对[[!DNL Privacy Service API]](https://developer.adobe.com/experience-platform-apis/references/privacy-service/)端点的RESTful API调用创建和管理隐私作业。 有关如何使用API的详细步骤，请参阅[Privacy ServiceAPI指南](api/overview.md)。

#### 使用UI {#ui}

>[!NOTE]
>
>Privacy ServiceUI当前仅支持访问和删除请求。 所有选择退出请求必须改通过API发出。

您可以使用带有Privacy ServiceUI的图形界面创建和监控隐私作业。 UI包含一个&#x200B;**[!UICONTROL 状态报表]**&#x200B;小组件，该小组件提供所有活动请求状态的可视表示形式，您可以使用内置&#x200B;**[!UICONTROL 请求生成器]**&#x200B;或通过上传JSON文件来创建请求。 有关使用UI的详细信息，请参阅[Privacy Service用户指南](ui/overview.md)。

### 监测隐私作业 {#monitor}

制定隐私作业后，您有多个选项可用于监控其状态和结果：

| 监测方法 | 描述 |
| --- | --- |
| PRIVACY SERVICEUI | 您可以使用Privacy ServiceUI监视仪表板查看所有活动请求状态的可视表示形式。 有关详细信息，请参阅[Privacy Service用户指南](ui/overview.md)。 |
| PRIVACY SERVICEAPI | 您可以使用Privacy ServiceAPI提供的查找端点以编程方式监控隐私作业的状态。 有关如何使用API的详细步骤，请参阅[Privacy ServiceAPI指南](./api/overview.md)。 |
| [!DNL Privacy Events] | [!DNL Privacy Events]使用发送到配置的webhook的Adobe I/O事件来促进高效的作业请求自动化。 它们可减少或消除轮询Privacy ServiceAPI以检查作业是否完成或工作流中是否已达到特定里程碑的需要。 有关详细信息，请参阅有关[订阅隐私事件](./privacy-events.md)的教程。 |

#### 针对非现有用户的响应 {#non-existing-users}

当您提交访问或删除请求时，即使找不到用户数据，如果调用成功完成，响应将始终返回`success`。 这意味着即使数据不存在，访问或删除也可以成功完成，而无需检索或删除任何数据。

## 后续步骤

本文档全面概述了Privacy Service以及开始使用该服务的功能所需的主要步骤。 有关使用Privacy Service的各个方面的更深入的信息，请参阅整个概述中链接的文档。

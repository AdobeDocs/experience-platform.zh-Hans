---
keywords: Experience Platform；主页；热门主题；GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_hat;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Privacy Service概述
topic-legacy: overview
description: Privacy Service使您能够促进在Experience Cloud数据操作中自动遵守法律隐私法规。
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 2%

---

# [!DNL Privacy Service] 概述

为了提供更好的客户体验，您需要收集和存储客户的个人数据。 使用此数据时，了解并尊重客户的隐私至关重要。 新的法律和组织规定正在用户提供相应的权利，允许他们请求访问或删除您的数据存储中的用户个人数据。

Adobe Experience Platform [!DNL Privacy Service]是为应对企业管理其客户个人数据方式的根本转变而开发的。 [!DNL Privacy Service]的核心目的是自动遵守数据隐私法规，如果违反这些法规，可能会导致大量罚款和中断您业务的数据操作。

[!DNL Privacy Service] 提供RESTful API和用户界面，帮助您管理客户数据请求。借助[!DNL Privacy Service]，您可以提交从Adobe Experience Cloud应用程序访问和删除个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

## [!DNL Privacy Service]入门 {#getting-started}

要使用[!DNL Privacy Service]，需要根据贵组织的隐私要求、您从客户那里收集的身份数据的类型以及将CRM系统与服务接口的最佳方式，做出一些关键决策。

这些决定可通过以下问题进行总结：

1. **我从客户那里收集了哪些信息？**
   * 要最好地利用[!DNL Privacy Service]，您必须对从客户那里收集的数据类型以及其中哪些数据受隐私法规的约束有详细的了解。 有关更多信息，请参阅[determining privacy requirements](#requirements)一节。
1. **我的数据是否已正确标记？**
   * 必须正确标记数据，以便服务确定在隐私作业期间要访问或删除的字段。 有关更多信息，请参阅[标签数据](#label)一节。
1. **我知道要发送哪些ID吗 [!DNL Privacy Service]?**
   * 在发送隐私请求时，必须提供特定于特定Adobe应用程序的单个客户ID。 有关更多信息，请参阅[提供身份数据](#identity)和[发出隐私请求](#requests)的章节。
1. **如何跟踪我的隐私工作？**
   * 发出隐私请求后，有多个选项可用于跟踪其状态和结果。 有关更多信息，请参阅[监控隐私作业](#monitor)一节。

以下各节提供了这些重要先决条件步骤的一般指导，并提供了指向进一步[!DNL Privacy Service]文档的链接，以了解更多详细信息。

### 确定贵组织的隐私要求 {#requirements}

根据您的业务性质及其运营的管辖区，您的数据操作可能受法律隐私法规的约束。 这些法规通常允许您的客户请求访问您从他们那里收集的数据，并有权请求删除所存储的数据。 在整个文档中，这些客户对其个人数据的请求都称为“隐私请求”。

有关[!DNL Privacy Service]管理请求的不同法律隐私法规的详细信息（包括关键术语和常见问题的解答），请参阅[隐私法规文档](./regulations/overview.md)。

如果您的数据操作属于任何受支持法规的权限范围，请查看其文档以了解重要信息，例如他们为客户提供的特定隐私权，以及遵守隐私请求的合规窗口。 在确定如何将[!DNL Privacy Service]集成到CRM系统中，以及客户如何与您的网站进行交互以发出隐私请求时，应考虑此信息。

除法律法规外，在做出这些决策时，还应考虑适用于贵组织的任何组织或行业标准。

### 为隐私请求设置标签数据 {#label}

根据您使用的[!DNL Experience Cloud]应用程序，必须为应响应隐私请求而应访问或删除的特定数据字段设置标签。 标记数据的过程因应用程序而异。 要了解如何为每个受支持的Adobe应用程序设置数据标签，请参阅[Experience Cloud应用程序](./experience-cloud-apps.md)上的文档。

### 确定要发送到[!DNL Privacy Service]的身份数据类型 {#identity}

为了[!DNL Privacy Service]处理客户的隐私请求，该请求本身必须提供该客户的至少一个唯一标识值。 唯一标识值是可用于识别个人及其存储在[!DNL Experience Cloud]数据存储中的个人数据的任何信息。 [!DNL Privacy Service] 使用此身份信息根据请求的性质（访问、删除或选择退出）查找和处理客户的个人数据。

根据您的CRM系统所使用的[!DNL Experience Cloud]应用程序，您必须为每个客户提供的身份值的类型和数量会有所不同。 某些应用程序会使用自己的内部客户ID值(如Adobe Target ID)，而其他解决方案则依赖于Adobe[!DNL Experience Cloud Identity Service](ECID)中的全局标识符，该标识符可跟踪所有[!DNL Experience Cloud]应用程序中的客户活动。 此外，一般的个人信息（如电子邮件地址或电话号码）也可用作有效的身份数据。

有关隐私请求[标识数据的文档](./identity-data.md)提供了有关[!DNL Privacy Service]可接受的标识信息类型的更多详细信息。 该文档还就如何利用Adobe技术在客户与您的网站交互时从他们那里有效地检索适当的身份信息，并在API请求中将该数据发送到[!DNL Privacy Service]提供了指导。

### 开始发出隐私请求 {#requests}

确定企业的隐私需求并确定要发送到[!DNL Privacy Service]的标识值后，您便可以开始发出隐私请求。 [!DNL Privacy Service] 允许您通过API或UI发送隐私请求。

>[!IMPORTANT]
>
>以下部分提供了相关文档的链接，这些文档介绍了如何在API或UI中发出通用隐私请求。 但是，根据您所使用的[!DNL Experience Cloud]应用程序，您在请求有效负载中必须发送的字段可能与这些指南中显示的示例不同。
>
>在遵循API或UI指南时，请参阅[Privacy Service和Experience Cloud应用程序](./experience-cloud-apps.md)上的文档，以获取有关如何为特定[!DNL Experience Cloud]应用程序的隐私请求设置格式的进一步文档。
>
>另外，请务必注意，隐私请求是跨Experience Cloud应用程序异步处理的。 Privacy Service收到请求后，每个应用程序可能需要数分钟到数周的时间才能完成请求。 完成每个请求所花费的时间取决于您正在处理的应用程序，以及需要处理的数据量。

#### 使用 API

[[!DNL Privacy Service API]](https://www.adobe.io/experience-platform-apis/references/privacy-service/)提供了使用RESTful API调用创建和管理隐私作业的多个端点，允许您以编程方式处理[!DNL Experience Cloud]应用程序的隐私法规合规性。 有关如何使用API的详细步骤，请参阅[Privacy ServiceAPI开发人员指南](api/getting-started.md)。

#### 使用UI

>[!NOTE]
>
>[!DNL Privacy Service] UI当前仅支持访问和删除请求。 所有选择退出请求都必须改为通过API发出。

[!DNL Privacy Service] UI允许您使用图形界面创建和监视隐私作业。 UI包含&#x200B;**[!UICONTROL 状态报表]**&#x200B;小组件，该小组件提供所有活动请求状态的直观表示形式，并允许您使用内置的&#x200B;**[!UICONTROL 请求生成器]**&#x200B;或上传JSON文件来创建新请求。 有关使用UI的更多信息，请参阅[Privacy Service用户指南](ui/overview.md)。

### 监控隐私作业 {#monitor}

完成隐私作业后，有多个选项可用于监控其状态和结果：

| 监控方法 | 描述 |
| --- | --- |
| [!DNL Privacy Service] UI | [!DNL Privacy Service] UI提供了监视功能板，让您能够查看所有活动请求状态的可视表示形式。 有关更多信息，请参阅[Privacy Service用户指南](ui/overview.md)。 |
| [!DNL Privacy Service] API | 您可以使用[!DNL Privacy Service] API提供的查找端点以编程方式监控隐私作业的状态。 有关如何使用API的详细步骤，请参阅[Privacy Service开发人员指南](./api/getting-started.md)。 |
| [!DNL Privacy Events] | [!DNL Privacy Events] 利用发送到已配置WebHook的Adobe I/O事件，以便于高效地自动执行作业请求。它们可减少或消除轮询[!DNL Privacy Service] API以检查作业是否完成或是否已达到工作流中的特定里程碑的需要。 有关更多信息，请参阅[订阅隐私事件](./privacy-events.md)的教程。 |

## 后续步骤

本文档提供了[!DNL Privacy Service]的高级概述以及开始使用服务功能所需的主要步骤。 有关使用[!DNL Privacy Service]的各个方面的更多深入信息，请参阅整个概述中链接的文档。

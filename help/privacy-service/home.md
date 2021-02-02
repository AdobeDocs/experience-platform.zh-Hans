---
keywords: Experience Platform；主页；热门主题；GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_t;PDPA_THA;lgpd;LGPD;lgpd;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Adobe Experience Platform Privacy Service概述
topic: overview
description: Privacy Service允许您促进Experience Cloud数据操作中自动遵守法律隐私法规。
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 0%

---


# Adobe Experience Platform[!DNL Privacy Service]概述

为了提供更好的客户体验，您需要收集和存储客户的个人数据。 使用这些数据时，了解和尊重客户的隐私非常重要。 新的法律和组织法规授予用户根据请求从数据存储中访问或删除其个人数据的权利。

Adobe Experience Platform[!DNL Privacy Service]是为应对企业管理其客户个人数据的方式发生根本性转变而开发的。 [!DNL Privacy Service]的主要目的是自动遵守数据隐私规定，如果违反这些规定，可能会对您的业务造成巨额罚款和中断数据操作。

[!DNL Privacy Service] 提供RESTful API和用户界面，帮助您管理客户数据请求。通过[!DNL Privacy Service]，您可以提交访问和删除Adobe Experience Cloud应用程序中的个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

## [!DNL Privacy Service] {#getting-started}入门

为了利用[!DNL Privacy Service]，您需要根据组织的隐私要求、您从客户那里收集的身份数据种类以及将CRM系统与服务连接的最佳方式，做出若干关键决策。

这些决定可以通过以下问题进行总结：

1. **我从我的客户那里收集哪些信息？**
   * 要最好地利用[!DNL Privacy Service]，您必须详细了解您从客户那里收集的数据类型，以及其中哪些数据受隐私法规的约束。 有关详细信息，请参阅[确定隐私要求](#requirements)一节。
1. **我是否正确标记了我的数据？**
   * 必须正确标记数据，以便服务确定在隐私作业期间要访问或删除哪些字段。 有关详细信息，请参见[标记数据](#label)一节。
1. **我知道要发送的ID吗 [!DNL Privacy Service]?**
   * 在发送隐私请求时，必须提供特定Adobe应用程序的特定客户ID。 有关详细信息，请参见关于[提供身份数据](#identity)和[提出隐私请求](#requests)的章节。
1. **如何跟踪我的隐私工作？**
   * 提出隐私请求后，有多种选项可用于跟踪其状态和结果。 有关详细信息，请参见[监视隐私作业](#monitor)一节。

以下各节提供这些重要入门步骤的一般指导，并提供进一步[!DNL Privacy Service]文档的链接以了解更多详细信息。

### 确定贵组织的隐私要求{#requirements}

根据您的业务性质及其运营所在的司法管辖区，您的数据操作可能受法律隐私法规的约束。 这些法规通常允许您的客户请求访问您从他们收集的数据，并请求删除该存储的数据。 在整个文档中，这些客户对其个人数据的请求称为“隐私请求”。

有关[!DNL Privacy Service]管理请求的不同法律隐私法规的详细信息（包括关键术语和常见问题的答案），请参阅[隐私法规文档](./regulations/overview.md)。

如果您的数据操作属于任何受支持法规的权限范围，请查看其文档以了解重要信息，如客户承担的特定隐私权以及遵守隐私要求的合规窗口。 在确定如何将[!DNL Privacy Service]集成到您的CRM系统中以及客户如何与您的网站交互以发出隐私请求时，应考虑此信息。

除法律法规外，在作出这些决定时，还应考虑适用于贵组织的任何组织或行业标准。

### 隐私请求的标签数据{#label}

根据您使用的[!DNL Experience Cloud]应用程序，您必须标记应根据隐私请求访问或删除的特定数据字段。 标记数据的过程因应用程序而异。 要了解如何为每个受支持的Adobe应用程序标记文档，请参见[Experience Cloud应用程序](./experience-cloud-apps.md)上的标签。

### 确定要发送到[!DNL Privacy Service] {#identity}的身份数据类型

要使[!DNL Privacy Service]处理客户的隐私请求，必须在请求本身中提供该客户的至少一个唯一标识值。 唯一标识值是可用于识别个人及其存储在[!DNL Experience Cloud]数据存储中的个人数据的任何信息。 [!DNL Privacy Service] 根据请求的性质（访问、删除或选择退出），使用此身份信息查找和处理客户的个人数据。

根据您的CRM系统所使用的[!DNL Experience Cloud]应用程序，您必须为每位客户提供的标识值的类型和数量将有所不同。 一些应用程序使用其自己的内部客户ID值(如Adobe TargetID)，而其他解决方案依赖于Adobe[!DNL Experience Cloud Identity Service](ECID)的全局标识符，该标识符跟踪所有[!DNL Experience Cloud]应用程序中的客户活动。 此外，电子邮件地址或电话号码等通用个人信息也可以作为有效身份数据。

隐私请求[标识文档](./identity-data.md)提供了有关[!DNL Privacy Service]接受的标识信息类型的更详细信息。 该文档还提供有关如何利用Adobe技术在客户与您的网站交互时从他们有效检索适当的身份信息以及在API请求中将该数据发送到[!DNL Privacy Service]的指导。

### 开始发出隐私请求{#requests}

一旦您确定了企业的隐私需求并决定了要发送到[!DNL Privacy Service]的标识值，您就可以开始发出隐私请求。 [!DNL Privacy Service] 允许您通过API或UI发送隐私请求。

>[!IMPORTANT]
>
>以下各节提供文档链接，其中涵盖如何在API或UI中发出通用隐私请求。 但是，根据您使用的[!DNL Experience Cloud]应用程序，您必须在请求有效负荷中发送的字段可能与这些指南中显示的示例不同。
>
>如果您按照API或UI指南进行操作，请参阅[Privacy Service和Experience Cloud应用程序](./experience-cloud-apps.md)上的文档，进一步了解如何为特定[!DNL Experience Cloud]应用程序设置隐私请求格式。
>
>请注意，隐私请求是跨Experience Cloud应用程序异步处理的。 Privacy Service收到请求后，每个应用程序可能需要花费几分钟到几周的时间来完成请求。 完成每个请求所花费的时间取决于您所使用的应用程序以及需要处理的数据量。

#### 使用API

[[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml)为使用RESTful API调用创建和管理隐私作业提供了多个端点，允许您以编程方式对[!DNL Experience Cloud]应用程序遵守隐私规定。 有关如何使用API的详细步骤，请参阅[Privacy ServiceAPI开发人员指南](api/getting-started.md)。

#### 使用UI

>[!NOTE]
>
>[!DNL Privacy Service] UI当前仅支持访问和删除请求。 必须改为通过API发出所有退出请求。

[!DNL Privacy Service] UI允许您使用图形界面创建和监视隐私作业。 该UI包含一个&#x200B;**[!UICONTROL 状态报告]**&#x200B;构件，它提供所有活动请求状态的可视表示，并允许您通过使用内置的&#x200B;**[!UICONTROL 请求生成器]**&#x200B;或上传JSON文件来创建新请求。 有关使用UI的详细信息，请参阅[Privacy Service用户指南](ui/overview.md)。

### 监视隐私作业{#monitor}

完成隐私工作后，您可以使用多个选项来监视其状态和结果：

| 监控方法 | 描述 |
| --- | --- |
| [!DNL Privacy Service] UI | [!DNL Privacy Service] UI提供监视仪表板，允许您视图所有活动请求状态的可视表示。 有关详细信息，请参阅[Privacy Service用户指南](ui/overview.md)。 |
| [!DNL Privacy Service] API | 您可以使用[!DNL Privacy Service] API提供的查找端点以编程方式监视隐私作业的状态。 有关如何使用API的详细步骤，请参阅[Privacy Service开发人员指南](./api/getting-started.md)。 |
| [!DNL Privacy Events] | [!DNL Privacy Events] 利用发送到已配置网页挂接的Adobe I/O事件，以便促进高效的工作请求自动化。它们减少或消除了轮询[!DNL Privacy Service] API的需求，以检查作业是否完成或是否已到达工作流中的特定里程碑。 有关详细信息，请参阅有关[订阅隐私事件](./privacy-events.md)的教程。 |

## 后续步骤

此文档提供了[!DNL Privacy Service]的高级概述以及使用服务功能进行开始所需的主要步骤。 有关使用[!DNL Privacy Service]的各个方面的详细信息，请参阅整个概述中链接的文档。

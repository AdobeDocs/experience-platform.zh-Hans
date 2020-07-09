---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: d358b200d574ca8de77ee2274836c03f7cc84c40
workflow-type: tm+mt
source-wordcount: '1587'
ht-degree: 5%

---


# Adobe Experience Platform Privacy Service概述

为了提供更好的客户体验，您需要收集和存储客户的个人数据。 使用这些数据时，了解和尊重客户的隐私非常重要。 新的法律和组织法规授予用户根据请求从数据存储中访问或删除其个人数据的权利。

Adobe Experience Platform Privacy Service是为应对企业管理其客户个人数据的方式的根本性转变而开发的。 Privacy Service的核心目的是自动遵守数据隐私规定，如果违反这些规定，可能会对您的业务造成重大罚款和中断数据操作。

Privacy Service提供RESTful API和用户界面，帮助您管理客户数据请求。 通过Privacy Service，您可以提交从Adobe Experience Cloud应用程序访问和删除个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

## Privacy Service入门 {#getting-started}

为了利用Privacy Service，您需要根据组织的隐私要求、您从客户那里收集的身份数据种类以及将CRM系统与服务连接的最佳方式，做出若干关键决策。

这些决定可以通过以下问题进行总结：

1. **我从我的客户那里收集哪些信息？**
   * 为了最好地利用Privacy Service，您必须对您从客户那里收集的数据类型以及其中哪些数据受隐私法规的约束有详细的了解。 有关详细信息，请参 [阅确定隐私要求](#requirements) 一节。
1. **我是否正确标记了我的数据？**
   * 必须正确标记数据，以便服务确定在隐私作业期间要访问或删除哪些字段。 有关详细信息，请 [参阅](#label) “标记数据”一节。
1. **我知道要发送给Privacy Service的ID吗？**
   * 发送隐私请求时，必须提供特定Adobe应用程序的个别客户ID。 有关详细信息，请 [参阅有关提供身](#identity)[份数据和提](#requests) 出隐私请求的章节。
1. **如何跟踪我的隐私工作？**
   * 提出隐私请求后，有多种选项可用于跟踪其状态和结果。 有关详细信息，请 [参阅“监视隐私](#monitor) ”作业一节。

以下各节提供这些重要先决条件步骤的一般指导，并提供指向进一步Privacy Service文档的链接以了解更多详细信息。

### 确定贵组织的隐私要求 {#requirements}

根据您的业务性质及其运营所在的司法管辖区，您的数据操作可能受法律隐私法规的约束。 这些法规通常允许您的客户请求访问您从他们收集的数据，并请求删除该存储的数据。 在整个文档中，这些客户对其个人数据的请求称为“隐私请求”。

下表概述了Privacy Service管理请求的法律隐私法规，包括文档链接以了解更多信息：

| 法规 | 描述 |
| --- | --- |
| CCPA（加利福利亚） | 《加州消费者隐私法案》(CCPA) 加强了对美国加利福尼亚州居民的隐私权和消费者保护。CCPA为加州居民提供了新的数据隐私权，包括访问和删除其个人数据、了解其个人数据是否被出售或披露（以及向谁）的权利，以及将其数选择退出据出售给第三方的权利。<br/><br/>更多文档的链接： <ul><li>[法律概述](https://oag.ca.gov/privacy/ccpa)</li><li>[CCPA常见问题解答](ccpa/faq.md)</li></ul> |
| GDPR(欧洲合并) | 《通用数据保护条例》(GDPR) 为欧盟成员国引入了几项新的数据隐私权，其中包括&#x200B;**访问权**&#x200B;和&#x200B;**被遗忘权**。这意味着被企业收集了个人数据的任何欧盟公民都可以随时请求访问或删除其数据。<br/><br/>更多文档的链接： <ul><li>[法律概述](https://gdpr-info.eu/)</li><li>[GDPR 常见问题解答](gdpr/faq.md)</li><li>[GDPR 术语](gdpr/terminology.md)</li></ul> |
| PDPA_THA（泰国） | 泰国《个人数据保护法》(PDPA)的出台旨在保护泰国数据所有者免遭非法收集、使用或披露其个人数据。 受欧洲合并GDPR的启发，该规定授予泰国公民访问或删除其存储的个人数据的权利。<br/><br/>更多文档的链接： <ul><li>[法律概述](https://www.dataprotectionreport.com/2020/02/thailand-personal-data-protection-law/)</li><li>[PDPA_THA常见问题解答](pdpa-tha/faq.md)</li><li>[PDPA_THA术语](pdpa-tha/terminology.md)</li></ul> |

如果您的数据操作属于上述任何法规的权限，请查看其文档以了解重要信息，如客户承担的特定隐私权以及遵守隐私要求的合规窗口。 在确定如何将Privacy Service集成到您的CRM系统中以及客户如何与您的网站交互以发出隐私请求时，应考虑这些信息。

除法律法规外，在作出这些决定时，还应考虑适用于贵组织的任何组织或行业标准。

### 为隐私请求标签数据 {#label}

根据您使用的Experience Cloud应用程序，您必须标记应根据隐私请求访问或删除的特定数据字段。 标记数据的过程因应用程序而异。 要了解如何为每个受支持的Adobe应用程序标记数据，请参阅文档 [Experience Cloud应用程序](./experience-cloud-apps.md)。

### 确定要发送到Privacy Service的身份数据类型 {#identity}

为了Privacy Service处理客户的隐私请求，该客户的至少一个唯一标识值必须在请求本身中提供。 唯一标识值是可用于识别个人及其存储在Experience Cloud数据存储中的个人数据的任何信息。 Privacy Service根据请求的性质（访问、删除或选择退出）使用此身份信息来查找和处理客户的个人数据。

根据您的CRM系统所使用的Experience Cloud应用程序，您必须为每位客户提供的标识值类型和数量将有所不同。 一些应用程序会利用自己的内部客户ID值(如Adobe TargetID)，而其他解决方案则依赖Adobe Experience Cloud Identity Service(ECID)的全局标识符，该标识符跟踪所有Experience Cloud应用程序中的客户活动。 此外，电子邮件地址或电话号码等通用个人信息也可以作为有效身份数据。

隐私请 [求的身份文档](./identity-data.md) ，提供了有关接受的身份信息类型的更多详细信息。 该文档还提供有关如何利用Adobe技术在客户与您的网站交互时从他们有效检索适当的身份信息以及在API请求中将该数据发送给Privacy Service的指导。

### 开始提出隐私请求 {#requests}

一旦您确定了企业的隐私需求，并决定了要发送给Privacy Service的身份值，您就可以开始提出隐私请求。 Privacy Service允许您通过API或UI发送隐私请求。

>[!IMPORTANT]
>
>以下各节提供文档链接，其中涵盖如何在API或UI中发出通用隐私请求。 但是，根据您使用的Experience Cloud应用程序，您必须在请求有效负荷中发送的字段可能与这些指南中显示的示例不同。
>
>在您阅读API或UI指南时，请参阅文档和 [Experience Cloud应用程序Privacy Service](./experience-cloud-apps.md) ，进一步了解如何格式化特定Experience Cloud应用程序的隐私请求。

#### 使用API

Privacy Service [API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) 为使用RESTful API调用创建和管理隐私作业提供了多个端点，允许您以编程方式为Experience Cloud应用程序遵循隐私法规。 有关如何使用API的详细步骤，请参阅 [Privacy ServiceAPI开发人员指南](api/getting-started.md)。

#### 使用UI

>[!NOTE]
>
>Privacy ServiceUI当前仅支持访问和删除请求。 必须改为通过API发出所有退出请求。

Privacy ServiceUI允许您使用图形界面创建和监视隐私作业。 UI包括状态 **报告构件** ，它提供所有活动请求状态的可视表示形式，并允许您通过使用内置的Request Builder或通过上传JSON文件创建 **新请求** 。 有关使用UI的详细信息，请参阅 [Privacy Service用户指南](ui/overview.md)。

### 监视隐私作业 {#monitor}

完成隐私工作后，您可以使用多个选项来监视其状态和结果：

| 监控方法 | 描述 |
| --- | --- |
| Privacy ServiceUI | Privacy ServiceUI提供了监视仪表板，允许您视图所有活动请求状态的可视表示形式。 有关详细 [信息，请参](ui/overview.md) 阅Privacy Service用户指南。 |
| Privacy ServiceAPI | 您可以使用Privacy ServiceAPI提供的查找端点以编程方式监视隐私作业的状态。 有关如何 [使用API的详细步骤](./api/getting-started.md) ，请参阅Privacy Service开发人员指南。 |
| 隐私事件 | 隐私事件利用发送到已配置网络挂接的Adobe I/O事件，以促进高效的作业请求自动化。 它们减少或消除了对Privacy ServiceAPI进行轮询以检查作业是否完成或是否到达工作流中的某个里程碑。 有关详细信息，请 [参阅订阅隐私事件](./privacy-events.md) 的教程。 |

## 后续步骤

本文档概括介绍了Privacy Service以及使用服务功能进行开始所需的主要步骤。 有关使用Privacy Service的各个方面的详细信息，请参阅整个概述中链接的文档。

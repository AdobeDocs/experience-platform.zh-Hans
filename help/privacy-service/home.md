---
keywords: Experience Platform；主页；热门主题；GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_bra;LGPD_BRA;
solution: Experience Platform
title: Privacy Service概述
topic-legacy: overview
description: Privacy Service允许您促进Experience Cloud数据操作中自动遵守法律隐私法规。
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 0%

---

# [!DNL Privacy Service] 概述

为了提供更好的客户体验，您需要收集和存储客户的个人数据。 使用这些数据时，了解和尊重客户的隐私非常重要。 新的法律和组织法规授予用户在请求时从您的数据存储中访问或删除其个人数据的权利。

Adobe Experience Platform [!DNL Privacy Service]是为应对企业管理其客户个人数据的方式发生根本性转变而开发的。 [!DNL Privacy Service]的核心目的是自动遵守数据隐私规定，如果违反这些规定，可能会对您的业务造成巨额罚款和中断数据操作。

[!DNL Privacy Service] 提供RESTful API和用户界面，帮助您管理客户数据请求。通过[!DNL Privacy Service]，您可以提交从Adobe Experience Cloud应用程序访问和删除个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

## [!DNL Privacy Service] {#getting-started}入门

为了使用[!DNL Privacy Service]，需要根据组织的隐私要求、您从客户那里收集的身份数据的种类以及将CRM系统与服务连接到一起的最佳方式，作出若干关键决策。

这些决定可通过以下问题概括：

1. **我从我的客户那里收集了哪些信息？**
   * 要最好地使用[!DNL Privacy Service]，您必须对您从客户那里收集的数据类型有详细的了解，其中哪些数据受隐私法规的约束。 有关详细信息，请参阅[确定隐私要求](#requirements)一节。
1. **我是否正确标记了我的数据？**
   * 必须正确标记数据，以便服务确定在隐私作业期间要访问或删除哪些字段。 有关详细信息，请参阅[标记数据](#label)一节。
1. **我知道要发送到哪个ID吗 [!DNL Privacy Service]?**
   * 发送隐私请求时，必须提供特定于特定Adobe应用程序的个别客户ID。 有关详细信息，请参见关于[提供标识数据](#identity)和[发出隐私请求](#requests)的章节。
1. **如何跟踪我的隐私工作？**
   * 提出隐私请求后，可通过多种方式跟踪其状态和结果。 有关详细信息，请参阅[监视隐私作业](#monitor)一节。

以下各节提供这些重要先决条件步骤的一般指导，并提供进一步[!DNL Privacy Service]文档的链接以了解更多详细信息。

### 确定您组织的隐私要求{#requirements}

根据您的业务性质及其运营所在的司法辖区，您的数据操作可能受法律隐私法规的约束。 这些法规通常会赋予您的客户请求访问您从他们那里收集的数据的权利，并授予请求删除存储数据的权利。 在整个文档中，这些客户对其个人数据的请求称为“隐私请求”。

有关[!DNL Privacy Service]管理请求的不同法律隐私法规的详细信息（包括关键术语和常见问题的答案），请参阅[隐私法规文档](./regulations/overview.md)。

如果您的数据操作属于任何受支持法规的权限，请查看其文档以了解重要信息，如客户承担的特定隐私权，以及遵守隐私要求的合规窗口。 在确定如何将[!DNL Privacy Service]集成到您的CRM系统中以及客户如何与您的网站交互以发出隐私请求时，应考虑此信息。

除法律法规外，在作出这些决定时，还应考虑适用于贵组织的任何组织或行业标准。

### 为隐私请求{#label}标签数据

根据您使用的[!DNL Experience Cloud]应用程序，您必须标记应根据隐私请求访问或删除的特定数据字段。 标记数据的过程因应用程序而异。 要了解如何为每个受支持的Adobe应用程序标记文档，请参阅[Experience Cloud应用程序](./experience-cloud-apps.md)上的标记。

### 确定要发送到[!DNL Privacy Service] {#identity}的身份数据类型

要使[!DNL Privacy Service]处理客户的隐私请求，该客户的至少一个唯一标识值必须在请求本身中提供。 唯一标识值是任何信息，可用于标识个人及其在[!DNL Experience Cloud]数据存储中存储的个人数据。 [!DNL Privacy Service] 根据请求的性质（访问、删除或选择退出），使用此身份信息查找和处理客户的个人数据。

根据您的CRM系统所使用的[!DNL Experience Cloud]应用程序，您必须为每位客户提供的身份值的类型和数量将有所不同。 一些应用程序使用其自己的内部客户ID值(如Adobe Target ID)，而其他解决方案依赖来自Adobe[!DNL Experience Cloud Identity Service](ECID)的全局标识符来跟踪所有[!DNL Experience Cloud]应用程序中的客户活动。 此外，诸如电子邮件地址或电话号码之类的通用个人信息也可以作为有效的身份数据。

有关隐私请求[标识数据](./identity-data.md)的文档提供了有关[!DNL Privacy Service]接受的标识信息类型的更详细信息。 该文档还就如何利用Adobe技术在客户与您的网站交互时从他们有效检索适当的身份信息以及在API请求中将该数据发送到[!DNL Privacy Service]提供指导。

### 开始发出隐私请求{#requests}

确定业务的隐私需求并决定要发送到[!DNL Privacy Service]的标识值后，您可以开始发出隐私请求。 [!DNL Privacy Service] 允许您通过API或UI发送隐私请求。

>[!IMPORTANT]
>
>以下部分提供了文档链接，这些文档涵盖如何在API或UI中发出通用隐私请求。 但是，根据您使用的[!DNL Experience Cloud]应用程序，必须在请求负载中发送的字段可能与这些指南中显示的示例不同。
>
>随着API或UI指南的推出，请参阅[Privacy Service和Experience Cloud应用程序](./experience-cloud-apps.md)上的文档，进一步了解如何设置特定[!DNL Experience Cloud]应用程序的隐私请求的格式。
>
>还必须注意的是，隐私请求是跨Experience Cloud应用程序异步处理的。 Privacy Service收到请求后，每个应用程序可能需要几分钟到几周的时间才能完成请求。 完成每个请求所需的时间取决于您所使用的应用程序以及需要处理的数据量。

#### 使用API

[[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml)为使用RESTful API调用创建和管理隐私作业提供了多个端点，允许您以编程方式处理[!DNL Experience Cloud]应用程序的隐私规定合规性。 有关如何使用API的详细步骤，请参阅[Privacy Service API开发人员指南](api/getting-started.md)。

#### 使用UI

>[!NOTE]
>
>[!DNL Privacy Service] UI当前仅支持访问和删除请求。 所有退出请求都必须通过API提出。

[!DNL Privacy Service] UI允许您使用图形界面创建和监视隐私作业。 该UI包含一个&#x200B;**[!UICONTROL Status Report]**&#x200B;构件，它提供所有活动请求状态的可视表示形式，并允许您通过使用内置的&#x200B;**[!UICONTROL Request Builder]**&#x200B;或通过上传JSON文件创建新请求。 有关使用UI的详细信息，请参阅[Privacy Service用户指南](ui/overview.md)。

### 监视隐私作业{#monitor}

完成隐私工作后，您可以使用多个选项来监视其状态和结果：

| 监控方法 | 描述 |
| --- | --- |
| [!DNL Privacy Service] UI | [!DNL Privacy Service] UI提供了监视仪表板，允许您视图所有活动请求状态的可视表示形式。 有关详细信息，请参阅[Privacy Service用户指南](ui/overview.md)。 |
| [!DNL Privacy Service] API | 您可以使用[!DNL Privacy Service] API提供的查找端点以编程方式监视隐私作业的状态。 有关如何使用API的详细步骤，请参阅[Privacy Service开发人员指南](./api/getting-started.md)。 |
| [!DNL Privacy Events] | [!DNL Privacy Events] 利用发送到已配置webhook的Adobe I/O事件，以便于高效地执行作业请求自动化。它们减少或消除了轮询[!DNL Privacy Service] API的需求，以检查作业是否完成或是否到达工作流中的特定里程碑。 有关详细信息，请参阅教程[订阅隐私事件](./privacy-events.md)。 |

## 后续步骤

本文档提供了[!DNL Privacy Service]的高级概述以及使用服务功能进行开始所需的主要步骤。 有关使用[!DNL Privacy Service]的各个方面的详细信息，请参阅整个概述中链接的文档。

---
keywords: Experience Platform；主页；热门主题；GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_hat;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Privacy Service概述
description: Privacy Service使您能够促进在Experience Cloud数据操作中自动遵守法律隐私法规。
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 21347074ed6160511888d4b543133dfd1ec4d35c
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 5%

---

# [!DNL Privacy Service] 概述

为了提供更好的客户体验，您需要收集和存储客户的个人数据。 使用此数据时，了解并尊重客户的隐私至关重要。 新的法律和组织规定正在用户提供相应的权利，允许他们请求访问或删除您的数据存储中的用户个人数据。

Adobe Experience Platform [!DNL Privacy Service] 是为应对企业管理其客户个人数据的方式发生根本转变而开发的。 的核心目的 [!DNL Privacy Service] 是自动遵守数据隐私法规，如果违反这些法规，可能会导致贵机构的巨额罚款和中断数据运营。

[!DNL Privacy Service] 提供RESTful API和用户界面，帮助您管理客户数据请求。 使用 [!DNL Privacy Service]，您可以提交从Adobe Experience Cloud应用程序访问和删除个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

>[!IMPORTANT]
>
>Privacy Service仅适用于数据主体和消费者权限请求。 不支持或允许将Privacy Service用于数据清理或维护的任何其他用途。 Adobe有法律义务及时履行这些义务。 因此，不允许对Privacy Service进行负载测试，因为它是仅生产环境，并且会造成有效隐私请求的不必要积压。
>
>现已设置硬性的每日上载限制，以帮助防止滥用服务。 发现滥用系统的用户将禁用其对服务的访问权限。 随后将与他们举行会议，讨论他们的行动并讨论可接受的Privacy Service用途。

## 入门 [!DNL Privacy Service] {#getting-started}

为了利用 [!DNL Privacy Service]，需要根据贵组织的隐私要求、您从客户那里收集的身份数据类型以及将CRM系统与服务接口的最佳方式，做出一些关键决策。

这些决定可通过以下问题进行总结：

1. **我从客户那里收集了哪些信息？**
   * 要充分利用 [!DNL Privacy Service]，则您必须对从客户那里收集的数据类型以及其中哪些数据受隐私法规的约束具有详细了解。 请参阅 [确定隐私要求](#requirements) 以了解更多信息。
1. **我的数据是否已正确标记？**
   * 必须正确标记数据，以便服务确定在隐私作业期间要访问或删除的字段。 请参阅 [标签数据](#label) 以了解更多信息。
1. **我知道要发送哪些ID吗 [!DNL Privacy Service]?**
   * 在发送隐私请求时，必须提供特定于特定Adobe应用程序的单个客户ID。 请参阅 [提供身份数据](#identity)  和 [发出隐私请求](#requests) 以了解更多信息。
1. **如何跟踪我的隐私工作？**
   * 发出隐私请求后，有多个选项可用于跟踪其状态和结果。 请参阅 [监控隐私作业](#monitor) 以了解更多信息。

以下各节提供了这些重要先决条件步骤的一般指导，并提供了进一步指南 [!DNL Privacy Service] 文档以了解更多详细信息。

### 确定贵组织的隐私要求 {#requirements}

根据您的业务性质及运营所在的司法管辖区，您的数据运营可能会受到隐私法规的约束。这些法规通常赋予您的客户请求访问您从他们那里收集的数据的权利，并且这些客户有权请求删除所存储的数据。在整个文档中，这些客户对其个人数据的请求都称为“隐私请求”。

有关以下各项的不同法律隐私法规的详细信息 [!DNL Privacy Service] 管理的请求，包括关键术语和常见问题解答，请参阅 [隐私法规文档](./regulations/overview.md).

如果您的数据操作属于任何受支持法规的权限范围，请查看其文档以了解重要信息，例如他们为客户提供的特定隐私权，以及遵守隐私请求的合规窗口。 在确定如何集成时，应考虑此信息 [!DNL Privacy Service] ，以及客户如何与您的网站进行交互以发出隐私请求。

除法律法规外，在做出这些决策时，还应考虑适用于贵组织的任何组织或行业标准。

### 为隐私请求设置标签数据 {#label}

根据 [!DNL Experience Cloud] 您所使用的应用程序中，您必须为应响应隐私请求而应访问或删除的特定数据字段设置标签。 标记数据的过程因应用程序而异。 要了解如何为每个受支持的Adobe应用程序设置数据标签，请参阅 [Experience Cloud应用程序](./experience-cloud-apps.md).

### 确定要发送到的身份数据类型 [!DNL Privacy Service] {#identity}

为 [!DNL Privacy Service] 要处理客户的隐私请求，该请求本身必须提供该客户的至少一个唯一标识值。 唯一标识值是可用于识别个人及其存储在您 [!DNL Experience Cloud] 数据存储。 [!DNL Privacy Service] 使用此身份信息根据请求的性质（访问、删除或选择退出）查找和处理客户的个人数据。

根据 [!DNL Experience Cloud] 您的CRM系统所使用的应用程序，您必须为每个客户提供的身份值的类型和数量将有所不同。 某些应用程序会使用其自己的内部客户ID值(如Adobe Target ID)，而其他解决方案则依赖来自Adobe的全局标识符 [!DNL Experience Cloud Identity Service] (ECID)，可跨所有渠道跟踪客户活动 [!DNL Experience Cloud] 应用程序。 此外，一般的个人信息（如电子邮件地址或电话号码）也可用作有效的身份数据。

上的文档 [隐私请求的身份数据](./identity-data.md) 提供了有关为 [!DNL Privacy Service]. 该文档还就如何利用Adobe技术在客户与您的网站交互时从他们那里有效地检索适当的身份信息，并将该数据发送到 [!DNL Privacy Service] 在API请求中。

### 开始发出隐私请求 {#requests}

确定业务的隐私需求并确定要发送到的标识值后 [!DNL Privacy Service]，则可以开始发出隐私请求。 [!DNL Privacy Service] 允许您通过API或UI发送隐私请求。

>[!IMPORTANT]
>
>以下部分提供了相关文档的链接，这些文档介绍了如何在API或UI中发出通用隐私请求。 但是，根据 [!DNL Experience Cloud] 您使用的应用程序中，您在请求有效负载中必须发送的字段可能与这些指南中显示的示例不同。
>
>在遵循API或UI指南时，请参阅 [Privacy Service和Experience Cloud应用程序](./experience-cloud-apps.md) 有关如何为特定用户的隐私请求设置格式的进一步文档 [!DNL Experience Cloud] 应用程序。
>
>另外，请务必注意，隐私请求是跨Experience Cloud应用程序异步处理的。 Privacy Service收到请求后，每个应用程序可能需要数分钟到数周的时间才能完成请求。 完成每个请求所花费的时间取决于您正在处理的应用程序，以及需要处理的数据量。

#### 使用 API

的 [[!DNL Privacy Service API]](https://www.adobe.io/experience-platform-apis/references/privacy-service/) 为使用RESTful API调用创建和管理隐私作业提供了多个端点，允许您以编程方式为您的隐私法规合规性 [!DNL Experience Cloud] 应用程序。 有关如何使用API的详细步骤，请参阅 [Privacy ServiceAPI指南](api/overview.md).

#### 使用UI

>[!NOTE]
>
>的 [!DNL Privacy Service] UI当前仅支持访问和删除请求。 所有选择退出请求都必须改为通过API发出。

的 [!DNL Privacy Service] UI允许您使用图形界面创建和监视隐私作业。 UI包括 **[!UICONTROL 状态报表]** 小组件可直观地表示所有活动请求的状态，并允许您使用内置的创建新请求 **[!UICONTROL 请求生成器]** 或通过上传JSON文件。 有关使用UI的更多信息，请参阅 [Privacy Service用户指南](ui/overview.md).

### 监控隐私作业 {#monitor}

完成隐私作业后，有多个选项可用于监控其状态和结果：

| 监控方法 | 描述 |
| --- | --- |
| [!DNL Privacy Service] UI | 的 [!DNL Privacy Service] UI提供了监控功能板，让您能够查看所有活动请求状态的可视表示形式。 请参阅 [Privacy Service用户指南](ui/overview.md) 以了解更多信息。 |
| [!DNL Privacy Service] API | 您可以使用提供的查找端点以编程方式监控隐私作业的状态 [!DNL Privacy Service] API。 请参阅 [Privacy ServiceAPI指南](./api/overview.md) 以了解有关如何使用API的详细步骤。 |
| [!DNL Privacy Events] | [!DNL Privacy Events] 利用发送到已配置WebHook的Adobe I/O事件，以便于高效地自动执行作业请求。 它们可减少或消除轮询 [!DNL Privacy Service] API，以检查作业是否完成或是否已到达工作流中的特定里程碑。 请参阅 [订阅隐私事件](./privacy-events.md) 以了解更多信息。 |

## 后续步骤

本文档提供了 [!DNL Privacy Service] 以及开始使用服务功能所需的主要步骤。 有关使用的各个方面的更多详细信息，请参阅整个概述中链接的文档 [!DNL Privacy Service].

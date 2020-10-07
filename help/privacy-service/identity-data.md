---
keywords: Experience Platform;home;popular topics;ECID;ecid
solution: Experience Platform
title: 隐私请求的身份数据
topic: overview
description: 本文档提供有关如何配置数据操作和利用Adobe技术有效检索客户隐私请求的适当身份信息的一般指导。
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 3%

---


# 隐私请求的身份数据

为了Adobe Experience Platform [!DNL Privacy Service] 处理客户对其私有数据（包括访问、删除或选择退出销售请求）的请求，必须向其提供唯一标识符，将特定客户链接到您启用Adobe Experience Cloud的应用程序中存储的私有数据。 [!DNL Privacy Service] 然后使用这些标识符收集存储在客户身份下的所有数据 [!DNL Experience Cloud]，并根据客户的请求进行处理。

本文档提供有关如何配置数据操作和利用Adobe技术有效检索客户隐私请求的适当身份信息的一般指导。

## 身份与命名空间

当客户可以通过多个不同的渠道与您的品牌进行交互时，协调从这些许多交互中记录的不同标识符可能会非常困难。 这反过来又会使很难确定哪些数据属于应用程序中的特定人 [!DNL Experience Cloud] 员。

例如，在中处理Adobe请求时，标 [!DNL Privacy Service]识可以表示在控制域下设置的Cookie值、在第三方域下并与Adobe共享的Cookie值，或您在IMS组织内显式定义的自定义标识符。

因此，每个发送身份的命名空间 [!DNL Privacy Service] 都必须附上一个提供上下文的来源，将身份价值与其系统相关联。 命名空间可以表示一个通用概念，如电子邮件地址（“电子邮件”），或将标识与特定应用程序(如Adobe Advertising CloudID(“AdCloud”)或Adobe TargetID(“TNTID”))关联。

Adobe Experience Platform标识服务维护全球定义和用户定义标识命名空间的存储。 有关命名空间的更多详细信息，请参 [阅身份命名空间概述](../identity-service/namespaces.md)。 有关常用的标准命名空间和命名空间限定符的列表，请 [!DNL Privacy Service]参阅开发 [人员指南的](api/appendix.md) 附录部分。

## ECID和选择加入服务

Adobe Experience Cloud [!DNL Identity Service] 作为一个通用的标识框架， [!DNL Experience Cloud]并为每个站点访客分配一个唯一的永久ID。 该 [!DNL Experience Cloud] ID(ECID)通过使用第一方Cookie来跟踪客户的活动，可以跨多个应用程序唯一标识设备，并允许您在不同的应用程序中标识同一站点访客及其 [!DNL Experience Cloud] 数据。 See the [Experience Cloud Identity Service overview](https://docs.adobe.com/content/help/zh-Hans/id-service/using/intro/overview.html) for more information.

选择加入服务是一种扩展，它 [!DNL Experience Cloud Identity Service]允许您在应用程序上设置协议，让访客确定您是否可以在访客的设备或浏览器上设置Cookie。 有关选择加入服务的更多详细信息（包括如何为您的应用程序设置服务），请参 [阅选择加入服务文档](https://docs.adobe.com/content/help/zh-Hans/id-service/using/implementation/opt-in-service/optin-overview.html)。

一旦您的站点访客被分配了ECID，您就可以利用该Adobe [!DNL Privacy JavaScript Library] 来检索这些ID以用于隐私请求，如下一节所述。

## [!DNL Privacy JS Library]

它提 [!DNL Adobe Privacy JavaScript Library] 供了几个功能，允许您检索和删除存储在浏览器中的客户身份。 库可以配置为从多个Adobe应用程序（包括ECID）检索身份信息。 通过使用回呼或承诺，您可以以编程方式成功处理检索到的ID并将它们发送到 [!DNL Privacy Service] API。

有关更多信 [!DNL Privacy JS Library]息（包括几个常用用例的代码示例），请参阅 [隐私JS库概述](js-library.md)。

## 后续步骤

本文档简要概述了检索客户身份数据以用于隐私请求所涉及的核心概念。 建议您查看每个部分中提供的文档链接，以了解有关这些概念和服务的更多详细信息。 有关如何将检索到的ID发 [!DNL Privacy Service] 送到以创建访问、删除或选择退出销售请求的步骤，请参阅Privacy Service开 [发人员指南](api/getting-started.md)。
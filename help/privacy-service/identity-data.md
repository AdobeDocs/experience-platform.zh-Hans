---
keywords: Experience Platform；主页；热门主题；ECID;ecid
solution: Experience Platform
title: 隐私请求的标识数据
topic-legacy: overview
description: 本文档就如何配置数据操作和利用Adobe技术有效检索适当的客户隐私请求身份信息提供了一般指导。
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 3%

---

# 隐私请求的标识数据

为了使Adobe Experience Platform [!DNL Privacy Service]能够处理客户对其私有数据的请求（包括访问、删除或选择退出销售请求），必须向其提供唯一标识符，将特定客户链接到您启用Adobe Experience Cloud的应用程序中存储的私有数据。 [!DNL Privacy Service] 然后使用这些标识符收集存储在客户身份下的所有数据，并 [!DNL Experience Cloud]根据客户的请求对其进行处理。

本文档就如何配置数据操作和利用Adobe技术有效检索适当的客户隐私请求身份信息提供了一般指导。

## 身份和命名空间

当客户可以通过多个不同的渠道与您的品牌进行交互时，协调从这些许多交互中记录的不同标识符可能会非常困难。 这反过来又使得很难确定哪些数据属于[!DNL Experience Cloud]应用程序中的特定人。

例如，在[!DNL Privacy Service]中处理客户数据请求时，标识可以表示在Adobe控制域下设置的Cookie值、在第三方域下并与Adobe共享的Cookie值，或您在IMS组织中显式定义的自定义标识符。

因此，要求发送到[!DNL Privacy Service]的每个身份都附带一个命名空间，通过将身份值与其来源系统相关来提供上下文。 命名空间可以表示一个通用概念，如电子邮件地址（“电子邮件”），或将标识与特定应用程序(如Adobe Advertising Cloud ID(“AdCloud”)或Adobe Target ID(“TNTID”))关联。

Adobe Experience Platform Identity Service维护全局定义和用户定义标识命名空间的存储。 有关命名空间的详细信息，请参阅[标识命名空间概述](../identity-service/namespaces.md)。 有关[!DNL Privacy Service]中常用的标准命名空间和命名空间限定符的列表，请参阅开发人员指南中的[附录部分](api/appendix.md)。

## ECID和选择加入服务

Adobe Experience Cloud [!DNL Identity Service]用作[!DNL Experience Cloud]的通用标识框架，并为每个站点访客分配一个唯一的永久ID。 [!DNL Experience Cloud] ID(ECID)通过使用第一方Cookie来跟踪客户的活动，可以跨多个应用程序唯一标识设备，并允许您在不同的[!DNL Experience Cloud]应用程序中标识同一站点访客及其数据。 有关详细信息，请参阅[Experience Cloud标识服务概述](https://docs.adobe.com/content/help/zh-Hans/id-service/using/intro/overview.html)。

选择加入服务是[!DNL Experience Cloud Identity Service]的扩展，它允许您在应用程序上设置协议，让访客确定您是否可以在访客的设备或浏览器上设置Cookie。 有关选择加入服务的详细信息（包括如何为应用程序设置服务），请参阅[选择加入服务文档](https://docs.adobe.com/content/help/zh-Hans/id-service/using/implementation/opt-in-service/optin-overview.html)。

在为您的站点访客分配了ECID后，您可以使用Adobe[!DNL Privacy JavaScript Library]来检索这些ID以用于隐私请求，如下一节所述。

## [!DNL Privacy JS Library]

[!DNL Adobe Privacy JavaScript Library]提供了几个功能，允许您检索和删除存储在浏览器中的客户身份。 库可以配置为从包括ECID在内的多个Adobe应用程序检索身份信息。 通过使用回调或承诺，您可以以编程方式成功处理检索到的ID并将它们发送到[!DNL Privacy Service] API。

有关[!DNL Privacy JS Library]的详细信息（包括几个常见用例的代码示例），请参阅[隐私JS库概述](js-library.md)。

## 后续步骤

本文档简要概述了检索客户身份数据以用于隐私请求所涉及的核心概念。 建议您查看每个部分中提供的文档链接，以了解有关这些概念和服务的更多详细信息。 有关如何将检索到的ID发送到[!DNL Privacy Service]以创建访问、删除或选择退出销售请求的步骤，请参阅[Privacy Service开发人员指南](api/getting-started.md)。

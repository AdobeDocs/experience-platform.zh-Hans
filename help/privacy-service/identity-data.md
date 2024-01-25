---
keywords: Experience Platform；主页；热门主题；ECID；ecid
solution: Experience Platform
title: 隐私请求的身份数据
description: 本文档提供了有关如何配置数据操作和利用Adobe技术有效检索适合客户隐私请求的身份信息的一般指导。
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 1%

---

# 隐私请求的身份数据

为了Adobe Experience Platform [!DNL Privacy Service] 要处理客户对其私有数据的请求（包括访问、删除或选择退出销售请求），必须向其提供唯一标识符，以将特定客户与其在支持Adobe Experience Cloud的应用程序中存储的私有数据相关联。 [!DNL Privacy Service] 然后，使用这些标识符收集存储在中的客户身份下的所有数据 [!DNL Experience Cloud]，并根据客户的请求进行处理。

本文档提供了有关如何配置数据操作和利用Adobe技术有效检索适合客户隐私请求的身份信息的一般指导。

## 身份和命名空间

当客户可以通过多个不同的渠道与您的品牌进行交互时，很难协调从这些多次交互中记录的不同标识符。 这反过来又可能会导致难以确定哪些数据属于您中的特定人员 [!DNL Experience Cloud] 应用程序。

例如，在中处理客户数据请求时 [!DNL Privacy Service]，则身份可以表示在Adobe控制的域下设置的Cookie值、在第三方域下设置并与Adobe共享的Cookie值，或者您在组织内明确定义的自定义标识符。

因此，需要发送每个身份到 [!DNL Privacy Service] 随附命名空间，该命名空间通过将身份值与其原始系统关联来提供上下文。 命名空间可以表示通用概念，例如电子邮件地址（“电子邮件”），也可以将身份与特定应用程序关联，例如Adobe Advertising Cloud ID (“AdCloud”)或Adobe Target ID (“TNTID”)。

Adobe Experience Platform Identity Service维护全局定义和用户定义的身份命名空间存储。 有关命名空间的更多详细信息，请参见 [身份命名空间概述](../identity-service/features/namespaces.md). 有关中常用的标准命名空间和命名空间限定符的列表 [!DNL Privacy Service]，请参见 [附录部分](api/appendix.md) 在API指南中。

## ECID和选择加入服务

Adobe Experience Cloud [!DNL Identity Service] 用作通用识别框架，用于 [!DNL Experience Cloud]，并为每个网站访客分配一个唯一的永久ID。 此 [!DNL Experience Cloud] ID (ECID)通过使用第一方Cookie跟踪客户活动，可以跨多个应用程序唯一识别设备，并且允许您在不同中识别同一网站访客及其数据 [!DNL Experience Cloud] 应用程序。 请参阅 [Experience CloudIdentity Service概述](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hans) 以了解更多信息。

选择加入服务，扩展 [!DNL Experience Cloud Identity Service]，您可以在应用程序上设置协议，以让访客确定是否可以在访客的设备或浏览器上设置Cookie。 有关选择加入服务的更多详细信息（包括如何为您的应用程序设置服务），请参阅 [选择加入服务文档](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hans).

为您的网站访客分配ECID后，即可使用Adobe [!DNL Privacy JavaScript Library] 以检索这些ID以便在隐私请求中使用，如下节所述。

## [!DNL Privacy JS Library]

此 [!DNL Adobe Privacy JavaScript Library] 提供了若干功能，可让您检索和删除存储在浏览器中的客户身份。 库可以配置为从多个Adobe应用程序（包括ECID）中检索身份信息。 通过使用回调或承诺，您可以通过编程方式处理成功检索的ID并将它们发送到 [!DNL Privacy Service] API。

有关详情 [!DNL Privacy JS Library]，包括几个常见用例的代码示例，请参阅 [隐私JS库概述](js-library.md).

## 后续步骤

本文档简要概述了检索用于隐私请求的客户身份数据时涉及的中心概念。 建议您查看每个部分提供的文档链接，以了解有关这些概念和服务的更多详细信息。 有关如何将检索的ID发送到的步骤 [!DNL Privacy Service] 有关创建访问、删除或选择退出销售请求，请参阅 [Privacy ServiceAPI指南](api/overview.md).

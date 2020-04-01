---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 隐私请求的标识数据
topic: overview
translation-type: tm+mt
source-git-commit: f2fe9c01c8355d0b312a0236f76085d1743aa8cc

---


# 隐私请求的标识数据

为了使Adobe Experience Platform Privacy Service能够处理客户对其私有数据（包括访问、删除或选择退出销售请求）的请求，必须向其提供唯一标识符，该标识符将特定客户与其在您支持Adobe Experience Cloud的应用程序中存储的私有数据相关联。 然后，隐私服务会使用这些标识符来收集Experience Cloud中存储在客户标识下的所有数据，并根据客户的请求进行处理。

本文档提供有关如何配置数据操作和利用Adobe技术有效检索客户隐私请求的适当身份信息的一般指导。

## 身份与命名空间

当客户可以通过多个不同的渠道与您的品牌进行交互时，协调从这些许多交互中记录的不同标识符可能会非常困难。 这反过来又可能使得很难确定哪些数据属于Experience Cloud应用程序中的特定人员。

例如，在隐私服务中处理客户数据请求时，标识可能表示在Adobe控制域下设置的cookie值、在第三方域下并与Adobe共享的cookie值，或您在IMS组织中明确定义的自定义标识符。

因此，发送到隐私服务的每个身份都必须附有一项命名空间 **** ，该通过将身份值与其来源系统相关联来提供上下文。 命名空间可以表示通用概念，如电子邮件地址（“电子邮件”），或将标识与特定应用程序(如Adobe Advertising Cloud ID(“AdCloud”)或Adobe目标ID(“TNTID”))关联。

Adobe Experience Platform Identity Service维护着全球定义和用户定义标识命名空间的存储。 有关命名空间的更多详细信息，请参阅 [标识命名空间概述](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md)。 有关隐私服务中常用的标准命名空间和命名空间限定符的列表，请参阅开发人员指 [南中的附录](api/appendix.md) 。

## ECID和选择加入服务

Adobe Experience Cloud Identity Service用作Experience Cloud的通用标识框架，并为每个站点访客分配一个唯一的永久ID。 Experience Cloud ID(ECID)通过使用第一方Cookie跟踪客户的活动，可以跨多个应用程序唯一标识设备，并允许您在不同的Experience Cloud应用程序中标识同一站点访客及其数据。 See the [Experience Cloud Identity Service overview](https://docs.adobe.com/content/help/en/id-service/using/intro/overview.html) for more information.

Opt-in Service是Experience Cloud Identity Service的扩展，它允许您在应用程序上设置协议，让访客决定您是否可以在访客的设备或浏览器上设置Cookie。 有关选择加入服务的更多详细信息（包括如何为您的应用程序设置服务），请参阅 [选择加入服务文档](https://docs.adobe.com/content/help/en/id-service/using/implementation/opt-in-service/optin-overview.html)。

在为站点访客分配ECID后，您可以利用Adobe隐私JavaScript库检索这些ID以用于隐私请求，如下一节所述。

## 隐私JS库

Adobe隐私JavaScript库提供几个功能，允许您检索和删除存储在浏览器中的客户身份。 库可以配置为从多个Adobe应用程序（包括ECID）检索身份信息。 通过使用回呼或承诺，您可以以编程方式处理成功检索的ID并将它们发送到Privacy Service API。

有关隐私JS库的更多信息（包括几个常见用例的代码示例），请参阅隐 [私JS库概述](js-library.md)。

## 后续步骤

本文档简要概述了检索客户身份数据以用于隐私请求的核心概念。 建议您查看每个部分中提供的文档链接，以了解有关这些概念和服务的更多详细信息。 有关如何将检索到的ID发送到隐私服务以创建访问、删除或选择退出销售请求的步骤，请参阅隐私服务开发 [人员指南](api/getting-started.md)。
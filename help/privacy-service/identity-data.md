---
keywords: Experience Platform；主页；热门主题；ECID;ecid
solution: Experience Platform
title: 隐私请求的身份数据
description: 本文档就如何配置数据操作和利用Adobe技术有效检索客户隐私请求的适当身份信息提供了一般指导。
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 2%

---

# 隐私请求的标识数据

为了Adobe Experience Platform [!DNL Privacy Service] 要处理客户的私有数据请求（包括访问、删除或选择退出销售请求），必须向其提供唯一标识符，以将特定客户关联到在您启用了Adobe Experience Cloud的应用程序中存储的私有数据。 [!DNL Privacy Service] 然后使用这些标识符收集存储在 [!DNL Experience Cloud]，并根据客户的请求进行处理。

本文档就如何配置数据操作和利用Adobe技术有效检索客户隐私请求的适当身份信息提供了一般指导。

## 身份和命名空间

当客户可以通过多个不同渠道与您的品牌进行交互时，协调从这些多次交互中记录的不同标识符可能会非常困难。 这反过来又会导致难以确定哪些数据属于您的 [!DNL Experience Cloud] 应用程序。

例如，在处理 [!DNL Privacy Service]，标识可以表示在Adobe控制域下设置的Cookie值、在第三方域下与Adobe共享的Cookie值，或您在组织内明确定义的自定义标识符。

因此，每个身份都必须发送到 [!DNL Privacy Service] 与一个命名空间相伴，该命名空间通过将标识值与其源系统相关联来提供上下文。 命名空间可以表示一个通用概念，如电子邮件地址（“电子邮件”），或将标识与特定应用程序(如Adobe Advertising Cloud ID(“AdCloud”)或Adobe Target ID(“TNTID”))相关联。

Adobe Experience Platform Identity服务维护全局定义和用户定义的身份命名空间的存储。 有关命名空间的更多详细信息，请参阅 [身份命名空间概述](../identity-service/namespaces.md). 有关中常用的标准命名空间和命名空间限定符列表 [!DNL Privacy Service]，请参阅 [附录节](api/appendix.md) （在API指南中）。

## ECID和选择加入服务

Adobe Experience Cloud [!DNL Identity Service] 用作 [!DNL Experience Cloud]，并为每个网站访客分配一个唯一的永久性ID。 的 [!DNL Experience Cloud] ID(ECID)通过使用第一方Cookie跟踪客户的活动，可以跨多个应用程序唯一标识设备，并允许您识别同一网站访客及其在不同应用程序中的数据 [!DNL Experience Cloud] 应用程序。 请参阅 [Experience Cloud标识服务概述](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) 以了解更多信息。

选择加入服务， [!DNL Experience Cloud Identity Service]，用于在应用程序上设置协议，以允许访客确定您是否可以在访客的设备或浏览器上设置Cookie。 有关选择加入服务（包括如何为您的应用程序设置服务）的更多详细信息，请参阅 [选择加入服务文档](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hans).

为您的网站访客分配ECID后，您便可以利用Adobe [!DNL Privacy JavaScript Library] 以检索这些ID以在隐私请求中使用，如下一节中所述。

## [!DNL Privacy JS Library]

的 [!DNL Adobe Privacy JavaScript Library] 提供了多个函数，用于检索和删除存储在浏览器中的客户身份。 库可以配置为从多个Adobe应用程序（包括ECID）中检索身份信息。 通过使用回调或承诺，您可以以编程方式处理成功检索的ID，并将它们发送到 [!DNL Privacy Service] API。

有关 [!DNL Privacy JS Library]，包括几个常见用例的代码示例，请参阅 [隐私JS库概述](js-library.md).

## 后续步骤

本文档简要概述了检索客户身份数据以用于隐私请求所涉及的核心概念。 建议您查看每个部分中提供的文档链接，以了解有关这些概念和服务的更多详细信息。 有关如何将检索到的ID发送到 [!DNL Privacy Service] 要创建访问、删除或选择退出销售请求，请参阅 [Privacy ServiceAPI指南](api/overview.md).

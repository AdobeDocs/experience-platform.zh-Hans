---
keywords: Experience Platform；主页；热门主题；一般REST；一般REST
solution: Experience Platform
title: 通用REST API源连接器概述
description: 了解如何使用API或用户界面将通用REST API连接到Adobe Experience Platform。
exl-id: e3449e33-7261-4aa2-bce9-5530eb4fcc68
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# （测试版） [!DNL Generic REST API]

>[!NOTE]
>
>的 [!DNL Generic REST API] 来源为测试版。 请参阅 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标签的连接器的更多信息。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用构建、标记和增强传入数据 [!DNL Platform] 服务。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

平台支持从协议应用程序中摄取数据，包括 [!DNL Generic REST API].

的 [!DNL Generic REST API] 源允许您将来自基于REST的应用程序的数据引入平台。 [!DNL Generic REST API] 支持基本身份验证和基于OAuth 2刷新代码的身份验证。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表。 无法将特定于区域的IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面以了解更多信息。

以下文档提供了有关如何连接 [!DNL Generic REST API] 源到平台。

## 连接 [!DNL Generic REST API] to [!DNL Platform] 使用API

- [使用流服务API创建通用REST API基连接](../../tutorials/api/create/protocols/generic-rest.md)
- [使用流量服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为协议源创建数据流](../../tutorials/api/collect/protocols.md)

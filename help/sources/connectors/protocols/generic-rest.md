---
keywords: Experience Platform；主页；热门主题；通用REST；通用Rest
solution: Experience Platform
title: 通用REST API源连接器概述
description: 了解如何使用API或用户界面将Generic REST API连接到Adobe Experience Platform。
exl-id: e3449e33-7261-4aa2-bce9-5530eb4fcc68
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# (Beta) [!DNL Generic REST API]

>[!NOTE]
>
>此 [!DNL Generic REST API] 源为测试版。 请参阅 [源概述](../../home.md#terms-and-conditions) 有关使用Beta标记的连接器的更多信息。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Platform支持从协议应用程序中摄取数据，包括 [!DNL Generic REST API].

此 [!DNL Generic REST API] 源允许您将数据从基于REST的应用程序带入Platform。 [!DNL Generic REST API] 支持基本身份验证和OAuth 2刷新基于代码的身份验证。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于地区的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面，以了解更多信息。

以下文档提供了有关如何连接 [!DNL Generic REST API] 源到平台使用API。

## Connect [!DNL Generic REST API] 到 [!DNL Platform] 使用API

- [使用流服务API创建通用REST API基本连接](../../tutorials/api/create/protocols/generic-rest.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为协议源创建数据流](../../tutorials/api/collect/protocols.md)

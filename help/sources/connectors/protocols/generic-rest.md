---
keywords: Experience Platform；主页；热门主题；通用REST；通用Rest
solution: Experience Platform
title: 常规REST API Source连接器概述
description: 了解如何使用API或用户界面将通用REST API连接到Adobe Experience Platform。
exl-id: e3449e33-7261-4aa2-bce9-5530eb4fcc68
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# (Beta) [!DNL Generic REST API]

>[!NOTE]
>
>[!DNL Generic REST API]源为测试版。 有关使用带有Beta标记的连接器的更多信息，请参阅[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform允许从外部源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform支持从协议应用程序（包括[!DNL Generic REST API]）中摄取数据。

[!DNL Generic REST API]源允许您将数据从基于REST的应用程序引入Experience Platform。 [!DNL Generic REST API]支持基本身份验证和OAuth 2刷新基于代码的身份验证。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

以下文档提供了有关如何使用API将[!DNL Generic REST API]源连接到Experience Platform的信息。

## 使用API将[!DNL Generic REST API]连接到[!DNL Experience Platform]

- [使用流服务API创建常规REST API基本连接](../../tutorials/api/create/protocols/generic-rest.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为协议源创建数据流](../../tutorials/api/collect/protocols.md)

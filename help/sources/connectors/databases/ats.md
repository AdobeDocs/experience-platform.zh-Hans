---
keywords: Experience Platform；主页；热门主题；Azure表存储；Azure表存储；ATS;ATS
solution: Experience Platform
title: Azure表存储源连接器概述
topic-legacy: overview
description: 了解如何使用API或用户界面将Azure表存储连接到Adobe Experience Platform。
exl-id: 096e01b1-7e95-4e30-87de-d0976f8b438a
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# （测试版）[!DNL Azure Table Storage]连接器

>[!NOTE]
>
>[!DNL Azure Table Storage]连接器处于测试阶段。 有关使用测试版标记的连接器的更多信息，请参阅[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用[!DNL Platform]服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

[!DNL Experience Platform] 支持从第三方数据库摄取数据。[!DNL Platform] 可以连接到不同类型的数据库，如关系数据库、 NoSQL数据库或data warehouse。对数据库提供程序的支持包括[!DNL Azure Table Storage]。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表。 无法将特定于区域的IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 有关更多信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页面。

>[!IMPORTANT]
>
>[!DNL Azure Table Storage]源连接器当前不支持与平台的同一区域连接。 这意味着如果您的Azure实例使用与Platform相同的网络区域，则无法建立与Platform源的连接。 目前，仅支持跨区域连接。 有关更多信息，请联系您的Adobe客户经理。

以下文档提供了有关如何使用API或用户界面将[!DNL Azure Table Storage]连接到[!DNL Platform]的信息：

## 使用API将[!DNL Azure Table Storage]连接到[!DNL Platform]

- [使用流服务API创建Azure表存储基连接](../../tutorials/api/create/databases/ats.md)
- [使用流服务API探索数据库源的数据结构和内容](../../tutorials/api/explore/database-nosql.md)
- [使用流服务API为数据库源创建数据流](../../tutorials/api/collect/database-nosql.md)

## 使用UI将[!DNL Azure Table Storage]连接到[!DNL Platform]

- [在UI中创建Azure表存储源连接](../../tutorials/ui/create/databases/ats.md)
- [在UI中为数据库源连接创建数据流](../../tutorials/ui/dataflow/databases.md)

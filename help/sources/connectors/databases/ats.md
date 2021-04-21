---
keywords: Experience Platform；主页；热门主题；Azure表存储;azure表存储;ATS;ats
solution: Experience Platform
title: Azure表存储源连接器概述
topic-legacy: overview
description: 了解如何使用API或用户界面将Azure表存储连接到Adobe Experience Platform。
exl-id: 096e01b1-7e95-4e30-87de-d0976f8b438a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# （测试版）[!DNL Azure Table Storage]连接器

>[!NOTE]
>
>[!DNL Azure Table Storage]连接器处于测试状态。 有关使用测试版标记的连接器的详细信息，请参阅[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform允许从外部源摄取数据，同时为您提供使用[!DNL Platform]服务构建、标记和增强传入数据的能力。 您可以从各种来源收集数据，如Adobe应用程序、基于云的存储、数据库和许多其他来源。

[!DNL Experience Platform] 支持从第三方数据库中摄取数据。[!DNL Platform] 可以连接到不同类型的数据库，如关系、NoSQL或data warehouse。对数据库提供程序的支持包括[!DNL Azure Table Storage]。

## IP地址允许列表

在使用源连接器之前，必须向允许列表添加IP地址列表。 如果无法将您的区域特定IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 有关详细信息，请参阅[ IP地址允许列表](../../ip-address-allow-list.md)页。

>[!IMPORTANT]
>
>[!DNL Azure Table Storage]源连接器当前不支持与平台的同一区域连接。 这意味着，如果您的Azure实例使用与平台相同的网络区域，则无法建立到平台源的连接。 目前，仅支持跨区域连接。 有关详细信息，请与您的Adobe客户经理联系。

以下文档提供了如何使用API或用户界面将[!DNL Azure Table Storage]连接到[!DNL Platform]的信息：

## 使用API将[!DNL Azure Table Storage]连接到[!DNL Platform]

- [使用流服务API创建Azure表存储源连接](../../tutorials/api/create/databases/ats.md)
- [使用Flow Service API浏览数据库系统](../../tutorials/api/explore/database-nosql.md)
- [使用流服务API从数据库收集数据](../../tutorials/api/collect/database-nosql.md)

## 使用UI将[!DNL Azure Table Storage]连接到[!DNL Platform]

- [在UI中创建Azure表存储源连接](../../tutorials/ui/create/databases/ats.md)
- [在UI中为数据库连接配置数据流](../../tutorials/ui/dataflow/databases.md)

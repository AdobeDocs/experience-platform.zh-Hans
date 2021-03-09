---
keywords: Experience Platform；主页；热门主题；AzureData Explorer;azure数据浏览器
solution: Experience Platform
title: AzureData Explorer源连接器概述
topic: 概述
description: 了解如何使用API或用户界面将AzureData Explorer连接到Adobe Experience Platform。
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# （测试版）[!DNL Azure Data Explorer]连接器

>[!NOTE]
>
>[!DNL Azure Data Explorer]连接器处于测试状态。 有关使用测试版标记的连接器的详细信息，请参阅[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform为[!DNL Microsoft]、MySQL和[!DNL Azure]等数据库提供程序提供本机连接。 您可以将这些系统中的数据导入[!DNL Platform]。

支持不同类型的第三方数据库，包括关系型、NoSQL或data warehouse。 对数据库提供程序的支持包括[!DNL Azure Data Explorer]。

## IP地址允许列表

在使用源连接器之前，必须向允许列表添加IP地址列表。 如果无法将您的区域特定IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 有关详细信息，请参阅[ IP地址允许列表](../../ip-address-allow-list.md)页。

>[!IMPORTANT]
>
>[!DNL Azure Data Explorer]源连接器当前不支持与平台的同一区域连接。 这意味着，如果您的Azure实例使用与平台相同的网络区域，则无法建立到平台源的连接。 目前，仅支持跨区域连接。 有关详细信息，请与您的Adobe客户经理联系。

以下文档提供了如何使用API或用户界面将[!DNL Azure Data Explorer]连接到[!DNL Platform]的信息：

## 使用API将[!DNL Azure Data Explorer]连接到[!DNL Platform]

- [使用流服务API创建AzureData Explorer源连接](../../tutorials/api/create/databases/data-explorer.md)
- [使用Flow Service API浏览数据库系统](../../tutorials/api/explore/database-nosql.md)
- [使用流服务API从数据库收集数据](../../tutorials/api/collect/database-nosql.md)

## 使用UI将[!DNL Azure Data Explorer]连接到[!DNL Platform]

- [在UI中创建AzureData Explorer源连接](../../tutorials/ui/create/databases/data-explorer.md)
- [在UI中为数据库连接配置数据流](../../tutorials/ui/dataflow/databases.md)
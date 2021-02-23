---
keywords: Experience Platform；主页；热门主题；Google PubSub;google pubsub
solution: Experience Platform
title: Google PubSub源连接器概述
topic: 概述
description: 了解如何使用API或用户界面将Google PubSub连接到Adobe Experience Platform。
translation-type: tm+mt
source-git-commit: 0af90253f04377149986aedf2e9d3012ca06d4f8
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# （测试版）[!DNL Google PubSub]连接器

>[!NOTE]
>
>[!DNL Google PubSub]连接器处于测试状态。 有关使用测试版标记的连接器的详细信息，请参见[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform为[!DNL AWS]、[!DNL Google Cloud Platform]和[!DNL Azure]等云提供商提供本机连接，允许您将这些系统中的数据引入平台，以用于下游服务和目标。

云存储源无需下载、格式化或上传，即可将您的数据导入平台。 收录的数据可以格式化为XDM JSON、XDM Perface或分隔。 流程的每个步骤都集成到源工作流中。 平台允许您实时导入[!DNL Azure Event Hubs]中的数据。

## IP地址允许列表

在使用源连接器之前，必须向允许列表添加IP地址列表。 如果无法将您的区域特定IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 有关详细信息，请参阅[ IP地址允许列表](../../ip-address-allow-list.md)页。

## 将[!DNL Google PubSub]连接到平台

以下文档提供了有关如何使用API或用户界面将[!DNL Google PubSub]连接到平台的信息：

### 使用API

- [使用流服务API创建Google PubSub源连接](../../tutorials/api/create/cloud-storage/google-pubsub.md)
- [使用Flow Service API收集流数据](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中创建Google PubSub源连接](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
- [在UI中为云存储连接配置数据流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
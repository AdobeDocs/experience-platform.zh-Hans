---
keywords: Experience Platform；主页；热门主题；Azure事件集线器；azure事件集线器；事件集线器；事件集线器
solution: Experience Platform
title: Azure事件集线器源连接器概述
topic-legacy: overview
description: 了解如何使用API或用户界面将Azure事件集线器连接到Adobe Experience Platform。
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
translation-type: tm+mt
source-git-commit: 6dac267be93241bffb4eb5092a6e8da5093c63a6
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# [!DNL Azure Event Hubs] 连接器

Adobe Experience Platform为AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等云提供商提供本机连接。 您可以将这些系统中的数据导入[!DNL Platform]。

云存储源可以将您自己的数据导入[!DNL Platform]，而无需下载、格式化或上传。 收录的数据可以格式化为XDM JSON、XDM Perface或分隔。 流程的每个步骤都集成到源工作流中。 [!DNL Platform] 让您能够实时导入 [!DNL Azure Event Hubs] 数据。

## IP地址允许列表

在使用源连接器之前，必须向允许列表添加IP地址列表。 如果无法将您的区域特定IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 有关详细信息，请参阅[ IP地址允许列表](../../ip-address-allow-list.md)页。

## 将[!DNL Azure Event Hubs]连接到[!DNL Platform]

以下文档提供了如何使用API或用户界面将[!DNL Azure Event Hubs]连接到[!DNL Platform]的信息：

### 使用API

- [使用流服务API创建Azure事件集线器源连接](../../tutorials/api/create/cloud-storage/eventhub.md)
- [使用Flow Service API收集流数据](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中创建Azure事件集线器源连接](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [在UI中为云存储连接配置数据流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
